# Mojo 矩阵乘法

本文介绍了如何在 Mojo 中编写矩阵乘法（matmul）算法。我们将从一个纯 Python 实现开始，接着过渡到一个简单的实现，该实现基本上与纯 Python 实现相同，然后引入类型，并继续通过向量化、分块和并行化来优化实现。

首先，我们来定义矩阵乘法。给定两个维度分别为 ***M x K*** 和 ***K × N*** 的稠密矩阵 ***A*** 和 ***B***，计算它们的点积 ***C = A.B*** 的公式为：

{% math %}
C_{i,j} += \sum_{k \in [0 \cdots K)} A_{i,k} B_{k,j}
{% endmath %}

> 请查看我们关于矩阵乘法（matmul）以及它对机器学习和深度学习工作负载的重要性的[博客文章](https://www.modular.com/blog/ais-compute-fragmentation-what-matrix-multiplication-teaches-us)。

本文档内容先从一个与 Python 完全相同的实现开始（实际上只是更改文件扩展名），然后看看如何通过为实现添加类型来提高性能，最后通过利用现代硬件提供的向量化和并行化功能来扩展实现。在执行过程中，我们会报告所达到的 GFlops（每秒浮点操作次数）。

## Python 实现

首先，让我们直接根据定义在Python中实现矩阵乘法（matmul）。

```python
%%python
def matmul_python(C, A, B):
    for m in range(C.rows):
        for k in range(A.cols):
            for n in range(C.cols):
                C[m, n] += A[m, k] * B[k, n]
```

让我们使用 128x128 的矩阵对我们的实现进行性能基准测试，并报告所达到的 GFlops 值。

```python
%%python
import numpy as np
from timeit import timeit

class Matrix:
    def __init__(self, value, rows, cols):
        self.value = value
        self.rows = rows
        self.cols = cols
        
    def __getitem__(self, idxs):
        return self.value[idxs[0]][idxs[1]]
    
    def __setitem__(self, idxs, value):
        self.value[idxs[0]][idxs[1]] = value

def benchmark_matmul_python(M, N, K):
    A = Matrix(list(np.random.rand(M, K)), M, K)
    B = Matrix(list(np.random.rand(K, N)), K, N)
    C = Matrix(list(np.zeros((M, N))), M, N)
    secs = timeit(lambda: matmul_python(C, A, B), number=2)/2
    gflops = ((2*M*N*K)/secs) / 1e9
    print(gflops, "GFLOP/s")
    return gflops
```

```python
python_gflops = benchmark_matmul_python(128, 128, 128).to_float64()
```

> 0.0023380120845339905 GFLOP/s

## 将 Python 实现替换为 Mojo

使用 Mojo 就像使用 Python 一样简单。首先，让我们导入 Mojo 标准库中我们要使用的模块：
{% fold summary="导入实用程序并定义 Matrix （单击以显示/隐藏）" %}
```python
from benchmark import Benchmark
from sys.intrinsics import strided_load
from utils.list import VariadicList
from math import div_ceil, min
from memory import memset_zero
from memory.unsafe import DTypePointer
from random import rand, random_float64
from sys.info import simdwidthof
from runtime.llcl import Runtime
```
{% endfold %}
接下来，我们可以复制并粘贴我们的 Python 代码。Mojo 是 Python 的超集，因此相同的 Python 代码将作为 Mojo 代码运行。

```python
# This exactly the same Python implementation, 
# but is infact Mojo code!
def matmul_untyped(C, A, B):
    for m in range(C.rows):
        for k in range(A.cols):
            for n in range(C.cols):
                C[m, n] += A[m, k] * B[k, n]
```

接着，我们可以对实现进行性能基准测试。与之前一样，我们使用了一个 128x128 的矩阵

```python
fn matrix_getitem(self: object, i: object) raises -> object:
    return self.value[i]


fn matrix_setitem(self: object, i: object, value: object) raises -> object:
    self.value[i] = value
    return None


fn matrix_append(self: object, value: object) raises -> object:
    self.value.append(value)
    return None


fn matrix_init(rows: Int, cols: Int) raises -> object:
    let value = object([])
    return object(
        Attr("value", value), Attr("__getitem__", matrix_getitem), Attr("__setitem__", matrix_setitem), 
        Attr("rows", rows), Attr("cols", cols), Attr("append", matrix_append),
    )

def benchmark_matmul_untyped(M: Int, N: Int, K: Int, python_gflops: Float64):
    C = matrix_init(M, N)
    A = matrix_init(M, K)
    B = matrix_init(K, N)
    for i in range(M):
        c_row = object([])
        b_row = object([])
        a_row = object([])
        for j in range(N):
            c_row.append(0.0)
            b_row.append(random_float64(-5, 5))
            a_row.append(random_float64(-5, 5))
        C.append(c_row)
        B.append(b_row)
        A.append(a_row)

    @parameter
    fn test_fn():
        try:
            _ = matmul_untyped(C, A, B)
        except:
            pass

    let secs = Float64(Benchmark().run[test_fn]()) / 1_000_000_000
    _ = (A, B, C)
    let gflops = ((2*M*N*K)/secs) / 1e9
    let speedup : Float64 = gflops / python_gflops
    print(gflops, "GFLOP/s, a", speedup.value, "x speedup over Python")
```

```python
benchmark_matmul_untyped(128, 128, 128, python_gflops)
```

> 0.010705118393665017 GFLOP/s, a 4.5787267159479832 x speedup over Python

请注意，我们在不费吹灰之力的情况下获得了巨大的加速。

## 向 Python 实现添加类型

尽管上述程序在性能上优于 Python，但我们仍然可以进一步优化 Mojo 以获得更好的性能。如果我们告诉 Mojo 输入的数据类型，它可以优化掉许多代码并减少分派成本（与 Python 不同，Python 仅用于类型检查，而 Mojo 还利用类型信息进行性能优化）。

为了实现这一点，首先让我们定义一个矩阵（Matrix）结构。矩阵结构包含了一个数据指针以及大小字段。虽然矩阵结构可以根据任何数据类型进行参数化，但在这里，为了简洁起见，我们将数据类型设置为 Float32。

```python
struct Matrix:
    var data: DTypePointer[DType.float32]
    var rows: Int
    var cols: Int

    fn __init__(inout self, rows: Int, cols: Int):
        self.data = DTypePointer[DType.float32].alloc(rows * cols)
        rand(self.data, rows*cols)
        self.rows = rows
        self.cols = cols

    fn __del__(owned self):
        self.data.free()

    fn zero(inout self):
        memset_zero(self.data, self.rows * self.cols)

    @always_inline
    fn __getitem__(self, y: Int, x: Int) -> Float32:
        return self.load[1](y, x)

    @always_inline
    fn load[nelts:Int](self, y: Int, x: Int) -> SIMD[DType.float32, nelts]:
        return self.data.simd_load[nelts](y * self.cols + x)

    @always_inline
    fn __setitem__(self, y: Int, x: Int, val: Float32):
        return self.store[1](y, x, val)

    @always_inline
    fn store[nelts:Int](self, y: Int, x: Int, val: SIMD[DType.float32, nelts]):
        self.data.simd_store[nelts](y * self.cols + x, val)
```

> 请注意，我们在`getitem`和`setitem`方法中使用了`load`和`store`方法。在初始的矩阵乘法实现中，这并没有太大差异，但在稍后的优化向量化版本中，我们将利用这一点。

有了上述的矩阵类型，我们可以有效地复制并粘贴 Python 的实现，只需添加类型注解即可：

```python
# Note that C, A, and B have types.
fn matmul_naive(C: Matrix, A: Matrix, B: Matrix):
    for m in range(C.rows):
        for k in range(A.cols):
            for n in range(C.cols):
                C[m, n] += A[m, k] * B[k, n]
```

随着我们的改进，我们将对这些实现进行性能基准测试，因此让我们编写一个辅助函数来为我们执行这项任务：

```python
@always_inline
fn benchmark[
    func: fn (Matrix, Matrix, Matrix) -> None
](M: Int, N: Int, K: Int, base_gflops: Float64):
    var C = Matrix(M, N)
    C.zero()
    var A = Matrix(M, K)
    var B = Matrix(K, N)

    @always_inline
    @parameter
    fn test_fn():
        _ = func(C, A, B)

    let secs = Float64(Benchmark().run[test_fn]()) / 1_000_000_000
    # Prevent the matrices from being freed before the benchmark run
    _ = (A, B, C)
    let gflops = ((2 * M * N * K) / secs) / 1e9
    let speedup: Float64 = gflops / base_gflops
    # print(gflops, "GFLOP/s", speedup, " speedup")
    print(gflops, "GFLOP/s, a", speedup.value, "x speedup over Python")
```

基准测试显示出了显著的加速效果。我们将矩阵的大小增加到 512x512，因为 Mojo 比 Python 要快得多。

```python
benchmark[matmul_naive](512, 512, 512, python_gflops)
```

> 3.8678966720972414 GFLOP/s, a 1654.3527288346697 x speedup over Python

添加类型注解与原始的无类型版本相比，带来了巨大的改进。

## 向量化最内层循环

通过利用向量指令，我们可以比上述的实现更进一步。与假定矢量宽度不同，我们使用`simd_width`查询指定数据类型的 smid 宽度。这使得我们的代码具有可移植性，可以在不同硬件上使用。利用 SIMD 指令非常简单，如下所示：

```python
# Mojo has SIMD vector types, we can vectorize the Matmul code as follows.
alias nelts = simdwidthof[DType.float32]() # The SIMD vector width.
fn matmul_vectorized_0(C: Matrix, A: Matrix, B: Matrix):
    for m in range(C.rows):
        for k in range(A.cols):
            for nv in range(0, C.cols, nelts):
                C.store[nelts](m,nv, C.load[nelts](m,nv) + A[m,k] * B.load[nelts](k,nv))
        
            # Handle remaining elements with scalars.
            for n in range(nelts*(C.cols//nelts), C.cols):
                C[m,n] += A[m,k] * B[k,n]
```

我们可以对上述实现进行性能基准测试。需要注意的是，许多编译器可以检测到简单的循环并对其进行优化。但是，Mojo 允许您明确且精确地控制应用哪些优化。

```python
benchmark[matmul_vectorized_0](512, 512, 512, python_gflops)
```

> 16.643427805584807 GFLOP/s, a 7118.6235159696162 x speedup over Python

矢量化是一种常见的优化技术，而 Mojo 提供了一个高阶函数，可以帮助您执行矢量化操作。这个`vectorize`函数接受一个矢量宽度和一个与矢量宽度相关的函数作为参数，并将以矢量化的方式来进行评估。

```python
# Simplify the code by using the builtin vectorize function
from algorithm import vectorize
fn matmul_vectorized_1(C: Matrix, A: Matrix, B: Matrix):
    for m in range(C.rows):
        for k in range(A.cols):
            @parameter
            fn dot[nelts : Int](n : Int):
                C.store[nelts](m,n, C.load[nelts](m,n) + A[m,k] * B.load[nelts](k,n))
            vectorize[nelts, dot](C.cols)
```

两种实现在性能方面仅存在细微差别：

```python
benchmark[matmul_vectorized_1](512, 512, 512, python_gflops)
```

> 15.99219798204404 GFLOP/s, a 6840.0835426954536 x speedup over Python

## 并行化矩阵乘法

为了从现代处理器中获得最佳性能，必须利用它们拥有的多个核心。

对于并行代码，我们需要引入一个共享线程池的基准函数，否则它会在每次基准测试迭代中引入延迟，因为它会创建一个新的运行时。您可以在 `with Runtime() as rt` 看到：

```python

@always_inline
fn benchmark_parallel[
    func: fn (Matrix, Matrix, Matrix, Runtime) -> None
](M: Int, N: Int, K: Int, base_gflops: Float64):
    var C = Matrix(M, N)
    C.zero()
    var A = Matrix(M, K)
    var B = Matrix(K, N)

    with Runtime() as rt:
        @always_inline
        @parameter
        fn test_fn():
            _ = func(C, A, B, rt)

        let secs = Float64(Benchmark().run[test_fn]()) / 1_000_000_000
        # Prevent the matrices from being freed before the benchmark run
        _ = (A, B, C)
        let gflops = ((2 * M * N * K) / secs) / 1e9
        let speedup: Float64 = gflops / base_gflops
        # print(gflops, "GFLOP/s", speedup, " speedup")
        print(gflops, "GFLOP/s, a", speedup.value, "x speedup over Python")
```

使用 Mojo ，我们可以轻松地使用`parallelize`函数并行运行代码。

让我们修改我们的矩阵乘法（matmul）实现，并将其改为多线程化（为简单起见，我们仅在 M 维度上使用 `parallelize`）:

```python
# Parallelize the code by using the builtin parallelize function
from algorithm import parallelize
fn matmul_parallelized(C: Matrix, A: Matrix, B: Matrix, rt: Runtime):
    @parameter
    fn calc_row(m: Int):
        for k in range(A.cols):
            @parameter
            fn dot[nelts : Int](n : Int):
                C.store[nelts](m,n, C.load[nelts](m,n) + A[m,k] * B.load[nelts](k,n))
            vectorize[nelts, dot](C.cols)
        
    parallelize[calc_row](rt, C.rows)
```

我们可以对并行矩阵乘法实现进行性能基准测试。

```python
benchmark_parallel[matmul_parallelized](512, 512, 512, python_gflops)
```

> 146.47273560634375 GFLOP/s, a 62648.408267546874 x speedup over Python

## 矩阵乘法的分块操作

分块是对矩阵乘法的一种优化操作，用于增加缓存局部性。其思想是保持子矩阵在缓存中，增加重用。`tile`函数本身可以在Mojo中编写为：

```python
from algorithm import Static2DTileUnitFunc as Tile2DFunc
```

```python
# Perform 2D tiling on the iteration space defined by end_x and end_y.
fn tile[tiled_fn: Tile2DFunc, tile_x: Int, tile_y: Int](end_x: Int, end_y: Int):
    # Note: this assumes that ends are multiples of the tiles.
    for y in range(0, end_y, tile_y):
        for x in range(0, end_x, tile_x):
            tiled_fn[tile_x, tile_y](x, y)
```

上述代码将在定义为区间 ({% math %}[0, end_x]{% endmath %}, {% math %}[0, end_y]{% endmath %}) 的二维迭代空间上执行二维分块操作。一旦我们在上面进行了定义，就可以在我们的矩阵乘法内核中使用它。为了简单起见，我们选择`4` 作为分块的高度，并且由于我们还想要进行矢量化，我们将使用 `4 * nelts` 作为分块的宽度（因为我们在列上进行矢量化）。

```python
# Use the above tile function to perform tiled matmul.
fn matmul_tiled_parallelized(C: Matrix, A: Matrix, B: Matrix, rt: Runtime):
    @parameter
    fn calc_row(m: Int):
        @parameter
        fn calc_tile[tile_x: Int, tile_y: Int](x: Int, y: Int):
            for k in range(y, y + tile_y):
                @parameter
                fn dot[nelts : Int,](n : Int):
                    C.store[nelts](m,n + x, C.load[nelts](m,n+x) + A[m,k] * B.load[nelts](k,n+x))
                vectorize[nelts, dot](tile_x)

        # We hardcode the tile factor to be 4.
        alias tile_size = 4
        tile[calc_tile, nelts * tile_size, tile_size](A.cols, C.cols)

    parallelize[calc_row](rt, C.rows)
```

同样，我们可以对分块并行矩阵乘法实现进行性能基准测试：

```python
benchmark_parallel[matmul_tiled_parallelized](512, 512, 512, python_gflops)
```

> 146.70664459435014 GFLOP/s, a 62748.45436634752 x speedup over Python

在上述实现中的一个开销来源是我们没有展开通过 dot 函数的`vectorize`引入的循环。在 Mojo 中，我们可以通过`vectorize_unroll`高阶函数来实现这一点：

```python
# Unroll the vectorized loop by a constant factor.
from algorithm import vectorize_unroll
fn matmul_tiled_unrolled_parallelized(C: Matrix, A: Matrix, B: Matrix, rt: Runtime):
    @parameter
    fn calc_row(m: Int):
        @parameter
        fn calc_tile[tile_x: Int, tile_y: Int](x: Int, y: Int):
            for k in range(y, y + tile_y):
                @parameter
                fn dot[nelts : Int,](n : Int):
                    C.store[nelts](m,n+x, C.load[nelts](m,n+x) + A[m,k] * B.load[nelts](k,n+x))

                # Vectorize by nelts and unroll by tile_x/nelts
                # Here unroll factor is 4
                vectorize_unroll[nelts, tile_x//nelts, dot](tile_x)

        alias tile_size = 4
        tile[calc_tile, nelts*tile_size, tile_size](A.cols, C.cols)
      
    parallelize[calc_row](rt, C.rows)
```

同样，我们可以使用展开的向量化内部循环对新的分块并行矩阵乘法实现进行基准测试：

```python
benchmark_parallel[matmul_tiled_unrolled_parallelized](512, 512, 512, python_gflops)
```

> 166.67781596455771 GFLOP/s, a 71290.399680624279 x speedup over Python

## 寻找`tile_factor`

```python
from autotune import autotune, search
from time import now
from memory.unsafe import Pointer

alias matmul_fn_sig_type = fn(Matrix, Matrix, Matrix, Runtime) -> None
```

tile factor 的选择可以极大地影响整个矩阵乘法的性能，但最佳的 tile factor 在很大程度上取决于硬件，受缓存配置和其他难以建模的影响因素的影响。我们希望编写可移植的代码，而无需了解硬件的所有细节，因此我们可以要求 Mojo 使用自动调整功能来自动选择最佳的 tile factor。

```python
# Autotune the tile size used in the matmul.
@adaptive
fn matmul_autotune_impl(C: Matrix, A: Matrix, B: Matrix, rt: Runtime, /):
    @parameter
    fn calc_row(m: Int):
        @parameter
        fn calc_tile[tile_x: Int, tile_y: Int](x: Int, y: Int):
            for k in range(y, y + tile_y):
                @parameter
                fn dot[nelts : Int,](n : Int):
                    C.store[nelts](m,n+x, C.load[nelts](m,n+x) + A[m,k] * B.load[nelts](k,n+x))
                vectorize_unroll[nelts, tile_x // nelts, dot](tile_x)

        # Instead of hardcoding to tile_size = 4, search for the fastest 
        # tile size by evaluting this function as tile size varies.
        alias tile_size = autotune(1, 2, 4, 8, 16, 32)
        tile[calc_tile, nelts * tile_size, tile_size](A.cols, C.cols)
      
    parallelize[calc_row](rt, C.rows)
```

这将生成多个矩阵乘法函数的候选项。为了让 Mojo 如何找到最佳的分块因子（tile factor），我们提供了一个评估器函数，Mojo 可以使用它来评估每个候选项。

```python
fn matmul_evaluator(funcs: Pointer[matmul_fn_sig_type], size: Int) -> Int:
    print("matmul_evaluator, number of candidates: ", size)

    let eval_begin: Int = now()

    # This size is picked at random, in real code we could use a real size
    # distribution here.
    let M = 512
    let N = 512
    let K = 512
    print("Optimizing for size:", M, "x", N, "x", K)

    var best_idx: Int = -1
    var best_time: Int = -1

    alias eval_iterations = 10
    alias eval_samples = 10

    var C = Matrix(M, N)
    var A = Matrix(M, K)
    var B = Matrix(K, N)
    let Cptr = Pointer[Matrix].address_of(C).address
    let Aptr = Pointer[Matrix].address_of(A).address
    let Bptr = Pointer[Matrix].address_of(B).address
    with Runtime() as rt:
        # Find the function that's the fastest on the size we're optimizing for
        for f_idx in range(size):
            let func = funcs.load(f_idx)

            @always_inline
            @parameter
            fn wrapper():
                func(C, A, B, rt)
            let cur_time = Benchmark(1, 100_000, 500_000_000, 1000_000_000).run[wrapper]()

            if best_idx < 0:
                best_idx = f_idx
                best_time = cur_time
            if best_time > cur_time:
                best_idx = f_idx
                best_time = cur_time

        let eval_end: Int = now()
        # Prevent matrices from being destroyed before we finished benchmarking them.
        _ = A.data
        _ = B.data
        _ = C.data
        print("Time spent in matmul_evaluator, ms:", (eval_end - eval_begin) // 1000000)
        print("Best candidate idx:", best_idx)
        return best_idx
```

最后，我们需要定义一个入口函数来简单地调用最佳候选者。

```python
fn matmul_autotune(C: Matrix, A: Matrix, B: Matrix, rt: Runtime):
    alias best_impl: matmul_fn_sig_type
    search[
        matmul_fn_sig_type,
        VariadicList(matmul_autotune_impl.__adaptive_set),
        matmul_evaluator -> best_impl
    ]()
    # Run the best candidate
    return best_impl(C, A, B, rt)
```

让我们对新的实现进行基准测试：

```python
benchmark_parallel[matmul_autotune](512, 512, 512, python_gflops)
```

> matmul_evaluator, number of candidates:  6 
>
> Optimizing for size: 512 x 512 x 512 
>
> Time spent in matmul_evaluator, ms: 8949 
>
> Best candidate idx: 2 
>
> 180.14895626059092 GFLOP/s, a 77052.192096131941 x speedup over Python

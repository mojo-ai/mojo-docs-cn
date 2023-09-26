# Mojo 中的 Mandelbrot 算法与 Python 绘图

Mojo 不仅适用于编写高性能代码，还可以让我们充分利用庞大的 Python 生态系统中的库和工具。借助无缝的 Python 互操作性，Mojo 可以充分发挥 Python 在特定领域的优势，特别是在 GUI 方面，而不会在关键代码性能上妥协。让我们来看看如何在 Mojo 中实现经典的 Mandelbrot 集合算法。

本教程展示了 Mojo 在两个方面的用法。首先， 它展示了 Mojo 可以用于开发不规则应用的高效程序。其次，它展示了我们如何利用 Python 来可视化结果。

{% reveal text="查看代码" %}

from benchmark import Benchmark
from complex import ComplexSIMD, ComplexFloat64
from math import iota
from python import Python
from runtime.llcl import num_cores, Runtime
from algorithm import parallelize, vectorize
from tensor import Tensor
from utils.index import Index
alias float_type = DType.float64
alias simd_width = 2 * simdwidthof[float_type]()

{% endreveal %}

首先设置一些参数，您可以尝试更改这些参数值以查看不同的效果：

```python
alias width = 960
alias height = 960
alias MAX_ITERS = 200

alias min_x = -2.0
alias max_x = 0.6
alias min_y = -1.5
alias max_y = 1.5
```

[Mandelbrot](https://en.wikipedia.org/wiki/Mandelbrot_set) 算法的核心涉及到需要为每个像素点计算一个迭代的复杂函数，直至它“逃离”半径为 2 的复数圆，并记录逃离所需的迭代次数：

$$
z_{i+1} = z_i^2 + c
$$

```python
# Compute the number of steps to escape.
def mandelbrot_kernel(c: ComplexFloat64) -> Int:
    z = c
    for i in range(MAX_ITERS):
        z = z * z + c
        if z.squared_norm() > 4:
            return i
    return MAX_ITERS


def compute_mandelbrot() -> Tensor[float_type]:
    # create a matrix. Each element of the matrix corresponds to a pixel
    t = Tensor[float_type](height, width)

    dx = (max_x - min_x) / width
    dy = (max_y - min_y) / height

    y = min_y
    for row in range(height):
        x = min_x
        for col in range(width):
            t[Index(row, col)] = mandelbrot_kernel(ComplexFloat64(x, y))
            x += dx
        y += dy
    return t
```

绘制逃离所需的迭代次数并赋予其一些颜色，将为我们提供典型的 Mandelbrot 集合图。为了渲染它，我们可以直接在 Mojo 中利用 Python 的 matplotlib 库！

```python
def show_plot(tensor: Tensor[float_type]):
    alias scale = 10
    alias dpi = 64

    np = Python.import_module("numpy")
    plt = Python.import_module("matplotlib.pyplot")
    colors = Python.import_module("matplotlib.colors")

    numpy_array = np.zeros((height, width), np.float64)

    for row in range(height):
        for col in range(width):
            numpy_array.itemset((col, row), tensor[col, row])

    fig = plt.figure(1, [scale, scale * height // width], dpi)
    ax = fig.add_axes([0.0, 0.0, 1.0, 1.0], False, 1)
    light = colors.LightSource(315, 10, 0, 1, 1, 0)

    image = light.shade(numpy_array, plt.cm.hot, colors.PowerNorm(0.3), "hsv", 0, 0, 1.5)
    plt.imshow(image)
    plt.axis("off")
    plt.show()

show_plot(compute_mandelbrot())
```

![mandelbrot result](https://docs.modular.com/mojo/notebooks/Mandelbrot_files/figure-html/cell-5-output-1.png)

## 向量化 Mandelbrot

前面我们展示了 Mandelbrot 算法的原生实现，但有两个方法可以加快它的运行速度。当已知一个像素点已经逃离时，我们可以提前停止循环的迭代，并利用 Mojo 对硬件的访问，通过向量化循环来同时计算多个像素。为此，我们将使用 `vectorize` 高阶生成器。

首先我们以向量化的方式来定义主迭代循环

```python
fn mandelbrot_kernel_SIMD[
    simd_width: Int
](c: ComplexSIMD[float_type, simd_width]) -> SIMD[float_type, simd_width]:
    """A vectorized implementation of the inner mandelbrot computation."""
    let cx = c.re
    let cy = c.im
    var x = SIMD[float_type, simd_width](0)
    var y = SIMD[float_type, simd_width](0)
    var y2 = SIMD[float_type, simd_width](0)
    var iters = SIMD[float_type, simd_width](0)

    var t: SIMD[DType.bool, simd_width] = True
    for i in range(MAX_ITERS):
        if not t.reduce_or():
            break
        y2 = y*y
        y = x.fma(y + y, cy)
        t = x.fma(x, y2) <= 4
        x = x.fma(x, cx - y2)
        iters = t.select(iters + 1, iters)
    return iters
```

上述函数以 `simd_width` 为参数，处理 simd_width 个像素。只有在向量通道内的所有像素都完成后，才会逃离。我们可以使用与上述相同的迭代循环，但这次我们将在每行内进行向量化处理。我们使用 `vectorize` 生成器来实现这个简单的函数调用。

```python
fn vectorized():
    let t = Tensor[float_type](height, width)

    @parameter
    fn worker(row: Int):
        let scale_x = (max_x - min_x) / width
        let scale_y = (max_y - min_y) / height

        @parameter
        fn compute_vector[simd_width: Int](col: Int):
            """Each time we oeprate on a `simd_width` vector of pixels."""
            let cx = min_x + (col + iota[float_type, simd_width]()) * scale_x
            let cy = min_y + row * scale_y
            let c = ComplexSIMD[float_type, simd_width](cx, cy)
            t.data().simd_store[simd_width](row * width + col, mandelbrot_kernel_SIMD[simd_width](c))

        # Vectorize the call to compute_vector where call gets a chunk of pixels.
        vectorize[simd_width, compute_vector](width)

    
    @parameter
    fn bench[simd_width: Int]():
        for row in range(height):
            worker(row)

    let vectorized = Benchmark().run[bench[simd_width]]() / 1e6
    print("Vectorized", ":", vectorized, "ms")

    try:
        _ = show_plot(t)
    except e:
        print("failed to show plot:", e.value)

vectorized()
```

> Vectorized : 12.177345000000001 ms

![vectorize result](https://docs.modular.com/mojo/notebooks/Mandelbrot_files/figure-html/cell-7-output-2.png)

## 并行化 Mandelbrot

虽然上述的向量化实现非常高效，但通过在列上进行并行化，我们可以获得更好的性能。在 Mojo 中，使用 `parallelize` 高阶函数实现这一点同样也很简单。只需要更改执行调用的函数即可。

```python
fn parallelized():
    let t = Tensor[float_type](height, width)

    @parameter
    fn worker(row: Int):
        let scale_x = (max_x - min_x) / width
        let scale_y = (max_y - min_y) / height

        @parameter
        fn compute_vector[simd_width: Int](col: Int):
            """Each time we oeprate on a `simd_width` vector of pixels."""
            let cx = min_x + (col + iota[float_type, simd_width]()) * scale_x
            let cy = min_y + row * scale_y
            let c = ComplexSIMD[float_type, simd_width](cx, cy)
            t.data().simd_store[simd_width](row * width + col, mandelbrot_kernel_SIMD[simd_width](c))

        # Vectorize the call to compute_vector where call gets a chunk of pixels.
        vectorize[simd_width, compute_vector](width)

    
    with Runtime() as rt:
        @parameter
        fn bench_parallel[simd_width: Int]():
            parallelize[worker](rt, height, height)

        let parallelized = Benchmark().run[bench_parallel[simd_width]]() / 1e6
        print("Parallelized:", parallelized, "ms")

    try:
        _ = show_plot(t)
    except e:
        print("failed to show plot:", e.value)

parallelized()
```

> Parallelized: 1.4245639999999999 ms

![parallelize result](https://docs.modular.com/mojo/notebooks/Mandelbrot_files/figure-html/cell-8-output-2.png)

## 基准测试

在本节中，我们将尺寸增加到 4096x4096 并进行 1000 次迭代以进行更大的测试，以测试 CPU 的性能。

```python
fn compare():
    let t = Tensor[float_type](height, width)

    @parameter
    fn worker(row: Int):
        let scale_x = (max_x - min_x) / width
        let scale_y = (max_y - min_y) / height

        @parameter
        fn compute_vector[simd_width: Int](col: Int):
            """Each time we oeprate on a `simd_width` vector of pixels."""
            let cx = min_x + (col + iota[float_type, simd_width]()) * scale_x
            let cy = min_y + row * scale_y
            let c = ComplexSIMD[float_type, simd_width](cx, cy)
            t.data().simd_store[simd_width](row * width + col, mandelbrot_kernel_SIMD[simd_width](c))

        # Vectorize the call to compute_vector where call gets a chunk of pixels.
        vectorize[simd_width, compute_vector](width)

    
    @parameter
    fn bench[simd_width: Int]():
        for row in range(height):
            worker(row)

    let vectorized = Benchmark().run[bench[simd_width]]() / 1e6
    print("Number of threads:", num_cores())
    print("Vectorized:", vectorized, "ms")

    # Parallelized
    with Runtime() as rt:
        @parameter
        fn bench_parallel[simd_width: Int]():
            parallelize[worker](rt, height, height)

        let parallelized = Benchmark().run[bench_parallel[simd_width]]() / 1e6
        print("Parallelized:", parallelized, "ms")
        print("Parallel speedup:", vectorized / parallelized)

    _ = t # Make sure tensor isn't destroyed before benchmark is finished
```

```python
compare()
```

>Number of threads: 16
>
> Vectorized: 12.171849 ms
>
> Parallelized: 1.3043979999999999 ms
>
> Parallel speedup: 9.3313919524562294


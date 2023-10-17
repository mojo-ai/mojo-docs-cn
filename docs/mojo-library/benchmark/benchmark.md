# benchmark

实现了用于运行时基准测试的 Benchmark 类。

你可以从 `benchmark` 包中导入这些 API。例如：

```python
from benchmark import Benchmark
```

## `Benchmark`

一个用于基准测试的测试框架。

该类允许对给定的函数（作为参数传递）进行基准测试，并配置各种基准测试参数，如预热迭代次数、最大迭代次数、最小和最大运行时间。

**Fields**：

- **num_warmup** (`Int`)：在主要基准测试循环之前执行的预热迭代次数。

- **max_iters** (`Int`)：在主要基准测试循环中执行的最大迭代次数。

- **min_time_ns** (`Int`)：在主要基准测试循环中花费的最小时间（以纳秒为单位）。

- **max_time_ns** (`Int`)：在主要基准测试循环中花费的最大时间（以纳秒为单位）。

**Functions**：

### `__init__`

```python
__init__(inout self: Self, num_warmup: Int, max_iters: Int, min_time_ns: Int, max_time_ns: Int)
```

构造一个新的基准测试对象。

给定一个函数，基准测试对象将对其进行基准测试，直到经过了 min_time_ns 的时间，并且达到了 max_time_ns 或 max_iters 的限制。

**Args**：

- **num_warmup** (`Int`)：在开始基准测试之前运行的预热迭代次数（默认为2）。

- **max_iters** (`Int`)：最大运行迭代次数（默认为100,000）。

- **min_time_ns** (`Int`)：基准测试时间的上限，单位为纳秒（默认为500毫秒）。

- **max_time_ns** (`Int`)：基准测试时间的下限，单位为纳秒（默认为1秒）。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

### `__moveinit__`

```python
__moveinit__(inout self: Self, owned existing: Self)
```

### `run`

```python
run[func: fn() capturing -> None](self: Self) -> Int
```

对给定的函数进行基准测试。

基准测试会一直持续，直到经过 min_time_ns 的时间，并且达到 max_time_ns 或 max_iters。

**Parameters**：

- **func** (`fn() capturing -> None`)：要进行基准测试的函数。

**Returns**：

func 的平均执行时间，以纳秒为单位。

## `clobber_memory`

```python
clobber_memory()
```

强制将所有待处理的内存写入刷新到内存中。

这样确保编译器不会优化掉它认为不必要的内存写入。

实际上，这个操作对内存读取和写入起到了屏障的作用。

## `keep`

```python
keep(val: Bool)
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Args**：

- **val** (`Bool`)：不要优化掉的值。

```python
keep(val: Int)
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Args**：

- **val** (`Int`)：不要优化掉的值。

```python
keep[type: DType, simd_width: Int](val: SIMD[type, simd_width])
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Parameters**：

- **type** (`DType`)：输入和输出SIMD向量的数据类型。

- **simd_width** (`Int`)：输入和输出SIMD向量的宽度。

**Args**：

- **val** (`SIMD[type, simd_width]`)：不要优化掉的值。

```python
keep[type: DType](val: DTypePointer[type])
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Parameters**：

- **type** (`DType`)：输入的类型。

**Args**：

- **val** (`DTypePointer[type]`)：不要优化掉的值。

```python
keep[type: AnyType](val: Pointer[*"type"])
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Parameters**：

- **type**(`AnyType`)：输入的类型。

**Args**：

- **val** (`Pointer[*"type"]`)：不要优化掉的值。

```python
keep[type: AnyType](inout *val: "type")
```

向编译器提供一个提示，不要优化掉变量的使用。

这在基准测试中非常有用，可以避免编译器删除要进行基准测试的代码，因为该变量在副作用方面没有被使用。

**Parameters**：

- **type**(`AnyType`)：输入的类型。

**Args**：

- **val** (`*"type"`)：不要优化掉的值。


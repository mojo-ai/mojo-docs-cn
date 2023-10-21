# random 模块

提供用于生成随机数的函数。

你可以从 `random` 包中导入这些 API，例如：

```python
from random import seed
```

## `seed`
`seed()`

使用当前时间来初始化随机数生成器。

`seed(a: Int)`
使用提供的值来初始化随机数生成器。

**参数（Args）**：

- **a** (`Int`): 种子值。

## `random_float64`
`random_float64(min: SIMD[f64, 1], max: SIMD[f64, 1]) -> SIMD[f64, 1]`

从指定范围内返回一个随机的 `Float64` 数。

**参数（Args）**：

- **min** (`SIMD[f64, 1]`): 范围内的最小值（默认为0.0）。
- **max** (`SIMD[f64, 1]`): 范围内的最大值（默认为1.0）。

**返回（Returns）**：

指定范围内的随机数。



## `random_si64`
`random_si64(min: SIMD[si64, 1], max: SIMD[si64, 1]) -> SIMD[si64, 1]`

从指定范围内返回一个随机的Int64数。

**参数（Args）**：

- **min** (`SIMD[si64, 1]`): 范围内的最小值。
- **max** (`SIMD[si64, 1]`): 范围内的最大值。

**返回（Returns）**：

指定范围内的随机数。



## `random_ui64`
`random_ui64(min: SIMD[ui64, 1], max: SIMD[ui64, 1]) -> SIMD[ui64, 1]`

从指定范围内返回一个随机的 `UInt64` 数。

**参数（Args）**：

- **min** (`SIMD[ui64, 1]`): 范围内的最小值。
- **max** (`SIMD[ui64, 1]`): 范围内的最大值。

**返回（Returns）**：

指定范围内的随机数。



## `randint`
`randint[type: DType](ptr: DTypePointer[type], size: Int, low: Int, high: Int)`

用均匀分布的随机数填充内存，范围为[low, high]。

**约束（Constraints）：**

数据类型应为整数。

**参数（Parameters）**：

- **type** (`DType`): 指针的数据类型。

**参数（Args）**：

- **ptr** (`DTypePointer[type]`): 要填充的内存区域的指针。
- **size** (`Int`): 要填充的元素数量。
- **low** (`Int`): 随机数的最小值。
- **high** (`Int`): 随机数的最大值。



## `rand`
`rand[type: DType](ptr: DTypePointer[type], size: Int)`

用均匀分布的随机值填充内存。

**参数（Parameters）**：

- **type** (`DType`): 指针的数据类型。

**参数（Args）**：

- **ptr** (`DTypePointer[type]`): 要填充的内存区域的指针。
- **size** (`Int`): 要填充的元素数量。



`rand[type: DType](*shape: Int) -> Tensor[type]`

构建一个具有指定形状并填充随机元素的新张量。

**参数（Parameters）**：

- **type** (`DType`): 张量的数据类型。

**参数（Args）**：

- **shape** (`*Int`): 张量的形状。

**返回（Returns）**：

一个具有指定形状并填充随机元素的新张量。



`rand[type: DType](owned shape: TensorShape) -> Tensor[type]`

构建一个具有指定形状并填充随机元素的新张量。

**参数（Parameters）**：

- **type** (`DType`): 张量的数据类型。

**参数（Args）**：

- **shape** (`TensorShape`): 张量的形状。

**返回（Returns）**：

一个具有指定形状并填充随机元素的新张量。



`rand[type: DType](owned spec: TensorSpec) -> Tensor[type]`

构建一个具有指定规格并填充随机元素的新张量。

**参数（Parameters）**：

- **type** (`DType`): 张量的数据类型。

**参数（Args）**：

- **spec** (`TensorSpec`): 张量的规格。

**返回（Returns）**：

一个具有指定规格并填充随机元素的新张量。



## `randn_float64`
`randn_float64(mean: SIMD[f64, 1], variance: SIMD[f64, 1]) -> SIMD[f64, 1]`

从正态分布（均值为 mean，方差为 variance）中抽取一个随机的双精度浮点数。

**参数（Args）**：

- **mean** (`SIMD[f64, 1]`): 正态分布的均值。
- **variance** (`SIMD[f64, 1]`): 正态分布的方差。

**返回（Returns）**：

从正态分布中抽取的随机float64。



## `randn`
`randn[type: DType](ptr: DTypePointer[type], size: Int, mean: SIMD[f64, 1], variance: SIMD[f64, 1])`

用从正态分布（均值为 mean，方差为 variance）中抽取的随机值填充内存。

**约束（Constraints）：**

数据类型应为浮点数。

**参数（Parameters）**：

- **type** (`DType`): 指针的数据类型。

**参数（Args）**：

- **ptr** (`DTypePointer[type]`): 要填充的内存区域的指针。
- **size** (`Int`): 要填充的元素数量。
- **mean** (`SIMD[f64, 1]`): 正态分布的均值。
- **variance** (`SIMD[f64, 1`]): 正态分布的方差。

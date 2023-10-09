# tensor

实现 `Tensor`（张量）类型。

示例：

```python
from tensor import Tensor, TensorSpec, TensorShape
from utils.index import Index
from random import rand

let height = 256
let width = 256
let channels = 3

# Create the tensor of dimensions height, width, channels
# and fill with random values.
let image = rand[DType.float32](height, width, channels)

# Declare the grayscale image.
let spec = TensorSpec(DType.float32, height, width)
var gray_scale_image = Tensor[DType.float32](spec)

# Perform the RGB to grayscale transform.
for y in range(height):
  for x in range(width):
    let r = image[y,x,0]
    let g = image[y,x,1]
    let b = image[y,x,2]
    gray_scale_image[Index(y,x)] = 0.299 * r + 0.587 * g + 0.114 * b

print(gray_scale_image.shape().__str__())
```

## `Tensor`

具备基础数据并支持 DType 参数化的张量类型。

**Parameters**：

- **dtype** (`DType`)：张量的基础元素类型。

**Functions**：

### `__init__`

```python
__init__(inout self: Self)
```

TensorShape 默认初始值设定项。

```python
__init__(inout self: Self, *dims: Int)
```

采用提供的 `dims` 分配张量。

**Args**：

- **dims** (`*Int`)：张量维度。

```python
__init__(inout self: Self, owned shape: TensorShape)
```

采用提供的 `shape` 分配张量。

**Args**：

- **shape** (`TensorShape`)：张量形状

```python
__init__(inout self: Self, owned spec: TensorSpec)
```

采用提供的 `spec` 分配张量。

**Args**：

- **spec** (`TensorSpec`)：张量规范。

```python
__init__(inout self: Self, owned ptr: DTypePointer[dtype], owned shape: TensorShape)
```

从提供的指针和形状初始化张量。调用方放弃传入的指针的所有权。

**Args**：

- **ptr** (`DTypePointer[dtype]`)：数据指针。
- **shape** (`TensorShape`)：张量形状。

```python
__init__(inout self: Self, owned ptr: DTypePointer[dtype], owned spec: TensorSpec)
```

从提供的指针和规范初始化张量。调用方放弃传入的指针的所有权。

**Args**：

- **ptr** (`DTypePointer[dtype]`)：数据指针。
- **spec** (`TensorSpec`)：张量规范。

### `__copyinit__`

```python
__copyinit__(inout self: Self, other: Self)
```

创建现有张量的深层拷贝。

**Args**：

- **other** (`Self`)：将从中复制的张量。

### `__moveinit__`

```python
__moveinit__(inout self: Self, owned existing: Self)
```

张量的移动初始值设定项。

**Args**：

- **existing** (`Self`)：要移动的张量。

### `__del__`

```python
__del__(owned self: Self)
```

删除规范并释放任何拥有的内存。

### `__getitem__`

```python
__getitem__(self: Self, index: Int) -> SIMD[dtype, 1]
```

获取指定索引处的值。

**Args**：

- **index** (`Int`)：要检索的值索引。

**Returns**：

指定索引处的值。

```python
__getitem__(self: Self, *indices: Int) -> SIMD[dtype, 1]
```

获取指定指示处的值。

**Args**：

- **indices** (`Int`)：要检索的值指示。

**Returns**：

指定指示处的值。

```python
__getitem__(self: Self, indices: VariadicList[Int]) -> SIMD[dtype, 1]
```

获取指定指示处的值。

**Args**：

- **indices** (`VariadicList[Int]`)：要检索的值指示。

**Returns**：

指定指示处的值。

```python
__getitem__[len: Int](self: Self, indices: StaticIntTuple[len]) -> SIMD[dtype, 1]
```

获取指定指示处的 SIMD 值。

**Parameters**：

- **len** (`Int`)：指示的长度。

**Args**：

- **indices** (`StaticIntTuple[len]`)：要检索的值指示。

**Returns**：

指定指示处的值。

### `__setitem__`

```python
__setitem__(inout self: Self, index: Int, val: SIMD[dtype, 1])
```

设置指定索引处的值。

**Args**：

- **index** (`Int`)：要设置的值的索引。
- **val** (`SIMD[dtype, 1]`)：要存储的值。

```python
__setitem__(inout self: Self, indices: VariadicList[Int], val: SIMD[dtype, 1])
```

设置指定指示处的值。

**Args**：

- **indices** (`VariadicList[Int]`)：要设置的值的指示。
- **val** (`SIMD[dtype, 1]`)：要存储的值。

```python
__setitem__[len: Int](inout self: Self, indices: StaticIntTuple[len], val: SIMD[dtype, 1])
```

设置指定指示处的值。

**Parameters**：

- **len** (`Int`)：指示的长度。

**Args**：

- **indices** (`StaticIntTuple[len]`)：要设置的值的指示。
- **val** (`SIMD[dtype, 1]`)：要存储的值。

### `__eq__`

```python
__eq__(self: Self, other: Self) -> Bool
```

如果两个张量相同，则返回 True，否则返回 False。

**Args**：

- **other** (`Self`)：另一个要比较的张量。

**Returns**：

如果两个张量相同，则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, other: Self) -> Bool
```

如果两个张量不相同，则返回 True，否则返回 False。

**Args**：

- **other** (`Self`)：另一个要比较的张量。

**Returns**：

如果两个张量不相同，则为 True，否则为 False。

### `data`

```python
data(self: Self) -> DTypePointer[dtype]
```

获取指向张量的基础数据指针。

**Returns**：

张量的基础数据指针。

### `type`

```python
type(self: Self) -> DType
```

获取张量的基础 DType。

**Returns**：

张量的基础 DType。

### `rank`

```python
rank(self: Self) -> Int
```

获取张量的秩。

**Returns**：

张量的秩。

### `num_elements`

```python
num_elements(self: Self) -> Int
```

获取张量中元素的总数。

**Returns**：

张量中元素的总数。

### `bytecount`

```python
bytecount(self: Self) -> Int
```

获取张量的总字节数。

**Returns**：

张量的总字节数。

### `spec`

```python
spec(self: Self) -> TensorSpec
```

获取张量的规范。

**Returns**：

张量的基础张量规范。

### `shape`

```python
shape(self: Self) -> TensorShape
```

获取张量的形状。

**Returns**：

张量的基础张量形状。

### `dim`

```python
dim(self: Self, idx: Int) -> Int
```

获取指定索引处的维度。

**Args**：

- **idx** (`Int`)：维度索引。

**Returns**：

指定索引处的维度。

### `simd_load`

```python
simd_load[simd_width: Int](self: Self, index: Int) -> SIMD[dtype, simd_width]
```

获取指定索引处的 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。

**Args**：

- **index** (`Int`)：要检索的值索引。

**Returns**：

指定索引处的 SIMD 值。

```python
simd_load[simd_width: Int](self: Self, *indices: Int) -> SIMD[dtype, simd_width]
```

获取指定指示处的 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。

**Args**：

- **indices** (`Int`)：要检索的值指示。

**Returns**：

指定指示处的 SIMD 值。

```python
simd_load[simd_width: Int](self: Self, indices: VariadicList[Int]) -> SIMD[dtype, simd_width]
```

获取指定指示处的 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。

**Args**：

- **indices** (`VariadicList[Int]`)：要检索的值指示。

**Returns**：

指定指示处的 SIMD 值。

```python
simd_load[simd_width: Int, len: Int](self: Self, indices: StaticIntTuple[len]) -> SIMD[dtype, simd_width]
```

获取指定指示处的 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。
- **len** (`Int`)：指示的长度。

**Args**：

- **indices** (`StaticIntTuple[len]`)：要检索的值指示。

**Returns**：

指定指示处的 SIMD 值。

### `simd_store`

```python
simd_store[simd_width: Int](inout self: Self, index: Int, val: SIMD[dtype, simd_width])
```

在指定索引处设置 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。

**Args**：

- **index** (`Int`)：要设置的值索引。
- **val** (`SIMD[dtype, simd_width]`)：要存储的 SIMD 值。

```python
simd_store[simd_width: Int](inout self: Self, indices: VariadicList[Int], val: SIMD[dtype, simd_width])
```

在指定的指示处设置 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。

**Args**：

- **indices** (`VariadicList[Int]`)：要设置的值指示。
- **val** (`SIMD[dtype, simd_width]`)：要存储的 SIMD 值。

```python
simd_store[simd_width: Int, len: Int](inout self: Self, indices: StaticIntTuple[len], val: SIMD[dtype, simd_width])
```

在指定的指示处设置 SIMD 值。

**Parameters**：

- **simd_width** (`Int`)：矢量的 SIMD 宽度。
- **len** (`Int`)：指示的长度。

**Args**：

- **indices** (`StaticIntTuple[len]`)：要设置的值指示。
- **val** (`SIMD[dtype, simd_width]`)：要存储的 SIMD 值。

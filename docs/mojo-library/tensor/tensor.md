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

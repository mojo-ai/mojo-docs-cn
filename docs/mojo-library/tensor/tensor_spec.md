# tensor_spec

实现 `TensorSpec` 类型。

您可以从 `tensor`（张量）包中导入这些 API。例如：

```python
from tensor import TensorSpec
```

## `TensorSpec`

张量形状和 dtype 的空间高效表示。此结构体实现值语义并拥有其基础数据。

**Fields**：

- **shape** (`TensorShape`)：规范的基础形状。
  
**Functions**：

### `__init__`

```python
__init__(inout self: Self)
```

TensorShape 的默认初始化。

```python
__init__(inout self: Self, type: DType, *shapes: Int)
```

从提供的 dtype 和 shapes 初始化 TensorSpec。

**Args**：

- **type** (`DType`)：规范的 dtype。
- **shapes** (`*Int`)：用于初始化形状的 shapes。

```python
__init__(inout self: Self, type: DType, shapes: VariadicList[Int])
```

从提供的 dtype 和 shapes 初始化 TensorSpec。

**Args**：

- **type** (`DType`)：规范的 dtype。
- **shapes** (`VariadicList[Int]`)：用于初始化形状的 shapes。

```python
__init__(inout self: Self, type: DType, owned shape: TensorShape)
```

从提供的 dtype 和 shape 初始化 TensorSpec。

**Args**：

- **type** (`DType`)：规范的 dtype。
- **shapes** (`TensorShape`)：用于初始化形状的 shapes。

### `__copyinit__`

```python
__copyinit__(inout self: Self, other: Self)
```

创建现有规范的深层拷贝。

**Args**：

- **other** (`Self`)：要复制的规范。

### `__moveinit__`

```python
__moveinit__(inout self: Self, owned existing: Self)
```

规范的移动初始化。

**Args**：

- **existing** (`Self`)：要移动的规范。

### `__del__`

```python
__del__(owned self: Self)
```

### `__getitem__`

```python
__getitem__(self: Self, index: Int) -> Int
```

获取指定索引处的维度。

**Args**：

- **index** (`Int`)：维度索引。

**Returns**：

指定索引处的维度。

### `__eq__`

```python
__eq__(self: Self, other: Self) -> Bool
```

如果两个值相同，则返回 True，否则返回 False。

**Args**：

- **other** (`Self`)：另一个要比较的 TensorSpec。

**Returns**：

如果两个规格相同，则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, other: Self) -> Bool
```

如果两个值不相同，则返回 True，否则返回 False。

**Args**：

- **other** (`Self`)：另一个要比较的 TensorSpec。

**Returns**：

如果两个规格不相同，则为 True，否则为 False。

### `rank`

```python
rank(self: Self) -> Int
```

获取规范的秩。

**Returns**：

规范的秩。

### `dtype`

```python
dtype(self: Self) -> DType
```

获取规范的 DType。

**Returns**：

规范的 DType。

### `num_elements`

```python
num_elements(self: Self) -> Int
```

获取规范中元素的总数。

**Returns**：

规范中元素的总数。

### `bytecount`

```python
bytecount(self: Self) -> Int
```

获取总字节计数。

**Returns**：

总字节计数。

### `__repr__`

```python
__repr__(self: Self) -> String
```

返回规范的字符串表示形式。

**Returns**：

规范的字符串表示形式。

### `__str__`

```python
__str__(self: Self) -> String
```

返回规范的字符串表示形式。

**Returns**：

规范的字符串表示形式。

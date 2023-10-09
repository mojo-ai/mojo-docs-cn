# tensor_shape

实现 `TensorShape` 类型。

您可以从 `tensor`（张量）包中导入这些 API。例如：

```python
from tensor import TensorShape
```

## `TensorShape`

张量形状的空间高效表示形式。此结构体实现值语义并拥有其基础数据。

**Functions**

### `__init__`

```python
__init__(inout self: Self)
```

TensorShape 的默认初始化。

```python
__init__(inout self: Self, *shapes: Int)
```

根据提供的值初始化 TensorShape。

**Args**：

- **shapes** (`*Int`)：用于初始化形状。

```python
__init__(inout self: Self, shapes: VariadicList[Int])
```

根据提供的值初始化 TensorShape。

**Args**：

- **shapes** (`VariadicList[Int]`)：用于初始化形状。

### `__copyinit__`

```python
__copyinit__(inout self: Self, other: Self)
```

创建现有形状的深层拷贝。

**Args**：

- **other** (`Self`)：要复制的形状。

### `__moveinit__`

```python
__moveinit__(inout self: Self, owned existing: Self)
```

形状的移动初始化。

**Args**：

- **existing** (`Self`)：要移动的形状。

### `__del__`

```python
__del__(owned self: Self)
```

删除形状并释放任何拥有的内存。

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

- **other** (`Self`)：另一个要比较的 TensorShape。

**Returns**：

如果两个形状相同，则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, other: Self) -> Bool
```

如果两个值不相同，则返回 True，否则返回 False。

**Args**：

- **other** (`Self`)：另一个要比较的 TensorShape。

**Returns**：

如果两个形状不相同，则为 True，否则为 False。

### `rank`

```python
rank(self: Self) -> Int
```

获取形状的秩。

**Returns**：

形状的排名。

### `num_elements`

```python
num_elements(self: Self) -> Int
```

获取形状中元素的总数。

**Returns**：

形状中元素的总数。

### `__repr__`

```python
__repr__(self: Self) -> String
```

返回形状的字符串表示形式。

**Returns**：

形状的字符串表示形式。

### `__str__`

```python
__str__(self: Self) -> String
```

返回形状的字符串表示形式。

**Returns**：

形状的字符串表示形式。

# vector

定义若干类似矢量的类。

您可以从 `utils` 包导入这些 API。例如：

```python
from utils.vector import InlinedFixedVector
```

## `InlinedFixedVector`

`InlinedFixedVector` 类型是具有小向量优化的动态分配向量。

`InlinedFixedVector` 不会调整大小或实现边界检查，它使用小向量大小（静态已知）和动态（编译时未知）插槽（slots）数进行初始化，当被释放时，它会释放其内存。

TODO：一旦我们有了特征（traits），它应调用它的元素析构函数。

此数据结构对于在编译时不知道所需元素数的应用很有用，但一旦在运行时可知，就可以保证等于或小于某个容量。

**Parameters**：

- **size** (`Int`)：静态的小矢量尺寸。
- **type** (`AnyType`)：元素的类型。

**Aliases**：

- `static_size = _26x27_size`
- `static_data_type = StaticTuple[size, *"type"]`

**Fields**：

- **static_data** (`StaticTuple[size, *"type"]`)：底层静态存储，用于小矢量。
- **dynamic_data** (`Pointer[*"type"]`)：底层动态存储，用于增长大矢量。
- **current_size** (`Int`)：矢量中的元素数。
- **capacity** (`Int`)：无需调整矢量大小即可容纳在矢量中的元素数量。

**Functions**：

### `__init__`

```python
__init__(inout self: Self, capacity: Int)
```

构造具有给定容量的 `InlinedFixedVector `。

`capacity - size` 用于动态分配。

**Args**：

- **capacity** (`Int`)：向量请求的容量。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

创建浅拷贝（它不复制数据）。

**Args**：

- **existing** (`Self`)：要复制的 `InlinedFixedVector `。

### `__getitem__`

```python
__getitem__(self: Self, i: Int) -> *"type"
```

获取给定索引处的向量元素。

**Args**：

- **i** (`Int`)：元素的索引。

**Returns**：

给定索引处的元素。

### `__setitem__`

```python
__setitem__(inout self: Self, i: Int, *value: "type")
```

在给定索引处设置向量元素。

**Args**：

- **i** (`Int`)：元素的索引。
- **value** (`*"type"`)：要分配的值。

### `deepcopy`

```python
deepcopy(self: Self) -> Self
```

创建此矢量的深层拷贝。

**Returns**：

此向量的拷贝。

### `append`

```python
append(inout self: Self, *value: "type")
```

向此向量追加一个值。

**Args**：

- **value** (`*"type"`)：要追加的值。

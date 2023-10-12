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

### `__len__`

```python
__len__(self: Self) -> Int
```

获取矢量中的元素数。

**Returns**：

矢量中的元素数。

### `clear`

```python
clear(inout self: Self)
```

清除矢量中的元素。

## `UnsafeFixedVector`

`UnsafeFixedVector ` 是动态分配的矢量，它不调整大小或进行边界检查。

它使用动态（在编译时未知）插槽（slots）数进行初始化，当被释放时，它会释放其内存。

TODO：一旦我们有了特征（traits），它就应调用它的元素析构函数。

此数据结构对于在编译时不知道所需元素数的应用很有用，但一旦在运行时可知，就可以保证等于或小于某个容量。

**Parameters**：

- **type** (`AnyType`)：元素的类型。

**Fields**：

- **data** (`Pointer[*"type"]`)：矢量的基础存储。
- **size** (`Int`)：矢量中的元素数。
- **capacity** (`Int`)：矢量中可以容纳的元素数量。

**Functions**：

### `__init__`

```python
__init__(inout self: Self, capacity: Int)
```

构造具有给定容量的 `UnsafeFixedVector`。

**Args**：

- **capacity** (`Int`)：向量的请求容量。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

创建浅拷贝（它不复制数据）。

**Args**：

- **existing** (`Self`)：要复制的 `UnsafeFixedVector`。

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
__setitem__(self: Self, i: Int, *value: "type")
```

在给定索引处设置向量元素。

**Args**：

- **i** (`Int`)：元素的索引。
- **value** (`*"type"`)：要分配的值。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取矢量中的元素数。

**Returns**：

矢量中的元素数。

### `append`

```python
append(inout self: Self, *value: "type")
```

向此向量追加一个值。

**Args**：

- **value** (`*"type"`)：要追加的值。

### `clear`

```python
clear(inout self: Self)
```

清除矢量中的元素。

## `DynamicVector`

`DynamicVector` 类型是动态分配的矢量。

它支持根据需要从后部进行推入（push）和弹出（pop），调整基础存储的大小。释放后，它会释放内存。

TODO：一旦我们有了特征（traits），它就应调用它的元素析构函数。
TODO：它应执行边界检查。

**Parameters**：

- **type** (`AnyType`)：元素的类型。

**Fields**：

- **data** (`Pointer[*"type"]`)：矢量的基础存储。
- **size** (`Int`)：矢量中的元素数。
- **capacity** (`Int`)：无需调整矢量大小即可容纳在矢量中的元素数量。

**Functions**：

### `__init__`

```python
__init__(inout self: Self)
```

构造一个空向量。

```python
__init__(inout self: Self, capacity: Int)
```

构造具有给定容量的向量。

**Args**：

- **capacity** (`Int`)：向量的请求容量。

```python
__init__(inout self: Self, pointer: Pointer[*"type"], size: Int)
```

使用给定的指针和大小构造向量。

**Args**：

- **pointer** (`Pointer[*"type"]`)：指向缓冲区的指针。
- **size** (`Int`)：缓冲区的大小。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

创建浅拷贝（它不复制数据）。

**Args**：

- **existing** (`Self`)：要复制的 `DynamicVector`。

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

### `__len__`

```python
__len__(self: Self) -> Int
```

获取矢量中的元素数。

**Returns**：

矢量中的元素数。

### `resize`

```python
resize(inout self: Self, size: Int)
```

将矢量大小调整为给定的新尺寸。

如果新尺寸小于当前尺寸，末尾的元素将被丢弃。如果新尺寸大于当前尺寸，则向量将附加未初始化的元素至最大请求尺寸。

**Args**：

- **size** (`Int`)：新的尺寸

### `deepcopy`

```python
deepcopy(self: Self) -> Self
```

创建此矢量的深层拷贝。

**Returns**：

此向量的副本。

### `reserve`

```python
reserve(inout self: Self, new_capacity: Int)
```

保留请求的容量。

如果当前容量大于或相等，则不进行操作。否则，将重新分配存储并移动数据。

**Args**：

- **new_capacity** (`Int`)：新的容量。

### `push_back`

```python
push_back(inout self: Self, *value: "type")
```

向此向量追加一个值。

**Args**：

- **value** (`*"type"`)：要追加的值。

### `pop_back`

```python
pop_back(inout self: Self) -> *"type"
```

从此向量的后部弹出一个值。

**Returns**：

弹出的值。

### `clear`

```python
clear(inout self: Self)
```

清除矢量中的元素。

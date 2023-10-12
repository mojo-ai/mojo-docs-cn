# static_tuple

实现静态大小的统一容器 `StaticTuple`。

您可以从 `utils` 包导入这些 API。例如：

```python
from utils.static_tuple import StaticTuple
```

## `StaticTuple`

包含同类型元素的静态大小的元组类型。

**Parameters**：

- **size** (`Int`)：元组的大小。
- **_element_type** (`AnyType`)：元组中元素的类型。

**Aliases**：

- `element_type = _90x31__element_type`
- `type = array<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$int"::@Int> size, "value">, _element_type>`

**Fields**：

- **array** (`array<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$int"::@Int> size, "value">, _element_type>`)：静态元组的基础存储。

**Functions**：

### `__init__`

```python
__init__() -> Self
```

构造一个空的（未定义的）元组。

**Returns**：

元组。

```python
__init__(*elems: _element_type) -> Self
```

在给定一组参数的情况下构造静态元组。

**Args**：

- **elems** (`*_element_type`)：元素类型。

**Returns**：

元组。

```python
__init__(values: VariadicList[_element_type]) -> Self
```

使用指定的值创建元组常量。

**Args**：

- **values** (`VariadicList[_element_type]`)：值列表。

**Returns**：

填充了值的元组。

```python
__init__(array: array<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$int"::_Int> size, "value">, _element_type>) -> Self
```

### `__getitem__`

```python
__getitem__[index: Int](self: Self) -> _element_type
```

返回给定索引处元组的值。

**Parameters**：

- **index** (`Int`)：元组的索引。

**Returns**：

指定位置处的值。

```python
__getitem__(self: Self, index: Int) -> _element_type
```

返回给定动态索引处元组的值。

**Args**：

- **index** (`Int`)：元组的索引。

**Returns**：

指定位置处的值。

### `__setitem__`

```python
__setitem__[index: Int](inout self: Self, val: _element_type)
```

将单个值存储在元组中的指定索引处。

**Parameters**：

- **index** (`Int`)：元组的索引。

**Args**：

- **val** (`_element_type`)：要存储的值。

```python
__setitem__(inout self: Self, index: Int, val: _element_type)
```

将单个值存储在元组中指定的动态索引处。

**Args**：

- **index** (`Int`)：元组的索引。
- **val** (`_element_type`)：要存储的值。

### `__len__`

```python
__len__(self: Self) -> Int
```

返回数组的长度。这是一个已知的常量值。

**Returns**：

列表的大小。

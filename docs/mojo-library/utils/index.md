# index

实现 `StaticIntTuple`，其用于表示 N-D 指示。

您可以从 `utils` 包导入这些 API。例如

```python
from utils.index import StaticIntTuple
```

**Aliases**：

* `mlir_bool = scalar<bool>`

`StaticIntTuple`

实现与大小无关索引函数的基础结构体。

**Parameters**：

- **size** (`Int`)：元组的大小。

**Fields**：

- **data** (`StaticTuple[size, Int]`)：元组值的基础存储。

**Functions**：

`__init__`

```python
__init__() -> Self
```

构造给定大小的静态整型元组。

**Returns**：

构造的元组。

```python
__init__(value: index) -> Self
```

构造给定元素值的大小为 1 的静态整型元组。

**Args**：

- **value** (`index`)：初始值。

**Returns**：

构造的元组。

```python
__init__(*elems: Int) -> Self
```

在给定一组参数的情况下构造一个静态整型元组。

**Args**：

- **elems** (`*Int`)：用于构造元组的元素。

**Returns**：

构造的元组。

```python
__init__(elem: Int) -> Self
```

在给定一组参数的情况下构造一个静态整型元组。

**Args**：

- **elems** (`Int`)：添加至元组中的元素。

**Returns**：

构造的元组。

```python
__init__(values: VariadicList[Int]) -> Self
```

使用指定的值创建元组常量。

**Args**：

- **values** (`VariadicList[Int]`)：值列表。

**Returns**：

填充值的元组。

```python
__init__(values: DimList) -> Self
```

使用指定的值创建元组常量。

**Args**：

- **values** (`DimList`)：值列表。

**Returns**：

填充值的元组。

```python
__init__(data: StaticTuple[size, Int]) -> Self
```

`__getitem__`

```python
__getitem__(self: Self, index: Int) -> Int
```

按索引从元组中获取元素。

**Args**：

- **index** (`Int`)：元素索引。

**Returns**：

元组元素值。

`__setitem__`

```python
__setitem__[index: Int](inout self: Self, val: Int)
```

在给定静态索引处设置元组中的元素。

**Parameters**：

- **index** (`Int`)：元素索引。

**Args**：

- **val** (`Int`)：要存储的值。

```python
__setitem__(inout self: Self, index: Int, val: Int)
```

在元组中的给定索引处设置一个元素。

**Args**：

- **index** (`Int`)：元素索引。
- **val** (`Int`)：要存储的值。

`__lt__`

```python
__lt__(self: Self, rhs: Self) -> Bool
```

使用 LT 比较两个元组。

如果 lhs 的所有相应元素都小于 rhs，则该元组小于另一个元组。

注意：这不是词法比较。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

`__le__`

```python
__le__(self: Self, rhs: Self) -> Bool
```

使用 LE 比较两个元组。

如果 lhs 的所有相应元素都小于或等于 rhs，则该元组小于或等于另一个元组。

注意：这不是词法比较。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

`__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

将此元组与另一个元组进行比较以判断是否相等。

如果所有相应的元素相等，则两个元组相等。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

`__ne__`

```python
__ne__(self: Self, rhs: Self) -> Bool
```

将此元组与另一个元组进行比较以判断是否不相等。

如果 LHS 中至少一个元素不等于 RHS 中的相应元素，则两个元组不相等。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

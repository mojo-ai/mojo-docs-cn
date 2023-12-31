# index

实现 `StaticIntTuple`，其用于表示 N-D 指示。

您可以从 `utils` 包导入这些 API。例如：

```python
from utils.index import StaticIntTuple
```

**Aliases**：

* `mlir_bool = scalar<bool>`

## `StaticIntTuple`

实现与大小无关索引函数的基础结构体。

**Parameters**：

- **size** (`Int`)：元组的大小。

**Fields**：

- **data** (`StaticTuple[size, Int]`)：元组值的基础存储。

**Functions**：

### `__init__`

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

### `__getitem__`

```python
__getitem__(self: Self, index: Int) -> Int
```

按索引从元组中获取元素。

**Args**：

- **index** (`Int`)：元素索引。

**Returns**：

元组元素值。

### `__setitem__`

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

### `__lt__`

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

### `__le__`

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

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

将此元组与另一个元组进行比较以判断是否相等。

如果所有相应的元素相等，则两个元组相等。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

### `__ne__`

```python
__ne__(self: Self, rhs: Self) -> Bool
```

将此元组与另一个元组进行比较以判断是否不相等。

如果 LHS 中至少一个元素不等于 RHS 中的相应元素，则两个元组不相等。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

### `__gt__`

```python
__gt__(self: Self, rhs: Self) -> Bool
```

使用 GT 比较两个元组。

如果 lhs 的所有相应元素都大于 rhs，则该元组大于另一个元组。

注意：这不是词法比较。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

### `__ge__`

```python
__ge__(self: Self, rhs: Self) -> Bool
```

使用 GE 比较两个元组。

如果 lhs 的所有相应元素都大于或等于 rhs，则该元组大于或等于另一个元组。

**Args**：

- **rhs** (`Self`)：右侧元组。

**Returns**：

比较结果。

### `__add__`

```python
__add__(self: Self, rhs: Self) -> Self
```

执行逐元素整型加法。

**Args**：

- **rhs** (`Self`)：右侧操作数。

**Returns**：

生成的索引元组。

### `__sub__`

```python
__sub__(self: Self, rhs: Self) -> Self
```

执行逐元素整型减法。

**Args**：

- **rhs** (`Self`)：右侧操作数。

**Returns**：

生成的索引元组。

### `__mul__`

```python
__mul__(self: Self, rhs: Self) -> Self
```

执行逐元素整型乘法。

**Args**：

- **rhs** (`Self`)：右侧操作数。

**Returns**：

生成的索引元组。

### `__floordiv__`

```python
__floordiv__(self: Self, rhs: Self) -> Self
```

执行逐元素整型除法（向下取整）。

**Args**：

- **rhs** (`Self`)：右侧操作数。

**Returns**：

生成的索引元组。

### `__len__`

```python
__len__(self: Self) -> Int
```

返回元组的大小。

**Returns**：

元组大小。

### `as_tuple`

```python
as_tuple(self: Self) -> StaticTuple[size, Int]
```

将 StaticIntTuple 转换为 StaticTuple。

**Returns**：

对应的 StaticTuple 对象。

### `flattened_length`

```python
flattened_length(self: Self) -> Int
```

返回元组的平展长度。

**Returns**：

元组的平展长度。

### `remu`

```python
remu(self: Self, rhs: Self) -> Self
```

执行逐元素整型无符号取模。

**Args**：

- **rhs** (`Self`)：右侧操作数。

**Returns**：

生成的索引元组。

## `Index`

```python
Index(x: Int) -> StaticIntTuple[1]
```

从给定值构造一维索引。

**Args**：

- **x** (`Int`)：初始值。

**Returns**：

构造的 StaticIntTuple。

```python
Index(x: Int, y: Int) -> StaticIntTuple[2]
```

从给定值构造二维索引。

**Args**：

- **x** (`Int`)：第一个初始值。
- **y** (`Int`)：第二个初始值。

**Returns**：

构造的 StaticIntTuple。

```python
Index(x: Int, y: Int, z: Int) -> StaticIntTuple[3]
```

从给定值构造三维索引。

**Args**：

- **x** (`Int`)：第一个初始值。
- **y** (`Int`)：第二个初始值。
- **z** (`Int`)：第三个初始值。

**Returns**：

构造的 StaticIntTuple。

```python
Index(x: Int, y: Int, z: Int, w: Int) -> StaticIntTuple[4]
```

从给定值构造四维索引。

**Args**：

- **x** (`Int`)：第一个初始值。
- **y** (`Int`)：第二个初始值。
- **z** (`Int`)：第三个初始值。
- **w** (`Int`)：第四个初始值。

**Returns**：

构造的 StaticIntTuple。

```python
Index(x: Int, y: Int, z: Int, w: Int, v: Int) -> StaticIntTuple[5]
```

从给定值构造五维索引。

**Args**：

- **x** (`Int`)：第一个初始值。
- **y** (`Int`)：第二个初始值。
- **z** (`Int`)：第三个初始值。
- **w** (`Int`)：第四个初始值。
- **v** (`Int`)：第五个初始值。

**Returns**：

构造的 StaticIntTuple。

## `product`

```python
product[size: Int](tuple: StaticIntTuple[size], end_idx: Int) -> Int
```

计算元组中给定索引范围的元素乘积。

**Parameters**：

- **size** (`Int`)：元组的大小。

**Args**：

- **tuple** (`StaticIntTuple[size]`)：要获取乘积的元组。
- **end_idx** (`Int`)：结束索引。

**Returns**：

给定范围内所有元组元素的乘积。

```python
product[size: Int](tuple: StaticIntTuple[size], start_idx: Int, end_idx: Int) -> Int
```

计算给定索引范围内元组中值的乘积。

**Parameters**：

- **size** (`Int`)：元组的大小。

**Args**：

- **tuple** (`StaticIntTuple[size]`)：要获取乘积的元组。
- **start_idx** (`Int`)：区域的起始索引。
- **end_idx** (`Int`)：区域的结束索引。

**Returns**：

给定范围内所有元组元素的乘积。

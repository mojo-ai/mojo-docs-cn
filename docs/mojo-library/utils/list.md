# list

用于处理静态列表和可变参数列表的工具包。

您可以从 `utils` 包导入这些 API。例如：

```python
from utils.list import Dim
```

## `Dim`

使用可选整数建模的静态或动态维度。

此类用于表示可选的静态维度。当值存在时，维度具有该静态值。当值不存在时，维度是动态的。

**Aliases**：

- `type = Variant[i1, Int]`

**Fields**：

- **value** (`Variant[i1, Int]`)：指示维度是动态的布尔值，或维度的静态值。

**Functions**：

### `__init__`

```python
__init__(value: Int) -> Self
```

创建静态已知的维度。

**Args**：

- **value** (`Int`)：静态维度值。

**Returns**：

具有静态值的维度。

```python
__init__(value: index) -> Self
```

创建静态已知的维度。

**Args**：

- **value** (`index`)：静态维度值。

**Returns**：

具有静态值的维度。

```python
__init__() -> Self
```

创建动态维度。

**Returns**：

无静态值的维度值。

```python
__init__(value: Variant[i1, Int]) -> Self
```

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

如果维度具有静态值，则返回 True。

**Returns**：

维度是否具有静态值。

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

比较两个维度是否相等。

**Args**：

- **rhs** (`Self`)：另一个维度。

**Returns**：

如果维度相同，则为 True。

### `__mul__`

```python
__mul__(self: Self, rhs: Self) -> Self
```

两个维度相乘。

如果其中任何一个未知，则结果也是未知的。

**Args**：

- **rhs** (`Self`)：另一个维度。

**Returns**：

两个维度的乘积。

### `has_value`

```python
has_value(self: Self) -> Bool
```

如果维度具有静态值，则返回 True。

**Returns**：

维度是否具有静态值。

### `is_dynamic`

```python
is_dynamic(self: Self) -> Bool
```

如果维度具有动态值，则返回 True。

**Returns**：

维度是否动态。

### `get`

```python
get(self: Self) -> Int
```

获取静态维度值。

**Returns**：

静态维度值。

### `is_multiple`

```python
is_multiple[alignment: Int](self: Self) -> Bool
```

检查维度是否对齐。

**Parameters**：

- **alignment** (`Int`)：对齐要求。

**Returns**：

维度是否对齐。

## `DimList`

此类型表示维度列表。每个维度可以有一个静态值，也可以没有值（动态维度）。

**Fields**：

- **value** (`VariadicList[Dim]`)：维度列表的基础存储。

**Functions**：

### `__init__`

```python
__init__(values: VariadicList[Dim]) -> Self
```

从给定的值列表创建维度列表。

**Args**：

- **values** (`VariadicList[Dim]`)：初始维度值列表。

**Returns**：

维度列表。

```python
__init__(*values: Dim) -> Self
```

从给定的维度值创建维度列表。

**Args**：

- **values** (`*Dim`)：初始维度值。

**Returns**：

维度列表。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取 `DimList` 的大小。

**Returns**：

`DimList` 中的元素数。

### `at`

```python
at[i: Int](self: Self) -> Dim
```

获取指定索引处的维度。

**Parameters**：

- **i** (`Int`)：维度索引。

**Returns**：

指定索引处的维度。

### `product`

```python
product[length: Int](self: Self) -> Dim
```

计算列表中所有维度的乘积。

如果有任何动态的，则结果为动态维度值。

**Parameters**：

- **length** (`Int`)：列表中的元素数。

**Returns**：

所有维度的乘积。

### `product_range`

```python
product_range[start: Int, end: Int](self: Self) -> Dim
```

计算列表中某个维度范围的乘积。

如果范围中的任何内容是动态的，则结果为动态维度值。

**Parameters**：

- **start** (`Int`)：起始索引。
- **end** (`Int`)：结束索引。

**Returns**：

所有维度的乘积。

### `contains`

```python
contains[length: Int](self: Self, value: Dim) -> Bool
```

确定维度列表是否包含指定的维度值。

**Parameters**：

- **length** (`Int`)：列表中的元素数。

**Args**：

- **value** (`Dim`)：要查找的值。

**Returns**：

如果列表包含指定值的维度，则为 True。

### `all_known`

```python
all_known[length: Int](self: Self) -> Bool
```

确定是否所有维度都是静态已知的。

**Parameters**：

- **length** (`Int`)：列表中的元素数。

**Returns**：

如果所有维度都具有静态值，则为 True。

### `create_unknown`

```python
create_unknown[length: Int]() -> Self
```

创建所有动态维度值的维度列表。

**Parameters**：

- **length** (`Int`)：列表中的元素数。

**Returns**：

所有动态维度值的列表。

## `VariadicList`

用于访问可变参函数的参数的类。提供函数参数的“列表”视图，以便可以访问参数列表的大小和每个单独的参数。

**Parameters**：

- **type** (`AnyType`)：列表中元素的类型。

**Aliases**：

- `StorageType = variadic<*"type">`

**Fields**：

- **value** (`variadic<*"type">`)：可变参数列表的基础存储。

**Functions**：

### `__init__`

```python
__init__(*value: *"type") -> Self
```

从参数的可变列表构造 `VariadicList `。

**Args**：

- **value** (`**"type"`)：用于构造可变列表的可变参数列表。

**Returns**：

构造的 `VariadicList`。

```python
__init__(*value: *"type") -> Self
```

从可变参数类型构造 `VariadicList `。

**Args**：

- **value** (`**"type"`)：用于构造可变列表的可变参数列表。

**Returns**：

构造的 `VariadicList`。

### `__getitem__`

```python
__getitem__(self: Self, index: Int) -> *"type"
```

获取可变列表中的单个元素。

**Args**：

- **index** (`Int`)：要在列表中访问的元素的索引。

**Returns**：

列表中与给定索引对应的元素。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取列表的大小。

**Returns**：

可变列表中的元素数。

## `VariadicListMem`



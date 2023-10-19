# simd

实现 SIMD 结构。

这些是 Mojo 内置的，因此您无需导入它们。

**Aliases**：

- `Int8 = SIMD[si8, 1]`：表示 8 位有符号标量整数。
- `UInt8 = SIMD[ui8, 1]`：表示 8 位无符号标量整数。
- `Int16 = SIMD[si16, 1]`：表示 16 位有符号标量整数。
- `UInt16 = SIMD[ui16, 1]`：表示 16 位无符号标量整数。
- `Int32 = SIMD[si32, 1]`：表示 32 位有符号标量整数。
- `UInt32 = SIMD[ui32, 1]`：表示 32 位无符号标量整数。
- `Int64 = SIMD[si64, 1]`：表示 64 位有符号标量整数。
- `UInt64 = SIMD[ui64, 1]`：表示 64 位无符号标量整数。
- `Float16 = SIMD[f16, 1]`：表示 16 位浮点值。
- `Float32 = SIMD[f32, 1]`：表示 32 位浮点值。
- `Float64 = SIMD[f64, 1]`：表示 64 位浮点值。

## `SIMD`

表示由硬件矢量元素支持的小矢量。

SIMD 允许跨多个矢量数据元素执行单个指令。

**Constraints**：

SIMD 矢量的大小为正数，且幂为2。

**Parameters**：

- **type** (`DType`)：SIMD 矢量元素的数据类型。
- **size** (`Int`)：SIMD 矢量的大小。

**Aliases**：

- element_type = _65x13_type`

**Fields**：

- **value** (`simd<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$int"::@Int> size, "value">, #lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> type, "value">>`)：矢量的基础存储。

**Functions**：

### `__init__`

```python
__init__() -> Self
```

SIMD 矢量的默认初始设定项。

默认情况下，SIMD 向量初始化为全零。

**Returns**：

元素为 0 的 SIMD 矢量。

```python
__init__(value: Int) -> Self
```

使用整型初始化 SIMD 向量。

整数值分布在 SIMD 矢量的所有元素中。

**Args**：

- **value** (`Int`)：输入值。

**Returns**：

其元素具有指定值的 SIMD 矢量。

```python
__init__(value: Bool) -> Self
```

使用布尔值初始化 SIMD 矢量。

布尔值分布在 SIMD 矢量的所有元素上。

**Args**：

- **value** (`Bool`)：布尔值。

**Returns**：

其元素具有指定值的 SIMD 矢量。

```python
__init__(value: simd<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$int"::_Int> size, "value">, #lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>) -> Self
```

使用基础 mlir 值初始化 SIMD 矢量。

**Args**：

- **value** (`simd<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$int"::_Int> size, "value">, #lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>`)：输入值。

**Returns**：

其元素具有指定值的 SIMD 矢量。

```python
__init__(*elems: SIMD[type, 1]) -> Self
```

通过可变参数元素列表构造 SIMD 向量。

如果只有一个输入值，则会将其拼接到 SIMD 矢量的所有元素。否则，输入值将分配给 SIMD 矢量的相应元素。

**Constraints**：

输入值的数量为 1 或等于 SIMD 矢量的大小。

**Args**：

- **elems** (`*SIMD[type, 1]`)：用于构造 SIMD 矢量的元素的可变参数列表。

**Returns**：

构造的 SIMD 向量。

```python
__init__(value: FloatLiteral) -> Self
```

使用 FP64 值初始化 SIMD 矢量。

输入值在 SIMD 矢量的所有元素上叠加（broadcast 方式）。

**Args**：

- **value** (`FloatLiteral`)：输入值。

**Returns**：

元素具有指定值的 SIMD 向量。

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

将 SIMD 矢量转换为布尔标量值。

**Returns**：

如果 SIMD 矢量中的所有元素都不为零，则为 True，否则为 False。

### `__getitem__`

```python
__getitem__(self: Self, idx: Int) -> SIMD[type, 1]
```

从向量中获取元素。

**Args**：

- **idx** (`Int`)：元素索引。

**Returns**：

处于位置 `idx` 的值。

### `__setitem__`

```python
__setitem__(inout self: Self, idx: Int, val: SIMD[type, 1])
```

设置矢量中的元素。

**Args**：

- **idx** (`Int`)：元素索引。
- **val** (`SIMD[type, 1]`)：要设置的值。

```python
__setitem__(inout self: Self, idx: Int, val: scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>)
```

设置矢量中的元素。

**Args**：

- **idx** (`Int`)：要设置的索引。
- **val** (`scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>`)：要设置的值。

### `__neg__`

```python
__neg__(self: Self) -> Self
```

定义一元 `-` 操作。

**Returns**：

对 SIMD 向量取否。

### `__pos__`

```python
__pos__(self: Self) -> Self
```

定义一元 `+` 操作。

**Returns**：

SIMD 向量。

### `__invert__`

```python
__invert__(self: Self) -> Self
```

返回 `~self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Returns**：

`~self` 的值。

### `__lt__`

```python
__lt__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用小于方式比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] < rhs[i]` 表达式。

### `__le__`

```python
__le__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用小于或相等的方式来比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] <= rhs[i]` 表达式。

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用等于方式比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] == rhs[i]` 表达式。

### `__ne__`

```python
__ne__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用不等于方式比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] != rhs[i]` 表达式。

### `__gt__`

```python
__gt__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用大于方式比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] > rhs[i]` 表达式。

### `__ge__`

```python
__ge__(self: Self, rhs: Self) -> SIMD[bool, size]
```

使用大于等于方式比较两个 SIMD 向量。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

具有相同大小的新的布尔 SIMD 向量，其位于 `i` 处的元素为 True 或 False 依赖于 `self[i] >= rhs[i]` 表达式。

### `__add__`

```python
__add__(self: Self, rhs: Self) -> Self
```

计算 `self + rhs`。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

一个新向量，其位于 `i` 处的元素计算为 `self[i] + rhs[i]`。

### `__sub__`

```python
__sub__(self: Self, rhs: Self) -> Self
```

计算 `self - rhs`。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

一个新向量，其位于 `i` 处的元素计算为 `self[i] - rhs[i]`。

### `__mul__`

```python
__mul__(self: Self, rhs: Self) -> Self
```

计算 `self * rhs`。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

一个新向量，其位于 `i` 处的元素计算为 `self[i] * rhs[i]`。

### `__truediv__`

```python
__truediv__(self: Self, rhs: Self) -> Self
```

计算 `self / rhs`。

**Args**：

- **rhs** (`Self`)：rhs 操作数。

**Returns**：

一个新向量，其位于 `i` 处的元素计算为 `self[i] / rhs[i]`。

### `__floordiv__`

```python
__floordiv__(self: Self, rhs: Self) -> Self
```

返回向下取整的 self 和 rhs 的除法。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **rhs** (`Self`)：要除的值。

**Returns**：

`floor(self / rhs)` 值。

### `__mod__`

```python
__mod__(self: Self, rhs: Self) -> Self
```

返回 self 除以 rhs 的余数。

**Args**：

- **rhs** (`Self`)：要除的值。

**Returns**：

将 self 除以 rhs 的余数。

### `__pow__`

```python
__pow__(self: Self, rhs: Int) -> Self
```

计算提升到输入整数值为幂的向量。

**Args**：

- **rhs** (`Int`)：指数值。

**Returns**：

一个 SIMD 向量，其中每个元素都提升到指定指数值的幂。

```python
__pow__[rhs_type: DType](self: Self, rhs: SIMD[rhs_type, size]) -> Self
```

计算提升到输入整数值为幂的向量。

**Parameters**：

- **rhs_type** (`DType`)：SIMD 矢量（rhs）的 `dtype`。

**Args**：

- **rhs** (`SIMD[rhs_type, size]`)：指数值。

**Returns**：

一个 SIMD 向量，其中每个元素都提升到指定指数值的幂。

### `__lshift__`

```python
__lshift__(self: Self, rhs: Self) -> Self
```

返回 `self << rhs`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self << rhs`。

### `__rshift__`

```python
__rshift__(self: Self, rhs: Self) -> Self
```

返回 `self >> rhs`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self >> rhs`。

### `__and__`

```python
__and__(self: Self, rhs: Self) -> Self
```

TBD

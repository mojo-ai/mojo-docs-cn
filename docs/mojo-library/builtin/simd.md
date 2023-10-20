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

SIMD 矢量的大小为正数，且幂为 2。

**Parameters**：

- **type** (`DType`)：SIMD 矢量元素的数据类型。
- **size** (`Int`)：SIMD 矢量的大小。

**Aliases**：

- `element_type = _65x13_type`

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

返回 `self & rhs`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self & rhs`。

### `__or__`

```python
__or__(self: Self, rhs: Self) -> Self
```

返回 `self | rhs`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self | rhs`。

### `__xor__`

```python
__xor__(self: Self, rhs: Self) -> Self
```

返回 `self ^ rhs`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self ^ rhs`。

### `__radd__`

```python
__radd__(self: Self, value: Self) -> Self
```

返回 `value + self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value + self`。

### `__rsub__`

```python
__rsub__(self: Self, value: Self) -> Self
```

返回 `value - self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value - self`。

### `__rmul__`

```python
__rmul__(self: Self, value: Self) -> Self
```

返回 `value * self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value * self`。

### `__rtruediv__`

```python
__rtruediv__(self: Self, value: Self) -> Self
```

返回 `value / self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value / self`。

### `__rfloordiv__`

```python
__rfloordiv__(self: Self, value: Int) -> Int
```

返回 `value // self`。

**Args**：

- **value** (`Int`)：另一个值。

**Returns**：

`value // self`。

### `__rmod__`

```python
__rmod__(self: Self, value: Int) -> Int
```

返回 `value % self`。

**Args**：

- **value** (`Int`)：另一个值。

**Returns**：

`value % self`。

### `__rlshift__`

```python
__rlshift__(self: Self, value: Self) -> Self
```

返回 `value << self`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value << self`。

### `__rrshift__`

```python
__rrshift__(self: Self, value: Self) -> Self
```

返回 `value >> self`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value >> self`。

### `__rand__`

```python
__rand__(self: Self, value: Self) -> Self
```

返回 `value & self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value & self`。

### `__ror__`

```python
__ror__(self: Self, value: Self) -> Self
```

返回 `value | self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value | self`。

### `__rxor__`

```python
__rxor__(self: Self, value: Self) -> Self
```

返回 `value ^ self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value ^ self`。

### `__iadd__`

```python
__iadd__(inout self: Self, rhs: Self)
```

执行就地（in-place）相加。

向量中位于 `i` 的每个元素进行 `self[i] + rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行加法操作的 rhs。

### `__isub__`

```python
__isub__(inout self: Self, rhs: Self)
```

执行就地（in-place）相减。

向量中位于 `i` 的每个元素进行 `self[i] - rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行减法操作的 rhs。

### `__imul__`

```python
__imul__(inout self: Self, rhs: Self)
```

执行就地（in-place）相乘。

向量中位于 `i` 的每个元素进行 `self[i] * rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行乘法操作的 rhs。

### `__itruediv__`

```python
__itruediv__(inout self: Self, rhs: Self)
```

执行就地（in-place）相除（浮点数）。

向量中位于 `i` 的每个元素进行 `self[i] / rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行除法操作的 rhs。

### `__ifloordiv__`

```python
__ifloordiv__(inout self: Self, rhs: Self)
```

执行就地（in-place）相除（向下取整）。

向量中位于 `i` 的每个元素进行 `self[i] // rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行除法操作的 rhs。

### `__imod__`

```python
__imod__(inout self: Self, rhs: Self)
```

执行就地（in-place）取余。

向量中位于 `i` 的每个元素进行 `self[i] % rhs[i]` 运算。

**Args**：

- **rhs** (`Self`)：执行取余操作的 rhs。

### `__ipow__`

```python
__ipow__(inout self: Self, rhs: Int)
```

执行就地（in-place）幂运算。

向量中位于 `i` 的每个元素进行 `pow(self[i], rhs)` 运算。

**Args**：

- **rhs** (`Int`)：执行幂运算的 rhs。

### `__ilshift__`

```python
__ilshift__(inout self: Self, rhs: Self)
```

计算 `self << rhs` 并将结果保存在 `self`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__irshift__`

```python
__irshift__(inout self: Self, rhs: Self)
```

计算 `self >> rhs` 并将结果保存在 `self`。

**Constraints**：

SIMD 矢量的元素类型必须是整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__iand__`

```python
__iand__(inout self: Self, rhs: Self)
```

计算 `self & rhs` 并将结果保存在 `self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ixor__`

```python
__ixor__(inout self: Self, rhs: Self)
```

计算 `self ^ rhs` 并将结果保存在 `self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ior__`

```python
__ior__(inout self: Self, rhs: Self)
```

计算 `self | rhs` 并将结果保存在 `self`。

**Constraints**：

SIMD 矢量的元素类型必须是布尔值或整型。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取 SIMD 矢量的长度。

**Returns**：

SIMD 矢量的长度。

### `splat`

```python
splat(x: Bool) -> Self
```

创建新 SIMD 向量，其元素与输入值相同的。

**Args**：

- **x** (`Bool`)：输入值。

**Returns**：

元素与输入值相同的新 SIMD 向量。

```python
splat(x: SIMD[type, 1]) -> Self
```

创建新 SIMD 向量，其元素与输入值相同的。

**Args**：

- **x** (`SIMD[type, 1]`)：输入标量值。

**Returns**：

元素与输入值相同的新 SIMD 向量。

### `cast`

```python
cast[target: DType](self: Self) -> SIMD[target, size]
```

将 SIMD 矢量的元素强制转换为目标元素类型。

**Parameters**：

- **target** (`DType`)：DType 目标。

**Returns**：

一个新的 SIMD 向量，其元素已转换为目标元素类型。

### `__int__`

```python
__int__(self: Self) -> Int
```

强制转换为 Int 值。如果存在小数分量，则该值将被截断为零。

**Constraints**：

SIMD 矢量的大小必须为 1。

**Returns**：

整型值。

### `to_int`

```python
to_int(self: Self) -> Int
```

强制转换为 Int 值。如果存在小数分量，则该值将被截断为零。

**Constraints**：

SIMD 矢量的大小必须为 1。

**Returns**：

SIMD 矢量中单个整数元素的值。

### `fma`

```python
fma(self: Self, multiplier: Self, accumulator: Self) -> Self
```

执行乘法累加运算，即：`self*multiplier + accumulator`。

**Args**：

- **multiplier** (`Self`)：进行乘法运算的值。
- **accumulator** (`Self`)：进行累加运算的值。

**Returns**：

一个新的向量，其位于 `i` 的元素进行 `self[i]*multiplier[i] + accumulator[i]` 运算。

### `shuffle`

```python
shuffle[*mask: Int](self: Self) -> Self
```

使用指定的掩码（permutation），将当前向量值与 `other` 值随机混合。

**Parameters**：

- **mask** (`*Int`)：要在随机混合中使用的排列。

**Returns**：

长度为 `len` 的新向量，其中位于 `i` 的值为 `(self)[permutation[i]]`。

```python
shuffle[*mask: Int](self: Self, other: Self) -> Self
```

使用指定的掩码（permutation），将当前向量值与 `other` 值随机混合。

**Parameters**：

- **mask** (`*Int`)：要在随机混合中使用的排列。

**Args**：

- **other** (`Self`)：另一个要随机混合的向量。

**Returns**：

长度为 `len` 的新向量，其中位于 `i` 的值为 `(self+other)[permutation[i]]`。

### `slice`

```python
slice[output_width: Int](self: Self, offset: Int) -> SIMD[type, output_width]
```

返回具有给定偏移量且指定宽度的矢量切片。

**Constraints**：

`output_width + offset` 不得超过此 SIMD 矢量的大小。

**Parameters**：

- **output_width** (`Int`)：输出 SIMD 矢量大小。

**Args**：

- **offset** (`Int`)：切片的给定偏移量。

**Returns**：

元素映射到 `self[offset:offset+output_width]` 的新向量。

### `min`

```python
min(self: Self, other: Self) -> Self
```

计算两个向量之间的元素最小值。

**Args**：

- **other** (`Self`)：另一个 SIMD 向量。

**Returns**：

一个新的 SIMD 向量，其位于 `i` 的每个元素为 `min(self[i], other[i])`。

### `max`

```python
max(self: Self, other: Self) -> Self
```

计算两个向量之间的元素最大值。

**Args**：

- **other** (`Self`)：另一个 SIMD 向量。

**Returns**：

一个新的 SIMD 向量，其位于 `i` 的每个元素为 `max(self[i], other[i])`。

### `reduce`

```python
reduce[func: fn[DType, Int](SIMD[*(0,0), *(0,1)], SIMD[*(0,0), *(0,1)]) capturing -> SIMD[*(0,0), *(0,1)]](self: Self) -> SIMD[type, 1]
```

使用提供的归约运算符约简矢量。

**Parameters**：

- **func** (`fn[DType, Int](SIMD[*(0,0), *(0,1)], SIMD[*(0,0), *(0,1)]) capturing -> SIMD[*(0,0), *(0,1)]`)：要应用于此 SIMD 中的元素的归约函数。

**Returns**：

一个新的标量，它是所有矢量元素的约简。

### `reduce_max`

```python
reduce_max(self: Self) -> SIMD[type, 1]
```

使用 `max` 运算符约简向量。

**Constraints**：

向量的元素类型必须是整型或浮点型。

**Returns**：

向量的最大元素。

### `reduce_min`

```python
reduce_min(self: Self) -> SIMD[type, 1]
```

使用 `min` 运算符约简向量。

**Constraints**：

向量的元素类型必须是整型或浮点型。

**Returns**：

向量的最小元素。

### `reduce_add`

```python
reduce_add(self: Self) -> SIMD[type, 1]
```

使用 `add` 运算符约简向量。

**Returns**：

所有矢量元素的总和。

### `reduce_mul`

```python
reduce_mul(self: Self) -> SIMD[type, 1]
```

使用 `mul` 运算符约简向量。

**Constraints**：

向量的元素类型必须是整型或浮点型。

**Returns**：

所有矢量元素的乘积。

### `reduce_and`

```python
reduce_and(self: Self) -> Bool
```

使用 `and` 运算符约简布尔向量。

**Constraints**：

向量的元素类型必须是布尔类型。

**Returns**：

如果向量中的所有元素都为 True，则为 True，否则为 False。

### `reduce_or`

```python
reduce_or(self: Self) -> Bool
```

使用 `or` 运算符约简布尔向量。

**Constraints**：

向量的元素类型必须是布尔类型。

**Returns**：

如果向量中的任何元素为 True，则为 True，否则为 False。

### `select`

```python
select[result_type: DType](self: Self, true_case: SIMD[result_type, size], false_case: SIMD[result_type, size]) -> SIMD[result_type, size]
```

根据 SIMD 矢量的当前布尔值选择 `true_case` 或 `false_case` 的值。

**Parameters**：

- **result_type** (`DType`)：输入和输出 SIMD 矢量的元素类型。

**Args**：

- **true_case** (`SIMD[result_type, size]`)：如果位置值为 True，则选择此值。
- **false_case** (`SIMD[result_type, size]`)：如果位置值为 False，则选择此值。

**Returns**：

形式为 `[true_case[i] if elem else false_case[i] in enumerate(self)]` 的新向量。

### `rotate_left`

```python
rotate_left[shift: Int](self: Self) -> Self
```

通过 `shift` 元素将 SIMD 矢量的元素向左移（rotate 方式）。

**Constraints**：

`-size <= shift < size`

**Parameters**：

- **shift** (`Int`)：将 SIMD 矢量的元素向左移（rotate 方式）的位置数。

**Returns**：

SIMD 矢量通过 `shift` 元素向左移（rotate 方式）。

### `rotate_right`

```python
rotate_right[shift: Int](self: Self) -> Self
```

通过 `shift` 元素将 SIMD 矢量的元素向右移（rotate 方式）。

**Constraints**：

`-size < shift <= size`

**Parameters**：

- **shift** (`Int`)：将 SIMD 矢量的元素向右移（rotate 方式）的位置数。

**Returns**：

SIMD 矢量通过 `shift` 元素向右移（rotate 方式）。

### `shift_left`

```python
shift_left[shift: Int](self: Self) -> Self
```

通过 `shift` 元素将 SIMD 矢量的元素向左移动（无 rotate，用零填充）。

**Constraints**：

`0 <= shift <= size`

**Parameters**：

- **shift** (`Int`)：将 SIMD 矢量的元素向左移（无 rotate，用零填充）的位置数。

**Returns**：

SIMD 矢量通过移位元素向左移（无 rotate，用零填充）。

### `shift_right`

```python
shift_right[shift: Int](self: Self) -> Self
```

通过 `shift` 元素将 SIMD 矢量的元素向右移动（无 rotate，用零填充）。

**Constraints**：

`0 <= shift <= size`

**Parameters**：

- **shift** (`Int`)：将 SIMD 矢量的元素向右移（无 rotate，用零填充）的位置数。

**Returns**：

SIMD 矢量通过移位元素向右移（无 rotate，用零填充）。

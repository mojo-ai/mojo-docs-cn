# int

实现 Int 类。

这些均为 Mojo 内置，因此您无需导入它们。

## `Int`

此类型表示整数值。

**Fields**：

- **value** (`index`)：整数值的基础存储。

**Functions**：

### `__init__`

```python
__init__() -> Self
```

默认构造函数。

**Returns**：

构造的 Int 对象。

```python
__init__(value: Self) -> Self
```

从另一个 Int 值构造 Int。

**Args**：

- **value** (`Self`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: index) -> Self
```

从给定的索引值构造 Int。

**Args**：

- **value** (`index`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: scalar<si16>) -> Self
```

从给定的 Int16 值构造 Int。

**Args**：

- **value** (`scalar<si16>`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: scalar<si32>) -> Self
```

从给定的 Int32 值构造 Int。

**Args**：

- **value** (`scalar<si32>`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: scalar<si64>) -> Self
```

从给定的 Int64 值构造 Int。

**Args**：

- **value** (`scalar<si64>`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: scalar<index>) -> Self
```

从给定的索引值构造 Int。

**Args**：

- **value** (`scalar<index>`)：初始化值。

**Returns**：

构造的 Int 对象。

```python
__init__(value: IntLiteral) -> Self
```

从给定的 IntLiteral 值构造 Int。

**Args**：

- **value** (`IntLiteral`)：初始化值。

**Returns**：

构造的 Int 对象。

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

将此 Int 转换为 Bool。

**Returns**：

如果值等于 0，则为 False，否则为 True。

### `__neg__`

```python
__neg__(self: Self) -> Self
```

返回 -self。

**Returns**：

-self 值。

### `__pos__`

```python
__pos__(self: Self) -> Self
```

返回 +self。

**Returns**：

+self 值。

### `__invert__`

```python
__invert__(self: Self) -> Self
```

返回 ~self。

**Returns**：

~self 值。

### `__lt__`

```python
__lt__(self: Self, rhs: Self) -> Bool
```

使用 LT 比较 Int 与 RHS。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 小于 RHS Int，则为 True，否则为 False。

### `__le__`

```python
__le__(self: Self, rhs: Self) -> Bool
```

使用 LE 比较此 Int 与 RHS。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 小于或等于 RHS Int，则为 True，否则为 False。

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

使用 EQ 比较此 Int 与 RHS。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 等于 RHS Int 则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, rhs: Self) -> Bool
```

使用 NE 比较此 Int 与 RHS 。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 不等于 RHS Int，则为 True，否则为 False。

### `__gt__`

```python
__gt__(self: Self, rhs: Self) -> Bool
```

使用 GT 比较此 Int 与 RHS。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 大于 RHS Int，则为 True，否则为 False。

### `__ge__`

```python
__ge__(self: Self, rhs: Self) -> Bool
```

使用 GE 比较此 Int 与 RHS。

**Args**：

- **rhs** (`Self`)：另一个要比较的 Int。

**Returns**：

如果此 Int 大于或等于 RHS Int 则为 True，否则为 False。

### `__add__`

```python
__add__(self: Self, rhs: Self) -> Self
```

返回 `self + rhs`。

**Args**：

- **rhs** (`Self`)：要添加的值。

**Returns**：

`self + rhs` 的值。

### `__sub__`

```python
__sub__(self: Self, rhs: Self) -> Self
```

返回 `self - rhs`。

**Args**：

- **rhs** (`Self`)：要减去的值。

**Returns**：

`self - rhs` 的值。

### `__mul__`

```python
__mul__(self: Self, rhs: Self) -> Self
```

返回 `self * rhs`。

**Args**：

- **rhs** (`Self`)：要乘以的值。

**Returns**：

`self * rhs` 的值。

### `__truediv__`

```python
__truediv__(self: Self, rhs: Self) -> SIMD[f64, 1]
```

返回 `self` 和 `rhs` 的浮点除法。

**Args**：

- **rhs** (`Self`)：要除以的值。

**Returns**：

`float(self)/float(rhs)` 的值。

### `__floordiv__`

```python
__floordiv__(self: Self, rhs: Self) -> Self
```

返回 `self` 和 `rhs` 的除法，四舍五入到最接近的整数。

**Args**：

- **rhs** (`Self`)：要除以的值。

**Returns**：

`floor(self/rhs)` 的值。

### `__mod__`

```python
__mod__(self: Self, rhs: Self) -> Self
```

返回除以 rhs 的 self 余数。

**Args**：

- **rhs** (`Self`)：要除以的值。

**Returns**：

将 self 除以 rhs 的余数。

### `__pow__`

```python
__pow__(self: Self, rhs: Self) -> Self
```

返回 pow(self， rhs)。

使用 Russian Peasant 方法计算整数的幂。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`pow(self, rhs)` 值。

### `__lshift__`

```python
__lshift__(self: Self, rhs: Self) -> Self
```

返回 `self << rhs`。

**Args**：

- **rhs** (`Self`)：要位移的值。

**Returns**：

`self << rhs`。

### `__rshift__`

```python
__rshift__(self: Self, rhs: Self) -> Self
```

返回 `self >> rhs`。

**Args**：

- **rhs** (`Self`)：要位移的值。

**Returns**：

`self >> rhs`。

### `__and__`

```python
__and__(self: Self, rhs: Self) -> Self
```

返回 `self & rhs`。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self & rhs`。

### `__or__`

```python
__or__(self: Self, rhs: Self) -> Self
```

返回 `self | rhs`。

**Args**：

- **rhs** (`Self`)：RHS 值。

**Returns**：

`self | rhs`。

### `__xor__`

```python
__xor__(self: Self, rhs: Self) -> Self
```

返回 `self ^ rhs`。

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

### `__rfloordiv__`

```python
__rfloordiv__(self: Self, value: Self) -> Self
```

返回 `value // self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value // self`。

### `__rmod__`

```python
__rmod__(self: Self, value: Self) -> Self
```

返回 `value % self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value % self`。

### `__rpow__`

```python
__rpow__(self: Self, value: Self) -> Self
```

返回 `pow(value,self)`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`pow(value,self)`。

### `__rlshift__`

```python
__rlshift__(self: Self, value: Self) -> Self
```

返回 `value << self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value << self`。

### `__rrshift__`

```python
__rrshift__(self: Self, value: Self) -> Self
```

返回 `value >> self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value >> self`。

### `__rand__`

```python
__rand__(self: Self, value: Self) -> Self
```

返回 `value & self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value & self`。

### `__ror__`

```python
__ror__(self: Self, value: Self) -> Self
```

返回 `value | self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value | self`。

### `__rxor__`

```python
__rxor__(self: Self, value: Self) -> Self
```

返回 `value ^ self`。

**Args**：

- **value** (`Self`)：另一个值。

**Returns**：

`value ^ self`。

### `__iadd__`

```python
__iadd__(inout self: Self, rhs: Self)
```

计算 `self + rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__isub__`

```python
__isub__(inout self: Self, rhs: Self)
```

计算 `self - rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__imul__`

```python
__imul__(inout self: Self, rhs: Self)
```

计算 `self * rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__itruediv__`

```python
__itruediv__(inout self: Self, rhs: Self)
```

计算 `self / rhs` 并转换为 int，并将结果保存在 self 中。

由于 `floor(self / rhs)` 等价于 `self // rhs`，因此产生与 `__ifloordiv__` 相同的结果。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ifloordiv__`

```python
__ifloordiv__(inout self: Self, rhs: Self)
```

计算 `self // rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__imod__`

```python
__imod__(inout self: Self, rhs: Self)
```

计算 `self % rhs` 并将结果保存在 self。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ipow__`

```python
__ipow__(inout self: Self, rhs: Self)
```

计算 `pow(self， rhs)` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ilshift__`

```python
__ilshift__(inout self: Self, rhs: Self)
```

计算 `self << rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__irshift__`

```python
__irshift__(inout self: Self, rhs: Self)
```

计算 `self >> rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__iand__`

```python
__iand__(inout self: Self, rhs: Self)
```

计算 `self & rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ixor__`

```python
__ixor__(inout self: Self, rhs: Self)
```

计算 `self ^ rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__ior__`

```python
__ior__(inout self: Self, rhs: Self)
```

计算 `self | rhs` 并将结果保存在 self 中。

**Args**：

- **rhs** (`Self`)：RHS 值。

### `__int__`

```python
__int__(self: Self) -> Self
```

获取整数值（Int 的标识函数）。

**Returns**：

整型值。

### `__mlir_index__`

```python
__mlir_index__(self: Self) -> index
```

转换为索引。

**Returns**：

对应的 __mlir_type.index 值。

### `__index__`

```python
__index__(self: Self) -> Self
```

如果 self 适合用作列表的索引则返回转换为整数的 self。

对于 Int 类型，这只是值。

**Returns**：

对应的 Int 值。

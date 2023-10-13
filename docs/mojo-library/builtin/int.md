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



# float\_literal

实现 FloatLiteral 类。

这些是 Mojo 内置的，因此您无需导入它们。

## `FloatLiteral`[](#floatliteral)

Mojo 浮点文字类型。

**别名：**

* `fp_type = scalar<f64>`

**域：**

* **value**  （`scalar<f64>`）：浮点值的基础存储。

**函数：**

### `__init__`[](#init__)

`__init__(value: Self) -> Self`

转发构造函数。

**参数：**

* **value** （`Self`）：双精度值。

**返回：**

值。

`__init__(value: f64) -> Self`

从内置 MLIR f64 值创建双精度值。

**参数：**

* **value** （`f64`）：基础 MLIR 值。

**返回：**

双精度值。

`__init__(value: Int) -> Self`

将整数转换为双精度值。

**参数：**

* **value** （`Int`）：整数值。

**返回：**

双精度值的整数值。

`__init__(value: IntLiteral) -> Self`

将 IntLiteral 转换为双精度值。

**参数：**

* **value** （`IntLiteral`）：整数值。

**返回：**

双精度值的整数值。

`__init__(value: scalar<f64>) -> Self`

### `__bool__`[](#bool__)

`__bool__(self: Self) -> Bool`

如果双精度值不为零，则为真。

**返回：**

如果非零，则为 true。

### `__neg__`[](#neg__)

`__neg__(self: Self) -> Self`

返回双精度值的取反。

**返回：**

取反的双精度值。

### `__lt__`[](#lt__)

`__lt__(self: Self, rhs: Self) -> Bool`

小于比较。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果此值小于`rhs` ，则为 True。

### `__le__`[](#le__)

`__le__(self: Self, rhs: Self) -> Bool`

小于或等于比较。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果此值小于或等于`rhs` ，则为 True。

### `__eq__`[](#eq__)

`__eq__(self: Self, rhs: Self) -> Bool`

比较相等。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果它们相等，则为 true。

### `__ne__`[](#ne__)

`__ne__(self: Self, rhs: Self) -> Bool`

比较不相等。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果它们不相等，则为 true。

### `__gt__`[](#gt__)

`__gt__(self: Self, rhs: Self) -> Bool`

大于比较。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果此值大于 ，则为 True。`rhs`

### `__ge__`[](#ge__)

`__ge__(self: Self, rhs: Self) -> Bool`

大于或等于比较。

**参数：**

* **rhs** （`Self`）：要比较的值。

**返回：**

如果此值大于或等于`rhs` ，则为 True。

### `__add__`[](#add__)

`__add__(self: Self, rhs: Self) -> Self`

双精度值相加。

**参数：**

* **rhs** （`Self`）：要添加的值。

**返回：**

两个值的总和。

### `__sub__`[](#sub__)

`__sub__(self: Self, rhs: Self) -> Self`

减去两个双精度值。

**参数：**

* **rhs** （`Self`）：要减去的值。

**返回：**

两个值的差值。

### `__mul__`[](#mul__)

`__mul__(self: Self, rhs: Self) -> Self`

乘以两个双精度值。

**参数：**

* **rhs** （`Self`）：要相乘的值。

**返回：**

两个值的乘积。

### `__truediv__`[](#truediv__)

`__truediv__(self: Self, rhs: Self) -> Self`

双精度值相除。

**参数：**

* **rhs** （`Self`）：要除以的值。

**返回：**

两个值的商。

### `__floordiv__`[](#floordiv__)

`__floordiv__(self: Self, rhs: Self) -> Self`

将两个双精度值作除法，向负无穷大四舍五入。

**参数：**

* **rhs** （`Self`）：要除以的值。

**返回：**

两个值的商，向负无穷大四舍五入。

### `__mod__`[](#mod__)

`__mod__(self: Self, rhs: Self) -> Self`

计算除以值的余数。

**参数：**

* **rhs** （`Self`）： 除数。

**返回：**

余数。

### `__pow__`[](#pow__)

`__pow__(self: Self, rhs: Self) -> Self`

计算幂指数。

**参数：**

* **rhs** （`Self`）：指数。

**返回：**

提高到指数的当前值。

### `__radd__`[](#radd__)

`__radd__(self: Self, rhs: Self) -> Self`

反向加法运算符。

**参数：**

* **rhs** （`Self`）：要添加的值。

**返回：**

此值和给定值的总和。

### `__rsub__`[](#rsub__)

`__rsub__(self: Self, rhs: Self) -> Self`

反向减法运算符。

**参数：**

* **rhs** （`Self`）：要从中减去的值。

**返回：**

从给定值中减去此值的结果。

### `__rmul__`[](#rmul__)

`__rmul__(self: Self, rhs: Self) -> Self`

反向乘法运算符。

**参数：**

* **rhs** （。`Self`）：要相乘的值

**返回：**

给定数字和这个的乘积。

### `__rtruediv__`[](#rtruediv__)

`__rtruediv__(self: Self, rhs: Self) -> Self`

反向除法运算。

**参数：**

* **rhs** （`Self`）： 要除以此的值。

**返回：**

将给定值除以此的结果。

### `__rfloordiv__`[](#rfloordiv__)

`__rfloordiv__(self: Self, rhs: Self) -> Self`

反向向下取整除法运算。

**参数：**

* **rhs** （。`Self`）：要按地板除以此的值

**返回：**

将给定值除以此的结果，取余数。

### `__rmod__`[](#rmod__)

`__rmod__(self: Self, rhs: Self) -> Self`

反转余数。

**参数：**

* **rhs** （`Self`）： 除数。

**返回：**

将给定值除以此后的余数。

### `__rpow__`[](#rpow__)

`__rpow__(self: Self, rhs: Self) -> Self`

反向取幂。

**参数：**

* **rhs** （`Self`）：要提高到这个幂的数字。

**返回：**

按此值提高给定数字的结果。

### `__iadd__`[](#iadd__)

`__iadd__(inout self: Self, rhs: Self)`

就地添加运算符。

**参数：**

* **rhs** （`Self`）：要添加的值。

### `__isub__`[](#isub__)

`__isub__(inout self: Self, rhs: Self)`

就地减法运算符。

**参数：**

* **rhs** （`Self`）：要减去的值。

### `__imul__`[](#imul__)

`__imul__(inout self: Self, rhs: Self)`

就地乘法运算符。

**参数：**

* **rhs** （`Self`）：要相乘的值。

### `__itruediv__`[](#itruediv__)

`__itruediv__(inout self: Self, rhs: Self)`

就地除法。

**参数：**

* **rhs** （`Self`）：要除以的值。

### `__ifloordiv__`[](#ifloordiv__)

`__ifloordiv__(inout self: Self, rhs: Self)`

就地向下取整除法。

**参数：**

* **rhs** （`Self`）：要除以的值。

### `__imod__`[](#imod__)

`__imod__(inout self: Self, rhs: Self)`

就地余数。

**参数：**

* **rhs** （`Self`）： 除数。

### `__ipow__`[](#ipow__)

`__ipow__(inout self: Self, rhs: Self)`

就地幂指数。

**参数：**

* **rhs** （`Self`）：指数。

### `to_int`[](#to_int)

`to_int(self: Self) -> Int`

强制转换为浮点值到 Int。如果存在小数分量，则该值将被截断为零。

**返回：**

整数形式的值。

### `__int__`[](#int__)

`__int__(self: Self) -> Int`

强制转换为浮点值到 Int。如果存在小数分量，则该值将被截断为零。

**返回：**

整数形式的值。

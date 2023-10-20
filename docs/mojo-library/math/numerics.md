# numerics

定义用于处理数值类型的实用程序。

可以从`math`包中导入这些 API。例如：

```
from math.numeric import FPUtils
```

## `FPUtils`[](#fputils)

用于处理 FP 值的实用程序函数的集合。

**约束：**

类型为浮点型。

**Parameters：**

* **type**（`DType`）：坚实的FP d型（FP32 / FP64 /等）。

**别名：**

* `integral_type = _integral_type_of[$builtin::$dtype::DType][_137x16_type]()`：浮点类型的等效整数类型。

**功能：**

### `mantissa_width`[](#mantissa_width)

`mantissa_width() -> Int`

返回浮点类型的尾数宽度。

**返回：**

尾数宽度。

### `max_exponent`[](#max_exponent)

`max_exponent() -> Int`

返回浮点类型的最大指数。

**返回：**

最大指数。

### `exponent_width`[](#exponent_width)

`exponent_width() -> Int`

返回浮点类型的指数宽度。

**返回：**

指数宽度。

### `mantissa_mask`[](#mantissa_mask)

`mantissa_mask() -> Int`

返回浮点类型的尾数掩码。

**返回：**

尾数面具。

### `exponent_bias`[](#exponent_bias)

`exponent_bias() -> Int`

返回浮点类型的指数偏差。

**返回：**

指数偏差。

### `sign_mask`[](#sign_mask)

`sign_mask() -> Int`

返回浮点类型的符号掩码。它由`1 << (exponent_width + mantissa_mask)` 计算。

**返回：**

符号掩码。

### `exponent_mask`[](#exponent_mask)

`exponent_mask() -> Int`

返回浮点类型的指数掩码。它由`~(sign_mask | mantissa_mask)` 计算。

**返回：**

指数掩码。

### `exponent_mantissa_mask`[](#exponent_mantissa_mask)

`exponent_mantissa_mask() -> Int`

返回浮点类型的指数掩码和尾数掩码。它由`exponent_mask + mantissa_mask` 计算。

**返回：**

指数和尾数面具。

### `quiet_nan_mask`[](#quiet_nan_mask)

`quiet_nan_mask() -> Int`

返回浮点类型的安静 NaN 掩码。

掩码的定义是：

```
(1<<exponent_width-1)<<mantissa_width + 1<<(mantissa_width-1)
```

**返回：**

安静的NaN面具。

### `bitcast_to_integer`[](#bitcast_to_integer)

`bitcast_to_integer(value: SIMD[type, 1]) -> Int`

将浮点值位转换为整数。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点类型。

**返回：**

浮点值的整数表示形式。

### `bitcast_from_integer`[](#bitcast_from_integer)

`bitcast_from_integer(value: Int) -> SIMD[type, 1]`

从整数对浮点值进行位转换。

**参数：**

* **value** （`Int`）：整型值。

**返回：**

Int 的浮点表示形式。

### `get_sign`[](#get_sign)

`get_sign(value: SIMD[type, 1]) -> Bool`

返回浮点值的符号。如果设置了标志，则为 True，否则为 False。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点类型。

**返回：**

如果设置了符号，则返回 True，否则返回 False。

### `set_sign`[](#set_sign)

`set_sign(value: SIMD[type, 1], sign: Bool) -> SIMD[type, 1]`

设置浮点值的符号。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。
* **sign** （`Bool`）： 如果为 true，则设置符号，否则为 false。

**返回：**

返回带有符号集的浮点值。

### `get_exponent`[](#get_exponent)

`get_exponent(value: SIMD[type, 1]) -> Int`

返回浮点值的指数位。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。

**返回：**

返回指数位。

### `get_exponent_without_bias`[](#get_exponent_without_bias)

`get_exponent_without_bias(value: SIMD[type, 1]) -> Int`

返回浮点值的指数位。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。

**返回：**

返回指数位。

### `set_exponent`[](#set_exponent)

`set_exponent(value: SIMD[type, 1], exponent: Int) -> SIMD[type, 1]`

设置浮点值的指数位。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。
* **mantissa** （`Int`）：指数位。

**返回：**

返回设置了指数位的浮点值。

### `get_mantissa`[](#get_mantissa)

`get_mantissa(value: SIMD[type, 1]) -> Int`

获取浮点值的尾数位。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。

**返回：**

尾数位。

### `set_mantissa`[](#set_mantissa)

`set_mantissa(value: SIMD[type, 1], mantissa: Int) -> SIMD[type, 1]`

设置浮点值的尾数位。

**参数：**

* **value** （`SIMD[type, 1]`）：浮点值。
* **mantissa**（`Int`）：尾数位。

**返回：**

返回设置了尾数位的浮点值。

### `pack`[](#pack)

`pack(sign: Bool, exponent: Int, mantissa: Int) -> SIMD[type, 1]`

根据其构成符号、指数和尾数构造浮点值。

**参数：**

* **sign** （`Bool`）：浮点值的符号。
* **exponent** （`Int`）：浮点值的指数。
* **mantissa**（`Int`）：浮点值的尾数。

**返回：**

返回浮点值。

## `FlushDenormals`[](#flushdenormals)

刷新和异常在上下文中设置为零，状态在退出时恢复到以前的值。

**域：**

* **state** （`SIMD[si32, 1]`）：当前状态。

**功能：**

### `__init__`[](#init__)

`__init__(inout self: Self)`

初始化同花顺异常。

### `__enter__`[](#enter__)

`__enter__(self: Self)`

输入上下文。这会将非正常值设置为零。

### `__exit__`[](#exit__)

`__exit__(self: Self)`

退出上下文。这将恢复以前的 FPState。

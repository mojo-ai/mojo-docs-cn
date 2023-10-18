# complex

实现 Complex 类型。

可以从 `complex` 包中导入这些 API。例如：

```
from complex import ComplexSIMD
```

**别名：**

* `ComplexFloat32 = ComplexSIMD[f32, 1]`

<!---->

* `ComplexFloat64 = ComplexSIMD[f64, 1]`

## `ComplexSIMD`[](#complexsimd)

表示复数的 SIMD 值。

该类提供了操作复数的基本方法。

**Parameters：**

* **type** （`DType`）：值的 DType。
* **size** （`Int`）：值的 SIMD 宽度。

**域：**

* **re** （`SIMD[type, size]`）：复数 SIMD 值的实际部分。

<!---->

* **im** （`SIMD[type, size]`）：复数 SIMD 值的虚部。

**函数：**

### `__init__`[](#init__)

`__init__(re: SIMD[type, size], im: SIMD[type, size]) -> Self`

### `__neg__`[](#neg__)

`__neg__(self: Self) -> Self`

否定复数值。

**返回：**

复数值的负数。

### `__add__`[](#add__)

`__add__(self: Self, rhs: Self) -> Self`

添加两个复值。

**参数：**

* **rhs** （`Self`）：要添加的复数。

**返回：**

此值和 RHS 复数值的总和。

### `__mul__`[](#mul__)

`__mul__(self: Self, rhs: Self) -> Self`

将两个复数值相乘。

**参数：**

* **rhs** （`Self`）：要乘以的复数值。

**返回：**

此值和 RHS 复数值的乘积。

### `norm`[](#norm)

`norm(self: Self) -> SIMD[type, size]`

返回复数值的大小。

**返回：**

的值。`sqrt(re*re + im*im)`

### `squared_norm`[](#squared_norm)

`squared_norm(self: Self) -> SIMD[type, size]`

返回复数值的平方量级。

**返回：**

的值。`re*re + im*im`

### `fma`[](#fma)

`fma(self: Self, b: Self, c: Self) -> Self`

计算 FMA 操作。

计算融合了与其他两个复数的多重加法：`result = self * b + c`

**参数：**

* **b** （`Self`）： 乘数复数值。
* **c** （`Self`）： 要添加的复数。

**返回：**

计算的`Self * B + C`复数值。

### `squared_add`[](#squared_add)

`squared_add(self: Self, c: Self) -> Self`

计算平方相加运算。

计算`Self * Self + C`。

**参数：**

* **c** （`Self`）： 要添加的复数。

**返回：**

计算的`Self * Self + C`复数值。

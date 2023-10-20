# polynomial

提供两种用于计算多项式的实现。

可以从`math`包中导入这些 API。例如：

```
from math.polynomial import polynomial_evaluate
```

## `polynomial_evaluate`[](#polynomial_evaluate)

`polynomial_evaluate[simd_width: Int, dtype: DType, coefficients: VariadicList[SIMD[dtype, simd_width]]](x: SIMD[dtype, simd_width]) -> SIMD[dtype, simd_width]`

使用传入值和指定系数计算 1 次多项式。

这些方法使用[埃斯特林](https://en.wikipedia.org/wiki/Estrin%27s_scheme)方案或霍纳方案评估多项式。Estrin 方案仅适用于 4 到 10 度之间的多项式。霍纳方案适用于任何多项式次数的多项式。

**Parameters：**

* **simd\_width** （`Int`）： 计算值的simd\_width。
* **dtype** （`DType`）：值的 dtype。
* **coefficients **（`VariadicList[SIMD[dtype, simd_width]]`）：系数。

**参数：**

* **x** （`SIMD[dtype, simd_width]`）：用于计算多项式的值。

**返回：**

使用指定值和常数系数的多项式求值结果。

`polynomial_evaluate[simd_width: Int, dtype: DType, coefficients: VariadicList[SIMD[dtype, simd_width]]](x: SIMD[dtype, simd_width]) -> SIMD[dtype, simd_width]`

使用霍纳方案计算多项式。

霍纳方案通过执行以下计算将多项式计算为 ，其中是一个标量，是一个系数列表：`horner(val, coeffs)``val``coeffs``[c0, c1, c2, ..., cn]`

```
horner(val, coeffs) = c0 + val * (c1 + val * (c2 + val * (... + val * cn)))
            = fma(val, horner(val, coeffs[1:]), c0)
```

**参数：**

* **simd\_width** （`Int`）： 计算值的simd\_width。
* **dtype** （`DType`）：值的 dtype。
* **coefficients**（`VariadicList[SIMD[dtype, simd_width]]`）：系数。

**参数：**

* **x** （`SIMD[dtype, simd_width]`）：用于计算多项式的值。

**返回：**

使用指定值和常数系数的多项式求值结果。

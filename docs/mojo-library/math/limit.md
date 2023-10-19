# limit

提供用于查询类型的各种数值属性的接口。

可以从`math`包中导入这些 API。例如：

```
from math.limit import inf
```

## `inf`[](#inf)

`inf[type: DType]() -> SIMD[type, 1]`

获取给定 dtype 的 +inf 值。

**约束：**

只能用于 FP dtype。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

给定 dtype 的 +inf 值。

## `neginf`[](#neginf)

`neginf[type: DType]() -> SIMD[type, 1]`

获取给定 dtype 的 -inf 值。

**约束：**

只能用于 FP dtype。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

给定 dtype 的 -inf 值。

## `isinf`[](#isinf)

`isinf[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

检查该值是否无限。

对于非 FP 数据类型，这始终为 False。

**Parameters：**

* **type** （`DType`）：值 dtype。
* **simd\_width** （`Int`）： SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要检查的值。

**返回：**

如果 val 是无限的，则为 true，否则为 false。

## `isfinite`[](#isfinite)

`isfinite[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

检查该值是否是无限的。

对于非 FP 数据类型，始终为 True。

**Parameters：**

* **type** （`DType`）：值 dtype。
* **simd\_width** （`Int`）： SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要检查的值。

**返回：**

如果 val 是有限的，则为 true，否则为 False。

## `max_finite`[](#max_finite)

`max_finite[type: DType]() -> SIMD[type, 1]`

返回类型的最大有限值。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

类型的最大可表示值。不包括浮点类型的无穷大。

## `max_or_inf`[](#max_or_inf)

`max_or_inf[type: DType]() -> SIMD[type, 1]`

返回类型的最大值。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

浮点类型的类型或无穷大的最大值。

## `min_finite`[](#min_finite)

`min_finite[type: DType]() -> SIMD[type, 1]`

返回 type 的最小（最低）有限值。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

类型的最小可表示值。不包括浮点类型的负无穷大。

## `min_or_neginf`[](#min_or_neginf)

`min_or_neginf[type: DType]() -> SIMD[type, 1]`

返回类型的最小值。

**Parameters：**

* **type** （`DType`）：值 dtype。

**返回：**

浮点类型的类型或无穷大的最小值。

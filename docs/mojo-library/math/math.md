# math

定义实用数学工具。

可以从`math`包中导入这些 API。例如：

```
from math import mul
```

## `mod`[](#mod)

`mod[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对两个 SIMD 向量执行元素取模运算。

**Parameters：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：操作的分子。
* **y** （`SIMD[type, simd_width]`）：运算的分母。

**返回：**

x 除以 y 的余数。

## `mul`[](#mul)

`mul[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行两个 SIMD 向量的元素乘法。

**Parameters：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：第一个要相乘的 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：第二个要相乘的 SIMD 向量。

**返回：**

x 和 y 的元素乘法。

## `sub`[](#sub)

`sub[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对两个 SIMD 向量执行元素减法。

**Parameters：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 将从中减去 y 的 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）： 要从 x 中减去的 SIMD 向量。

**返回：**

SIMD 矢量 x - y 的元素减法。

## `add`[](#add)

`add[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行两个 SIMD 向量的元素加法。

**Parameters：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：要添加的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要添加的第二个 SIMD 向量。

**返回：**

x 和 y 的元素相加。

## `div`[](#div)

`div[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对两个 SIMD 向量执行元素除法。

**`DType`：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 包含股息的 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）： 包含商的 SIMD 向量。

**返回：**

SIMD 向量 x 与 SIMD 向量 y 的元素除法（这是 x / y）。

## `clamp`[](#clamp)

`clamp[type: DType, simd_width: Int](x: SIMD[type, simd_width], lower_bound: SIMD[type, simd_width], upper_bound: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

将 SIMD 矢量中的值固定在特定范围内。

钳位操作将输入 SIMD 矢量中的值在向上取整和下限值处切断。例如，将`[0, 1, 2, 3]`钳位到下限 1 和向上取整 2 的 SIMD 向量将返回 `[1, 1, 2, 2]`。

**Parameters：**

* **type** （`DType`）： 输入 SIMD 向量的 DType。
* **simd\_width** （`Int`）： 输入 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 用于执行钳位操作的 SIMD 矢量。
* **lower\_bound** （`SIMD[type, simd_width]`）：要夹紧到的最小范围。
* **upper\_bound** （`SIMD[type, simd_width]`）：要夹紧到的最大值范围。

**返回：**

包含 x 的新 SIMD 向量，夹紧在 lower\_bound 和 upper\_bound 内。

## `abs`[](#abs)

`abs(x: Int) -> Int`

获取整数的绝对值。

**参数：**

* **x** （`Int`）： 取其绝对值的值。

**返回：**

x 的绝对值。

`abs[type: DType, simd_width: Int](x: ComplexSIMD[type, simd_width]) -> SIMD[type, simd_width]`

对复数值的每个元素执行元素绝对值操作（范数）。

**`Int`：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`ComplexSIMD[type, simd_width]`）：要对其执行绝对值的复向量。

**返回：**

x 的元素绝对值。

`abs[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行绝对值。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行绝对值的 SIMD 矢量。

**返回：**

x 的元素绝对值。

## `rotate_bits_left`[](#rotate_bits_left)

`rotate_bits_left[shift: Int](x: Int) -> Int`

将输入的位向左移动`shift`位（带环绕）。

**约束：**

`-size <= shift < size`

**Parameters：**

* **shift** （`Int`）：将整数的位向左旋转的位位置数（带环绕）。

**参数：**

* **x** （`Int`）：输入值。

**返回：**

输入由`shift`元素向左旋转（带环绕）。

`rotate_bits_left[shift: Int, type: DType, width: Int](x: SIMD[type, width]) -> SIMD[type, width]`

按`shift`位置（带环绕）将 SIMD 矢量的每个元素的位向左移动。

**约束：**

`0 <= shift < size`只能轮换无符号类型。

**Parameters：**

* **shift** （`Int`）：将 SIMD 矢量的每个元素的位向左移动的位置数（带环绕）。
* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, width]`）： 要对其执行操作的 SIMD 矢量。

**返回：**

每个元素的位向左移动的 SIMD 矢量（带环绕）。

## `rotate_bits_right`[](#rotate_bits_right)

`rotate_bits_right[shift: Int](x: Int) -> Int`

将输入的位向左移动`shift`位（带环绕）。

**约束：**

`-size <= shift < size`

**Parameters：**

* **shift** （`Int`）：将整数的位向左旋转的位位置数（带环绕）。

**参数：**

* **x** （`Int`）：输入值。

**返回：**

输入向左旋转`shift`位（带环绕）。

`rotate_bits_right[shift: Int, type: DType, width: Int](x: SIMD[type, width]) -> SIMD[type, width]`

按`shift`位置（带环绕）将 SIMD 矢量的每个元素的位向右移动。

**约束：**

`0 <= shift < size`只能旋转无符号类型。

**Parameters：**

* **shift** （`Int`）：将 SIMD 矢量的每个元素的位向左向右移动的位置数（带环绕）。
* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, width]`）： 要对其执行操作的 SIMD 矢量。

**返回：**

 SIMD 矢量的每个元素的位向右移动`shift`位（带环绕）。

## `rotate_left`[](#rotate_left)

`rotate_left[shift: Int](x: Int) -> Int`

将输入的位向左移动`shift`位（带环绕）。

**约束：**

`-size <= shift < size`

**Parameters：**

* **shift** （`Int`）：将整数的位向左旋转的位位置数（带环绕）。

**参数：**

* **x** （`Int`）：输入值。

**返回：**

输入由元素向左旋转`shift`元素（带环绕）。

`rotate_left[shift: Int, type: DType, size: Int](x: SIMD[type, size]) -> SIMD[type, size]`

将 SIMD 矢量的元素向左移动`shift`元素（使用环绕）。

**约束：**

`-size <= shift < size`

**Parameters：**

* **shift** （`Int`）：将 SIMD 矢量的元素向左旋转的位置数（带环绕）。
* **type** （`DType`）：输入和输出 SIMD 矢量的`DType`。
* **size** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, size]`）：输入值。

**返回：**

SIMD 矢量的元素向左旋转`shift`位（带环绕）。

## `rotate_right`[](#rotate_right)

`rotate_right[shift: Int](x: Int) -> Int`

将输入的位向右移动`shift`位（带环绕）。

**约束：**

`-size <= shift < size`

**Parameters：**

* **shift** （`Int`）：将整数的位向右旋转的位位置数（带环绕）。

**参数：**

* **x** （`Int`）：输入值。

**返回：**

输入由元素向右旋转`shift`位（带环绕）。

`rotate_right[shift: Int, type: DType, size: Int](x: SIMD[type, size]) -> SIMD[type, size]`

将 SIMD 矢量的元素向右移动`shift`元素（使用环绕）。

**约束：**

`-size < shift <= size`

**Parameters：**

* **shift** （`Int`）：将 SIMD 矢量的元素向右旋转（带环绕）的位置数。
* **type** （`DType`）：输入和输出 SIMD 矢量的`DType`。
* **size** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, size]`）：输入值。

**返回：**

SIMD 矢量的元素向右旋转`shift`位（带环绕）。

## `floor`[](#floor)

`floor[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行向下取整。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要执行向下取整的 SIMD 矢量。

**返回：**

x的元素向下取整。

## `ceil`[](#ceil)

`ceil[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行元素向上取整。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 用于执行向上取整的 SIMD 矢量。

**返回：**

x 的元素向上取整。

## `ceildiv`[](#ceildiv)

`ceildiv(x: Int, y: Int) -> Int`

返回将 x 除以 y 的舍入结果。

**参数：**

* **x** （`Int`）：分子。
* **y** （`Int`）：分母。

**返回：**

将 x 除以 y 的向上取整。

## `trunc`[](#trunc)

`trunc[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行元素截断。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行截断的 SIMD 矢量。

**返回：**

x 的元素截断。

## `round`[](#round)

`round[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行元素舍入。

此舍入到最接近的整数，并且连接远离零。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**Parameters：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行舍入的 SIMD 向量。

**返回：**

x 的元素四舍五入。

## `roundeven`[](#roundeven)

`roundeven[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 向量的元素执行元素银行家舍入。

此舍入到最接近的整数，与最接近的偶数值连接。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行舍入的 SIMD 向量。

**返回：**

元素对 x 的奇进偶舍。

## `round_half_down`[](#round_half_down)

`round_half_down[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

舍入与较小的整数相连。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行舍入的 SIMD 向量。

**返回：**

x 评估的元素四舍五入与较小的整数相关。

## `round_half_up`[](#round_half_up)

`round_half_up[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

舍入较大的整数。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行舍入的 SIMD 向量。

**返回：**

x 评估的元素四舍五入与较大的整数相关。

## `sqrt`[](#sqrt)

`sqrt(x: Int) -> Int`

对整数执行平方根。

**参数：**

* **x** （`Int`）：要对其执行平方根的整数值。

**返回：**

x 的平方根。

`sqrt[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行元素平方根。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 用于执行平方根的 SIMD 向量。

**返回：**

x 的元素平方根。

## `rsqrt`[](#rsqrt)

`rsqrt[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对 SIMD 矢量的元素执行元素倒数平方根。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 用于执行倒数平方根的 SIMD 向量。

**返回：**

x 的元素倒数平方根。

## `exp2`[](#exp2)

`exp2[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算元素 2 的 n 次幂，其中 n 是输入 SIMD 矢量的元素。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要对其执行 exp2 的 SIMD 矢量。

**返回：**

载体按元素计算，其中 n 是输入 SIMD 向量中的一个元素。

## `ldexp`[](#ldexp)

`ldexp[type: DType, simd_width: Int](x: SIMD[type, simd_width], exp: SIMD[si32, simd_width]) -> SIMD[type, simd_width]`

计算元素 ldexp 函数。

ldexp 函数将浮点值 x 乘以数字 2 的 exp 幂。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 浮点值的 SIMD 向量。
* **exp** （`SIMD[si32, simd_width]`）： 包含指数的 SIMD 向量。

**返回：**

包含 ldexp 在 x 和 exp 上的元素结果的向量。

## `exp`[](#exp)

`exp[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

逐个计算`e^{X_i}`，其中 `X_i` 是输入 SIMD 向量中`i`位置的元素。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：输入 SIMD 矢量。

**返回：**

一个 SIMD 向量，包含`e`提高到`Xi`输入 SIMD 矢量中的`Xi`元素的幂。

## `frexp`[](#frexp)

`frexp[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> StaticTuple[2, SIMD[type, simd_width]]`

将浮点值分解为小数部分和指数部分。

**约束：**

`type`必须是浮点值。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：输入值。

**返回：**

包含输入浮点值的小数部分和指数部分的两个 SIMD 向量的元组。

## `log`[](#log)

`log[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行 SIMD 矢量的元素级自然对数（基数 E）。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 对其执行对数运算的向量。

**返回：**

包含对x上执行自然对数基数E的结果的向量。

## `log2`[](#log2)

`log2[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行 SIMD 矢量的元素对数（基数 2）。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 对其执行对数运算的向量。

**返回：**

包含对数基数 2 在 x 上执行的结果的向量。

## `copysign`[](#copysign)

`copysign[type: DType, simd_width: Int](magnitude: SIMD[type, simd_width], sign: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

返回一个值，该值具有第一个操作数的大小和第二个操作数的符号。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **magnitude ** （`SIMD[type, simd_width]`）：要使用的量级。
* **sign ** （`SIMD[type, simd_width]`）：要复制的符号。

**返回：**

将符号从符号复制到量级。

## `erf`[](#erf)

`erf[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

在 SIMD 矢量上执行元素 Erf。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 用于执行元素 Erf 的 SIMD 向量。

**返回：**

元素 Erf 操作的结果。

## `tanh`[](#tanh)

`tanh[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行 tanh 函数的元素计算。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：要对其执行元素 tanh 的向量。

**返回：**

元素 tanh 操作的结果。

## `isclose`[](#isclose)

`isclose[type: DType, simd_width: Int](a: SIMD[type, simd_width], b: SIMD[type, simd_width], absolute_tolerance: SIMD[type, 1], relative_tolerance: SIMD[type, 1]) -> SIMD[bool, simd_width]`

检查两个输入值在数值上是否在容差范围内。

当类型为积分时，则检查相等性。当类型为浮点型时，这将检查两个输入值是否在数值上是收盘价，使用公式。

与Python不同，这个实现是对称的。即.`math.isclose``isclose(a,b) == isclose(b,a)`

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **a** （`SIMD[type, simd_width]`）：要比较的第一个值。
* **b** （`SIMD[type, simd_width]`）：要比较的第二个值。
* **absolute\_tolerance** （`SIMD[type, 1]`）： 绝对公差。
* **relative\_tolerance** （`SIMD[type, 1]`）： 相对公差。

**返回：**

一个布尔向量，其中 a 和 b 在指定的容差内相等。

`isclose[type: DType, simd_width: Int](a: SIMD[type, simd_width], b: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

检查两个输入值在数值上是否在公差范围内，atol=1e-08 和 rtol=1e-05。

当类型为积分时，则检查相等性。当类型为浮点型时，这将使用 abs（a - b） <= max（rtol \* max（abs（a）， abs（b））， atol） 公式检查两个输入值是否在数值上接近。默认的绝对和相对公差是从 numpy 默认值中选取的。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **a** （`SIMD[type, simd_width]`）：要比较的第一个值。
* **b** （`SIMD[type, simd_width]`）：要比较的第二个值。

**返回：**

一个布尔向量，其中 a 和 b 在容差范围内相等，atol=1e-08 且 rtol=1e-05。

## `all_true`[](#all_true)

`all_true[simd_width: Int](val: SIMD[bool, simd_width]) -> Bool`

如果 SIMD 矢量中的所有元素都为真，则返回 True，否则返回 False。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[bool, simd_width]`）：要简化的 SIMD 向量。

**返回：**

如果 SIMD 矢量中的所有值均为真，则为 True，否则为假。

## `any_true`[](#any_true)

`any_true[simd_width: Int](val: SIMD[bool, simd_width]) -> Bool`

如果 SIMD 矢量中的任何元素为真，则返回 True，否则返回 False。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[bool, simd_width]`）：要简化的 SIMD 向量。

**返回：**

如果 SIMD 矢量中的任何值为真，则为 True，否则为假。

## `none_true`[](#none_true)

`none_true[simd_width: Int](val: SIMD[bool, simd_width]) -> Bool`

如果 SIMD 矢量中的所有元素均为 False，则返回 True，否则返回 False。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[bool, simd_width]`）：要简化的 SIMD 向量。

**返回：**

如果 SIMD 矢量中的所有值均为 False，则为 True，否则为 False。

## `reduce_bit_count`[](#reduce_bit_count)

`reduce_bit_count[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> Int`

返回一个标量，其中包含给定向量中设置的总位数。

**约束：**

输入必须是整数或布尔类型。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （）：要简化的 SIMD 向量。`SIMD[type, simd_width]`

**返回：**

跨向量所有元素的设置位计数。

## `iota`[](#iota)

`iota[type: DType, simd_width: Int]() -> SIMD[type, simd_width]`

创建包含递增序列（从 0 开始）的 SIMD 向量。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**返回：**

值的递增序列，从 0 开始。

`iota[type: DType, simd_width: Int](offset: SIMD[type, 1]) -> SIMD[type, simd_width]`

创建包含从偏移开始的递增序列的 SIMD 向量。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **offset** （`SIMD[type, 1]`）：开始序列的值。默认值为零。

**返回：**

从偏移量开始的递增值序列。

`iota[type: DType](inout buff: DTypePointer[type], len: Int, offset: Int)`

用从偏移到偏移 + len - 1（间隔为 1）的数字填充缓冲区。

该函数不返回任何内容，缓冲区就地更新。

**Parameters：**

* **type** （`DType`）：基础数据的 DType。

**参数：**

* **buff** （`DTypePointer[type]`）：要填充的缓冲区。
* **len** （`Int`）：要填充的缓冲区的长度。
* **offset** （`Int`）：要在索引 0 处填充的值。

`iota[type: DType](inout v: DynamicVector[SIMD[type, 1]], offset: Int)`

用从偏移到偏移 + len - 1 的数字填充矢量，间隔为 1。

该函数不返回任何内容，向量就地更新。

**Parameters：**

* **type** （`DType`）：基础数据的 DType。

**参数：**

* **v** （`DynamicVector[SIMD[type, 1]]`）：要填充的矢量。
* **offset** （`Int`）：要在索引 0 处填充的值。

`iota(inout v: DynamicVector[Int], offset: Int)`

用从偏移到偏移 + len - 1 的数字填充矢量，间隔为 1。

该函数不返回任何内容，向量就地更新。

**参数：**

* **v** （`DynamicVector[Int]`）：要填充的矢量。
* **offset** （`Int`）：要在索引 0 处填充的值。

## `is_power_of_2`[](#is_power_of_2)

`is_power_of_2[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 SIMD 矢量是否包含 2 的整数幂执行元素检查。

如果结果 SIMD 矢量的值是 2 的整数幂，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要对其执行is\_power\_of\_2的 SIMD 矢量。

**返回：**

如果 val 中的相应元素是 2 的幂，则包含 True 的 SIMD 向量，否则为 False。

`is_power_of_2(val: Int) -> Bool`

检查整数是否为 2 的幂。

**参数：**

* **val** （`Int`）：要检查的整数。

**返回：**

如果 val 是 2 的幂，则为 true，否则为 False。

## `is_odd`[](#is_odd)

`is_odd(val: Int) -> Bool`

对整数值是否为奇数执行元素检查。

**参数：**

* **val** （`Int`）：要检查的整数值。

**返回：**

如果输入为奇数，则为 True，否则为 False。

`is_odd[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 SIMD 矢量是否包含奇数值执行元素检查。

如果结果 SIMD 矢量的元素为奇数，则为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要检查的 SIMD 向量。

**返回：**

如果 val 中的相应元素为奇数，则包含 True 的 SIMD 向量，否则为 False。

## `is_even`[](#is_even)

`is_even(val: Int) -> Bool`

对整数值是否为偶数执行元素检查。

**参数：**

* **val** （`Int`）：要检查的整数值。

**返回：**

如果输入为偶数，则为 True，否则为 False。

`is_even[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 SIMD 矢量是否包含偶数值执行元素检查。

结果 SIMD 矢量的元素如果值为偶数，则为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要检查的 SIMD 向量。

**返回：**

如果 val 中的相应元素为偶数，则包含 True 的 SIMD 向量，否则为 False。

## `fma`[](#fma)

`fma(a: Int, b: Int, c: Int) -> Int`

对输入执行`fma`（融合乘加）。

结果是`(a * b) + c` 。

**参数：**

* **a** （`Int`）：第一个输入。
* **b** （`Int`）：第二个输入。
* **c** （`Int`）：第三个输入。

**返回：**

`(a * b) + c`.

`fma[type: DType, simd_width: Int](a: SIMD[type, simd_width], b: SIMD[type, simd_width], c: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对输入执行元素`fma`（融合乘加）。

结果 SIMD 向量中的每个元素都是哪里,和是索引处的元素分别在 A、B 和 C 中。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **a** （`SIMD[type, simd_width]`）：输入的第一个向量。
* **b** （`SIMD[type, simd_width]`）：输入的第二个向量。
* **c** （`SIMD[type, simd_width]`）：输入的第三个向量。

**返回：**

a、b 和 c 的元素`fma`操作。

## `reciprocal`[](#reciprocal)

`reciprocal[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

取 SIMD 矢量的元素倒数。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：要对其执行元素倒数运算的 SIMD 向量。

**返回：**

一个 SIMD 向量，表示 x 的元素倒数。

## `identity`[](#identity)

`identity[type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

获取 SIMD 矢量的标识。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：要获取其标识的 SIMD 向量。

**返回：**

x 的恒等式，即 x。

## `greater`[](#greater)

`greater[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否大于 y 中的值执行元素检查。

如果 x 中的相应元素大于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素大于 y 中的相应元素，则包含 True 的 SIMD 向量，否则为 False。

## `greater_equal`[](#greater_equal)

`greater_equal[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否大于或等于 y 中的值执行元素检查。

如果 x 中的相应元素大于或等于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素大于或等于 y 中的相应元素，则包含 True（否则为 False）的 SIMD 向量。

## `less`[](#less)

`less[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否小于 y 中的值执行元素检查。

如果 x 中的相应元素小于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素小于 y 中的相应元素，则包含 True 的 SIMD 向量，否则为 False。

## `less_equal`[](#less_equal)

`less_equal[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否小于或等于 y 中的值执行元素检查。

如果 x 中的相应元素小于或等于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素小于或等于 y 中的相应元素，则包含 True 的 SIMD 向量，否则为 False。

## `equal`[](#equal)

`equal[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否等于 y 中的值执行元素检查。

如果 x 中的相应元素等于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素等于 y 中的相应元素，则包含 True 的 SIMD 向量，否则为 False。

## `logical_and`[](#logical_and)

`logical_and[simd_width: Int](x: SIMD[bool, simd_width], y: SIMD[bool, simd_width]) -> SIMD[bool, simd_width]`

执行元素逻辑和操作。

如果 x 和 y 中的相应元素均为真，则结果 SIMD 矢量的元素将为 True，否则为假。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[bool, simd_width]`）：第一个执行 And 运算的 SIMD 向量。
* **y** （`SIMD[bool, simd_width]`）：用于执行 And 运算的第二个 SIMD 向量。

**返回：**

如果 x 和 y 中的相应元素均为真，则包含 True 的 SIMD 向量，否则为 False。

## `logical_not`[](#logical_not)

`logical_not[simd_width: Int](x: SIMD[bool, simd_width]) -> SIMD[bool, simd_width]`

执行元素逻辑 Not 操作。

如果 x 中的相应元素为真，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[bool, simd_width]`）： 用于执行“非”操作的 SIMD 矢量。

**返回：**

如果 x 中的相应元素为真，则包含 True 的 SIMD 向量，否则为 False。

## `logical_xor`[](#logical_xor)

`logical_xor[simd_width: Int](x: SIMD[bool, simd_width], y: SIMD[bool, simd_width]) -> SIMD[bool, simd_width]`

执行元素逻辑异或操作。

如果 x 和 y 中只有一个对应的元素为真，则结果 SIMD 向量的元素将为 True，否则为 False。

**Parameters：**

* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[bool, simd_width]`）：执行 Xor 运算的第一个 SIMD 向量。
* **y** （`SIMD[bool, simd_width]`）：用于执行 Xor 运算的第二个 SIMD 向量。

**返回：**

包含 True 的 SIMD 向量，如果 x 和 y 中只有一个相应元素为真，否则为假。

## `not_equal`[](#not_equal)

`not_equal[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

对 x 中的值是否不等于 y 中的值执行元素检查。

如果 x 中的相应元素不等于 y 中的相应元素，则结果 SIMD 矢量的元素将为 True，否则为 False。

**Parameters：**

* **type** （`DType`）：输入 SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 要比较的第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：要比较的第二个 SIMD 向量。

**返回：**

如果 x 中的相应元素不等于 y 中的相应元素，则包含 True 的 SIMD 向量，否则为 False。

## `select`[](#select)

`select[type: DType, simd_width: Int](cond: SIMD[bool, simd_width], true_case: SIMD[type, simd_width], false_case: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

根据给定 SIMD 矢量的输入布尔值选择true\_case或false\_case的值。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的元素类型。
* **simd\_width** （`Int`）： 我们正在比较的 SIMD 矢量的宽度。

**参数：**

* **cond** （`SIMD[bool, simd_width]`）：要检查的布尔值向量。
* **true\_case** （`SIMD[type, simd_width]`）： 如果位置值为 True，则选择的值。
* **false\_case** （`SIMD[type, simd_width]`）： 如果位置值为 False，则选择的值。

**返回：**

形式的新向量。`[true_case[i] if cond[i] else false_case[i] in enumerate(self)]`

## `max`[](#max)

`max(x: Int, y: Int) -> Int`

获取两个整数的最大值。

**参数：**

* **x** （`Int`）： 整数输入到最大值
* **y** （`Int`）： 整数输入到最大值

**返回：**

最大值为 x 和 y。

`max[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行 x 和 y 的元素最大值。

结果 SIMD 矢量的元素将是 x 和 y 中相应元素的最大值。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：第二个 SIMD 向量。

**返回：**

包含 x 和 y 的元素最大值的 SIMD 向量。

## `min`[](#min)

`min(x: Int, y: Int) -> Int`

获取两个整数的最小值。

**参数：**

* **x** （`Int`）： 整数输入到最大值
* **y** （`Int`）： 整数输入到最大值

**返回：**

最小值为 x 和 y。

`min[type: DType, simd_width: Int](x: SIMD[type, simd_width], y: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

获取 x 和 y 的元素最小值。

结果 SIMD 矢量的元素将是 x 和 y 中相应元素的最小值。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）： 第一个 SIMD 向量。
* **y** （`SIMD[type, simd_width]`）：第二个 SIMD 向量。

**返回：**

包含元素最小值 x 和 y 的 SIMD 向量。

## `pow`[](#pow)

`pow[type: DType, simd_width: Int](lhs: SIMD[type, simd_width], rhs: Int) -> SIMD[type, simd_width]`

计算输入`pow`。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **lhs** （`SIMD[type, simd_width]`）：第一个输入参数。
* **rhs** （`Int`）：第二个输入参数。

**返回：**

`pow`的输入。

`pow[lhs_type: DType, rhs_type: DType, simd_width: Int](lhs: SIMD[lhs_type, simd_width], rhs: SIMD[rhs_type, simd_width]) -> SIMD[lhs_type, simd_width]`

计算浮点类型提升到另一个浮点类型的元素功率。

结果 SIMD 矢量的一个元素将是将 lhs 的相应元素提升为 rhs 的相应元素的结果。

**约束：**

`rhs_type`并且必须相同，并且必须是浮点类型。`lhs_type`

**Parameters：**

* **lhs\_type** （`DType`）： LHS SIMD 向量的 `dtype`。
* **rhs\_type** （`DType`）： RHS SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **LHS** （`SIMD[lhs_type, simd_width]`）：幂操作的基础。
* **rhs** （`SIMD[rhs_type, simd_width]`）：幂操作的指数。

**返回：**

包含元素 lhs 的 SIMD 向量，其幂为 rhs。

`pow[n: Int, type: DType, simd_width: Int](x: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算元素幂，其中指数是编译时已知的整数。

**约束：**

`n`必须是有符号`si32`类型。

**Parameters：**

* **n** （`Int`）： 幂操作的指数。
* **type** （`DType`）：x SIMD 矢量的 `dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **x** （`SIMD[type, simd_width]`）：幂操作的基础。

**返回：**

包含元素 x 的 SIMD 向量，其幂为 n 的幂。

## `div_ceil`[](#div_ceil)

`div_ceil(numerator: Int, denominator: Int) -> Int`

将一个整数除以另一个整数，然后向上舍入到最接近的整数。

**约束：**

如果分母为零，将引发异常。

**参数：**

* **numerator** （`Int`）：分子。
* **denominator** （`Int`）：分母。

**返回：**

分子的向上取整除以分母。

## `align_down`[](#align_down)

`align_down(value: Int, alignment: Int) -> Int`

返回小于或等于值的最接近对齐倍数。

**约束：**

如果对齐方式为零，将引发异常。

**参数：**

* **value** （`Int`）：要对齐的值。
* **alignment** （`Int`）：要对齐的值。

**返回：**

小于或等于输入值的对齐方式的最接近倍数。换句话说，向下取整（值/对齐）\*对齐。

## `align_up`[](#align_up)

`align_up(value: Int, alignment: Int) -> Int`

返回大于或等于值的最接近对齐倍数。

**约束：**

如果对齐方式为零，将引发异常。

**参数：**

* **value** （`Int`）：要对齐的值。
* **对齐** （`Int`）：要对齐的值。

**返回：**

大于或等于输入值的对齐方式的最接近倍数。换句话说，向上取整（值/对齐）\*对齐。

## `acos`[](#acos)

`acos[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`acos`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`acos`。

## `asin`[](#asin)

`asin[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`asin`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`asin`。

## `atan`[](#atan)

`atan[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`atan`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`atan`。

## `atan2`[](#atan2)

`atan2[type: DType, simd_width: Int](arg0: SIMD[type, simd_width], arg1: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`atan2`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg0** （`SIMD[type, simd_width]`）：第一个输入参数。
* **arg1** （`SIMD[type, simd_width]`）：第二个输入参数。

**返回：**

`atan2`的输入。

## `cos`[](#cos)

`cos[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`cos`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的。`cos`

## `sin`[](#sin)

`sin[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`sin`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`sin`。

## `tan`[](#tan)

`tan[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`tan`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`tan`。

## `acosh`[](#acosh)

`acosh[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`acosh`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`acosh`。

## `asinh`[](#asinh)

`asinh[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`asinh`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`asinh`。

## `atanh`[](#atanh)

`atanh[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`atanh`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`atanh`。

## `cosh`[](#cosh)

`cosh[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`cosh`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`cosh`。

## `sinh`[](#sinh)

`sinh[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`sinh`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`sinh`。

## `expm1`[](#expm1)

`expm1[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`expm1`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`expm1`。

## `log10`[](#log10)

`log10[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`log10`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`log10`。

## `log1p`[](#log1p)

`log1p[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`log1p`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`log1p`。

## `logb`[](#logb)

`logb[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`logb`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的。`logb`

## `cbrt`[](#cbrt)

`cbrt[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`cbrt`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`cbrt`。

## `hypot`[](#hypot)

`hypot[type: DType, simd_width: Int](arg0: SIMD[type, simd_width], arg1: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`hypot`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg0** （`SIMD[type, simd_width]`）：第一个输入参数。
* **arg1** （`SIMD[type, simd_width]`）：第二个输入参数。

**返回：**

的输入`hypot`。

## `erfc`[](#erfc)

`erfc[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`erfc`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`erfc`。

## `lgamma`[](#lgamma)

`lgamma[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`lgamma`。

**Constraints:**

The input must be of floating point type.

**Parameters:**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** (): The width of the input and output SIMD vector.`Int`

**参数:**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`lgamma`.

## `tgamma`[](#tgamma)

`tgamma[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`tgamma`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`tgamma`。

## `nearbyint`[](#nearbyint)

`nearbyint[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入。`nearbyint`

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`nearbyint`。

## `rint`[](#rint)

`rint[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`rint`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`rint`。

## `remainder`[](#remainder)

`remainder[type: DType, simd_width: Int](arg0: SIMD[type, simd_width], arg1: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`remainder`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg0** （`SIMD[type, simd_width]`）：第一个输入参数。
* **arg1** （`SIMD[type, simd_width]`）：第二个输入参数。

**返回：**

`remainder`的输入。

## `nextafter`[](#nextafter)

`nextafter[type: DType, simd_width: Int](arg0: SIMD[type, simd_width], arg1: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`nextafter`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg0** （`SIMD[type, simd_width]`）：第一个输入参数。
* **arg1** （`SIMD[type, simd_width]`）：第二个输入参数。

**返回：**

`nextafter`的输入。

## `j0`[](#j0)

`j0[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`j0`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`j0`。

## `j1`[](#j1)

`j1[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`j1`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`j1`。

## `y0`[](#y0)

`y0[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`y0`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`y0`。

## `y1`[](#y1)

`y1[type: DType, simd_width: Int](arg: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`y1`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg** （`SIMD[type, simd_width]`）：输入参数。

**返回：**

输入的`y1`。

## `scalb`[](#scalb)

`scalb[type: DType, simd_width: Int](arg0: SIMD[type, simd_width], arg1: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算输入`scalb`。

**约束：**

输入必须是浮点类型。

**Parameters：**

* **type** （`DType`）：输入和输出 SIMD 矢量的`dtype`。
* **simd\_width** （`Int`）：输入和输出 SIMD 矢量的宽度。

**参数：**

* **arg0** （`SIMD[type, simd_width]`）：第一个输入参数。
* **arg1** （`SIMD[type, simd_width]`）：第二个输入参数。

**返回：**

`scalb`的输入。

## `gcd`[](#gcd)

`gcd(a: Int, b: Int) -> Int`

计算两个整数的最大公约数。

**约束：**

输入必须是非负整数。

**参数：**

* **a** （`Int`）：第一个输入参数。
* **b** （`Int`）：第二个输入参数。

**返回：**

`gcd`的输入。

## `lcm`[](#lcm)

`lcm(a: Int, b: Int) -> Int`

计算两个整数的最小公约数。

**约束：**

输入必须是非负整数。

**参数：**

* **a** （`Int`）：第一个输入参数。
* **b** （`Int`）：第二个输入参数。

**返回：**

`lcm`的输入。

## `factorial`[](#factorial)

`factorial(n: Int) -> Int`

计算整数的阶乘。

**参数：**

* **n** （`Int`）：输入值。

**返回：**

输入的阶乘。

## `nan`[](#nan)

`nan[type: DType]() -> SIMD[type, 1]`

获取给定 dtype 的 NaN 值。

**约束：**

只能用于 FP dtype。

**参数：**

* **type** （`DType`）：值的 dtype。

**返回：**

给定 dtype 的 NaN 值。

## `isnan`[](#isnan)

`isnan[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[bool, simd_width]`

检查值是否不是数字 （NaN）。

**参数：**

* **type** （`DType`）：值的 dtype。
* **simd\_width** （`Int`）： SIMD 矢量的宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：要检查的值。

**返回：**

如果 val 为 NaN，则为 true，否则为 False。

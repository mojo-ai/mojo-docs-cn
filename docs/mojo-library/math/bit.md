# bit

提供位操作函数。

可以从`math`包中导入这些 API。例如：

```
from math.bit import ctlz
```

## `ctlz`[](#ctlz)

`ctlz(val: Int) -> Int`

计算整数的前导零的数目。

**参数：**

* **val** （`Int`）：输入值。

**返回：**

输入的前导零数。

`ctlz[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算 SIMD 矢量中每个元素的前导零数。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素包含输入值`i`位置的前导零的数量。

## `cttz`[](#cttz)

`cttz(val: Int) -> Int`

计算整数的尾随零数。

**参数：**

* **val** （`Int`）：输入值。

**返回：**

输入的尾随零数。

`cttz[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算 SIMD 矢量的尾随零数。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素包含输入值`i`位置处的尾随零数。

## `select`[](#select)

`select[type: DType, simd_width: Int](cond: SIMD[bool, simd_width], true_case: SIMD[type, simd_width], false_case: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

根据输入条件值执行元素选择。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **cond** （`SIMD[bool, simd_width]`）：条件。
* **true\_case** （`SIMD[type, simd_width]`）： 条件为 True 时要选取的值。
* **false\_case** （`SIMD[type, simd_width]`）： 条件为 False 时要选取的值。

**返回：**

一个 SIMD 值，其中`i`位置的元素包含`true_case[i]` 如果`cond[i]` 为 True ，相反则为`false_case[i]`。

## `bitreverse`[](#bitreverse)

`bitreverse[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

反转整数值的位模式。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中位于`i`位置的元素具有位于输入值`i`位置的元素的整数值的反向位模式。

## `bswap`[](#bswap)

`bswap[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

字节交换值。

将整数值或整数值的向量与偶数字节（16 位的正倍数）进行字节交换。这等效于具有以下语义的`llvm.bswap`内部函数：

`llvm.bswap.i16`内部函数返回一个 i16 值，该值交换了输入 i16 的高字节和低字节。类似地，`llvm.bswap.i32`内部函数返回一个 i32 值，该值交换了输入 i32 的四个字节，因此，如果输入字节编号为 0、1、2、3，则返回的 i32 的字节将按 3、2、1、0 顺序排列。`llvm.bswap.i48`，`llvm.bswap.i64` 和其他内部函数将此概念扩展到其他偶数字节长度（分别为 6 字节、8 字节和更多）。

**约束：**

字节数必须为偶数（位宽 % 16 == 0）。DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素是输入值`i`位置的元素的值，其字节已交换。

## `ctpop`[](#ctpop)

`ctpop[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算值中设置的位数。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素包含输入值`i`位置的元素中设置的位数。

## `bit_not`[](#bit_not)

`bit_not[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

对积分执行按位 NOT 运算。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。
**返回：**

一个 SIMD 值，其中`i`位置的元素计算为输入值`i`位置处整数值的按位逻辑非运算。

## `bit_and`[](#bit_and)

`bit_and[type: DType, simd_width: Int](a: SIMD[type, simd_width], b: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

执行按位与运算。

**约束：**

DType 必须是整数。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **a** （`SIMD[type, simd_width]`）：第一个输入值。
* **b** （`SIMD[type, simd_width]`）：第二个输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素计算为输入值`i`位置的元素的按位与。

## `bit_length`[](#bit_length)

`bit_length[type: DType, simd_width: Int](val: SIMD[type, simd_width]) -> SIMD[type, simd_width]`

计算表示整数所需的位数。

**约束：**

DType 必须是整数。该函数在调试版本中断言非整型 dtype，并在发布版本中返回 0。

**Parameters：**

* **type** （`DType`）：用于计算的`dtype`。
* **simd\_width** （`Int`）： 用于计算的 SIMD 宽度。

**参数：**

* **val** （`SIMD[type, simd_width]`）：输入值。

**返回：**

一个 SIMD 值，其中`i`位置的元素等于表示输入值`i`位置的整数所需的位数。

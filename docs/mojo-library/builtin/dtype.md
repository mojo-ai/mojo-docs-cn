# dtype

实现 DType 类。

这些是 Mojo 内置的，因此您无需导入它们。

## `DType`[](#dtype)

表示 DType 并提供使用它的方法。

**别名：**

* `type = dtype`

<!---->

* `invalid = invalid`：表示无效或未知的数据类型。

<!---->

* `bool = bool`：表示布尔数据类型。

<!---->

* `int8 = si8`：表示位宽为 8 的有符号整数类型。

<!---->

* `uint8 = ui8`：表示位宽为 8 的无符号整数类型。

<!---->

* `int16 = si16`：表示位宽为 16 的有符号整数类型。

<!---->

* `uint16 = ui16`：表示位宽为 16 的无符号整数类型。

<!---->

* `int32 = si32`：表示位宽为 32 的有符号整数类型。

<!---->

* `uint32 = ui32`：表示位宽为 32 的无符号整数类型。

<!---->

* `int64 = si64`：表示位宽为 64 的有符号整数类型。

<!---->

* `uint64 = ui64`：表示位宽为 64 的无符号整数类型。

<!---->

* `bfloat16 = bf16`：表示位宽为 16 的大脑浮点值。

<!---->

* `float16 = f16`：表示 IEEE754-2008 `binary16` 浮点值。

<!---->

* `float32 = f32`：表示 IEEE754-2008 `binary32` 浮点值。

<!---->

* `float64 = f64`：表示 IEEE754-2008 `binary64` 浮点值。

<!---->

* `index = index`：表示其位宽是系统上最大整数值的整数类型。

<!---->

* `address = address`：表示其位宽与硬件指针类型的位宽相同的指针类型（32 位计算机上为 32 位，64 位计算机上为 64 位）。

**域：**

* **value ** （`dtype`）：DType 值的基础存储。

**函数：**

### `__init__`[](#init__)

`__init__(value: dtype) -> Self`

### `__eq__`[](#eq__)

`__eq__(self: Self, rhs: Self) -> Bool`

将一个 DType 与另一个 DType 进行比较以实现相等。

**参数：**

* **rhs** （`Self`）： 要比较的 DType。

**返回：**

如果 DType 相同，则为 True，否则为 False。

### `__ne__`[](#ne__)

`__ne__(self: Self, rhs: Self) -> Bool`

将一个 DType 与另一个 DType 进行比较以获得不相等。

**参数：**

* **rhs** （`Self`）： 要比较的 DType。

**返回：**

如果 DType 相同，则为 False，否则为 True。

### `__str__`[](#str__)

`__str__(self: Self) -> StringLiteral`

获取 DType 的名称。

**返回：**

dtype 的名称。

### `get_value`[](#get_value)

`get_value(self: Self) -> dtype`

获取关联的内部 kgen.dtype 值。

**返回：**

kgen.dtype 值。

### `isa`[](#isa)

`isa[other: Self](self: Self) -> Bool`

检查此 DType 是否与指定为参数的另一个 DType 匹配。

**参数：**

* **other ** （`Self`）： 要比较的 DType。

**返回：**

如果 DType 相同，则为 True，否则为 False。

### `is_bool`[](#is_bool)

`is_bool(self: Self) -> Bool`

检查此 DType 是否为布尔值。

**返回：**

如果 DType 为布尔值，则为 True，否则为 False。

### `is_uint8`[](#is_uint8)

`is_uint8(self: Self) -> Bool`

检查此 DType 是否为 UInt8。

**返回：**

如果 DType 为 UInt8，则为 True，否则为 False。

### `is_int8`[](#is_int8)

`is_int8(self: Self) -> Bool`

检查此 DType 是否为 Int8。

**返回：**

如果 DType 为 Int8，则为 True，否则为 False。

### `is_uint16`[](#is_uint16)

`is_uint16(self: Self) -> Bool`

检查此 DType 是否为 UInt16。

**返回：**

如果 DType 为 UInt16，则为 True，否则为 False。

### `is_int16`[](#is_int16)

`is_int16(self: Self) -> Bool`

检查此 DType 是否为 Int16。

**返回：**

如果 DType 为 Int16，则为 True，否则为 False。

### `is_uint32`[](#is_uint32)

`is_uint32(self: Self) -> Bool`

检查此 DType 是否为 UInt32。

**返回：**

如果 DType 为 UInt32，则为 True，否则为 False。

### `is_int32`[](#is_int32)

`is_int32(self: Self) -> Bool`

检查此 DType 是否为 Int32。

**返回：**

如果 DType 为 Int32，则为 True，否则为 False。

### `is_uint64`[](#is_uint64)

`is_uint64(self: Self) -> Bool`

检查此 DType 是否为 UInt64。

**返回：**

如果 DType 为 UInt64，则为 True，否则为 False。

### `is_int64`[](#is_int64)

`is_int64(self: Self) -> Bool`

检查此 DType 是否为 Int64。

**返回：**

如果 DType 为 Int64，则为 True，否则为 False。

### `is_bfloat16`[](#is_bfloat16)

`is_bfloat16(self: Self) -> Bool`

检查此 DType 是否为 BFloat16。

**返回：**

如果 DType 为 BFloat16，则为 true，否则为 False。

### `is_float16`[](#is_float16)

`is_float16(self: Self) -> Bool`

检查此 DType 是否为 Float16。

**返回：**

如果 DType 为 Float16，则为 True，否则为 False。

### `is_float32`[](#is_float32)

`is_float32(self: Self) -> Bool`

检查此 DType 是否为 Float32。

**返回：**

如果 DType 为 Float32，则为 True，否则为 False。

### `is_float64`[](#is_float64)

`is_float64(self: Self) -> Bool`

检查此 DType 是否为 Float64。

**返回：**

如果 DType 为 Float64，则为 True，否则为 False。

### `is_index`[](#is_index)

`is_index(self: Self) -> Bool`

检查此 DType 是否为索引。

**返回：**

如果 DType 为索引，则为 True，否则为 False。

### `is_address`[](#is_address)

`is_address(self: Self) -> Bool`

检查此 DType 是否为“地址”。

**返回：**

如果 DType 为“地址”则为 true，否则为 false。

### `is_unsigned`[](#is_unsigned)

`is_unsigned(self: Self) -> Bool`

如果类型参数无符号，则返回 True，否则返回 False。

**返回：**

如果输入类型参数无符号，则返回 True。

### `is_signed`[](#is_signed)

`is_signed(self: Self) -> Bool`

如果类型参数是有符号的，则返回 True，否则返回 False。

**返回：**

如果输入类型参数是有符号的，则返回 True。

### `is_integral`[](#is_integral)

`is_integral(self: Self) -> Bool`

如果类型参数为整数，则返回 True，否则返回 False。

**返回：**

如果输入类型参数为整数，则返回 True。

### `is_floating_point`[](#is_floating_point)

`is_floating_point(self: Self) -> Bool`

如果类型参数为浮点数，则返回 True，否则返回 False。

**返回：**

如果输入类型参数为浮点数，则返回 True。

### `sizeof`[](#sizeof)

`sizeof(self: Self) -> Int`

返回当前 DType 的大小（以字节为单位）。

**返回：**

返回当前 DType 的大小（以字节为单位），如果大小未知，则返回 -1。

### `bitwidth`[](#bitwidth)

`bitwidth(self: Self) -> Int`

返回当前 DType 的大小（以位为单位）。

**返回：**

返回当前 DType 的大小（以位为单位），如果大小未知，则返回 -1。

### `dispatch_integral`[](#dispatch_integral)

`dispatch_integral[func: fn[DType]() capturing -> None](self: Self)`

派发与当前 DType 对应的整数函数。

**约束：**

DType 必须是整数类型。

**Parameters：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

`dispatch_integral[func: fn[DType]() capturing -> None](self: Self, out_chain: OutputChainPtr)`

派发与当前 DType 对应的整数函数。

**约束：**

DType 必须是整数类型。

**Parameters：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

**参数：**

* **out\_chain** （`OutputChainPtr`）： 用于报告错误的输出链。

### `dispatch_floating`[](#dispatch_floating)

`dispatch_floating[func: fn[DType]() capturing -> None](self: Self)`

调度与当前 DType 对应的浮点函数。

**约束：**

DType 必须是浮点数。

**参数：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

`dispatch_floating[func: fn[DType]() capturing -> None](self: Self, out_chain: OutputChainPtr)`

调度与当前 DType 对应的浮点函数。

**约束：**

DType 必须是浮点数或整数型。

**Parameters：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

**参数：**

* **out\_chain** （`OutputChainPtr`）： 用于报告错误的输出链。

### `dispatch_arithmetic`[](#dispatch_arithmetic)

`dispatch_arithmetic[func: fn[DType]() capturing -> None](self: Self)`

派发与当前 DType 对应的函数。

**Parameters：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

`dispatch_arithmetic[func: fn[DType]() capturing -> None](self: Self, out_chain: OutputChainPtr)`

派发与当前 DType 对应的函数。

**Parameters：**

* **func** （`fn[DType]() capturing -> None`）：在要调度的 dtype 函数上参数化。

**参数：**

* **out\_chain** （`OutputChainPtr`）： 用于报告错误的输出链。

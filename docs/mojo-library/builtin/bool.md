# 布尔

实现布尔类。

这些是Mojo内置的，无需导入。

## `Bool`[](#bool)

Mojo 中使用的原始布尔标量值。

**域：**

* **value ** （`scalar<bool>`）：布尔值的基础存储。

**函数：**

### `__init__`[](#init__)

`__init__(value: i1) -> Self`

给定一个 \_\_mlir\_type.i1 值，构造布尔值。

**参数：**

* **value ** （`i1`）：初始 \_\_mlir\_type.i1 值。

**返回：**

构造的布尔值。

`__init__[width: Int](value: SIMD[bool, width]) -> Self`

在给定 SIMD 值的情况下构造一个布尔值。

如果 SIMD 值中有多个元素，则使用 and 运算符减小值。

**参数：**

* **value** （`SIMD[bool, width]`）：初始 SIMD 值。

**返回：**

构造的布尔值。

`__init__(value: scalar<bool>) -> Self`

### `__bool__`[](#bool__)

`__bool__(self: Self) -> Self`

转换为布尔值。

**返回：**

此值。

### `__mlir_i1__`[](#mlir_i1__)

`__mlir_i1__(self: Self) -> i1`

将此布尔值转换为 \_\_mlir\_type.i1。

此方法是编译器用于在控制流条件下测试布尔对象的特殊钩子。它应该由 Bool 实现，而不是其他布尔可转换类型实现（它们应该实现`__bool__`）。

**返回：**

布尔值的基础值。

### `__invert__`[](#invert__)

`__invert__(self: Self) -> Self`

反转布尔值。

**返回：**

如果对象为假，则为 true，否则为 False。

### `__eq__`[](#eq__)

`__eq__(self: Self, rhs: Self) -> Self`

将此布尔值与 RHS 进行比较。

执行布尔值和参数之间的相等比较。当用户使用`==`时，将调用此方法。

**参数：**

* **rhs** （`Self`）：相等语句的 rhs 值。

**返回：**

如果两个值匹配，则为 True，否则为 False。

### `__ne__`[](#ne__)

`__ne__(self: Self, rhs: Self) -> Self`

将此布尔值与 RHS 进行比较。

在布尔值和参数之间执行非相等比较。当用户使用`!=`时，将调用此方法。

**参数：**

* **rhs** （`Self`）：不相等语句的 rhs 值。

**返回：**

如果两个值匹配，则为 False，否则为 True。

### `__and__`[](#and__)

`__and__(self: Self, rhs: Self) -> Self`

计算 `self & rhs` 。

将布尔值和参数进行按位与操作。当用户使用`and`时，将调用此方法。

**参数：**

* **rhs** （`Self`）：和语句的 rhs 值。

**返回：**

`self & rhs`.

### `__or__`[](#or__)

`__or__(self: Self, rhs: Self) -> Self`

计算 `self | rhs` 。

将布尔值和参数进行按位或操作。当用户使用`or`时，将调用此方法。

**参数：**

* **rhs** （`Self`）： 或语句的 rhs 值。

**返回：**

`self | rhs`.

### `__xor__`[](#xor__)

`__xor__(self: Self, rhs: Self) -> Self`

计算`self ^ rhs`。

将布尔值和参数进行按位异或操作。当用户使用`^`时，将调用此方法。

**参数：**

* **rhs** （`Self`）：异或语句的 rhs 值。

**返回：**

`self ^ rhs`.

### `__rand__`[](#rand__)

`__rand__(self: Self, value: Self) -> Self`

返回`value & self`。

**参数：**

* value （`Self`）：另一个值。

**返回：**

`value & self`.

### `__ror__`[](#ror__)

`__ror__(self: Self, value: Self) -> Self`

返回`value | self`。

**参数：**

* value （`Self`）：另一个值。

**返回：**

`value | self`.

### `__rxor__`[](#rxor__)

`__rxor__(self: Self, value: Self) -> Self`

返回`value ^ self`。

**参数：**

* value （`Self`）：另一个值。

**返回：**

`value ^ self`.

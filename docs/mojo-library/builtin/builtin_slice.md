# builtin\_slice

实现切片。

这些是Mojo内置的，因此您无需导入它们。

## `slice`[](#slice)

表示一个切片表达式。

此类型的对象是在使用切片语法`[a:b:c]`时生成的。

**域：**

* **start** （`Int`）：切片的起始索引。

<!---->

* **end** （`Int`）：切片的结束索引。

<!---->

* **step** （`Int`）：切片的步长增量值。

**函数：**

### `__init__`[](#init__)

`__init__(end: Int) -> Self`

在给定结束值的情况下构造切片。

**参数：**

* **end**  （`Int`）：结束值。

**返回：**

构造的切片。

`__init__(start: Int, end: Int) -> Self`

在给定开始值和结束值的情况下构造切片。

**参数：**

* **start** （`Int`）：起始值。
* **end** （`Int`）：结束值。

**返回：**

构造的切片。

`__init__[T0: AnyType, T1: AnyType, T2: AnyType](start: T0, end: T1, step: T2) -> Self`

在给定开始、结束和步长值的情况下构造切片。

**Parameters：**

* **T0** （`AnyType`）：起始值的类型。
* **T1** （`AnyType`）：结束值的类型。
* **T2** （`AnyType`）：步长值的类型。

**参数：**

* **start** （`T0`）：起始值。
* **end** （`T1`）：结束值。
* **step** （`T2`）：步骤值。

**返回：**

构造的切片。

### `__getitem__`[](#getitem__)

`__getitem__(self: Self, idx: Int) -> Int`

获取切片索引。

**参数：**

* **idx** （`Int`）： 索引。

**返回：**

切片索引。

### `__eq__`[](#eq__)

`__eq__(self: Self, other: Self) -> Bool`

将此切片与另一个切片进行比较。

**参数：**

* **其他** （`Self`）：要比较的切片。

**返回：**

如果此切片的开始值、结束值和步长值与另一个切片的相应值匹配，则为 True;否则为 False。

### `__ne__`[](#ne__)

`__ne__(self: Self, other: Self) -> Bool`

将此切片与另一个切片进行比较。

**参数：**

* **other** （`Self`）：要比较的切片。

**返回：**

如果此切片的开始值、结束值和步长值与另一个切片的相应值匹配，则为 False;否则为 True。

### `__len__`[](#len__)

`__len__(self: Self) -> Int`

返回切片的长度。

**返回：**

切片的长度。

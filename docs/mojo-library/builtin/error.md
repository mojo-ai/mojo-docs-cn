# 错误

实现错误类。

这些是Mojo内置的，因此您无需导入它们。

## `Error`[](#error)

此类型表示错误。

**域：**

* **data** （`DTypePointer[si8]`）：指向被引用的字符串数据的开头的指针。

<!---->

* **loaded\_length** （`Int`）：被引用的字符串的长度。错误实例有条件地拥有其错误消息。为了减小错误实例的大小，我们使用长度字段的符号位来存储所有权值。当loaded\_length为负数时，表示所有权，并在析构函数中自由执行。

**函数：**

### `__init__`[](#init__)

`__init__() -> Self`

默认构造函数。

**返回：**

构造的错误对象。

`__init__(value: StringLiteral) -> Self`

使用给定字符串文本构造 Error 对象。

**参数：**

* **value ** （`StringLiteral`）：错误消息。

**返回：**

构造的错误对象。

`__init__(src: String) -> Self`

使用给定字符串构造一个 Error 对象。

**参数：**

* **src** （`String`）： 错误消息。

**返回：**

构造的错误对象。

`__init__(src: StringRef) -> Self`

使用给定的字符串 ref 构造一个 Error 对象。

**参数：**

* **src** （`StringRef`）： 错误消息。

**返回：**

构造的错误对象。

### `__copyinit__`[](#copyinit__)

`__copyinit__(existing: Self) -> Self`

创建现有错误的深层副本。

**返回：**

原始错误的副本。

### `__del__`[](#del__)

`__del__(owned self: Self)`

释放内存（如果已分配）。

### `__str__`[](#str__)

`__str__(self: Self) -> String`

将错误转换为字符串表示形式。

**返回：**

错误消息的字符串。

### `__repr__`[](#repr__)

`__repr__(self: Self) -> String`

将错误转换为可打印的表示形式。

**返回：**

错误消息的可打印表示形式。

# path 模块

别名（Aliases）：

`DIR_SEPARATOR = cond(apply(:!lit.signature<("self": !kgen.declref<@"$builtin"::@"$bool"::@Bool> borrow) -> i1> @"$builtin"::@"$bool"::@Bool::@"__mlir_i1__($builtin::$bool::Bool)", apply(:!lit.signature<() -> !kgen.declref<@"$builtin"::@"$bool"::@Bool>> @"$sys"::@"$info"::@"os_is_windows()")), #lit.struct<{value: string = "\\"}>, #lit.struct<{value: string = "/"}>)`

## Path
Path 对象

**字段（Fields）**：

- **path** (`String`): 路径的底层字符串表示。

方法（Functions）：

### `__init__`
`__init__(inout self: Self)`
用当前目录初始化路径。

`__init__(inout self: Self, path: StringLiteral)`
使用提供的路径初始化路径。

**参数（Args）**：

- **path**(`StringLiteral`): 文件系统路径。

`__init__(inout self: Self, path: StringRef)`
使用提供的路径初始化路径。

**参数（Args）：**

- **path** (`StringRef`): 文件系统路径。

`__init__(inout self: Self, path: String)`
使用提供的路径初始化路径。

**参数（Args）：**

- **path** (`String`): 文件系统路径。



### `__copyinit__`
`__copyinit__(inout self: Self, existing: Self)`
路径结构的复制构造函数。

**参数（Args）：**

- **existing** (`Self`): 要从中复制的现有结构。

### `__del__`
__del__(owned self: Self)



### `__truediv__`
`__truediv__(self: Self, suffix: Self) -> Self`
使用系统定义的路径分隔符连接两个路径。

**参数（Args）：**

- **suffix** (`Self`): 要附加到路径的后缀。

**返回（Returns）：**

带有附加后缀的新路径。

`__truediv__(self: Self, suffix: StringLiteral) -> Self`
使用系统定义的路径分隔符连接两个路径。

**参数（Args）：**

- **suffix** (`StringLiteral`): 要附加到路径的后缀。

**返回（Returns）：**

带有附加后缀的新路径。

`__truediv__(self: Self, suffix: StringRef) -> Self`
使用系统定义的路径分隔符连接两个路径。

**参数（Args）：**

- **suffix** (`StringRef`): 要附加到路径的后缀。

**返回（Returns）：**

带有附加后缀的新路径。

`__truediv__(self: Self, suffix: String) -> Self`
使用系统定义的路径分隔符连接两个路径。

**参数（Args）：**

- **suffix** (`String`): 要附加到路径的后缀。

**返回（Returns）：**

带有附加后缀的新路径。



### `__str__`
`__str__(self: Self) -> String`
返回路径的字符串表示。

**返回（Returns）：**
路径的字符串表示。



### `__repr__`
`__repr__(self: Self) -> String`
返回路径的可打印表示。

**返回（Returns）：**
路径的可打印表示。

### `cwd`
`cwd() -> Path`
获取当前目录。

**返回（Returns）：**
当前目录。

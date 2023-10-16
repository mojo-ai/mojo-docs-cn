# 文件


实现基于文件的方法。

这些是 Mojo 内置的，因此您无需导入它们。

例如，读取文件的方法如下：

```
var  f = open("my_file.txt", "r")
print(f.read())
f.close()
```

或者使用语句自动关闭文件：`with`

```
with open("my_file.txt", "r") as f:
  print(f.read())
```

## `FileHandle`[](#filehandle)

打开的文件的 FileHandle。

**域：**

* **handle** （`DTypePointer[invalid]`）：指向文件句柄的基础指针。

**函数：**

### `__init__`[](#init__)

`__init__(inout self: Self)`

默认构造函数。

`__init__(inout self: Self, path: StringLiteral, mode: StringLiteral)`

使用文件路径和模式构造 FileHandle。

**参数：**

* **路径** （`StringLiteral`）：文件路径。
* **mode** （`StringLiteral`）：打开文件的模式（模式可以是“r”或“w”）。

`__init__(inout self: Self, path: String, mode: String)`

使用文件路径和模式构造 FileHandle。

**参数：**

* **路径** （`String`）：文件路径。
* **mode** （`String`）：打开文件的模式（模式可以是“r”或“w”）。

`__init__(inout self: Self, path: StringRef, mode: StringRef)`

使用文件路径和字符串构造 FileHandle。

**参数：**

* **路径** （`StringRef`）：文件路径。
* **mode** （`StringRef`）：打开文件的模式（模式可以是“r”或“w”）。

### `__moveinit__`[](#moveinit__)

`__moveinit__(inout self: Self, owned existing: Self)`

移动 FileHandle 的构造函数。

**参数：**

* **existing** （`Self`）：现有 FileHandle。

### `__takeinit__`[](#takeinit__)

`__takeinit__(inout self: Self, inout existing: Self)`

移动 FileHandle 的构造函数。

**参数：**

* **existing** （`Self`）：现有 FileHandle。

### `__del__`[](#del__)

`__del__(owned self: Self)`

关闭 FileHandle。

### `close`[](#close)

`close(inout self: Self)`

关闭 FileHandle。

### `read`[](#read)

`read(self: Self) -> String`

从文件中读取数据。

**返回：**

文件的内容。

### `write`[](#write)

`write(self: Self, data: StringLiteral)`

将数据写入文件。

**参数：**

* **data** （`StringLiteral`）：要写入文件的数据。

`write(self: Self, data: String)`

将数据写入文件。

**参数：**

* **data** （`String`）：要写入文件的数据。

`write(self: Self, data: StringRef)`

将数据写入文件。

**参数：**

* **data** （`StringRef`）：要写入文件的数据。

### `__enter__`[](#enter__)

`__enter__(owned self: Self) -> Self`

进入上下文时要调用的函数。

## `open`[](#open)

`open(path: StringLiteral, mode: StringLiteral) -> FileHandle`

使用提供的模式打开路径指定的文件，返回 FileHandle。

**参数：**

* **path** （`StringLiteral`）：要打开的文件的路径。
* **mode** （`StringLiteral`）：打开文件的模式（模式可以是“r”或“w”）。

**返回：**

FileHandle。

`open(path: StringRef, mode: StringRef) -> FileHandle`

使用提供的模式打开路径指定的文件，返回 FileHandle。

**参数：**

* **path** （`StringRef`）：要打开的文件的路径。
* **mode** （`StringRef`）：打开文件的模式（模式可以是“r”或“w”）。

**返回：**

FileHandle。

`open(path: String, mode: String) -> FileHandle`

使用提供的模式打开路径指定的文件，返回 FileHandle。

**参数：**

* **path** （`String`）：要打开的文件的路径。
* **mode** （`String`）：打开文件的模式。

**返回：**

FileHandle。

`open(path: Path, mode: String) -> FileHandle`

使用提供的模式打开路径指定的文件，返回 FileHandle。

**参数：**

* **path** （`Path`）：要打开的文件的路径。
* **mode** （`String`）：打开文件的模式（模式可以是“r”或“w”）。

**返回：**

FileHandle。

# Python 模块

Python 模块实现了 Python 与 Mojo 之间的互操作性。

你可以从 `python` 包中导入这些 API。例如：

```python
from python import Python
```

## `Python`

提供了一些帮助你在 Mojo 中使用 Python 代码的方法。

**字段（Fields）：**

- **impl** (`_PythonInterfaceImpl`): Mojo Python 接口的底层实现。

**方法（Functions）：**

### `__init__`

`__init__(inout self: Self)`

默认构造函数。



### `__copyinit__`

`__copyinit__(inout self: Self, existing: Self)`

复制构造函数。

**参数（Args）：**

- **existing** (`Self`): 用于复制的现有实例。

  

### `eval`

`eval(inout self: Self, str: StringRef) -> Bool`

执行给定的 Python 代码。

**参数（Args）：**

- **str** (`StringRef`): 要执行的 Python 代码。

**返回（Returns）：**

如果代码执行成功则返回 `True`，如果代码引发异常则返回 `False`。



### `evaluate`

`evaluate(str: StringRef) -> PythonObject`

执行给定的 Python 代码。

**参数（Args）：**

- **str** (`StringRef`): 要评估的 Python 表达式。

返回（Returns）：

包含评估结果的 `PythonObject`。



### `add_to_path`

`add_to_path(str: StringRef)`

添加目录到 Python 路径。

这可能是为了通过 `import_module()` 导入 Python 模块。例如：

```python
from python import Python

# 指定路径到 `mypython.py` 模块
Python.add_to_path("path/to/module")
let mypython = Python.import_module("mypython")

let c = mypython.my_algorithm(2, 3)
```

**参数（Args）：**

- **str** (`StringRef`): 要导入的 Python 模块的路径。



### `import_module`

`import_module(str: StringRef) -> PythonObject`

导入 Python 模块。

这将为你提供一个模块对象，你可以像在 Python 中一样使用。例如：

```python
from python import Python

# 这等同于 Python 的 `import numpy as np`
let np = Python.import_module("numpy")
a = np.array([1, 2, 3])
```

**参数（Args）**：

- **str** (`StringRef1`): Python 模块名称。这个模块必须在可用的 Python 路径列表中可见（你可能需要使用 add_to_path() 添加模块的路径）。

**返回（Returns）**：

Python 模块。



### `dict`

`dict() -> Dictionary`

构建一个空的 Python 字典。

**返回（Returns）**：

构建的空 Python 字典。

### `__str__`

`__str__(inout self: Self, str: PythonObject) -> StringRef`

返回表示给定 Python 对象的字符串。

这个函数允许将 Python 对象转换为 Mojo 字符串类型。

**返回（Returns）**：

表示给定 Python 对象的 Mojo 字符串。



### `throw_python_exception_if_error_state`

`throw_python_exception_if_error_state(inout cpython: CPython)`

如果 CPython 解释器处于错误状态，就引发异常。

**参数（Args）**：

- **cpython** (`CPython`): 我们希望进行错误检查的 cpython 实例。



### `is_type`

`is_type(x: PythonObject, y: PythonObject) -> Bool`

测试 `x` 对象是否是 `y` 对象，与 Python 中的 `x is y` 相同。

**参数（Args）**：

- **x** (`PythonObject`): 比较中的左操作数值。
- **y** (`PythonObject`): 比较中的右操作数类型值。

**返回（Returns）**：

如果 `x` 和 `y` 是相同的对象，则返回 True，否则返回 False。



### `type`

`type(obj: PythonObject) -> PythonObject`

返回此 PythonObject 的类型。

**参数（Args）**：

- **obj** (`PythonObject`): 我们想要的 PythonObject 类型。

**返回（Returns）**：

包含类型对象的 PythonObject。



### `none`

`none() -> PythonObject`

获取表示 `None` 的 `PythonObject`。

**返回（Returns）**：

`PythonObject`，表示 `None`。

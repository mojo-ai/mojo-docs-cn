# param_env

实现了用于检索编译时定义的函数。

您可以使用这些函数根据在命令行上定义的 name-value 对来设置参数值或运行时常量。例如：

```python
from sys.param_env import is_defined
from tensor import Tensor, TensorSpec

alias float_type: DType = DType.float32 if is_defined["FLOAT32"]() else DType.float64

let spec = TensorSpec(float_type, 256, 256)
var image = Tensor[float_type](spec)
```

在命令行上：

```python
 mojo -D FLOAT_32 main.mojo
```

有关更多信息，请参阅[Mojo构建文档](https://mojo-docs-cn.vercel.app/mojo-cli/mojo-build.html)。mojo run 命令还支持 -D 选项。

你可以从 `sys` 包中导入这些 API。例如：

```python
from sys.param_env import is_defined
```

## `is_defined`

```python
is_defined[name: StringLiteral]() -> Bool
```

如果指定的值已定义，则返回 true。

**Parameters**：

- **name** (`StringLiteral`)：名称。

**Returns**：

如果名称已定义，则为true。

## `env_get_int`

```python
env_get_int[name: StringLiteral]() -> Int
```

尝试获取一个整数值定义。如果名称未定义，则编译失败。

**Parameters**：

- **name** (`StringLiteral`)：定义的名称。

**Returns**：

一个整数参数值。

```python
env_get_int[name: StringLiteral, default: Int]() -> Int
```

尝试获取一个整数值的定义。如果该名称未定义，则返回默认值。

**Parameters**：

- **name** (`StringLiteral`)：定义的名称。

- **default** (`Int`)：要使用的默认值。

**Returns**：

一个整数参数值。

## `env_get_string`

```python
env_get_string[name: StringLiteral]() -> StringLiteral
```

尝试获取一个字符串值的定义。如果该名称未定义，则编译失败。

**Parameters**：

- **name** (`StringLiteral`)：定义的名称。

**Returns**：

一个字符串参数值。

```python
env_get_string[name: StringLiteral, default: StringLiteral]() -> StringLiteral
```

尝试获取一个字符串值的定义。如果该名称未定义，则返回一个默认值。

**Parameters**：

- **name** (`StringLiteral`)：定义的名称。

- **default** (`Int`)：要使用的默认值。
  
**Returns**：

一个字符串参数值。




# env 模块

提供了与操作系统交互的基本工具。

你可以从 `os` 包中导入这些 API。例如：

```python
from os import setenv
```

## `setenv`

`setenv(name: StringRef, value: StringRef, overwrite: Bool) -> Bool`

​    修改或添加环境变量。

​    **约束（Constraints）：**

​    此函数仅在 macOS 或 Linux 上有效，否则返回 False。

​    **参数（Args）：**

- **name** (`StringRef`): 环境变量的名称。 
- **value** (`StringRef`): 环境变量的值。 
- **overwrite** (`Bool`): 如果已经存在具有给定名称的环境变量，只有在 `overwrite` 为 True 时才会更改其值。 

​    **返回（Returns）**：

​    如果名称为空或包含 = 字符，则返回 False。否则返回 True。



## `getenv`

`getenv(name: StringRef, default: StringRef) -> StringRef`

​    返回指定环境变量的值。

​    **约束（Constraints）**：

​    此函数仅在 macOS 或 Linux 上有效，否则返回空字符串。

​    **参数（Args）**：

- **name** (`StringRef`): 环境变量的名称。 
- **default** (`StringRef`): 如果环境变量不存在，要返回的默认值。 

​    **返回（Returns）**：

​    环境变量的值。



`getenv(name: StringRef) -> StringRef`

​    返回指定环境变量的值。如果环境变量不存在，将返回空字符串。

​    **约束（Constraints）**：

​    此函数仅在 macOS 或 Linux 上有效，否则返回空字符串。

​    **参数（Args）：**

- **name (`StringRef`):** 环境变量的名称。 

​    **返回（Returns）：**

​    环境变量的值。

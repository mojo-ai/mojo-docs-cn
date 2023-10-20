# arg

实现与执行和系统环境交互的函数和变量。

你可以从 `sys` 包中导入这些 API。例如：

```python
from sys import argv
```

## `argv`

```python
argv() -> VariadicList[StringRef]
```

命令行参数的列表。

**Returns**：

当调用 mojo 时提供的命令行参数列表。

# mojo

Mojo🔥 命令行接口。

## Synopsis

```python
mojo <command>
mojo [run-options] <path>
mojo [options]
mojo
```

## Description

`mojo` CLI 提供了 Mojo 开发所需的所有工具，例如：用于运行、编译和打包 Mojo 代码的命令。
下面列出了所有命令的列表，您可以通过向命令添加 `--help` 选项来了解每个命令的更多信息（例如：`mojo package --help`）。

同时，您可以省略 `run` 和 `repl` 命令。也就是说，您可以通过简单地将文件名传递给 `mojo` 来运行 Mojo 文件：

```python
mojo hello.mojo
```

您可以通过在没有命令的情况下运行 `mojo` 来启动 REPL 会话。

若将 `Mojo` 更新到最新版本，请使用 [`modular` tool](https://docs.modular.com/cli/)：

```python
modular update mojo
```

您可以使用 `mojo --version` 检查当前版本。有关 Mojo 更新的信息，请参阅 [Mojo changelog](https://docs.modular.com/mojo/changelog.html)。

## Commands

`run` - 生成并执行 Mojo 文件。

`build` - 从 Mojo 文件构建可执行文件。

`repl` - 启动 Mojo REPL。

`debug` - 启动 LLDB 调试器，支持调试 Mojo 程序。

`package ` - 编译 Mojo 包。

`format` - 格式化 Mojo 源文件。

`doc` - 从 Mojo 文件编译 docstrings。

`demangle` - 取消给定名称。

## Options

### Diagnostic options

`--version`，'-v'

打印 Mojo 版本并退出。

### Common options

`--help`，`-h`

显示帮助信息。

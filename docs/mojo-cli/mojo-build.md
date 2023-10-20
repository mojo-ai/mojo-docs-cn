# mojo build

从 Mojo 文件构建可执行文件。

## Synopsis

```python
mojo build [options] <path>
```

## Description

将给定路径处的 Mojo 文件编译为可执行文件。

默认情况下，可执行文件将保存到当前目录，其名称与输入文件相同，但是没有文件扩展名。

## Options

### Output options

`-o <PATH>`

设置可执行文件输出的路径和文件名。默认情况下，它将可执行文件输出到与 Mojo 文件相同的位置，具有相同的名称并且没有扩展名。

### Compilation options

`--no-optimization`，`-O0`

禁用编译器优化。这可能会减少编译 Mojo 源文件所需的时间。它还可能降低已编译可执行文件的运行时性能。

`--target-triple <TRIPLE>`

设置编译目标三元组。默认为主机目标。

`--target-cpu <CPU>`

设置编译目标 CPU。默认为主机 CPU。

`--target-features <FEATURES>`

设置编译目标 CPU 功能。默认为主机功能。

`-march <ARCHITECTURE>`

设置要为其生成代码的体系结构。

`-mcpu <CPU>`

设置要为其生成代码的 CPU。

`-mtune <TUNE>`

设置要为其优化代码的 CPU。

`-I <PATH>`

将给定路径附加到目录列表，用于搜索导入的 Mojo 文件。

`-D <KEY=VALUE>`

定义可从正在执行的 Mojo 源文件中使用的命名值。例如：`-D foo=42` 定义了一个名称 `foo`，当从 Mojo 程序中使用 `sys.param_env` 模块查询时，将产生编译时的值 `42`。

`--parsing-stdlib`

将输入文件解析为 Mojo 标准库。

### Diagnostic options

`--warn-missing-doc-strings`

发出 docstrings 缺失或部分告警。

`--max-notes-per-diagnostic <INTEGER>`

当 Mojo 编译器发出诊断时，它有时还会打印包含附加信息的注释。此选项设置通过诊断程序打印的注释数的上限阈值。如未指定，则默认最大值为 10。

### Experimental compilation options

`--debug-level <LEVEL>`

设置编译时要使用的调试信息级别。该值必须是以下值之一：`none`（默认值）、`line-tables` 或 `full`。注意：为某些 Mojo 程序生成调试信息时还存在若干未解决的 issues。

`--sanitize <CHECK>`

打开运行时检查。支持以下值：`address`（检测内存问题）和 `thread`（检测多线程问题）。注意：执行 Mojo 程序时不支持这些检查。

`--debug-info-language <LANGUAGE>`

设置要作为调试信息发出的语言。支持的语言：`Mojo` 和 `C`。`C` 为默认语言，这对于在不理解 Mojo 工具中启用基本调试和二进制分析时非常有用。

### Common options

`--help`，`-h`

显示帮助信息。

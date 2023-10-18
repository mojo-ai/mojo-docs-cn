# mojo run

构建并执行一个 Mojo 文件。

## Synopsis

```python
mojo run [options] <path>
```

## Description

在给定的路径上编译 Mojo 文件并立即执行它。执行此命令的另一种方式是简单地将文件传递给 mojo。例如：

```python
mojo hello.mojo
```

此命令本身的选项（如下面列出的选项）必须出现在输入文件路径参数之前。出现在 Mojo 源文件路径之后的任何命令行参数都被解释为该 Mojo 程序的参数。

## Options

### Compilation options

`--no-optimization`, `-O0`

禁用编译器优化。这可能会减少编译 Mojo 源文件所需的时间。它也可能会降低编译后可执行文件的运行时性能。

`--target-triple <TRIPLE>`

设置编译目标三元组。默认为主机目标。

`--target-cpu <CPU>`

设置编译目标CPU。默认为主机CPU。

`--target-features <FEATURES>`

设置编译目标CPU特性。默认为主机特性。

`-march <ARCHITECTURE>`

设置用于生成代码的架构。

`-mcpu <CPU>`

设置用于生成代码的CPU。

`-mtune <TUNE>`

设置用于调优代码的CPU。

`-I <PATH>`

将给定路径添加到搜索导入的 Mojo 文件的目录列表中。

`-D <KEY=VALUE>`

定义一个命名值，可以从执行的 Mojo 源文件中使用。例如：`-D foo=42` 定义了一个名为 `foo` 的值，在 Mojo 程序中使用 `sys.param_env` 模块查询时，会返回编译时的值 `42`。

`--parsing-stdlib`

将输入文件解析为 Mojo 标准库。

### Diagnostic options

`--warn-missing-doc-strings`

对于缺失或部分文档字符串发出警告。

`--max-notes-per-diagnostic <INTEGER>`

当 Mojo 编译器发出诊断时，有时还会打印附加信息的注释。此选项设置了可以与诊断一起打印的注释数量的上限。如果未指定，默认最大值为 10。

### Experimental compilation options

`--debug-level <LEVEL>`

设置编译时要使用的调试信息级别。该值必须是以下之一：`none`（默认值）、 `line-tables` 或 `full`。请注意，对于一些尚未解决的 Mojo 程序生成调试信息存在问题。

`--sanitize <CHECK>`

打开运行时检查。支持以下值：`address`（检测内存问题）和 `thread`（检测多线程问题）。请注意，在执行 Mojo 程序时，目前不支持这些检查。

`--debug-info-language <LANGUAGE>`

设置要作为调试信息的一部分发出的语言。支持的语言有：`Mojo` 和 `C`。`C` 是默认值，在不理解 Mojo 的工具中启用基本调试和二进制内省非常有用。

### Common options

`--help`, `-h`

显示帮助信息。

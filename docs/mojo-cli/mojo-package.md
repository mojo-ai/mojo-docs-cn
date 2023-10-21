# mojo package

编译一个 Mojo 包。

## Synopsis

`mojo package [options] <path>`

## Description

将一个 Mojo 源文件目录编译为一个二进制包，适合共享和导入到其他 Mojo 程序和模块中。

要创建一个 Mojo 包，首先在您的包目录中添加一个 `__init__.mojo` 文件。然后将该目录名称传递给该命令，并使用 `-o` 选项指定输出路径和文件名。

更多信息，请参阅[Mojo模块和包](https://mojo-docs-cn.vercel.app/get-started/modules-and-packages.html)。

## Options

### Output options

`-o <PATH>`

设置输出包的路径和文件名。文件名必须以 `.mojopkg` 或 `.📦` 结尾。在这里给出的文件名定义了您可以使用的包名称来导入代码（不包括文件扩展名）。如果您不指定此选项，则输出将写入标准输出( stdout )。

### Compilation options

`--no-optimization`, `-O0`

禁用编译器优化。这可能会减少编译 Mojo 源文件所需的时间。但同时也可能会降低编译后可执行文件的运行时性能。

`--target-triple <TRIPLE>`

设置编译目标三元组。默认为主机目标。

`--target-cpu <CPU>`

设置编译目标CPU。默认为主机CPU。

`--target-features <FEATURES>`

设置编译目标CPU特性。默认为主机特性。

`-march <ARCHITECTURE>`

设置生成代码的架构。

`-mcpu <CPU>`

设置要为其生成代码的CPU。

`-mtune <TUNE>`

设置要为其调整代码的CPU。

`-I <PATH>`

将给定的路径添加到搜索导入的 Mojo 文件的目录列表中。

`-D <KEY=VALUE>`

定义一个命名值，可以从正在执行的 Mojo 源文件中使用。例如：`-D foo=42` 定义了一个名为 `foo` 的名称，当使用 `sys.param_env` 模块从 Mojo 程序中查询时，将返回编译时的值`42`。

`--parsing-stdlib`

将输入文件解析为 Mojo 标准库。

### Diagnostic options

`--warn-missing-doc-strings`

对于缺失或部分文档字符串，发出警告。

`--max-notes-per-diagnostic <INTEGER>`

当 Mojo 编译器发出诊断时，有时还会打印带有附加信息的注释。此选项设置了可以与诊断一起打印的注释数量的上限。如果未指定，默认的最大值为 10。

### Experimental compilation options

`--debug-level <LEVEL>`

设置编译时要使用的调试信息级别。该值必须是以下之一：`none`（默认值），`line-tables` 或 `full`。请注意，为一些尚未解决的 Mojo 程序生成调试信息存在问题。

`--sanitize <CHECK>`

打开运行时检查。支持以下值：`address`（检测内存问题）和 `thread`（检测多线程问题）。请注意，在执行 Mojo 程序时，当前不支持这些检查。

`--debug-info-language <LANGUAGE>`

设置要作为调试信息的一部分发出的语言。支持的语言有：`Mojo` 和 `C`。 `C` 是默认值，在不理解 Mojo 的工具中启用基本调试和二进制内省非常有用。

### Common options

`--help`, `-h`

显示帮助信息。

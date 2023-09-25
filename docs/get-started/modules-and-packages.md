# Mojo 模块和软件包

Mojo 提供了一个打包系统，允许将代码库组织和编译为可导入文件。本页介绍了有关如何将代码组织到模块和包（这很像 Python），并展示如何使用 [`mojo package`](https://docs.modular.com/mojo/cli/package.html)命令创建打包的二进制文件。

## [Mojo 模块](#mojo-modules)

要了解 Mojo 包，首先需要了解 Mojo 模块。Mojo 模块是单个 Mojo 源文件，其中包含适合由导入它的其他文件使用的代码。例如，可以创建一个模块来定义结构，如下所示：

```
mymodule.mojo
```

```
struct MyPair:
    var first: Int
    var second: Int

    fn __init__(inout self, first: Int, second: Int):
        self.first = first
        self.second = second

    fn dump(self):
        print(self.first, self.second)
```

请注意，此代码没有 `main()` 函数，因此无法执行 `mymodule.mojo` 。但是，您可以将其导入另一个带有 `main()` 函数的文件并执行。

例如，下面介绍了如何导入 `MyPair` 到与 `main.mojo` 位于同一目录中的名为 `mymodule.mojo` 的文件：

```
main.mojo
```

```
from mymodule import MyPair

fn main():
    let mine = MyPair(2, 4)
    mine.dump()
```

或者，您可以导入整个模块，然后通过模块名称访问其成员。例如：

```
main.mojo
```

```
import mymodule

fn main():
    let mine = mymodule.MyPair(2, 4)
    mine.dump()
```

还可以使用 `as` 为导入的成员创建别名，如下所示：

```
main.mojo
```

```
import mymodule as my

fn main():
    let mine = my.MyPair(2, 4)
    mine.dump()
```

在此示例中，仅当 `mymodule.mojo` 与 `main.mojo` 位于同一目录中时，代码才可以允许。目前，如果文件位于其他目录中，则无法将 `.mojo` 文件作为模块导入。或者如下一节所述，也可以将目录视为 Mojo 包。

__

**注意：** Mojo 模块可能包含一个 `main()` 函数，也可能是可执行的，但这通常不是惯例，模块通常包括要导入并在其他 Mojo 程序中使用的 API。

## [Mojo 包](#mojo-packages)

Mojo 包是同一目录中 Mojo 模块的集合，此目录包含一个 `__init__.mojo` 文件。通过在目录中将模块组织在一起，可以一起导入或单独导入所有模块。还可以选择将包编译为更易于共享的 `.mojopkg` 或 `.📦` 文件。

您可以直接从源文件或编译的 `.mojopkg`/`.📦` 文件导入包及其模块。两者导入包的方式对 Mojo 没有本质的区别。从源文件导入时，目录名称用作包名称，而从已编译的包导入时，文件名是包名称（可以使用 [`mojo package`](https://docs.modular.com/mojo/cli/package.html)命令指定，可以与目录名称不同）。

例如，考虑具有以下文件的项目：

```
main.mojo
mypackage/
    __init__.mojo
    mymodule.mojo
```

`mymodule.mojo`与上述示例（带有 `MyPair` 结构体）中的代码相同，并且 `__init__.mojo` 为空。

在这种情况下，`main.mojo` 文件现在可以通过包名称导入 `MyPair` ，如下所示：
```
main.mojo
```

```
from mypackage.mymodule import MyPair

fn main():
    let mine = my.MyPair(2, 4)
    mine.dump()
```

请注意，这里 `__init__.mojo` 至关重要。如果删除它，则Mojo无法将该目录识别为包，并且无法导入 `mymodule` 。

然后，假设不希望 `mypackage` 源代码与 `main.mojo` 位于同一位置，可以将其编译成这样的包文件：

```
mojo package mypackage -o mypack.mojopkg
```

然后可以将 `mypackage` 源移动到其他位置，项目文件现在如下所示：

```
main.mojo
mypack.mojopkg
```

因为我们命名的包文件与目录不同，所以我们需要修复 import 语句：

```
main.mojo
```

```
from mypack.mymodule import MyPair
```

__

**注意：**如果要重命名包，则不能简单地编辑 `.mojopkg` 或 `.📦` 文件名，因为包名称已编码在文件中。您必须改为再次运行 `mojo package` 以指定新名称。

### [`__init__` 文件](#the-__init__-file)

如上所述，当目录被视为 Mojo 包时，必须包含 `__init__.mojo` 文件，并且可以为空。

目前， `.mojo` 文件中不支持顶级代码，因此与 Python 不同，无法在 `__init__.mojo` 文件中编写导入时执行的代码。但是，可以添加结构和函数，然后可以从包名称导入这些结构和函数。

然而，可以导入模块成员，而不是在 `__init__.mojo` 文件中添加 API，这和通过包名访问 API 效果一样，后者还需要 `<package_name>.<module_name>` 声明。

例如，假设有以下文件：

```
main.mojo
mypackage/
    __init__.mojo
    mymodule.mojo
```

现在让我们在 `__init__.mojo` 中添加以下行：

```
__init__.mojo
```

```
from .mymodule import MyPair
```

然后，可以再`main.mojo` 简化导入语句：

```
main.mojo
```

```
from mypackage import MyPair
```

此功能解释了为什么 Mojo 标准库中的某些成员可以从其包名称导入，而其他成员则需要表示 `<package_name>.<module_name>` 声明。例如，[`functional`](https://docs.modular.com/mojo/stdlib/algorithm/functional.html)模块包含在 `algorithm` 包中，因此您可以像这样导入该模块的成员（例如 `map()` 函数）：

```
from algorithm.functional import map
```

但是，`algorithm/__init__.mojo` 文件还包括以下行：
```
algorithm/__init__.mojo
```

```
from .functional import *
from .reduction import *
```

因此，通过声明包，您实际上可以从`functional` 或 `reduction` 包中导入任何内容。哪怕导入语句中删除 `functional` ，它也可以工作：

```
from algorithm import map
```

__

**注意：**将标准库中的哪些模块导入到包范围会有所不同，并且可能会发生变化。请参阅 [每个模块的文档](https://docs.modular.com/mojo/lib.html)，了解如何导入其成员。

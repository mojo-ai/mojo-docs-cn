Mojo 是一种功能强大的编程语言，主要用于高性能系统编程，因此它与 Rust 和 C++ 等其他系统语言有很多共同之处。然而，Mojo 也被设计成 Python 的超集，所以 Python 中许多语言功能和概念都可以很好地翻译成 Mojo。

例如，如果您位于 REPL 环境或 Jupyter notebook（如本文档）中，则可以像 Python 一样运行顶级代码：

```
print("Hello Mojo!")
```

```
Hello Mojo!
```

在其他系统编程语言中，您通常看不到这一点。

Mojo 保留了 Python 的动态功能和语言语法，它甚至允许你从 Python 包导入和运行代码。然而，重要的是 Mojo 是一种全新的语言，而不仅仅是带有语法糖的 Python 的新实现。Mojo 将 Python 语言提升到一个全新的水平，具有系统编程功能，强大的类型检查，内存安全，下一代编译器技术等等。然而，它仍然被设计为一种对通用编程有用的简单语言。

本页提供了对 Mojo 语言的简短介绍，只需要一点编程经验。所以让我们开始吧！

如果您是一位经验丰富的系统程序员，并且想要深入了解该语言，请查看 [Mojo 编程手册](https://docs.modular.com/mojo/programming-manual.html)。

## 语言基础[](#language-basics)

首先，Mojo 是一种编译语言，它的许多性能和内存安全功能都源于这一事实。Mojo 代码可以提前 （AOT） 或实时 （JIT） 编译。

像其他编译语言一样，Mojo 程序（ `.mojo`或`.🔥`文件）需要一个 `main()` 函数作为程序的入口点。例如：

```
fn main():
    var x: Int = 1
    x += 1
    print(x)
```

如果您了解 Python，可能期望函数名称是`def main()`而不是`fn main()` .两者实际上都可以在 Mojo 中运行，但使用`fn`略有不同，我们将在下面讨论。

当然，如果你正在构建一个 Mojo 模块（API 库），而不是一个 Mojo 程序，那么你的文件不需要`main()`函数（因为它将被其他有函数的程序导入）。

**注意：**当在 `.mojo`/`.🔥` 文件中编写代码时，无法运行此页面上所示的顶级代码——Mojo 程序或模块中的所有代码都必须封装在函数或结构中。但是，顶级代码在 REPL 或 Jupyter notebook（例如 [HelloMojo](https://github.com/modularml/mojo/blob/main/examples/notebooks/HelloMojo.ipynb)）中可以运行。

现在让我们解释一下 `main()` 函数中的代码。

### 语法和语义[](#syntax-and-semantics)

这很简单：Mojo 支持（或将支持）所有 Python 的语法和语义。如果你不熟悉 Python 语法，网上有很多很棒的资源可以教你。

例如，与 Python 一样，Mojo 使用换行符和缩进来定义代码块（不是大括号），Mojo 支持 Python 的所有控制流语法，例如`if`条件和`for`循环。

但是，Mojo 仍在演进中，因此 Python 中的一些内容尚未在 Mojo 中实现（参见 [Mojo 路线图](https://docs.modular.com/mojo/roadmap.html)）。所有缺失的 Python 功能都会及时实现，并且 Mojo 已经包含了 Python 中许多可用的特性和功能。

因此，以下各节将重点介绍 Mojo 独有的一些语言功能（与 Python 相比）。

### 函数[](#functions)

Mojo 函数可以用 `fn`（如上所示）或 `def`（如 Python）声明。 `fn` 声明强制实施强类型和内存安全行为， `def` 同时提供 Python 样式的动态行为。

 `fn` 和 `def` 函数都有其价值，学习它们很重要。但是，出于本介绍的目的，我们将仅关注 `fn` 函数。有关两者的更多详细信息，请参阅 [编程手册](https://docs.modular.com/mojo/programming-manual.html)。

在以下部分中，你将了解 `fn` 函数如何在代码中强制实施强类型和内存安全行为。

### 变量[](#variables)

您可以声明变量（例如上面`main()`函数中的`x`），使用 `var` 以创建可变值，或 使用 `let` 创建不可变值。

如果在上面的 `main()` 函数中将 `var` 更改为 `let` 并运行，则会收到如下编译器错误：

```
error: Expression [15]:7:5: expression must be mutable for in-place operator destination
    x += 1
    ^
```

这是因为 `let` 值不可变，因此无法递增。

如果完全删除 `var` 变量，则会收到报错，因为 `fn` 函数需要显式变量声明（与 Python 的 `def` 函数不同）。

最后，请注意， `x` 变量明确为 `Int` 类型。 `fn` 中的变量不需要声明类型，但有时是需要的。如果省略它，Mojo 会推断类型，如下所示：

```
fn do_math():
    let x: Int = 1
    let y = 2
    print(x + y)

do_math()
```

```
3
```

### 函数参数和返回[](#function-arguments-and-returns)

尽管函数体中声明的变量不需要类型，但 `fn` 函数的参数和返回值需要类型。

例如，下面介绍如何将 `Int` 类型声明为函数参数和返回值的类型：

```
fn add(x: Int, y: Int) -> Int:
    return x + y

z = add(1, 2)
print(z)
```

```
3
```

#### 参数可变性和所有权[](#argument-mutability-and-ownership)

Mojo 支持全值语义，并通过强大的值所有权模型（类似于 Rust 借用检查器）强制实施内存安全。所以下面简单介绍一下可以通过函数参数共享对值的引用。

请注意，上述代码中， `add()` 不会修改 `x` or `y` ，它只读取值。事实上，正如所写的那样，函数无法修改它们，因为默认情况下 `fn` 参数是**不可变引用**。

就参数约定而言，这称为“借用”，尽管它是 `fn` 函数的默认值，但可以使用 `borrowed` 这样的声明来明确它（其行为与上述 `add()` 函数完全相同）：

```
fn add(borrowed x: Int, borrowed y: Int) -> Int:
    return x + y
```

如果希望参数可变，则需要用 `inout` 来声明参数。这意味对函数内部对参数所做的更改在函数外部可见。

例如，此函数能够修改原始变量：

```
fn add_inout(inout x: Int, inout y: Int) -> Int:
    x += 1
    y += 1
    return x + y

var a = 1
var b = 2
c = add_inout(a, b)
print(a)
print(b)
print(c)
```

```
2
3
5
```

另一种选择是将参数声明为 `owned` ，这为函数提供了值的完全所有权（它是可变的并且保证唯一）。这样，函数可以修改值，而不必担心影响函数外部的变量。例如：

```
fn set_fire(owned text: String) -> String:
    text += "🔥"
    return text

fn mojo():
    let a: String = "mojo"
    let b = set_fire(a)
    print(a)
    print(b)

mojo()
```

```
mojo
mojo🔥
```

在这种情况下，Mojo 会复制 `a` 并将其作为 `text` 参数传递。原来的字符串 `a` 仍然活着。

但是，如果要授予函数值的所有权并且**不想**创建副本（对于某些类型来说，这可能是一个昂贵的操作），则可以在传递 `a` 给函数时添加 `^`“transfer” 运算符。传输运算符有效地销毁了局部变量名，以后任何调用它的尝试都会导致编译器错误。

尝试将 `set_fire()` 调用更改为如下所示：

```
    let b = set_fire(a^)
```

上述代码会收到一个错误，因为传输运算符销毁了变量 `a` ，因此当 `print()` 函数尝试使用 `a` 时，该变量不再初始化。
如果删除 `print(a)` ，则运行正常。

这些参数约定旨在为系统程序员提供对内存优化的完全控制，同时确保安全访问和及时释放 - Mojo 编译器确保没有两个变量可以同时可变访问相同的值，并且每个值的生存期都经过明确定义，以严格防止任何内存错误，例如“释放后使用”和“双重释放”。

**注意：**目前，Mojo 总是在函数返回值时制作副本。

## 结构[](#structures)

结构中可以将 types 或者 Objects 高度抽象化，结构类似于 Python 中的类：它们都支持方法、字段、运算符重载、元编程装饰器等。但是，Mojo 结构是完全静态的——它们在编译时绑定，因此它们不允许动态调度或进行任何运行时更改。（Mojo 将来也将支持类）

例如，下面是一个基本结构：

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

以下是使用它的方法：

```
let mine = MyPair(2, 4)
mine.dump()
```

```
2 4
```

如果你熟悉 Python，那么你应该熟悉 `__init__()` 方法和 `self` 参数。如果你不熟悉 Python，那么请注意，当我们调用 `dump()` 时，我们实际上并没有为 `self` 参数传递值。 `self` 的值会自动随结构的当前实例一起提供（它的用法类似于其他一些语言中 `this` ，用于引用对象/类型的当前实例）。

有关结构和其他特殊方法（也称为“dunder”方法）的更多详细信息，请参阅 [编程手册](https://docs.modular.com/mojo/programming-manual.html)。`__init__()`

## Python 集成[](#python-integration)

虽然 Mojo 仍在进行中，还不是 Python 的完整超集，但我们已经构建了一种原样导入 Python 模块的机制，因此可以立即利用现有的 Python 代码。这种机制使用 CPython 解释器来运行 Python 代码，使其可以与当今的所有 Python 模块无缝协作。

例如，以下是导入和使用 NumPy 的方法（必须安装 Python `numpy`）：

```
from python import Python

let np = Python.import_module("numpy")

ar = np.arange(15).reshape(3, 5)
print(ar)
print(ar.shape)
```

```
[[ 0  1  2  3  4]
 [ 5  6  7  8  9]
 [10 11 12 13 14]]
(3, 5)
```

**注意：**Mojo 还不是 Python 的一个功能完备的超集。因此，不能总是复制 Python 代码并在 Mojo 中运行。有关我们计划的更多详细信息，请参阅 [Mojo 路线图](https://docs.modular.com/mojo/roadmap.html)。

**谨慎：**当安装 Mojo 时，安装程序会在系统中搜索要与 Mojo 一起使用的 Python 版本，并将路径添加到`modular.cfg`配置文件中。如果更改 Python 版本或切换虚拟环境，Mojo 将查看错误的 Python 库，这可能会导致导入 Python 包时出现错误等问题（Mojo 仅显示`An error occurred in Python` - 这是一个单独的 [已知问题](https://github.com/modularml/mojo/issues/536)）。当前的解决方案是使用 `MOJO_PYTHON_LIBRARY` 环境变量覆盖 Mojo 的 Python 库路径。有关如何查找和设置此路径的说明，请参阅 [相关问题](https://github.com/modularml/mojo/issues/551)。

## 后续步骤[](#next-steps)

我们希望此页面涵盖了足够的基础知识，以帮助您入门。页面内容简短，所以如果你想更详细地了解这里涉及的任何主题，请查看 [Mojo 编程手册](https://docs.modular.com/mojo/programming-manual.html)。

- 如果要将代码打包为库，请阅读有关 [Mojo 模块和包](https://docs.modular.com/mojo/manual/get-started/packages.html) 的信息。
- 如果想探索一些 Mojo 代码，请查看我们在 [GitHub 上的代码示例](https://github.com/modularml/mojo/tree/main/examples#mojo-code-examples)。
- 要查看所有可用的 Mojo API，请查看 [Mojo 标准库参考](https://docs.modular.com/mojo/lib.html)。

**注意：**Mojo SDK 仍处于早期开发阶段。有些内容仍然很粗糙，但您可以期待语言和工具的不断变化和改进。请参阅 [已知问题](https://docs.modular.com/mojo/roadmap.html#mojo-sdk-known-issues) 并在 [GitHub 上报告任何其他问题](https://github.com/modularml/mojo/issues/new/choose)。

# Mojo 低级 IR

Mojo 是一种高级编程语言，其具有可扩展的现代特性。Mojo 还为开发者提供了低级原语特性，用于编写强大而具备零成本的抽象实现。

这些原语采用 MLIR 实现。MLIR 是用于编译器设计的可扩展中间表示 （IR） 格式。许多编程语言和编译器将其源程序转换为 MLIR，并且由于 Mojo 提供对 MLIR 特性的直接访问，这意味着 Mojo 程序可以从这些工具中受益。

更进一步，Mojo 将零成本抽象与 MLIR 互操作性的独特组合意味着 Mojo 程序可以充分利用与 MLIR 接口的任何内容。虽然这不是普通的 Mojo 程序员可能需要做的事情，但是在扩展系统以与新数据类型或深奥的新加速器功能进行对接时，这会是一项非常强大的功能。

为了说明这些想法，我们将在下面的 Mojo 中实现一个布尔类型，我们称之为 OurBool。我们将会广泛使用 MLIR，现在让我们从一个简短的入门开始。

## 何为 MLIR ？

MLIR 是程序的中间表示，其与汇编语言不同，汇编语言采用顺序指令集对内存中的值进行操作。

值得一提的是，MLIR 具有模块化和可扩展性。MLIR 由数量不断增长的“方言”组成。每种方言都定义了操作和优化方式，例如：“math”提供正弦和余弦等数学运算，amdgpu 提供特定于 AMD 处理器的操作等。

每种 MLIR 方言都可与其他方言进行互操作。这就是 MLIR 可以支持异构计算的原因所在：随着更新、更快的处理器和架构被开发，新的 MLIR 方言可生成适配这类场景的最优代码。任何新的 MLIR 方言都可以无缝地翻译成其他方言，随着越来越多方言被添加，现有的 MLIR 将会变得更加强大。

这也意味着我们自定义类型（例如：我们将在下面创建的 OurBool 类型）可用于为程序员提供一个高级、类似 Python 的接口。与此同时，面对将来出现的每个新处理器，Mojo 和 MLIR 也会对便捷且高级的类型进行优化。

关于 MLIR 为何是一项具有革命性的技术，还有许多内容要去写，但是先让我们回到 Mojo 并定义 OurBool 类型。在此过程中将会有机会去了解关于 MLIR 的更多信息。

## 定义`OurBool`类型

我们可以使用 Mojo 关键字`struct`定义一个新的类型`OurBool`：

```python
struct OurBool:
    var value: __mlir_type.i1
```

一个布尔值可以表示为 0 或 1，即“false”或“true”。为了存储这些信息，`OurBool`拥有一个单独成员，称为`value`，其类型在 MLIR 中表述为内置类型`i1`。实际上，您可以在 Mojo 中使用任何 MLIR 类型，方法是在类型名称前面加上前缀`__mlir_type`。

正如我们将在下面看到的，采用`i1`表示我们的布尔值将使我们能够利用与`i1`类型接口有关的所有 MLIR 操作和优化 — 而且会有很多！

定义`OurBool`之后，我们现在可以声明这种类型的变量：

```python
let a: OurBool
```

## 采用 MLIR

我们接下来会尝试创建一个`OurBool`实例。然而，此时这样做会导致一个报错：

```python
let a = OurBool() # error: 'OurBool' does not implement an '__init__' method
```

与 Python 一样，`__init__`是一种 [特殊方法]（https://docs.python.org/3/reference/datamodel.html#specialnames），它可用于自定义一种类型的行为。我们可以实现一个不带参数的`__init__`方法，其返回一个带有“false”值的`OurBool`。

```python
struct OurBool:
    var value: __mlir_type.i1

    fn __init__(inout self):
        self.value = __mlir_op.`index.bool.constant`[
            value : __mlir_attr.`false`,
        ]()
```

为了初始化底层的 'i1' 值，我们使用来自 ['index' 方言](https://mlir.llvm.org/docs/Dialects/IndexOps/) 的 MLIR 操作，其称之为 [`index.bool.constant`](https://mlir.llvm.org/docs/Dialects/IndexOps/#indexboolconstant-mlirindexboolconstantop)。

MLIR 的 'index' 方言为我们提供了操作内置 MLIR 类型的操作，例如我们用来存储`OurBool`值的`i1`。`index.bool.constant`操作将`true`或`false`编译时常量作为输入，并使用给定值生成类型为`i1`的运行时输出。

因此，如上所示，除了 MLIR 相关类型，Mojo 还提供通过`__mlir_op`前缀直接访问任一 MLIR 操作，并通过`__mlir_attr`前缀直接访问任一属性。MLIR 属性用于表示编译时常量。

如您所看到的，与 MLIR 交互的语法并不总是很优雅：MLIR 属性在方括号`[...]`之间传递，并且通过括号`(...)`执行操作，其支持获取运行时参数值。然而，大多数 Mojo 程序员不需要直接访问 MLIR，同时对于少数这样做的人来说，这种“丑陋”的语法赋予了他们超能力：他们可以定义高级类型，不仅易于使用，也支持在内部插入 MLIR 及其强大的方言系统。

我们认为这非常令人兴奋，但让我们回到现实：定义了一个`__init__`方法后，我们现在可以创建`OurBool`类型的实例：

```python
let b = OurBool()
```

## Mojo 值的语义

我们现在可以实例化`OurBool`，但是如何使用它则是另外一回事：

```python
let a = OurBool()
let b = a # error: 'OurBool' does not implement the '__copyinit__' method
```

Mojo 默认使用“值语义”，这意味着它希望在赋值给`b`时会创建一个副本`a`。但是 Mojo 并没有对如何复制 `OurBool` 或其底层的`i1`值做出任何假设。该错误表示我们应实现一个`__copyinit__`方法，该方法将实现复制逻辑。

然而，在我们的示例中，`OurBool`是一个非常简单的类型，只有一个“trivially copyable”成员。我们可以使用装饰器来告诉 Mojo 编译器，省去了我们自定义`__copyinit__`样板的麻烦。简单可复制类型（trivially copyable）必须实现一个返回自身实例的`__init__`方法，因此还必须重写我们的初始化实现。

```python
@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    fn __init__() -> Self:
        return Self {
            value: __mlir_op.`index.bool.constant`[
                value : __mlir_attr.`false`,
            ]()
        }
```

我们现在可以随心所欲地复制`OurBool`：

```python
let c = OurBool()
let d = c
```

## 编译时常量

只能表示“false”的布尔类型是无用的，让我们定义一个编译时常量，其可以表示`OurBool` true 和 false 值。

首先，让我们为`OurBool`定义另一个`__init__`构造函数，它将其`i1`值作为参数：

```python
@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    # ...

    fn __init__(value: __mlir_type.i1) -> Self:
        return Self {value: value}
```

以上允许我们使用`alias`关键字来定义编译时常量`OurBool`值。首先，让我们定义`OurTrue`：

```python
alias OurTrue = OurBool(__mlir_attr.`true`)
```

在这里，我们传入一个 MLIR 编译时常量值`true`，它具有我们新的构造函数`__init__`所期望的`i1`类型。我们可以对`OurFalse`使用略微不同的语法：

```python
alias OurFalse: OurBool = __mlir_attr.`false`
```

`OurFalse`被声明为`OurBool`类型，然后被赋值为`i1`类型 - 在这种情形下，我们添加的构造函数`OurBool`被隐式调用。

使用 true 和 false 常量，我们还可以简化`OurBool`对应的`__init__`构造函数。我们可以简单地返回`OurFalse`常量，而不是构造一个 MLIR 值：

```python
alias OurTrue = OurBool(__mlir_attr.`true`)
alias OurFalse: OurBool = __mlir_attr.`false`


@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    # We can simplify our no-argument constructor:
    fn __init__() -> Self:
        return OurFalse

    fn __init__(value: __mlir_type.i1) -> Self:
        return Self {value: value}
```

另外，我们可以在定义`OurBool`之前定义`OurTrue`。Mojo 编译器很智能，它可以识别出这个问题。

通过这些常量，我们现在可以定义同时具有 true 和 false 的`OurBool`变量：

```python
let e = OurTrue
let f = OurFalse
```

## 实现`__bool__`

当然，布尔值在编程中无处不在的原因在于它们可用于程序控制流。但是，当我们尝试以如下方式使用`OurBool`，则会报错：

```python
let a = OurTrue
if a: print("It's true!") # error: 'OurBool' does not implement the '__bool__' method
```

当 Mojo 尝试执行我们的程序时，它需要能够确定是否打印“It's true!”。它还不知道`OurBool`代表一个布尔值 — Mojo 仅识别到一个大小为 1 bit 的结构体。然而，Mojo 还提供了传递布尔特性的接口，这些接口与 Mojo 标准库类型（例如：`Bool`）使用的接口相同。实际上，这意味着 Mojo 为您提供了完全控制权：任何与语言标准库集成在一起的类型都可以用于自定义的版本中。

在我们的错误消息中，Mojo 告诉我们在`OurBool`中实现`__bool__`方法将表示它具有布尔特性。

值得庆幸的是，`__bool__`很容易实现：Mojo 标准库和内置类型都是在 MLIR 之上实现的，如同`OurBool`，内置`Bool`类型也定义了一个采用`i1`的构造函数：

```python
alias OurTrue = OurBool(__mlir_attr.`true`)
alias OurFalse: OurBool = __mlir_attr.`false`


@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    # ...

    fn __init__(value: __mlir_type.i1) -> Self:
        return Self {value: value}

    # Our new method converts `OurBool` to `Bool`:
    fn __bool__(self) -> Bool:
        return Bool(self.value)
```

现在我们可以在任何地方使用内置的`Bool`类型：

```python
let g = OurTrue
if g: print("It's true!")
```
> It's true!

## 避免使用`__mlir_i1__`进行类型转换

Our `OurBool` type is looking great, and by providing a conversion to `Bool`, it can be used anywhere the builtin `Bool` type can. But in the last section we promised you “full control,” the ability to define your own version of any type built into Mojo or its standard library. Surely `Bool` doesn’t implement `__bool__` to convert itself into `Bool`?

我们的`OurBool`类型看起来很棒，通过提供`Bool`转换，它可以在任何使用内置`Bool`类型的地方使用`OurBool`。但是在上一节中，我们向您承诺可具有“完全控制”的能力，即：能够自定义 Mojo 或其标准库中内置任何类型。确认`Bool`不会实现`__bool__`以将自己转换为`Bool`吗？

确实不会这么做：当 Mojo 计算条件表达式时，它实际上尝试通过搜索特殊的接口方法`__mlir_i1__`将其转换为一个 MLIR i1 值（自动转换为`Bool`是因为`Bool`已实现了`__mlir_i1__`方法）。

Again, Mojo is designed to be extensible and modular. By implementing all the special methods `Bool` does, we can create a type that can replace it entirely. Let’s do so by implementing `__mlir_i1__` on `OurBool`:

同时，Mojo 被设计为可扩展和模块化。通过实现所有`Bool`的特殊方法，我们可以创建一个完全替换它的类型。让我们通过在`OurBool`上实现`__mlir_i1__`来实现：

```python
alias OurTrue = OurBool(__mlir_attr.`true`)
alias OurFalse: OurBool = __mlir_attr.`false`


@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    fn __init__(value: __mlir_type.i1) -> Self:
        return Self {value: value}

    # ...

    # Our new method converts `OurBool` to `i1`:
    fn __mlir_i1__(self) -> __mlir_type.i1:
        return self.value
```

我们仍然可以像以前那样在条件中使用`OurBool`：

```python
let h = OurTrue
if h: print("No more Bool conversion!")
```
> No more Bool conversion!

但是这一次，并没有出现转换为`Bool`的情形。您可以尝试将`print`语句添加到`__bool__`和`__mlir_i1__`方法中，甚至完全删除`__bool__`方法。

## 通过 MLIR 添加功能

我们还有更多方法可以改进`OurBool`。其中许多涉及到特殊方法的实现，你可以从`Python`中识别出其中一些，还有一些是特定于 Mojo 的方法。例如，我们可以通过添加`__invert__`方法来实现`OurBool`值的反转。我们还可以添加一个`__eq__`方法，它将允许两个`OurBool`通过`==`运算符进行比较。

使得 Mojo 与众不同的是，我们可以使用 MLIR 实现其中的每一个方法。例如，为了实现`__eq__`，我们使用[`index.casts`](https://mlir.llvm.org/docs/Dialects/IndexOps/#indexcasts-mlirindexcastsop)操作将我们的`i1`值转换为 MLIR `index` 类型，然后使用[`index.cmp`](https://mlir.llvm.org/docs/Dialects/IndexOps/#indexcmp-mlirindexcmpop)操作来比较它们是否相等。通过实现`__eq__`方法，我们可以根据`__eq__`实现`__invert__`：

```python
alias OurTrue = OurBool(__mlir_attr.`true`)
alias OurFalse: OurBool = __mlir_attr.`false`


@register_passable("trivial")
struct OurBool:
    var value: __mlir_type.i1

    fn __init__(value: __mlir_type.i1) -> Self:
        return Self {value: value}

    # ...

    fn __mlir_i1__(self) -> __mlir_type.i1:
        return self.value

    fn __eq__(self, rhs: OurBool) -> Self:
        let lhsIndex = __mlir_op.`index.casts`[_type : __mlir_type.index](
            self.value
        )
        let rhsIndex = __mlir_op.`index.casts`[_type : __mlir_type.index](
            rhs.value
        )
        return Self(
            __mlir_op.`index.cmp`[
                pred : __mlir_attr.`#index<cmp_predicate eq>`
            ](lhsIndex, rhsIndex)
        )

    fn __invert__(self) -> Self:
        return OurFalse if self == OurTrue else OurTrue
```

这将允许我们将`~`运算符与`OurBool`一同使用：

```python
let i = OurFalse
if ~i: print("It's false!")
```
> It's false!

这种可扩展设计甚至允许内置 Mojo 类型，例如：`Bool`，`Int`，甚至在 Mojo 标准库中以 MLIR 实现`Tuple`，而不是硬编码至 Mojo 语言中。这也意味着这些类型几乎无法实现用户自定义类型无法实现的目标。

推而广之，这意味着 Mojo 为机器学习工作流而带来的强大性能提升，并不是在幕后执行的一些魔法 - 您可以自定义高级类型，在其实现中，通过使用低级 MLIR 来达到前所未有的性能和可控性。

## 对模块化的承诺

正如我们所所看到的，Mojo 与 MLIR 的集成允许 Mojo 程序员可以实现与 Mojo 内置和标准库类型相当的零成本抽象。

MLIR 是开源和可扩展的：一直在增加新的方言，然后这些方言就可以在 Mojo 使用。一直以来，Mojo 代码变得更加强大，并且针对新硬件进行了更多优化 - Mojo 程序员无需再进行额外的适配工作。

这也意味着您拥有自定义类型，无论是`OurBool`还是`OurTensor`，都可以用来为程序员提供易于使用且不变的接口。与此同时，MLIR 将为未来的计算环境优化这些便利且高级的类型。

简言之：Mojo 不是魔法，它是模块化。

安装 Mojo 后，可以使用 [Mojo CLI](https://docs.modular.com/mojo/cli/) 构建和编译 [Mojo](https://docs.modular.com/mojo/manual/get-started/setup.html) 程序。因此，让我们创建经典程序“Hello，world！"吧。

**开始之前**：如运行 `modular install mojo` 时的输出中提示，您必须设置 `MODULAR_HOME` 和 `PATH` 环境变量。例如，如果使用的是 bash，则可以按如下方式设置：

```bash
echo 'export MODULAR_HOME="$HOME/.modular"' >> ~/.bashrc

echo 'export PATH="$MODULAR_HOME/pkg/packages.modular.com_mojo/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc
```

如果在安装过程中遇到其他问题，请查看我们的[已知问题](https://docs.modular.com/mojo/roadmap.html#mojo-sdk-known-issues)。
:::

## 在 REPL 中运行代码[](#run-code-in-the-repl)

首先，尝试在 Mojo [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) 中运行一些代码，它允许您直接在命令提示符下编写和运行 Mojo 代码：

1. 要启动 REPL 会话，请输入 `mojo` 并按 Enter 键。
2. 然后输入 `print("Hello, world!")` 并按 Enter 两次（需要空行来指示表达式的结尾）。

就是这样！例如：

```bash
$ mojo
Welcome to Mojo! 🔥
Expressions are delimited by a blank line.
Type `:mojo help` for further assistance.
1> print("Hello, world!")
2.
Hello, world!
```

 REPL 中可以编写任意数量的代码。按 Enter 键开始新行并继续编写代码，当您希望 Mojo 评估代码时，可以按 Enter 两次。如果有要打印的内容，Mojo会打印并返回提示。

由于代码不会保存，REPL 主要用于简短的体验。因此当想编写一个真正的程序时，需要在 `.mojo` 源文件中编写代码。

## 构建并运行 Mojo 源文件[](#build-and-run-mojo-source-files)

现在让我们用源文件打印 “Hello， world”。Mojo 源文件使用 `.mojo` 或 `.🔥` 文件扩展名标识。

可以通过 `mojo` 命令来快速执行 Mojo 文件，也可以使用 `mojo build` 命令构建可执行文件。

### 运行 Mojo 文件[](#run-a-mojo-file)

首先，编写 Mojo 代码并执行它：

1. 创建一个名为 `hello.mojo` （或 `hello.🔥` ）的文件并添加以下代码：
   ```
   fn main():
      print("Hello, world!")
   ```

   保存文件并返回到终端。

2. 现在使用 `mojo` 命令运行它：

   ```bash
   mojo hello.mojo
   ```

   它应该立即打印消息：

   ```
   Hello, world!
   ```

如果这对您不起作用，请仔细检查代码看起来与步骤 1 中的代码完全相同，并确保正确 [安装 Mojo](https://docs.modular.com/mojo/manual/get-started/#install-mojo)。

### 构建可执行二进制文件[](#build-an-executable-binary)

现在，构建并运行可执行文件：

1. 使用 `build` 命令创建静态链接的二进制文件：

   ```bash
   mojo build hello.mojo
   ```

   它创建与 `.mojo` 文件同名的二进制文件，但可以使用该 `-o` 选项进行更改。

2. 然后运行可执行文件：

   ```bash
   ./hello
   ```

可执行文件是静态编译的二进制文件，这意味着它没有外部库依赖项，并且可以在与您自己的 CPU 体系结构相同的任何系统上运行。

## 后续步骤[](#next-steps)

* 如果你在 VS Code 中进行开发，请安装 [Mojo 扩展](https://marketplace.visualstudio.com/items?itemName=modular-mojotools.vscode-mojo)，以便获得语法突出显示、代码完成、诊断等。

* 如果您不熟悉 Mojo，请阅读 [Mojo 语言基础知识](https://docs.modular.com/mojo/manual/basics/)。

* 如果要将代码打包为库，请阅读有关 [Mojo 模块和包](https://docs.modular.com/mojo/manual/get-started/packages.html)的信息。

* 如果您想探索一些 Mojo 代码，请克隆我们的存储库以查看一些示例：

  ```bash
  git clone https://github.com/modularml/mojo.git
  ```

  然后在 IDE 中打开 `/examples` 目录以尝试我们的示例：

  * [代码示例](https://github.com/modularml/mojo/tree/main/examples/) 提供了带有标准库的各种演示，以帮助您学习Mojo的功能并启动自己的项目。
  * [Mojo notebooks](https://github.com/modularml/mojo/tree/main/examples/notebooks#readme) 与我们在 [Mojo Playground](https://playground.modular.com/) 上发布的 Jupyter notebook 相同，它们展示了各种语言功能。现在有了 Mojo SDK ，你也可以在 VS Code 或 JupyterLab 中运行它们。

* 要深入了解该语言，请查看 [Mojo编程手册](https://docs.modular.com/mojo/programming-manual.html)。

* 要查看所有可用的 Mojo API，请查看 [Mojo 标准库参考](https://docs.modular.com/mojo/lib.html)。

**注意**：Mojo SDK 仍处于早期开发阶段，但您可以期待语言和工具的不断改进。请参阅 [已知](https://docs.modular.com/mojo/roadmap.html#mojo-sdk-known-issues) 问题并在 [GitHub 上报告任何其他问题](https://github.com/modularml/mojo/issues/new/choose)。

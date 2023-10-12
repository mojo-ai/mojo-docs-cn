# 约束

实现编译时约束。

这些是Mojo内置的，因此您无需导入它们。

## `constrained`[](#constrained)

`constrained[cond: Bool, msg: StringLiteral]()`

编译时检查条件是否为真。

`constrained`与 C++ 中的`static_assert`类似，用于对闭包函数引入约束。在 Mojo 中，断言对函数施加了约束。断言失败时将显示该消息。

**Parameters：**

* **cond** （`Bool`）：要断言的布尔值。
* **msg** （`StringLiteral`）：失败时显示的消息。

`constrained[cond: Bool]()`

编译时检查条件是否为真。

`constrained`与 C++ 中的`static_assert`类似，用于对闭包函数引入约束。在 Mojo 中，断言对函数施加了约束。

**Parameters：**

* **cond** （`Bool`）：要断言的布尔值。

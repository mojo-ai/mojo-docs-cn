# debug\_assert

实现调试断言。

这些是 Mojo 内置的，因此您无需导入它们。

## `debug_assert`[](#debug_assert)

`debug_assert(cond: Bool, msg: StringLiteral)`

断言条件为真。

`debug_assert`与 C++ 中`assert`的类似。它在发布版本中是无操作的。

**参数：**

* **cond** （`Bool`）：要断言的布尔值。
* **msg** （`StringLiteral`）：失败时显示的消息。

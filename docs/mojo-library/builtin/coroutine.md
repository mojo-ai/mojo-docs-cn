# 协程

实现协程的类和方法。

这些是 Mojo 内置的，因此您无需导入它们。

## `CoroutineContext`[](#coroutinecontext)

表示回调闭包（fn\_ptr + captures）。

## `Coroutine`[](#coroutine)

表示协程。

协程可以暂停执行，保存程序的状态（包括局部变量的值和要执行的下一条指令的位置）。当协程恢复时，执行将从中断的位置继续，并恢复保存的状态。

**Parameters：**

* **type** （`AnyType`）：完成协程时返回的值的类型。

**函数：**

### `__init__`[](#init__)

`__init__(handle: !pop.coroutine<() -> !kgen.paramref<*"type">>) -> Self`

从句柄构造协程对象。

**参数：**

* handle （`!pop.coroutine<() -> !kgen.paramref<*"type">>`）：初始的**句柄**。

**返回：**

构造的协程对象。

### `__del__`[](#del__)

`__del__(owned self: Self)`

销毁协程对象。

### `__await__`[](#await__)

`__await__(self: Self) -> *"type"`

挂起当前协程，直到协程完成。

**返回：**

协程 promise  。

### `get_promise`[](#get_promise)

`get_promise(self: Self) -> Pointer[*"type"]`

将指针返回到存储异步函数结果的内存开头。

**返回：**

协程promise。

### `get`[](#get)

`get(self: Self) -> *"type"`

获取已实现的协程 promise 的值。

**返回：**

已实现的协程 promise 的值。

### `get_ctx`[](#get_ctx)

`get_ctx[ctx_type: AnyType](self: Self) -> Pointer[ctx_type]`

返回指向协程上下文的指针。

**Parameters：**

* **ctx\_type** （`AnyType`）：协程上下文的类型。

**返回：**

协程上下文。

### `__call__`[](#call__)

`__call__(self: Self) -> *"type"`

同步执行协程。

**返回：**

协程 promise 。

## `RaisingCoroutine`[](#raisingcoroutine)

表示可以调起的协程。

协程可以暂停执行，保存程序的状态（包括局部变量的值和要执行的下一条指令的位置）。当协程恢复时，执行将从中断的位置继续，并恢复保存的状态。

**Parameters：**

* **type** （`AnyType`）：完成协程时返回的值的类型。

**函数：**

### `__init__`[](#init__-1)

`__init__(handle: !pop.coroutine<() throws -> !pop.variant<!kgen.declref<_"$builtin"::_"$error"::_Error>, *"type">>) -> Self`

从句柄构造协程对象。

**参数：**

* handle （`!pop.coroutine<() throws -> !pop.variant<!kgen.declref<_"$builtin"::_"$error"::_Error>, *"type">>`）：初始的句柄。

**返回：**

构造的协程对象。

### `__del__`[](#del__-1)

`__del__(owned self: Self)`

销毁协程对象。

### `__await__`[](#await__-1)

`__await__(self: Self) -> *"type"`

挂起当前协程，直到协程完成。

**返回：**

协程 promise 。

### `get_promise`[](#get_promise-1)

`get_promise(self: Self) -> Pointer[Variant[Error, *"type"]]`

将指针返回到存储异步函数结果的内存开头。

**返回：**

协程 promise 。

### `get`[](#get-1)

`get(self: Self) -> *"type"`

获取已实现的协程 promise 的值。

**返回：**

已实现的协程 promise 的值。

### `get_ctx`[](#get_ctx-1)

`get_ctx[ctx_type: AnyType](self: Self) -> Pointer[ctx_type]`

返回指向协程上下文的指针。

**Parameters：**

* **ctx\_type** （）：协程上下文的类型。`AnyType`

**返回：**

协程上下文。

### `__call__`[](#call__-1)

`__call__(self: Self) -> *"type"`

同步执行协程。

**返回：**

协程 promise 。

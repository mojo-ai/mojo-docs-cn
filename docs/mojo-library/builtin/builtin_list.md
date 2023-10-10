# builtin\_list

实现 ListLiteral 类。

这些是 Mojo 内置的，无需导入。

## `ListLiteral`[](#listliteral)

文本异构列表表达式的类型。

列表由零个或多个值组成，以逗号分隔。

**参数：**

* **Ts** （`*AnyType`）：元素的类型。

**域：**

* storage  （`!pop.pack<Ts>`）：列表的基础存储。

**函数：**

### `__init__`[](#init__)

`__init__(args: !pop.pack<Ts>) -> Self`

从给定值构造列表文本。

**参数：**

* **args** （`!pop.pack<Ts>`）：初始化值。

**返回：**

构造的 ListLiteral 。

### `__len__`[](#len__)

`__len__(self: Self) -> Int`

获取列表长度。

**返回：**

此列表文本的长度。

### `get`[](#get)

`get[i: Int, T: AnyType](self: Self) -> T`

获取给定索引处的列表元素。

**参数：**

* **i** （`Int`）： 元素索引。
* **T** （`AnyType`）：元素类型。

**返回：**

给定索引处的元素。

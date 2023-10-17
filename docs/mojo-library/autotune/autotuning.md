# autotuning

实现自动调优功能。

你可以从 `algorithm` 包中导入这些 API。例如：

```python
from autotune import search
```

## `autotune`

```python
autotune[T: AnyType, *Ts: AnyType](value: T, values: !pop.pack<Ts>) -> T
```

将编译分叉（Forks compilation）以评估提供的每个值。

**Parameters**：

- **T** (`AnyType`)：第一个值类型。

- **Ts** (`*AnyType`)：其余参数的类型。

**Args**：

- **value** (`T`)：包中的第一个值。

- **values** (`!pop.pack<Ts>`)：尾部的值。

**Returns**：

在当前编译分支中正在使用的值。

## `autotune_fork`

```python
autotune_fork[type: AnyType, *values: *"type"]()
```

将编译分叉（Forks compilation）以评估提供的每个值。

**Parameters**：

- **type** (`AnyType`)：要评估的参数的类型。

- **values** (`**"type"`)：要评估的参数列表。

**Returns**：

在当前编译分支中正在使用的值。

## `search`

```python
search[fn_type: AnyType, candidates: VariadicList[fn_type], evaluator: fn(Pointer[fn_type], Int) -> Int]()
```

在所有候选项中找到最佳实现。

该函数使用提供的评估器在候选项列表中运行搜索。

评估器函数需要接受两个输入：指向所有候选项的数组的指针和该数组的大小，并返回最佳候选项的索引。

**Parameters**：

- **fn_type** (`AnyType`)：函数的签名类型。

- **candidates** (`VariadicList[fn_type]`)：要搜索的候选项列表。

- **evaluator** (`fn(Pointer[fn_type], Int) -> Int`)：评估函数。

**Returns**：

找到的最佳候选项。

## `cost_of`

```python
cost_of[fn_type: AnyType, func: fn_type]() -> Int
```

计算函数中的操作数。

这个函数接受一个函数引用，并通过计算扩展后函数中的MLIR操作数来估算调用该函数的“成本”。

FIXME：应该将这个函数标记为 @consteval 或等效的标记，以防止动态实例化 kgen.cost_of 。

**Parameters**：

- **fn_type** (`AnyType`)：函数的签名类型。

- **func** (`fn_type`): The function to evaluate.

**Returns**：

函数中扩展后的操作数的数量。

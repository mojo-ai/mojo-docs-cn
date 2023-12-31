# functional

实现高阶函数。

你可以从 `algorithm` 包中导入这些 API。例如：

```python
from algorithm import map
```

## 别名（Aliases）：

- `Static1DTileUnitFunc = fn[Int](Int) capturing -> None`：一个 1D 平铺函数（tiled function）的签名，它使用固定的平铺大小和偏移量执行某些工作。例如：func<tile_size: Int> (offset: Int)

- `Dynamic1DTileUnitFunc = fn(Int, Int) capturing -> None`：一个 1D 平铺函数（tiled function）的签名，它使用动态的平铺大小和偏移量执行某些工作。例如：func(offset: Int, tile_size: Int)

- `BinaryTile1DTileUnitFunc = fn[Int](Int, Int) capturing -> None`：一个平铺函数（tiled function）的签名，它使用动态的平铺大小和一个次要的静态平铺大小来执行一些工作。

- `Static2DTileUnitFunc = fn[Int, Int](Int, Int) capturing -> None`：一个2D 平铺函数（tiled function）的签名，它使用静态的平铺大小和偏移量来执行某些工作。例如：func<tile_size_x: Int, tile_size_y: Int> (offset_x: Int, offset_y: Int)

- `SwitchedFunction = fn[Bool]() capturing -> None`

- `SwitchedFunction2 = fn[Bool, Bool]() capturing -> None`

- `Static1DTileUnswitchUnitFunc = fn[Int, Bool](Int, Int) capturing -> None`：一个平铺函数（tiled function）的签名，它使用静态的平铺大小和偏移量来执行某些工作。例如：func<tile_size: Int> (offset: Int)

- `Dynamic1DTileUnswitchUnitFunc = fn[Bool](Int, Int, Int) capturing -> None`

## `map`

```python
map[func: fn(Int) capturing -> None](size: Int)
```

将一个函数映射到从 0 到 size 的范围上。

**Parameters**：

- **func**（`fn(Int) capturing -> None`）: 映射函数。

**Args**：

- **size**（`Int`）: 元素的数量。


示例：

```python
from algorithm import map

fn main():    
    fn stateful_nocapture(a: Int):
        print(a + 1)
        
    map[stateful_nocapture](3)

main()
```
> 1
> 
> 2
> 
> 3


## `unroll`

```python
unroll[count: Int, func: fn[Int]() capturing -> None]()
```

重复计算一个函数 count 次。

**Parameters**：

- **count**（`Int`）：重复次数。

- **func**（`fn[Int]() capturing -> None`）：要计算的函数。该函数应该接受一个整数参数。

示例：

```python
from algorithm import unroll

fn main():
    fn stateful_nocapture[a: Int]():
        print(a*a)
        
    unroll[3, stateful_nocapture]()
    
main()
```

> 0
>
> 1
>
> 4


```python
unroll[dim0: Int, dim1: Int, func: fn[Int, Int]() capturing -> None]()
```

重复计算一个函数 dim0 X dim1 次（二维嵌套循环）。

**Parameters**：

- **dim0**（`Int`）：第一维大小。

- **dim1**（`Int`）：第二维大小。

- **func**（`fn[Int, Int]() capturing -> None`）：要计算的函数，该函数应接受两个整数参数。

示例：

```python
from algorithm import unroll

fn main():
    fn stateful_nocapture[a: Int, b: Int]():
        print(a + b)
        
    unroll[2, 3, stateful_nocapture]()
    
main()
```

> 0
> 
> 1
> 
> 2
> 
> 1
> 
> 2
> 
> 3


```python
unroll[dim0: Int, dim1: Int, dim2: Int, func: fn[Int, Int, Int]() capturing -> None]()
```

重复计算一个函数 dim0 X dim1 X dim2 次（三维嵌套循环）。

**Parameters**：

- **dim0**（`Int`）：第一维大小。

- **dim1**（`Int`）：第二维大小。

- **dim2**（`Int`）：第三维大小。

- **func**（`fn[Int, Int, Int]() capturing -> None`）：要计算的函数，该函数应接受三个整数参数。

示例：

```python
from algorithm import unroll

fn main():
    fn stateful_nocapture[a: Int, b: Int, c: Int]():
        print(a + b + c)
        
    unroll[1, 2, 3, stateful_nocapture]()
    
main()
```

> 0
> 
> 1
> 
> 2
> 
> 1
> 
> 2
> 
> 3

## `vectorize`

```python
vectorize[simd_width: Int, func: fn[Int](Int) capturing -> None](size: Int)
```

以 simd 方式将一个参数化为 simd_width 的函数映射到从 0 到 size 的范围上。

**Parameters**：

- **simd_width**（`Int`）: SIMD 向量的宽度。

- **func**（`fn[Int](Int) capturing -> None`）：循环体的函数。

**Args**：

- **size**（`Int`）：总循环次数。

示例：

```python
from algorithm import vectorize

fn main():
    fn stateful_nocapture[a: Int](b: Int):
        print("a:", a, "b:", b)
        
    vectorize[4, stateful_nocapture](3)
    
main()
```

> a: 1 b: 0
> 
> a: 1 b: 1
> 
> a: 1 b: 2

## `vectorize_unroll`

```python
vectorize_unroll[simd_width: Int, unroll_factor: Int, func: fn[Int](Int) capturing -> None](size: Int)
```

将一个参数化在 simd_width 上的函数映射到从 0 到 size 的范围上，并以 simd 方式展开循环，展开因子为 unroll_factor。

**Parameters**：

- **simd_width** (Int)：SIMD 向量的宽度。

- **unroll_factor** (Int)：主循环的展开因子。

- **func** (`fn[Int](Int) capturing -> None`)：循环体的函数。
  
**Args**:

- **size** (`Int`)：总循环次数。

示例：

```python
from algorithm import vectorize_unroll

fn main():
    fn stateful_nocapture[a: Int](b: Int):
        print("a:", a, "b:", b)
        
    vectorize_unroll[4, 2, stateful_nocapture](3)
    
main()
```

> a: 1 b: 0
> 
> a: 1 b: 1
> 
> a: 1 b: 2

## `async_parallelize`

```python
async_parallelize[func: fn(Int) capturing -> None](out_chain: OutputChainPtr, num_work_items: Int)
```

并行执行 func(0) … func(num_work_items-1) 作为子任务，并立即返回。只有当所有子任务完成时，out_chain 才会被标记为 ready。

并行执行 func(0) … func(num_work_items-1) 作为子任务，并在所有函数返回时将 out_chain 标记为 ready。当子任务被调度但不一定完成时，此函数将返回。运行时可以以任意顺序和任意并发度执行子任务。

func 中的所有自由变量必须是“异步安全”的。这意味着：- 变量必须由按值传递的函数参数（即没有 &）或 let 绑定绑定。- 变量的类型必须是“异步安全”的，即标记为 @register_passable，并且任何内部指针都指向至少在 out_chain 准备就绪之前的生命周期内的内存。实际上，这意味着只能指向由运行时保持活动状态的缓冲区的指针。如果此要求过于繁重，请考虑使用 sync_parallelize。

如果 num_work_items 为 0，则在 async_parallelize 返回之前将 out_chain 标记为 ready。如果 num_work_items 为 1，则 func(0) 仍可以作为子任务执行。

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。
  
**Args**：

- **out_chain** (`OutputChainPtr`)：要向其发出完成信号的 out_chain。
  
- **num_work_items** (`Int`): 并行任务的数量。

## `sync_parallelize`

```python
sync_parallelize[func: fn(Int) capturing -> None](out_chain: OutputChainPtr, num_work_items: Int)
```

并行执行 func(0) ... func(num_work_items-1) 作为子任务。当所有子任务完成时，标记 out_chain 为就绪并返回。

在并行中执行 func(0) ... func(num_work_items-1) 作为子任务，并且只有当它们全部返回时才返回。运行时可以以任何顺序和任何并发度执行子任务。在返回之前，out_chain 将被标记为就绪。

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。

**Args**：

- **out_chain** (`OutputChainPtr`)：要向其发出完成信号的 out_chain。
  
- **num_work_items** (`Int`): 并行任务的数量。

## `parallelize`

```python
parallelize[func: fn(Int) capturing -> None]()
```

并行执行 func(0) ... func(N-1) 作为子任务，并且当所有子任务完成时返回。N 被选择为系统上的处理器数量。

在并行中执行 func(0) ... func(N-1) 作为子任务。此函数只有在所有子任务完成后才会返回。

*注意：创建并销毁本地运行时（local runtime）！不要在内核中使用！*

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。

```python
parallelize[func: fn(Int) capturing -> None](num_work_items: Int)
```

在并行中执行 func(0) ... func(num_work_items-1) 作为子任务，并在所有子任务完成后返回。

将 func(0) ... func(num_work_items-1) 作为子任务并行执行。只有在所有子任务完成后，该函数才会返回。

*注意：创建并销毁本地运行时（local runtime）！不要在内核中使用！*

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。

**Args**：

- **num_work_items** (`Int`): 并行任务的数量。

```python
parallelize[func: fn(Int) capturing -> None](rt: Runtime, num_work_items: Int)
```

在并行中执行 func(0) ... func(num_work_items-1) 作为子任务，并在所有子任务完成后返回。

将 func(0) ... func(num_work_items-1) 作为子任务并行执行。只有在所有子任务完成后，该函数才会返回。

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。

**Args**：

- **rt** (`Runtime`)：运行时（The runtime）。
  
- **num_work_items** (`Int`): 并行任务的数量。

```python
parallelize[func: fn(Int) capturing -> None](rt: Runtime, num_work_items: Int, num_workers: Int)
```

将 func(0) ... func(num_work_items-1) 作为子任务并行执行，并在所有子任务完成后返回。

将 func(0) ... func(num_work_items-1) 作为子任务并行执行。只有在所有子任务完成后，此函数才会返回。

**Parameters**：

- **func** (`fn(Int) capturing -> None`): 要调用的函数。

**Args**：

- **rt** (`Runtime`)：运行时（The runtime）。

- **num_work_items** (`Int`): 并行任务的数量。

- **num_workers** (`Int`)：执行时使用的工作数量。

## `tile`

```python
tile[workgroup_function: fn[Int](Int) capturing -> None, tile_size_list: VariadicList[Int]](offset: Int, upperbound: Int)
```

以指定的 tile 大小启动工作组的生成器。

一个工作组函数是一个可以处理可配置的连续 “tile” 工作负载的函数。例如，work_on\[3\](5) 应该在项 5，6，7 上启动计算，并且在语义上等同于 work_on\[1\](5)，work_on\[1\](6)，work_on\[1\](7)。

这个生成器将尝试按照给定的 tile 大小列表顺序进行处理。例如，tile\[func, (3,2,1)\](offset, upperbound) 将尝试从偏移量开始调用 func\[3\]，直到剩余的工作量从上限减少到小于3，然后尝试 func\[2\]，然后尝试 func\[1\]，以此类推。 

**Parameters**：

- **workgroup_function** (`fn[Int](Int) capturing -> None`)：工作组函数，用于处理一个 tile 的工作负载。

- **tile_size_list** (`VariadicList[Int]`)：启动工作的 tile 大小列表。

**Args**：

- **offset** (`Int`)：从哪个初始索引开始工作。
  
- **upperbound** (`Int`)：工作函数不应超过的运行时上限。

```python
tile[workgroup_function: fn(Int, Int) capturing -> None](offset: Int, upperbound: Int, tile_size_list: VariadicList[Int])
```

一个在指定的 tile 大小列表中启动工作组的生成器。

这是 tile 生成器的版本，适用于工作组函数可以将 tile 大小作为运行时值的情况。

**Parameters**：

- **workgroup_function** (`fn(Int, Int) capturing -> None`)：工作组函数，用于处理一个 tile 的工作负载。

**Args**：

- **offset** (`Int`)：从哪个初始索引开始工作。
  
- **upperbound** (`Int`)：工作函数不应超过的运行时上限。
  
- **tile_size_list** (`VariadicList[Int]`)：启动工作的 tile 大小列表。

```python
tile[secondary_tile_size_list: VariadicList[Int], secondary_cleanup_tile: Int, workgroup_function: fn[Int](Int, Int) capturing -> None](offset: Int, upperbound: Int, primary_tile_size_list: VariadicList[Int], primary_cleanup_tile: Int)
```

一个生成器，它在指定的 tile 大小列表中启动工作组，直到主要 tile 大小的总和超过上限。

**Parameters**：

- **secondary_tile_size_list** (`VariadicList[Int]`)：启动工作的静态 tile 大小列表。

- **secondary_cleanup_tile** (`Int`)：当主要 title 大小不完全适应上限时使用的最后一个静态 tile。

- **workgroup_function** (`fn[Int](Int, Int) capturing -> None`)：工作负载的一个 tile 的工作组函数。

**Args**：

- **offset** (`Int`)：从哪个初始索引开始工作。

- **upperbound** (`Int`)：工作函数不应超过的运行时上限。

- **primary_tile_size_list** (`VariadicList[Int]`)：启动工作的动态 tile 大小列表。
  
- **primary_cleanup_tile** (`Int`)：当主要 tile 大小不完全适应上限时使用的最后一个动态 tile。

```python
tile[workgroup_function: fn[Int, Int](Int, Int) capturing -> None, tile_sizes_x: VariadicList[Int], tile_sizes_y: VariadicList[Int]](offset_x: Int, offset_y: Int, upperbound_x: Int, upperbound_y: Int)
```

从 x 和 y 偏移开始，使用每个维度中可能的最大 tile 大小启动 workgroup_function，直到达到 x 和 y 的上限。

**Parameters**：

- **workgroup_function** (`fn[Int, Int](Int, Int) capturing -> None`)：为每个 title 和 offset 调用的函数。

- **tile_sizes_x** (`VariadicList[Int]`)：用于 workgroup_function 的第一个参数的 title 大小列表。

- **tile_sizes_y** (`VariadicList[Int]`)：用于 workgroup_function 的第二个参数的 title 大小列表。

**Args**：

- **offset_x** (`Int`)：传递给 workgroup_function 的初始 x 偏移量。

- **offset_y** (`Int`)：传递给 workgroup_function 的初始 y 偏移量。

- **upperbound_x** (`Int`)：传递给 workgroup_function 的最大 x 偏移量。
  
- **upperbound_y** (`Int`)：传递给 workgroup_function 的最大 y 偏移量。

## `unswitch`

```python
unswitch[switched_func: fn[Bool]() capturing -> None](dynamic_switch: Bool)
```

执行 unswitch 功能转换。

Unswitch 是一种简单的模式，类似于循环 unswitching pass，但扩展到了功能模式。该模式有助于以下代码转换，从而减少生成代码中的分支数量。

Before：

```python
for i in range(...)
    if i < xxx:
        ...
```

After:

```python
if i < ...
    for i in range(...)
        ...
else
    for i in range(...)
        if i < xxx:
            ...
```

该 unswitch 函数通过元参数将该模式泛化，并可用于执行循环 unswitching 和其他类似 simd 和 amx 的瓦片谓词提升。

TODO: 

- 泛化以支持多个谓词。

- 一旦嵌套的 lambda 表达式组合得当，应该能够轻松地使 unswitch 与 tile 组合起来。

**Parameters**：

- **switched_func** (`fn[Bool]() capturing -> None`)：包含可以 unswitched 的内部循环逻辑的函数。

**Args**：

-**dynamic_switch** (`Bool`)：动态条件，使 unswitched 的代码路径生效。

```python
unswitch[switched_func: fn[Bool, Bool]() capturing -> None](dynamic_switch_a: Bool, dynamic_switch_b: Bool)
```

执行 2-predicates 的 unswitch 功能转换。

**Parameters**：

- **switched_func** (`fn[Bool, Bool]() capturing -> None`)：The function containing the inner loop logic that has 2 predicates which can be unswitched.

**Args**：

- **dynamic_switch_a** (`Bool`)：第一个动态条件，使外部 unswitched 代码路径生效。

- **dynamic_switch_b** (`Bool`)：第二个动态条件，使内部 unswitched 代码路径生效。

## `tile_and_unswitch`

```python
tile_and_unswitch[workgroup_function: fn[Int, Bool](Int, Int) capturing -> None, tile_size_list: VariadicList[Int]](offset: Int, upperbound: Int)
```

执行 time 和 unswitch 功能转换。

一个可以 unswitched 的工作组函数的静态 tile 的变体。此生成器是 tile 和 unswitch 的融合版本，其中静态 unswitch 在工作负载的“内部”部分始终为真，并且仅在剩余 tile 上为假。

**Parameters**：

- **workgroup_function** (`fn[Int, Bool](Int, Int) capturing -> None`)：工作组函数，用于处理一个 tile 的工作负载。

- **tile_size_list** (`VariadicList[Int]`)：启动工作的 tile 大小列表。

**Args**：

- **offset** (`Int`)：从哪个初始索引开始工作。

- **upperbound** (`Int`)：工作函数不应超过的运行时上限。

```python
tile_and_unswitch[workgroup_function: fn[Bool](Int, Int, Int) capturing -> None](offset: Int, upperbound: Int, tile_size_list: VariadicList[Int])
```

执行 time 和 unswitch 功能转换。

一个可以 unswitched 的工作组函数的动态 tile 的变体。此生成器是 tile 和 unswitch 的融合版本，其中静态 unswitch 在工作负载的“内部”部分始终为真，并且仅在剩余 tile 上为假。

**Parameters**：

- **workgroup_function** (`fn[Bool](Int, Int, Int) capturing -> None`)：工作组函数，用于处理一个 tile 的工作负载。

**Args**：

- **offset** (`Int`)：从哪个初始索引开始工作。

- **upperbound** (`Int`)：工作函数不应超过的运行时上限。

- **tile_size_list** (`VariadicList[Int]`)：启动工作的 tile 大小列表。

## `elementwise`

```python
elementwise[rank: Int, simd_width: Int, func: fn[Int, Int](StaticIntTuple[*(0,1)]) capturing -> None](shape: StaticIntTuple[rank], out_chain: OutputChainPtr)
```

执行 `func[width，rank]（indices）` 作为适当的 width 和 indices 组合的子任务，以覆盖 shape 。

**Parameters**：

- **rank** (`Int`)：缓冲区的 rank 。

- **simd_width** (`Int`)：使用的 SIMD 向量宽度。
  
- **func** (`fn[Int, Int](StaticIntTuple[*(0,1)]) capturing -> None`)：函数体。
  
**Args**：

- **shape** (`StaticIntTuple[rank]`)：缓冲区的 shape 。

- **out_chain** (`OutputChainPtr`)：将结果附加到输出链中。

## `parallelize_over_rows`

```python
parallelize_over_rows[rank: Int, func: fn(Int, Int) capturing -> None](shape: StaticIntTuple[rank], axis: Int, out_chain: OutputChainPtr, grain_size: Int)
```

并行化函数在形状的 non-axis 维度上。

**Parameters**：

- **rank** (`Int`)：形状的秩。
  
- **func** (`fn(Int, Int) capturing -> None`)：对行范围调用的函数。

**Args**：

- **shape** (`StaticIntTuple[rank]`)：并行化的形状。

- **axis** (`Int`)：行是沿着形状的轴维度的切片。

- **out_chain** (`OutputChainPtr`)：将结果附加到输出链中。

- **grain_size** (`Int`)：使用额外线程的最小元素数量。

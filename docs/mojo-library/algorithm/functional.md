# functional

实现高阶函数。

你可以从 `algorithm` 包中导入这些API。例如：

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

将一个函数映射到从0到size的范围上。

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

- **simd_width**（`Int`）: SIMD向量的宽度。

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

- **simd_width** (Int)：SIMD向量的宽度。

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

将func(0) ... func(num_work_items-1) 作为子任务并行执行。只有在所有子任务完成后，该函数才会返回。

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

将func(0) ... func(num_work_items-1) 作为子任务并行执行，并在所有子任务完成后返回。

将func(0) ... func(num_work_items-1)作为子任务并行执行。只有在所有子任务完成后，此函数才会返回。

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

一个工作组函数是一个可以处理可配置的连续 “tile” 工作负载的函数。例如，work_on[3](5) 应该在项 5，6，7 上启动计算，并且在语义上等同于work_on[1](5)，work_on[1](6)，work_on[1](7)。

这个生成器将尝试按照给定的 tile 大小列表顺序进行处理。例如，tile[func, (3,2,1)](offset, upperbound) 将尝试从偏移量开始调用 func[3]，直到剩余的工作量从上限减少到小于3，然后尝试 func[2]，然后尝试 func[1]，以此类推。 

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

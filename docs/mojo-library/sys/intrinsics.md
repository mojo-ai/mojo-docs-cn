# intrinsics

定义内置函数。

你可以从 `intrinsics` 包中导入这些 API。例如：

```python
from sys.intrinsics import PrefetchLocality
```

## `PrefetchLocality`

预取局部性。

地址局部性、读写类型和缓存类型对应于LLVM预取内置函数的输入（参见LLVM预取局部性）。

**Aliases**：

- `NONE = __init__(0)`：无局部性。

- `LOW = __init__(1)`：低局部性。

- `MEDIUM = __init__(2)`：中局部性。

- `HIGH = __init__(3)`： 极端局部性（保留在缓存中）。

**Fields**：

- **value** (`SIMD[si32, 1]`)：要使用的预取局部性。它应该是一个在 [0, 3] 范围内的值。

**Functions**：

### `__init__`

```python
__init__(value: Int) -> Self
```

构建一个预取局部性选项。

**Args**：

- **value** (`Int`)：代表局部性的整数值。应该是在范围 [0, 3] 内的值。

**Returns**：

构建的预取局部性。

## `PrefetchRW`

预读取或写入。

**Aliases**：

- `READ = __init__(0)`：预读取。

- `WRITE = __init__(1)`：预写入。

**Fields**：

- **value** (`SIMD[si32, 1]`): 预读写。应该在 [0, 1] 范围内。

**Functions**：

### `__init__`

```python
__init__(value: Int) -> Self
```

构造一个预取读写选项。

**Args**：

- **value** (`Int`)： 一个表示要使用的预取读写选项的整数值。应该是在 [0, 1] 范围内的值。
  
**Returns**：

预读写选项已构建完成。

## `PrefetchCache`

预缓存类型。

**Aliases**：

- `INSTRUCTION = __init__(0)`：指令预取选项。

- `DATA = __init__(1)`：数据预取选项。

**Fields**：

- **value** (`SIMD[si32, 1]`)：缓存预取。它应该在 [0, 1] 范围内。

**Functions**：

### `__init__`

```python
__init__(value: Int) -> Self
```

构建一个预取选项。

**Args**：

- **value** (`Int`)：一个表示要使用的预取缓存选项的整数值。应该是 [0, 1] 范围内的值。
  
**Returns**：

构建的预取缓存类型。

## `PrefetchOptions`

用于预取内部调用的配置参数集合。

配置参数遵循与 LLVM 内部预取操作类似的接口，其中 “locality” 属性指定应用程序中的时间局部性水平，即相同数据再次访问的时间间隔。可能的局部性值包括：`NONE`，`LOW`，`MEDIUM` 和 `HIGH`。

该操作还接受一个 “cache tag” 属性，提供有关预取数据将如何使用的提示。可能的标签有：`ReadICache`，`ReadDCache` 和 `WriteDCache`。

注意：预取操作的实际行为和这些属性的具体解释取决于目标环境。

**Fields**：

- **rw** (`PrefetchRW`)：表示用于读取或写入的预取。

- **locality** (`PrefetchLocality`)：表示本地性级别。

- **cache** (`PrefetchCache`)：表示 i-cache 或 d-cache 的预取。

**Functions**：

### `__init__`

```python
__init__() -> Self
```

使用默认参数构造 PrefetchOptions 的实例。

Returns：

完成构造预取配置。

### `for_read`

```python
for_read(self: Self) -> Self
```

将预取目的设置为读取。

Returns：

更新后的预取参数。

### `for_write`

```python
for_write(self: Self) -> Self
```

将预取目的设置为写入。

Returns：

更新后的预取参数。

### `no_locality`

```python
no_locality(self: Self) -> Self
```

将预取位置设置为无。

Returns：

更新后的预取参数。

### `low_locality`

```python
low_locality(self: Self) -> Self
```

将预取位置设置为低。

Returns：

更新后的预取参数。

### `medium_locality`

```python
medium_locality(self: Self) -> Self
```

将预取位置设置为中。

Returns：

更新后的预取参数。

### `high_locality`

```python
high_locality(self: Self) -> Self
```

将预取位置设置为高。

Returns：

更新后的预取参数。

### `to_data_cache`

```python
to_data_cache(self: Self) -> Self
```

将预取目标设置为数据缓存。

Returns：

更新后的预取参数。

### `to_instruction_cache`

```python
to_instruction_cache(self: Self) -> Self
```

将预取目标设置为指令缓存。

Returns：

更新后的预取参数。

## `llvm_intrinsic`

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType]() -> *"type"
```

调用一个没有参数的 LLVM 内部函数。

调用一个名为 intrin 且返回类型为 type 的 LLVM 内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。

**Returns**：

调用没有参数的 LLVM 内部函数的结果。

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType, T0: AnyType](arg0: T0) -> *"type"
```

调用一个带有一个参数的 LLVM 内部函数。

在参数 arg0 上调用名称为 intrin，返回类型为 type 的内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。
  
- **T0** (`AnyType`)：内部函数的第一个参数（arg0）的类型。

**Args**：

- **arg0** (`T0`)：调用 LLVM 内部函数的参数。arg0 的类型必须是 T0。
  
**Returns**：

使用 arg0 作为参数调用 LLVM 内部函数的结果。

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType](arg0: T0, arg1: T1) -> *"type"
```

调用一个带有两个参数的 LLVM 内部函数。

在参数 arg0 和 arg1 上调用名称为 intrin，返回类型为 type 的内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。

- **T0** (`AnyType`)：内部函数的第一个参数（arg0）的类型。

- **T1** (`AnyType`)：内部函数的第二个参数（arg1）的类型。

**Args**：

- **arg0** (`T0`)：调用 LLVM 内部函数的第一个参数。arg0 的类型必须是 T0。

- **arg1** (`T1`)：调用 LLVM 内部函数的第二个参数。arg1 的类型必须是 T1。

**Returns**：

使用 arg0 和 arg1 作为参数调用 LLVM 内部函数的结果。

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType](arg0: T0, arg1: T1, arg2: T2) -> *"type"
```

调用一个带有三个参数的 LLVM 内部函数。

在参数 arg0，arg1 和 arg2 上调用名称为 intrin，返回类型为 type 的内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。

- **T0** (`AnyType`)：内部函数的第一个参数（arg0）的类型。

- **T1** (`AnyType`)：内部函数的第二个参数（arg1）的类型。

- **T2** (`AnyType`)：内部函数的第二个参数（arg2）的类型。

**Args**：

- **arg0** (`T0`)：调用 LLVM 内部函数的第一个参数。arg0 的类型必须是 T0。

- **arg1** (`T1`)：调用 LLVM 内部函数的第二个参数。arg1 的类型必须是 T1。

- **arg2** (`T2`)：调用 LLVM 内部函数的第二个参数。arg2 的类型必须是 T2。

**Returns**：

使用 arg0，arg1 和 arg2 作为参数调用 LLVM 内部函数的结果。

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType, T3: AnyType](arg0: T0, arg1: T1, arg2: T2, arg3: T3) -> *"type"
```

调用一个带有四个参数的 LLVM 内部函数。

在参数 arg0，arg1，arg2 和 arg3 上调用名称为 intrin，返回类型为 type 的内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。

- **T0** (`AnyType`)：内部函数的第一个参数（arg0）的类型。

- **T1** (`AnyType`)：内部函数的第二个参数（arg1）的类型。

- **T2** (`AnyType`)：内部函数的第二个参数（arg2）的类型。

- **T3** (`AnyType`)：内部函数的第二个参数（arg3）的类型。

**Args**：

- **arg0** (`T0`)：调用 LLVM 内部函数的第一个参数。arg0 的类型必须是 T0。

- **arg1** (`T1`)：调用 LLVM 内部函数的第二个参数。arg1 的类型必须是 T1。

- **arg2** (`T2`)：调用 LLVM 内部函数的第二个参数。arg2 的类型必须是 T2。

- **arg3** (`T3`)：调用 LLVM 内部函数的第二个参数。arg3 的类型必须是 T3。
  
**Returns**：

使用 arg0，arg1，arg2 和 arg3 作为参数调用 LLVM 内部函数的结果。

```python
llvm_intrinsic[intrin: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType, T3: AnyType, T4: AnyType](arg0: T0, arg1: T1, arg2: T2, arg3: T3, arg4: T4) -> *"type"
```

调用一个带有五个参数的 LLVM 内部函数。

在参数 arg0，arg1，arg2，arg3 和 arg4 上调用名称为 intrin，返回类型为 type 的内部函数。

**Parameters**：

- **intrin** (`StringLiteral`): LLVM 内部函数的名称。

- **type** (`AnyType`): 内部函数的返回类型。

- **T0** (`AnyType`)：内部函数的第一个参数（arg0）的类型。

- **T1** (`AnyType`)：内部函数的第二个参数（arg1）的类型。

- **T2** (`AnyType`)：内部函数的第二个参数（arg2）的类型。

- **T3** (`AnyType`)：内部函数的第二个参数（arg3）的类型。
  
- **T4** (`AnyType`)：内部函数的第二个参数（arg4）的类型。
  
**Args**：

- **arg0** (`T0`)：调用 LLVM 内部函数的第一个参数。arg0 的类型必须是 T0。

- **arg1** (`T1`)：调用 LLVM 内部函数的第二个参数。arg1 的类型必须是 T1。

- **arg2** (`T2`)：调用 LLVM 内部函数的第二个参数。arg2 的类型必须是 T2。

- **arg3** (`T3`)：调用 LLVM 内部函数的第二个参数。arg3 的类型必须是 T3。

- **arg4** (`T4`)：调用 LLVM 内部函数的第二个参数。arg4 的类型必须是 T4。
  
**Returns**：

使用 arg0，arg1，arg2，arg3 和 arg4 作为参数调用 LLVM 内部函数的结果。

## `external_call`

```python
external_call[callee: StringLiteral, type: AnyType]() -> *"type"
```

调用外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。

**Returns**：

外部函数调用的结果。

```python
external_call[callee: StringLiteral, type: AnyType, T0: AnyType](arg0: T0) -> *"type"
```

调用带一个参数的外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。
  
- **T0** (`AnyType`)：第一个参数的类型。

**Args**：

- **arg0** (`T0`)：第一个参数。

**Returns**：

外部函数调用的结果。

```python
external_call[callee: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType](arg0: T0, arg1: T1) -> *"type"
```

调用带两个参数的外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。
  
- **T0** (`AnyType`)：第一个参数的类型。

- **T1** (`AnyType`)：第二个参数的类型。

**Args**：

- **arg0** (`T0`)：第一个参数。

- **arg1** (`T1`)：第二个参数。

**Returns**：

外部函数调用的结果。

```python
external_call[callee: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType](arg0: T0, arg1: T1, arg2: T2) -> *"type"
```

调用带三个参数的外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。
  
- **T0** (`AnyType`)：第一个参数的类型。

- **T1** (`AnyType`)：第二个参数的类型。

- **T2** (`AnyType`)：第三个参数的类型。

**Args**：

- **arg0** (`T0`)：第一个参数。

- **arg1** (`T1`)：第二个参数。
  
- **arg2** (`T2`)：第三个参数。

**Returns**：

外部函数调用的结果。

```python
external_call[callee: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType, T3: AnyType](arg0: T0, arg1: T1, arg2: T2, arg3: T3) -> *"type"
```

调用带四个参数的外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。
  
- **T0** (`AnyType`)：第一个参数的类型。

- **T1** (`AnyType`)：第二个参数的类型。

- **T2** (`AnyType`)：第三个参数的类型。

- **T3** (`AnyType`)：第四个参数的类型。

**Args**：

- **arg0** (`T0`)：第一个参数。

- **arg1** (`T1`)：第二个参数。
  
- **arg2** (`T2`)：第三个参数。

- **arg3** (`T3`)：第四个参数。

**Returns**：

外部函数调用的结果。

```python
external_call[callee: StringLiteral, type: AnyType, T0: AnyType, T1: AnyType, T2: AnyType, T3: AnyType, T4: AnyType](arg0: T0, arg1: T1, arg2: T2, arg3: T3, arg4: T4) -> *"type"
```

调用带五个参数的外部函数。

**Parameters**：

- **callee** (`StringLiteral`)：外部函数的名称。

- **type** (`AnyType`)：返回类型。
  
- **T0** (`AnyType`)：第一个参数的类型。

- **T1** (`AnyType`)：第二个参数的类型。

- **T2** (`AnyType`)：第三个参数的类型。

- **T3** (`AnyType`)：第四个参数的类型。

- **T4** (`AnyType`)：第五个参数的类型。

**Args**：

- **arg0** (`T0`)：第一个参数。

- **arg1** (`T1`)：第二个参数。
  
- **arg2** (`T2`)：第三个参数。

- **arg3** (`T3`)：第四个参数。

- **arg4** (`T4`)：第五个参数。

**Returns**：

外部函数调用的结果。

## `gather`

```python
gather[type: DType, size: Int](base: SIMD[address, size], mask: SIMD[bool, size], passthrough: SIMD[type, size], alignment: Int) -> SIMD[type, size]
```

从SIMD向量中读取标量值，并将它们聚集到一个向量中。

gather 函数从 SIMD 向量的内存位置中读取标量值，并将它们聚集到一个向量中。内存位置是在 `base` 地址的指针向量中提供的。根据提供的掩码访问内存。掩码中的每个向量通道都有一个位，用于防止对被掩码掉的通道进行内存访问。结果向量中被掩码掉的通道来自 `passthrough` 操作数的相应通道。

 一般来说，对于一些指针向量 `base`，掩码 `mask` 和透传参数 `pass`，调用的形式如下：

```python
gather(base, mask, pass)
```

等价于以下的 C++ 量加载序列：

```python
for (int i = 0; i < N; i++)
  result[i] = mask[i] ? *base[i] : passthrough[i];
```

**Parameters**：

- **type** (`DType`)：返回 SIMD 缓冲区的 DType。

- **size** (`Int`)：返回 SIMD 缓冲区的大小。

**Args**：

- **base** (`SIMD[address, size]`)： 包含 gather 操作将访问的内存地址的向量。

- **mask** (`SIMD[bool, size]`)：一个二进制向量，它阻止对基础向量的特定通道进行内存访问。

- **passthrough** (`SIMD[type, size]`)：在结果向量中，被屏蔽的通道被替换为透传向量。
  
- **alignment** (`Int`)：源地址的对齐方式。必须是0或者一个二的幂常数整数值。

**Returns**：

包含收集操作结果的 SIMD[type, size]。

## `scatter`

```python
scatter[type: DType, size: Int](value: SIMD[type, size], base: SIMD[address, size], mask: SIMD[bool, size], alignment: Int)
```

从SIMD向量中获取标量值，并将它们 `scatters` 到指针向量中。

散布操作将来自 SIMD 内存位置向量的标量值存储到指针向量中，并将它们散布到指针向量中。内存位置以地址的形式在 'base' 指针向量中提供。根据提供的掩码存储内存。掩码为每个向量通道保留一个位，并用于防止对被屏蔽通道的内存访问。

`value` 操作数是要写入内存的向量值。`base` 操作数是一个指针向量，指向值元素应存储的位置。它具有与值操作数相同的基础类型。 `mask` 操作数是一个布尔值向量。 `mask` 和 `value` 操作数的类型必须具有相同数量的向量元素。

如果 _scatter 操作多次存储到相同的内存位置，则行为是未定义的。

一般来说，对于一些向量 %value、指针向量 %base 和掩码 %mask 的指令，形式如下：

```python
%0 = pop.simd.scatter %value, %base[%mask] : !pop.simd<N, type>
```

相当于 C++ 中以下标量加载的序列：

```python
for (int i = 0; i < N; i++)
  if (mask[i])
    base[i] = value[i];
```

**Parameters**：

- **type** (`DType`): value 的 DType。

- **size** (`Int`): value 的大小。

**Args**：

- **value** (`SIMD[type, size]`)：包含散射操作结果的向量。

- **base** (`SIMD[address, size]`)：包含散射访问的内存地址的向量。

- **mask** (`SIMD[bool, size]`)： 一个二进制向量，用于阻止对基础向量的某些通道进行内存访问。

- **alignment** (`Int`)：源地址的对齐方式。必须为 0 或 2 的幂常整数值。

## `prefetch`

```python
prefetch[type: DType, params: PrefetchOptions](addr: DTypePointer[type])
```

在使用之前，预取指令或数据到缓存中。

预取功能为目标提供预取提示，以便在使用之前将指令或数据预取到缓存中。

**Parameters**：

- **type** (`DType`)：存储在 addr 中的值的数据类型。

- **params** (`PrefetchOptions`)：预取内在函数的配置选项。

**Args**：

- **addr** (`DTypePointer[type]`)：预取的数据指针。

## `masked_load`

```python
masked_load[type: DType, size: Int](addr: DTypePointer[type], mask: SIMD[bool, size], passthrough: SIMD[type, size], alignment: Int) -> SIMD[type, size]
```

从内存中加载数据并返回，用来自传递向量的值替换掩码通道。

**Parameters**：

- **type** (`DType`)：返回 SIMD 缓冲区的 DType。

- **size** (`Int`)： 返回 SIMD 缓冲区的大小。

**Args**：

- **addr** (`DTypePointer[type]`)：加载的基指针。

- **mask** (`SIMD[bool, size]`)： 一个二进制向量，阻止对存储在 addr 处的内存的某些通道的内存访问。

- **passthrough** (`SIMD[type, size]`)：在结果向量中，被屏蔽掉的通道将被替换为通过向量。

- **alignment** (`Int`)：源地址的对齐方式。必须是 0 或 2 的幂常整数值。默认为 1。

**Returns**：

存储在 SIMD[type, size] 类型向量中的加载的内存。

## `masked_store`

```python
masked_store[type: DType, size: Int](value: SIMD[type, size], addr: DTypePointer[type], mask: SIMD[bool, size], alignment: Int)
```

在内存位置存储一个值，跳过被屏蔽的通道。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **size** (`Int`)：存储的值的大小。

**Args**：

- **value** (`SIMD[type, size]`)：包含要存储的数据的向量。

- **addr** (`DTypePointer[type]`)：存储数据的内存位置的向量。

- **mask** (`SIMD[bool, size]`)：一个二进制向量，用于阻止对某些值的内存访问。

- **alignment** (`Int`)：目标位置的对齐方式。必须是 0 或 2 的幂次整数常量值。

## `compressed_store`

```python
compressed_store[type: DType, size: Int](value: SIMD[type, size], addr: DTypePointer[type], mask: SIMD[bool, size])
```

压缩值的通道，跳过掩码通道，并存储在 addr 处。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **size** (`Int`)：存储的值的大小。

**Args**：

- **value** (`SIMD[type, size]`)：包含要存储的数据的向量。

- **addr** (`DTypePointer[type]`)：存储压缩数据的内存位置。

- **mask** (`SIMD[bool, size]`)：一个二进制向量，用于防止对某些值通道的内存访问。

## `strided_load`

```python
strided_load[type: DType, simd_width: Int](addr: DTypePointer[type], stride: Int, mask: SIMD[bool, simd_width]) -> SIMD[type, simd_width]
```

根据特定的步长从地址加载值。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **simd_width** (`Int`)：SIMD 向量的宽度。

**Args**：

- **addr** (`DTypePointer[type]`)：要从中加载数据的内存位置。

- **stride** (`Int`)：加载再次之前要跳过的通道数。

- **mask** (`SIMD[bool, simd_width]`)：一个二进制向量，防止对某些值的内存访问。

**Returns**：

一个包含加载数据的向量。

```python
strided_load[type: DType, simd_width: Int](addr: DTypePointer[type], stride: Int) -> SIMD[type, simd_width]
```

根据特定的步长从地址加载值。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **simd_width** (`Int`)：SIMD 向量的宽度。

**Args**：

- **addr** (`DTypePointer[type]`)：要从中加载数据的内存位置。

- **stride** (`Int`)：加载再次之前要跳过的通道数。

**Returns**：

一个包含加载数据的向量。

## `strided_store`

```python
strided_store[type: DType, simd_width: Int](value: SIMD[type, simd_width], addr: DTypePointer[type], stride: Int, mask: SIMD[bool, simd_width])
```

根据特定的步幅从地址加载值。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **simd_width** (`Int`)：SIMD 向量的宽度。

**Args**：

- **value** (`SIMD[type, simd_width]`)：存储的值。

- **addr** (`DTypePointer[type]`)：存储值的位置。

- **stride** (`Int`)：加载再次之前要跳过的通道数。

- **mask** (`SIMD[bool, simd_width]`)：一个二进制向量，阻止对某些值的内存访问。

```python
strided_store[type: DType, simd_width: Int](value: SIMD[type, simd_width], addr: DTypePointer[type], stride: Int)
```

根据特定的步幅从地址加载值。

**Parameters**：

- **type** (`DType`)：存储的值的数据类型。

- **simd_width** (`Int`)：SIMD 向量的宽度。

**Args**：

- **value** (`SIMD[type, simd_width]`)：存储的值。

- **addr** (`DTypePointer[type]`)：存储值的位置。

- **stride** (`Int`)：加载再次之前要跳过的通道数。



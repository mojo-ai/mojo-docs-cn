# intrinsics

定义内置函数。

你可以从 `complex` 包中导入这些 API。例如：

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

`__init__`

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

`__init__`

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

`__init__`

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

`__init__`

```python
__init__() -> Self
```

使用默认参数构造 PrefetchOptions 的实例。

**Returns**：

完成构造预取配置。

`for_read`

```python
for_read(self: Self) -> Self
```

将预取目的设置为读取。

**Returns**：

更新后的预取参数。

`for_write`

```python
for_write(self: Self) -> Self
```

将预取目的设置为写入。

**Returns**：

更新后的预取参数。

`no_locality`

```python
no_locality(self: Self) -> Self
```

将预取位置设置为无。

**Returns**：

更新后的预取参数。

`low_locality`

```python
low_locality(self: Self) -> Self
```

将预取位置设置为低。

**Returns**：

更新后的预取参数。

`medium_locality`

```python
medium_locality(self: Self) -> Self
```

将预取位置设置为中。

**Returns**：

更新后的预取参数。

`high_locality`

```python
high_locality(self: Self) -> Self
```

将预取位置设置为高。

**Returns**：

更新后的预取参数。

`to_data_cache`

```python
to_data_cache(self: Self) -> Self
```

将预取目标设置为数据缓存。

**Returns**：

更新后的预取参数。

`to_instruction_cache`

```python
to_instruction_cache(self: Self) -> Self
```

将预取目标设置为指令缓存。

**Returns**：

更新后的预取参数。



# info

实现了用于查询主机目标信息的方法。

你可以从 `sys` 包中导入这些 API。例如：

```python
from sys.info import is_x86
```

## `is_x86`

```python
is_x86() -> Bool
```

如果主机系统架构是 X86，则返回 True，否则返回 False。

**Returns**：

如果主机系统架构是 X86，则为 True，否则为 False。

## `has_sse4`

```python
has_sse4() -> Bool
```

如果主机系统具有 sse4，则返回 True，否则返回 False。

**Returns**：

如果主机系统具有 sse4，则为 True，否则为 False。

## `has_avx`

```python
has_avx() -> Bool
```

如果主机系统具有 AVX，则返回 True，否则返回 False。

**Returns**：

如果主机系统具有 AVX，则为 True，否则为 False。

## `has_avx2`

```python
has_avx2() -> Bool
```

如果主机系统具有 AVX2，则返回 True，否则返回 False。

**Returns**：

如果主机系统具有 AVX2，则为 True，否则为 False。

## `has_avx512f`

```python
has_avx512f() -> Bool
```

如果主机系统具有 AVX512，则返回 True，否则返回 False。

**Returns**：

如果主机系统具有 AVX512，则为 True，否则为 False。

## `has_avx512_vnni`

```python
has_avx512_vnni() -> Bool
```

如果主机系统具有 avx512_vnni，则返回 True，否则返回 False。

**Returns**：

如果主机系统具有 avx512_vnni，则为 True，否则为 False。

## `has_neon`

```python
has_neon() -> Bool
```

如果主机系统支持 Neon，则返回 True，否则返回 False。

**Returns**：

如果主机系统支持 Neon 指令集，则为 True。

## `is_apple_m1`

```python
is_apple_m1() -> Bool
```

如果主机系统是具有 AMX 支持的 Apple M1，则返回 True，否则返回 False。

**Returns**：

如果主机系统是具有 AMX 支持的 Apple M1，则为 True，否则为 False。

## `is_neoverse_n1`

```python
is_neoverse_n1() -> Bool
```

如果主机系统是 Neoverse N1 系统，则返回 True，否则返回 False。

**Returns**：

如果主机系统是 Neoverse N1 系统，则为 True，否则为 False。

## `has_intel_amx`

```python
has_intel_amx() -> Bool
```

如果主机系统支持 Intel AMX，则返回 True，否则返回 False。

**Returns**：

如果主机系统支持 Intel AMX，则为 True，否则为 False。

## `os_is_macos`

```python
os_is_macos() -> Bool
```

如果主机操作系统是 macOS，则返回 True。

**Returns**：

如果主机操作系统是 macOS，则为 True，否则为 False。

## `os_is_linux`

```python
os_is_linux() -> Bool
```

如果主机操作系统是 Linux，则返回 True。

**Returns**：

如果主机操作系统是 Linux，则为 True，否则为 False。

## `os_is_windows`

```python
os_is_windows() -> Bool
```

如果主机操作系统是 Windows，则返回 True。

**Returns**：

如果主机操作系统是 Windows，则为 True，否则为 False。

## `is_triple`

```python
is_triple[triple: StringLiteral]() -> Bool
```

如果编译器的目标三元组与输入匹配，则返回 True，否则返回 False。

**Parameters**：

- **triple** (`StringLiteral`)：要进行检查的三元组值。

**Returns**：

如果三元组匹配，则返回 True，否则返回 False。

## `triple_is_nvidia_cuda`

```python
triple_is_nvidia_cuda() -> Bool
```

如果编译器的目标三元组是 nvptx64-nvidia-cuda，则返回 True，否则返回 False。

**Returns**：

如果三元组的目标是 cuda，则返回 True，否则返回 False。

## `simdbitwidth`

```python
simdbitwidth() -> Int
```

返回主机系统的矢量大小（以 bits 为单位）。

**Returns**：

主机系统的矢量大小（以 bits 为单位）。

## `is_little_endian`

```python
is_little_endian() -> Bool
```

如果主机的字节顺序为小端，则返回 True，否则返回 False。

**Returns**：

如果主机目标是小端，则返回 True，否则返回 False。

## `is_big_endian`

```python
is_big_endian() -> Bool
```

如果主机的字节顺序为大端，则返回 True，否则返回 False。

**Returns**：

如果主机目标是大端，则返回 True，否则返回 False。

## `simd_byte_width`

```python
simd_byte_width() -> Int
```

返回主机系统的矢量大小（以 bytes 为单位）。

**Returns**：

主机系统的矢量大小（以 bytes 为单位）。

## `sizeof`

```python
sizeof[type: AnyType]() -> Int
```

返回类型的大小（以 bytes 为单位）。

**Parameters**：

- **type** (`AnyType`)：所讨论的类型。

**Returns**：

类型的字节大小。

```python
sizeof[type: DType]() -> Int
```

返回数据类型的大小（以 bytes 为单位）。

**Parameters**：

- **type** (`DType`)：所讨论的数据类型。

**Returns**：

数据类型的字节大小。

## `alignof`

```python
alignof[type: AnyType]() -> Int
```

Returns the align of (in bytes) of the type.

Parameters:

type (AnyType): The type in question.
Returns:

The alignment of the type in bytes.

```python
alignof[type: DType]() -> Int
```

Returns the align of (in bytes) of the dtype.

Parameters:

type (DType): The DType in question.
Returns:

The alignment of the dtype in bytes.



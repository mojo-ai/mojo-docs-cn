# stringref

实现 StringRef 类。

这些是 Mojo 内置的，因此您无需导入它们。

## `StringRef`

表示对字符串的常量引用，即：字符序列和长度（不需以 null 结尾）。

**Fields**：

- **data** (`DTypePointer[si8]`)：指向所引用的字符串数据开头的指针。
- **length** (`Int`)：被引用的字符串的长度。

**Functions**：

### `__init__`

```python
__init__(str: StringLiteral) -> Self
```

在给定常量字符串的情况下构造一个 StringRef 值。

**Args**：

- **str** (`StringLiteral`)：输入常量字符串。

**Returns**：

构造的 `StringRef` 对象。

```python
__init__(ptr: Pointer[SIMD[si8, 1]], len: Int) -> Self
```

从字符串（（可能非 0 终止的字符串）构造一个 StringRef 值。

构造函数采用原始指针和长度。

**Args**：

- **ptr** (`Pointer[SIMD[si8, 1]]`)：指向字符串的指针。
- **len** (`Int`)：字符串的长度。

**Returns**：

构造的 `StringRef ` 对象。

```python
__init__(ptr: DTypePointer[si8], len: Int) -> Self
```

从字符串（（可能非 0 终止的字符串）构造一个 StringRef 值。

构造函数采用原始指针和长度。

**Args**：

- **ptr** (`DTypePointer[si8]`)：指向字符串的指针。
- **len** (`Int`)：字符串的长度。

**Returns**：

构造的 `StringRef ` 对象。

```python
__init__(ptr: Pointer[SIMD[si8, 1]]) -> Self
```

从字符串（（可能非 0 终止的字符串）构造一个 StringRef 值。

构造函数采用原始指针和长度。

**Args**：

- **ptr** (`Pointer[SIMD[si8, 1]]`)：指向字符串的指针。

**Returns**：

构造的 `StringRef ` 对象。

```python
__init__(ptr: DTypePointer[si8]) -> Self
```

从字符串（（可能非 0 终止的字符串）构造一个 StringRef 值。

构造函数采用原始指针和长度。

**Args**：

- **ptr** (`DTypePointer[si8]`)：指向字符串的指针。

**Returns**：

构造的 `StringRef ` 对象。

### `__getitem__`

```python
__getitem__(self: Self, idx: Int) -> Self
```

获取指定位置的字符串值。

**Args**：

- **idx** (`Int`)：索引位置。

**Returns**：

指定位置处的字符。

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

比较两个字符串是否相等。

**Args**：

- **rhs** (`Self`)：另一个字符串。

**Returns**：

如果字符串匹配，则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, rhs: Self) -> Bool
```

比较两个字符串是否不相等。

**Args**：

- **rhs** (`Self`)：另一个字符串。

**Returns**：

如果字符串不匹配，则为 True，否则为 False。

### `__len__`

```python
__len__(self: Self) -> Int
```

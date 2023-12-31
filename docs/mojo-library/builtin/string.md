# string

实现用于字符串处理的基本对象方法。

这些是 Mojo 内置的，因此您无需导入它们。

## `String`

表示可变字符串。

**Functions**：

### `__init__`

```python
__init__(inout self: Self)
```

构造一个空字符串。

```python
__init__(inout self: Self, str: StringRef)
```

从 StringRef 对象构造一个字符串。

**Args**：

- **str** (`StringRef`)：要从中构造此字符串对象的 StringRef。

```python
__init__(inout self: Self, str: StringLiteral)
```

在给定常量字符串的情况下构造一个字符串值。

**Args**：

- **str** (`StringLiteral`)：输入常量字符串。

```python
__init__(inout self: Self, val: Bool)
```

构造一个表示布尔值的字符串。

**Args**：

- **val** (`Bool`)：布尔值。

```python
__init__(inout self: Self, num: Int)
```

构造一个表示整数值的字符串。

**Args**：

- **num** (`Int`)：整数值。

```python
__init__(inout self: Self, num: FloatLiteral)
```

构造表示浮点值的字符串。

**Args**：

- **num** (`FloatLiteral`)：浮点值。

```python
__init__[type: DType, simd_width: Int](inout self: Self, vec: SIMD[type, simd_width])
```

为给定的 SIMD 值构造一个字符串。

**Parameters**：

- **type** (`DType`)：SIMD 值的 dtype。
- **simd_width** (`Int`)：SIMD 值的宽度。

**Args**：

- **vec** (`SIMD[type, simd_width]`)：SIMD 值。

```python
__init__[type: DType, simd_width: Int](inout self: Self, vec: ComplexSIMD[type, simd_width])
```

为给定的复合值构造字符串。

**Parameters**：

- **type** (`DType`)：SIMD 值的 dtype。
- **simd_width** (`Int`)：SIMD 值的宽度。

**Args**：

- **vec** (`ComplexSIMD[type, simd_width]`)：复合值。

```python
__init__[size: Int](inout self: Self, tuple: StaticIntTuple[size])
```

从给定的 StaticIntTuple 构造一个字符串。

**Parameters**：

- **size** (`Int`)：元组的大小。

**Args**：

- **tuple** (`StaticIntTuple`)：输入元组。

```python
__init__(inout self: Self, ptr: Pointer[SIMD[si8, 1]], len: Int)
```

从缓冲区创建字符串。注意：字符串现在拥有缓冲区。

**Args**：

- **ptr** (`Pointer[SIMD[si8, 1]]`)：指向缓冲区的指针。
- **len** (`Int`)：缓冲区的长度。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

创建现有字符串的深层拷贝。

**Args**：

- **existing** (`Self`)：要复制的字符串。

### `__del__`

```python
__del__(owned self: Self)
```

释放字符串。

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

检查字符串是否为空。

**Returns**：

如果字符串为空，则为 True，否则为 False。

### `__getitem__`

```python
__getitem__(self: Self, idx: Int) -> Self
```

获取指定位置的字符。

**Args**：

- **idx** (`Int`)：索引值。

**Returns**：

包含指定位置字符的新字符串。

```python
__getitem__(self: Self, span: slice) -> Self
```

获取指定位置处的字符序列。

**Args**：

- **span** (`slice`)：指定新子字符串位置的切片。

**Returns**：

包含指定位置的字符串的新字符串。

### `__eq__`

```python
__eq__(self: Self, other: Self) -> Bool
```

比较两个字符串是否具有相同的值。

**Args**：

- **other** (`Self`)：rhs 操作数。

**Returns**：

如果字符串相等，则为 True，否则为 False。

### `__ne__`

```python
__ne__(self: Self, other: Self) -> Bool
```

比较两个字符串是否无相同值。

**Args**：

- **other** (`Self`)：rhs 操作数。

**Returns**：

如果字符串不相等，则为 True，否则为 False。

### `__add__`

```python
__add__(self: Self, other: Self) -> Self
```

通过在末尾追加另一个字符串来创建字符串。

**Args**：

- **other** (`Self`)：要追加的字符串。

**Returns**：

新构造的字符串。

### `__radd__`

```python
__radd__(self: Self, other: Self) -> Self
```

通过在开头加上另一个字符串来创建字符串。

**Args**：

- **other** (`Self`)：要预置的字符串。

**Returns**：

新构造的字符串。

```python
__radd__(self: Self, other: StringLiteral) -> Self
```

通过在开头加上另一个字符串来创建字符串。

**Args**：

- **other** (`StringLiteral`)：要预置的字符串。

**Returns**：

新构造的字符串。

### `__iadd__`

```python
__iadd__(inout self: Self, other: Self)
```

将另一个字符串追加到此字符串。

**Args**：

- **other** (`Self`)：要追加的字符串。

### `__len__`

```python
__len__(self: Self) -> Int
```

返回字符串长度。

**Returns**：

字符串长度。

### `join`

```python
join[rank: Int](self: Self, elems: StaticIntTuple[rank]) -> Self
```

使用当前字符串作为分隔符连接元组中的元素。

**Parameters**：

- **rank** (`Int`)：元组的大小。

**Args**：

- **elems** (`StaticIntTuple[rank]`)：输入元组。

**Returns**：

连接的字符串。

```python
join(self: Self, *lst: Int) -> Self
```

使用当前字符串作为分隔符联接整数元素。

**Args**：

- **lst** (`*Int`)：输入值。

**Returns**：

连接的字符串。

```python
join(self: Self, *strs: Self) -> Self
```

使用当前字符串作为分隔符联接字符串元素。

**Args**：

- **strs** (`*Self`)：输入值。

**Returns**：

连接的字符串。

## `ord`

```python
ord(s: String) -> Int
```

返回一个整数，该整数表示给定的单字符形式的字符串。

给定一个表示单个 ASCII 字符的字符串，返回一个表示该字符的代码点的整数。例如：`ord("a")` 返回整数 `97`。这是 `chr()` 函数的逆函数。

**Args**：

- **s** (`String`)：输入字符串，其必须仅含一个字符。

**Returns**：

一个整数，表示给定字符的代码点。

## `chr`

```python
chr(c: Int) -> String
```

返回基于给定 Unicode 代码点的字符串。

返回一个字符串，该字符表示其代码点（必须是介于 0 和 255 之间的正整数）是整数 `i`。例如：`chr(97)` 返回字符串 `"a"`。这是 `ord()` 函数的逆函数。

**Args**：

- **c** (`Int`)：一个介于 0 和 255 之间的整数，表示代码点。

**Returns**：

包含基于给定代码点的单个字符的字符串。

## `atol`

```python
atol(str: String) -> Int
```

将给定字符串解析为十进制整数并返回该值。

例如：`atol("19")` 返回 `19`。如果给定的字符串无法解析为整数值，则会引发错误。例如：`atol("hi")` 引发错误。

**Args**：

- **str** (`String`)：解析为十进制整数的字符串。

**Returns**：

表示字符串的整数值。

## `isdigit`

```python
isdigit(c: SIMD[si8, 1]) -> Bool
```

确定给定字符是否为数字 [0-9]。

**Args**：

- **c** (`SIMD[si8, 1]`)：要检查的字符。

**Returns**：

如果字符是数字，则为 True。

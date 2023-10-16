# len

提供 `len` 函数。

这些均为 Mojo 内置，因此您无需导入它们。

## `len`

```python
len[type: DType, size: Int](value: SIMD[type, size]) -> Int
```

返回给定 SIMD 值的长度。

**Parameters**：

- **type** (`DType`)：SIMD 值的元素类型。
- **size** (`Int`)：值中的元素个数。

**Args**：

- **value** (`SIMD[type, size]`)：SIMD 值。

**Returns**：

SIMD 值的长度。

```python
len[size: Int, type: AnyType](value: InlinedFixedVector[size, *"type"]) -> Int
```

返回给定固定向量的长度。

**Parameters**：

- **size** (`Int`)：值中的元素个数。
- **type** (`AnyType`)：值的元素类型。

**Args**：

- **value** (`InlinedFixedVector[size, *"type"]`)：矢量值。

**Returns**：

矢量的长度。

```python
len[type: AnyType](value: UnsafeFixedVector[*"type"]) -> Int
```

返回给定向量的长度。

**Parameters**：

- **type** (`AnyType`)：值的元素类型。

**Args**：

- **value** (`UnsafeFixedVector[*"type"]`)：矢量值。

**Returns**：

矢量的长度。

```python
len[type: AnyType](value: DynamicVector[*"type"]) -> Int
```

返回给定向量的长度。

**Parameters**：

- **type** (`AnyType`)：值的元素类型。

**Args**：

- **value** (`DynamicVector[*"type"]`)：矢量值。

**Returns**：

矢量的长度。

```python
len(value: String) -> Int
```

返回给定字符串的长度。

**Args**：

- **value** (`String`)：字符串。

**Returns**：

字符串的长度。

```python
len(value: StringRef) -> Int
```

返回给定字符串引用的长度。

**Args**：

- **value** (`StringRef`)：字符串。

**Returns**：

字符串的长度。

```python
len(value: StringLiteral) -> Int
```

返回给定字符串文本的长度。

**Args**：

- **value** (`StringLiteral`)：字符串文本。

**Returns**：

字符串文本的长度。

```python
len[size: Dim, type: DType](value: Buffer[size, type]) -> Int
```

返回给定缓冲区的长度。

**Parameters**：

- **size** (`Dim`)：值中的元素数。
- **type** (`DType`)：值的元素类型。

**Args**：

- **value** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区的长度。

```python
len[type: AnyType](value: VariadicList[*"type"]) -> Int
```

返回给定可变参数列表的长度。

**Parameters**：

- **type** (`AnyType`)：值的元素类型。

**Args**：

- **value** (`VariadicList[*"type"]`)：可变参数列表。

**Returns**：

可变参数列表的长度。

```python
len[type: AnyType](value: VariadicListMem[*"type"]) -> Int
```

返回给定可变参数列表的长度。

**Parameters**：

- **type** (`AnyType`)：值的元素类型。

**Args**：

- **value** (`VariadicListMem[*"type"]`)：可变参数列表。

**Returns**：

可变参数列表的长度。

```python
len[*types: AnyType](value: ListLiteral[types]) -> Int
```

返回给定列表文本的长度。

**Parameters**：

- **type** (`*AnyType`)：值的元素类型。

**Args**：

- **value** (`ListLiteral[types]`)：列表文本。

**Returns**：

列表文本的长度。

```python
len[*types: AnyType](value: Tuple[types]) -> Int
```

返回给定元组文本的长度。

**Parameters**：

- **type** (`*AnyType`)：值的元素类型。

**Args**：

- **value** (`Tuple[types]`)：元组文本。

**Returns**：

元组文本的长度。

```python
len[size: Int](value: StaticIntTuple[size]) -> Int
```

返回给定静态元组的长度。

**Parameters**：

- **size** (`*Int`)：值中的元素数。

**Args**：

- **value** (`StaticIntTuple[size]`)：静态元组。

**Returns**：

静态元组的长度。

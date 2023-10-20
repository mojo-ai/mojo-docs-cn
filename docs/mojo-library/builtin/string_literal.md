# string_literal

实现 StringLiteral 类。

这些是 Mojo 内置的，因此您无需导入它们。

## `StringLiteral`

此类型表示字符串文本。

为了与 C API 兼容，字符串文本都以 null 结尾，但这可能会发生变化。字符串文本将其长度存储为整数，其不包括 null 终止符。

**Aliases**：

- `type = string`

**Fields**：

- **value** (`string`)：字符串文本的基础存储。

**Functions**：

### `__init__`

```python
__init__(value: string) -> Self
```

从内置字符串类型创建字符串文本。

**Args**：

- **value** (`string`)：字符串值。

**Returns**：

字符串文本对象。

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

将字符串转换为布尔值。

**Returns**：

如果字符串不为空，则为 True。

### `__eq__`

```python
__eq__(self: Self, rhs: Self) -> Bool
```

比较两个字符串文本是否相等。

**Args**：

- **rhs** (`Self`)：要比较的字符串。

**Returns**：

如果它们相等，则为 true。

### `__ne__`

```python
__ne__(self: Self, rhs: Self) -> Bool
```

比较两个字符串文本的不等性。

**Args**：

- **rhs** (`Self`)：要比较的字符串。

**Returns**：

如果它们不相等，则为 true。

### `__add__`

```python
__add__(self: Self, rhs: Self) -> Self
```

连接两个字符串文本。

**Args**：

- **rhs** (`Self`)：要连接的字符串。

**Returns**：

连接的字符串。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取字符串长度。

**Returns**：

此字符串文本的长度。

### `data`

```python
data(self: Self) -> DTypePointer[si8]
```

获取指向基础数据的原始指针。

**Returns**：

指向数据的原始指针。

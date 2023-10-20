# tuple

实现元组类型。

这些是 Mojo 内置的，因此您无需导入它们。

## `Tuple`

文本元组表达式的类型。

元组由零个或多个值组成，采用逗号分隔。

**Parameters**：

- **Ts** (`*AnyType`)：元素类型。

**Fields**：

- **storage** (`!pop.pack<Ts>`)：元组的基础存储。

**Functions**：

### `__init__`

```python
__init__(args: !pop.pack<Ts>) -> Self
```

构造元组。

**Args**：

- **args** (`!pop.pack<Ts>`)：初始值。

**Returns**：

构造的元组。

### `__copyinit__`

```python
__copyinit__(existing: Self) -> Self
```

复制方式构造元组。

**Returns**：

构造的元组。

### `__len__`

```python
__len__(self: Self) -> Int
```

获取元组中的元素数。

**Returns**：

元组长度。

### `get`

```python
get[i: Int, T: AnyType](self: Self) -> T
```

获取元组元素。

**Parameters**：

- **i** (`Int`)：元素索引。
- **T** (`AnyType`)：元素类型。

**Returns**：

请求索引处的元组元素。

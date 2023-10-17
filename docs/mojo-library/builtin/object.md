# object

定义用于表示非类型化值的对象类型。

这些是 Mojo 内置的，因此您无需导入它们。

## `Attr`

通用对象的属性在构造时设置，之后可以读取和修改属性，但不能删除或添加任何属性。

**Fields**：

- **key** (`StringLiteral`)：属性的名称。
- **value** (`object`)：属性的值。

**Functions**：

### `__init__`

```python
__init__(inout self: Self, key: StringLiteral, owned value: object)
```

使用键和值初始化属性。

**Args**：

- **key** (`StringLiteral`)：字符串文本键。
- **value** (`object`)：属性的对象值。

### `__del__`

```python
__del__(owned self: Self)
```

## `object`

表示没有具体类型的对象。

这是 def 函数中没有类型注释的参数类型，例如：`def f(x): pass` 中的 `x` 类型。在这种情况下，任何类型的值都可以作为 `x` 参数传入，以便使用该值构造 `object` 类型。

**Aliases**：

- `nullary_function = fn() raises -> object`：空函数类型。
- `unary_function = fn(object) raises -> object`：一元函数类型。
- `binary_function = fn(object, object) raises -> object`：二进制函数类型。
- `ternary_function = fn(object, object, object) raises -> object`：三元函数类型。

**Functions**：

### `__init__`

```python
__init__(inout self: Self)
```

使用 `None` 值初始化对象。

```python
__init__(inout self: Self, impl: _ObjectImpl)
```

使用实现值初始化对象（仅供内部使用）。

**Args**：

- **impl** (`_ObjectImpl`)：对象实现。

```python
__init__(inout self: Self, none: None)
```

从 `None` 文本初始化 none 值对象。

**Args**：

- **none** (`None`)：None。

```python
__init__(inout self: Self, value: Int)
```

使用整数值初始化对象。

**Args**：

- **value** (`Int`)：整数值。

```python
__init__(inout self: Self, value: FloatLiteral)
```

使用浮点值初始化对象。

**Args**：

- **value** (`FloatLiteral`)：浮点值。

```python
__init__[dt: DType](inout self: Self, value: SIMD[dt, 1])
```

使用泛型标量值初始化对象。如果标量值类型为 bool，则将其转换为布尔值。否则，它将转换为相应的整数或浮点类型。

**Parameters**：

- **dt** (`DType`)：标量值类型。

**Args**：

- **value** (`SIMD[dt, 1]`)：标量值。

```python
__init__(inout self: Self, value: Bool)
```

从布尔值初始化对象。

**Args**：

- **value** (`Bool`)：布尔值。

```python
__init__(inout self: Self, value: StringLiteral)
```

从字符串文本初始化对象。

**Args**：

- **value** (`StringLiteral`)：字符串值。

```python
__init__(inout self: Self, value: StringRef)
```

从字符串引用初始化对象。

**Args**：

- **value** (`StringRef`)：字符串值。

```python
__init__[*Ts: AnyType](inout self: Self, value: ListLiteral[Ts])
```

从列表文本初始化对象。

**Parameters**：

- **Ts** (`*AnyType`)：列表元素类型。

**Args**：

- **value** (`ListLiteral[Ts]`)：列表值。

```python
__init__(inout self: Self, func: fn() raises -> object)
```

从不带参数的函数初始化对象。

**Args**：

- **func** (`fn() raises -> object`)：函数。

```python
__init__(inout self: Self, func: fn(object) raises -> object)
```

从接受一个参数的函数初始化对象。

**Args**：

- **func** (`fn(object) raises -> object`)：函数。

```python
__init__(inout self: Self, func: fn(object, object) raises -> object)
```

从接受两个参数的函数初始化对象。

**Args**：

- **func** (`fn(object, object) raises -> object`)：函数。

```python
__init__(inout self: Self, func: fn(object, object, object) raises -> object)
```

从接受三个参数的函数初始化对象。

**Args**：

- **func** (`fn(object, object, object) raises -> object`)：函数。

```python
__init__(inout self: Self, *attrs: Attr)
```

使用零个或多个属性的序列初始化对象。

**Args**：

- **attrs** (`*Attr`)：零个或多个属性。

### `__copyinit__`

```python
__copyinit__(inout self: Self, existing: Self)
```

复制对象。其克隆基础字符串值，并增加列表或字典的引用计数。

**Args**：

- **existing** (`Self`)：要复制的对象。

### `__moveinit__`

```python
__moveinit__(inout self: Self, owned existing: Self)
```

移动对象的值。

**Args**：

- **existing** (`Self`)：要移动的对象。

### `__del__`

```python
__del__(owned self: Self)
```

删除对象并释放所有拥有的内存。

### `__bool__`

```python
__bool__(self: Self) -> Bool
```

根据 Python 语义转换为布尔值。如果整数和浮点数不为零，则为 true；如果字符串和列表为非空，则为 true。

**Returns**：

对象是否被视为 true。

### `__getitem__`

```python
__getitem__(self: Self, i: Self) -> Self
```

从对象中获取第 i 项（仅对字符串、列表和字典有效）。

**Args**：

- **i** (`Self`)：字符串或列表索引或字典键。

**Returns**：

索引或键所对应的值。

```python
__getitem__(self: Self, *i: Self) -> Self
```

从对象中获取第 i 项，其中 i 是索引元组。

**Args**：

- **i** (`*Self`)：复合索引。

**Returns**：

索引处的值。

### `__setitem__`

```python
__setitem__(self: Self, i: Self, value: Self)
```

设置对象中的第 i 项（仅对字符串、列表和字典有效）。

**Args**：

- **i** (`*Self`)：字符串或列表索引或字典键。
- **value** (`Self`)：要设置的值。

```python
__setitem__(self: Self, i: Self, j: Self, value: Self)
```

TODO

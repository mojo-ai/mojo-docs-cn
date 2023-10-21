# object 模块

实现 PythonObject。

你可以从 `python` 包中导入这些 API。例如：

```python
from python.object import PythonObject
```

## `PythonObject`

 一个 Python 对象。

**字段（Fields）**：

**py_object** (`PyObjectPtr`): 指向底层 Python 对象的指针。 

**函数（Functions）：**

### `__init__`

 `__init__(inout self: Self)`

初始化对象，其值为 `None`。

`__init__(inout self: Self, none: None)`

从 `None` 字面值初始化一个空值对象。

**参数（Args）：**

- **none** (`None`): None。 

`__init__(inout self: Self, integer: Int)`

初始化对象，其值为整数。

**参数（Args）：**

- **integer** (`Int`): 整数值。 

`__init__(inout self: Self, float: FloatLiteral)`

初始化对象，其值为浮点数。

**参数（Args）**：

- **float** (`FloatLiteral`): 浮点数值。 

`__init__[dt: DType](inout self: Self, value: SIMD[dt, 1])`

用通用标量值初始化对象。如果标量值类型为布尔值，则将其转换为布尔值。否则，将其转换为适当的整数或浮点类型。

**参数（Parameters）**：

- **dt** (`DType`): 标量值类型。 

**参数（Args）**：

- **value** (`SIMD[dt, 1]`): 标量值。 

`__init__(inout self: Self, value: Bool)`

从布尔值初始化对象。

**参数（Args）**：

- **value** (`Bool`): 布尔值。

` __init__(inout self: Self, str: StringLiteral)`

从字符串字面值初始化对象。

**参数（Args）**：

- **str** (`StringLiteral`): 字符串值。 

`__init__(inout self: Self, str: StringRef)`

从字符串引用初始化对象。

**参数（Args）：**

- **str** (`StringRef)`: 字符串值。 

`__init__(inout self: Self, str: String)`

从字符串初始化对象。

**参数（Args）**：

- **str** (`String`): 字符串值。 

`__init__[*Ts: AnyType](inout self: Self, value: ListLiteral[Ts])`

从列表字面值初始化对象。

**参数（Parameters）：**

- **Ts** (`*AnyType`): 列表元素类型。 

**参数（Args）：**

- **value** (`ListLiteral[Ts]`): 列表值。 

`__init__[*Ts: AnyType](inout self: Self, value: Tuple[Ts])`

从元组字面值初始化对象。

**参数（Parameters）：**

- **Ts** (`*AnyType`): 元组元素类型。 

**参数（Args）：**

- **value** (`Tuple[Ts]`): 元组值。 

`__init__(inout self: Self, py_object: PyObjectPtr)`



### `__copyinit__`

`__copyinit__(inout self: Self, existing: Self)`

复制对象。

此操作会增加现有对象的底层引用计数。

**参数（Args）：**

- **existing** (`Self`): 要复制的值。 



### `__moveinit__`

`__moveinit__(inout self: Self, owned existing: Self)`



### `__del__`

 `__del__(owned self: Self)`

销毁对象。

此操作会减少指向对象的底层引用计数。



### `__bool__`

` __bool__(self: Self) -> Bool`

计算对象的布尔值。

**返回（Returns）：**

如果对象评估为真，则返回 true。



### `__getitem__`

 `__getitem(self: Self, *args: Self) -> Self`

返回给定键的值。

**参数（Args）：**

- **args** (`*Self`): 要在此对象上访问的单个键或一系列键。 

**返回（Returns）：**

给定键对应的值。



### `__neg__`

`__neg__(self: Self) -> Self`

取负值。

调用底层对象的 `__neg__` 方法。

**返回（Returns）：**

为该对象添加 `-` 运算符前缀的结果。对于大多数数值对象，这会返回负数。



### `__pos__`

`__pos__(self: Self) -> Self`

取正值。

调用底层对象的 `__pos__` 方法。

**返回（Returns）：**

为该对象添加 `+` 运算符前缀的结果。对于大多数数值对象，这将无影响。



### `__invert__`

`__invert__(self: Self) -> Self`

按位取反。

调用底层对象的 `__invert__` 方法。

**返回（Returns）：**

取反后的逻辑结果，即按位反转后的结果，从 0 到 1，从 1 到 0。



### `__lt__`

` __lt__(self: Self, rhs: Self) -> Self`

小于比较。用于按字典顺序比较字符串和列表。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。 

**返回（Returns）：**

如果对象小于右侧参数，则为 True。



### `__le__`

`__le__(self: Self, rhs: Self) -> Self`

小于或等于比较。用于按字典顺序比较字符串和列表。

**参数（Args）：**

- **rhs** (`Self`): 右侧值.

**返回（Returns）：**

如果对象小于或等于右侧参数，则为 True。



### `__eq__`

`__eq__(self: Self, rhs: Self) -> Self`

相等比较。用于比较字符串和列表的元素。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

如果对象相等，则为 True。



### `__ne__`

`__ne__(self: Self, rhs: Self) -> Self`

不相等比较。用于比较字符串和列表的元素。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

如果对象不相等，则为 True。



### `__gt__`

`__gt__(self: Self, rhs: Self) -> Self`

大于比较。用于按字典顺序比较字符串和列表的元素。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

如果左侧值更大，则为 True。



### `__ge__`

- `__ge__(self: Self, rhs: Self) -> Self`

  大于或等于比较。用于按字典顺序比较字符串和列表的元素。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

如果左侧值大于或等于右侧值，则为 True.

### `__add__`

- `__add__(self: Self, rhs: Self) -> Self`

  加法和连接。

  调用底层对象的 `__add__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

总和或连接的值。



### `__sub__`

`__sub__(self: Self, rhs: Self) -> Self`

减法。

调用底层对象的 `__sub__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

差异。



### `__mul__`

`__mul__(self: Self, rhs: Self) -> Self`

乘法。

调用底层对象的 `__mul__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 右侧值。

**返回（Returns）：**

乘积。

### `__truediv__`

`__truediv__(self: Self, rhs: Self) -> Self`

除法。

调用底层对象的 `__truediv__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的右侧值。

**返回（Returns）：**

将右侧值除以此对象的结果。



### `__floordiv__`

`__floordiv__(self: Self, rhs: Self) -> Self`

将自己和 rhs 的除法向下舍入到最接近的整数。

调用底层对象的 `__floordiv__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的右侧值。

**返回（Returns）：**

将此除以右侧值的结果，同时保留余数。



### `__mod__`

`__mod__(self: Self, rhs: Self) -> Self`

返回自己除以 rhs 的余数。

调用底层对象的 `__mod__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的值。

**返回（Returns）：**

将自己除以 rhs 的余数。



### `__pow__`

`__pow__(self: Self, rhs: Self) -> Self`

将此对象升至给定值的幂次方。

**参数（Args）：**

- **rhs** (`Self`): 指数。

**返回（Returns）：**

将此升至给定指数的结果。



### `__lshift__`

`__lshift__(self: Self, rhs: Self) -> Self`

位左移。

**参数（Args）：**

- **rhs** (`Self`): 按位将此对象向左移动的右侧值。

**返回（Returns）：**

这个值，按照给定值向左移动。

### `__rshift__`

`__rshift__(self: Self, rhs: Self) -> Self`

位右移。

**参数（Args）：**

- **rhs** (`Self`): 按位将此对象向右移动的右侧值。

**返回（Returns）：**

这个值，按照给定值向右移动。



### `__and__`

`__and__(self: Self, rhs: Self) -> Self`

按位与。

**参数（Args）：**

- **rhs** (`Self`): 用于按位与此对象的右侧值。

**返回（Returns）：**

此值与给定值的按位与结果。



### `__or__`

`__or__(self: Self, rhs: Self) -> Self`

按位或。

**参数（Args）：**

- **rhs** (`Self`): 用于按位或此对象的右侧值。

**返回（Returns）：**

此值与给定值的按位或结果。



### `__xor__`

`__xor__(self: Self, rhs: Self) -> Self`

异或。

**参数（Args）：**

- **rhs** (`Self`): 用于按位异或此对象的右侧值。

**返回（Returns）：**

此值与给定值的按位异或结果。



### `__radd__`

`__radd__(self: Self, lhs: Self) -> Self`

反向加法和连接。

调用底层对象的 `__radd__` 方法。

**参数（Args）：**

- **lhs** (`Self`): 用于添加或连接此对象的左侧值。

**返回（Returns）：**

总和。



### `__rsub__`

`__rsub__(self: Self, lhs: Self) -> Self`

反向减法。

调用底层对象的 `__rsub__` 方法。

**参数（Args）：**

- **lhs** (`Self`): 从中减去此对象的左侧值.

**返回（Returns）：**

从给定值减去此对象的结果。



### `__rmul__`

`__rmul__(self: Self, lhs: Self) -> Self`

反向乘法。

调用底层对象的 `__rmul__` 方法

**参数（Args）：**

- **lhs** (`Self`): 与此对象相乘的左侧值。

**返回（Returns）：**

乘法的产物。



### `__rtruediv__`

`__rtruediv__(self: Self, lhs: Self) -> Self`

反向除法。

调用底层对象的 `__rtruediv__` 方法。

**参数（Args）：**

- **lhs** (`Self`): 除此对象的左侧值。

**返回（Returns）：**

通过此除以给定值的结果。



### `__rfloordiv__`

`__rfloordiv__(self: Self, lhs: Self) -> Self`

反向地向下舍入除法。

调用底层对象的 `__rfloordiv__` 方法。

**参数（Args）：**

- **lhs** (`Self`): 由此对象除以的左侧值。

**返回（Returns）：**

通过此除以给定值的结果，除以任何余数。



### `__rmod__`

`__rmod__(self: Self, lhs: Self) -> Self`

反向取模。

调用底层对象的 `__rmod__` 方法。

**参数（Args）：**

- **lhs** (`Self`): 由此对象除以的左侧值。

**返回（Returns）：**

通过此除以给定值的余数。



### `__rpow__`

`__rpow__(self: Self, lhs: Self) -> Self`

反向幂次方。

**参数（Args）：**

- **lhs** (`Self`): 升至此对象的指数的数字。

**返回（Returns）：**

通过此指数升至给定值的结果。



### `__rlshift__`

`__rlshift__(self: Self, lhs: Self) -> Self`

反向按位左移。

**参数（Args）：**

- **lhs** (`Self`): 由此对象按位向左移动的左侧值。

**返回（Returns）：**

通过此左移的给定值。



### `__rrshift__`

`__rrshift__(self: Self, lhs: Self) -> Self`

反向按位右移.

**参数（Args）：**

- **lhs** (`Self`): 由此对象按位向右移动的左侧值。

**返回（Returns）：**

通过此右移的给定值。



### `__rand__`

`__rand__(self: Self, lhs: Self) -> Self`

反向按位与。

**参数（Args）：**

- **lhs** (`Self`): 与此对象按位与的左侧值。

**返回（Returns）：**

给定值与此的按位与结果。



### `__ror__`

`__ror__(self: Self, lhs: Self) -> Self`

反向按位或.

**参数（Args）：**

- **lhs** (`Self`): 与此对象按位或的左侧值。

**返回（Returns）：**

给定值与此的按位或结果。



### `__rxor__`

`__rxor__(self: Self, lhs: Self) -> Self`

反向按位异或。

**参数（Args）：**

- **lhs** (`Self`): 与此对象按位异或的左侧值。

**返回（Returns）：**

给定值与此的按位异或结果。



### `__iadd__`

`__iadd__(inout self: Self, rhs: Self)`

立即加法和连接。

**参数（Args）：**

- **rhs** (`Self`): 添加到此对象的右侧值。



### `__isub__`

`__isub__(inout self: Self, rhs: Self)`

立即减法。

**参数（Args）：**

- **rhs** (`Self`): 从此对象中减去的右侧值。



### `__imul__`

`__imul__(inout self: Self, rhs: Self)`

原地乘法.

调用底层对象的 `__imul__` 方法。

**参数（Args）：**

- **rhs** (`Self`): 由此对象相乘的右侧值。



### `__itruediv__`

`__itruediv__(inout self: Self, rhs: Self)`

立即除法。

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的值。



### `__ifloordiv__`

`__ifloordiv__(inout self: Self, rhs: Self)`

立即向下舍入除法。

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的值。



### `__imod__`

`__imod__(inout self: Self, rhs: Self)`

立即取模.

**参数（Args）：**

- **rhs** (`Self`): 用于除此对象的右侧值。



### `__ipow__`

`__ipow__(inout self: Self, rhs: Self)`

立即幂次方。

**参数（Args）：**

- **rhs** (`Self`): 指数。



### `__ilshift__`

`__ilshift__(inout self: Self, rhs: Self)`

立即按位左移。

**参数（Args）：**

- **rhs** (`Self`): 按位将此对象向左移动的右侧值。



### `__irshift__`

`__irshift__(inout self: Self, rhs: Self)`

立即按位右移。

**参数（Args）：**

- **rhs** (`Self`): 按位将此对象向右移动的右侧值。



### `__iand__`

`__iand__(inout self: Self, rhs: Self)`

立即按位与。

**参数（Args）：**

- **rhs** (`Self`): 与此对象按位与的右侧值。



### `__ixor__`

`__ixor__(inout self: Self, rhs: Self)`

立即按位异或。

**参数（Args）：**

- **rhs** (`Self`): 与此对象按位异或的右侧值。



### `__ior__`

`__ior__(inout self: Self, rhs: Self)`

立即按位或。

**参数（Args）：**

- **rhs** (`Self`): 与此对象按位或的右侧值。



### `__iter__`

`__iter__(inout self: Self) -> _PyIter`

如果支持，遍历对象。

**返回（Returns）：**

迭代器对象。



### `__getattr__`

`__getattr__(self: Self, name: StringLiteral) -> Self`

返回具有给定名称的对象属性的值。

**参数（Args）：**

- **name** (`StringLiteral`): 要返回的对象属性的名称。

**返回（Returns）：**

具有给定名称的对象属性的值。



### `__setattr__`

`__setattr__(self: Self, name: StringLiteral, newValue: Self)`

为具有给定名称的对象属性设置给定值。

**参数（Args）：**

- **name** (`StringLiteral`): 要设置的对象属性的名称。

- **newValue** (`Self`): 为该属性设置的新值。




### `__setattr__`

`__setattr__(self: Self, name: StringLiteral, newValue: Dictionary)`

为具有给定名称的对象属性设置给定字典。

**参数（Args）：**

- **name** (`StringLiteral`): 要设置的对象属性的名称。

- **newValue** (`Dictionary`): 为该属性设置的新字典值。




### `__call__`

`__call__(self: Self, *args: Self) -> Self`

调用底层对象，就像它是一个函数一样。

**返回（Returns）：**

调用对象的返回值。



### `__to_float64__`

`__to_float64__(self: Self) -> SIMD[f64, 1]`

返回对象的浮点表示。

**返回（Returns）：**

表示此对象的浮点值。



### `__index__`

`__index__(self: Self) -> Int`

返回对象的索引表示。

**返回（Returns）：**

表示此对象的索引值。



### `__to_string__`

`__to_string__(self: Self) -> String`

返回对象的字符串表示。

调用底层对象的 `__str__` 方法。

**返回（Returns）：**

表示此对象的字符串。

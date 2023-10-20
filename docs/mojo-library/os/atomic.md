# atomic 模块

实现了 Atomic 类。

你可以从 `os` 包中导入这些 API。例如：

```python
from os.atomic import Atomic
```

## `Atomic`

 表示一个具备原子操作的值。

该类提供了原子添加和减法方法，用于修改值。

**参数（Parameters）：**

- **_type** (`DType`): 值的数据类型。

 **别名（Aliases）：**

- `type = _21x15__type`

-  scalar_type = scalar<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> _type, "value">> 

**字段（Fields）：**

- value (`scalar<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> _type, "value">>`): 原子值。 

**函数（Functions）：**

### `__init__`

 `__init__(inout self: Self, value: SIMD[_type, 1])`

​    构造一个新的原子值。

​    **参数（Args）：**

   - value (`SIMD[_type, 1]`): 初始值，表示为 SIMD[type, 1] 类型。



 `__init__(inout self: Self, value: Int)`

​    构造一个新的原子值。

​    **参数（Args）：**

   - value (Int): 初始值，表示为 mlir.index 类型。

     

 `__init__(inout self: Self, value: scalar<#lit.struct.extract<:!kgen.declref<*"$builtin"::*"$dtype"::_DType> _type, "value">>)`

​    构造一个新的原子值。

​    **参数（Args）：**
        - **value** (`scalar<#lit.struct.extract<:!kgen.declref<*"$builtin"::*"$dtype"::_DType> _type, "value">>`): 初始值，表示为 pop.scalar 类型。



### `__iadd__`

 `__iadd__(inout self: Self, rhs: SIMD[_type, 1])`

​    执行原子的就地加法。

​    原子地用值和参数的算术加法结果替换当前值。即，它执行原子的后增操作。该操作是一个读-修改-写操作。内存受顺序的影响，顺序是顺序一致的。

​    **参数（Args）：**

        - **rhs** (`SIMD[_type, 1]`): 要添加的值。



### `__isub__`

`__isub__inout self: Self, rhs: SIMD[_type, 1])`

​    执行原子的就地减法。

   原子地用值和参数的算术减法结果替换当前值。即，它执行原子的后减操作。该操作是一个读-修改-写操作。内存受顺序的影响，顺序是顺序一致的。

​    **参数（Args）：**

        - **rhs** (`SIMD[_type, 1]`): 要减去的值。 



### `fetch_add`

 `fetch_add(inout self: Self, rhs: SIMD[_type, 1]) -> SIMD[_type, 1]`

​    执行原子的就地加法。

​    原子地用值和参数的算术加法结果替换当前值。即，它执行原子的后增操作。该操作是一个读-修改-写操作。内存受顺序的影响，顺序是顺序一致的。

​    参数（Args）：

        - **rhs** (`SIMD[_type, 1]`): 要添加的值。 

​    **返回（Returns）：**

​    加法前的原始值。

### `fetch_sub`

`fetch_sub(inout self: Self, rhs: SIMD[_type, 1]) -> SIMD[_type, 1]`

​    执行原子的就地减法。

​    原子地用值和参数的算术减法结果替换当前值。即，它执行原子的后减操作。该操作是一个读-修改-写操作。内存受顺序的影响，顺序是顺序一致的。

​    **参数（Args）：**

        - rhs (`SIMD[_type, 1]`): 要减去的值。

​    **返回（Returns）**：

​    减法前的原始值。

### `max`

`max(inout self: Self, rhs: SIMD[_type, 1])`

​    执行原子的就地最大值操作。

​    原子地用值和参数的最大值结果替换当前值。该操作是一个读-修改-写操作，按照顺序一致语义执行。

​    **约束（Constraints）：**

​    输入类型必须是整数或浮点数类型。

​    **参数（Args）：**

        - rhs (`SIMD[_type, 1]`): 最大值。



### `min`

`min(inout self: Self, rhs: SIMD[_type, 1])`

​    执行原子的就地最小值操作。

​    原子地用值和参数的最小值结果替换当前值。该操作是一个读-修改-写操作，按照顺序一致语义执行。

​    **约束（Constraints）：**

​    输入类型必须是整数或浮点数类型。

​    参数：

​        - rhs (`SIMD[_type, 1]`): 最小值。


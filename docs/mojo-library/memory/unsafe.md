# 不安全

模块

实现用于处理不安全指针的类。

您可以从 `memory`包中导入这些 API。例如：

```
from memory.unsafe import Pointer
```

## `Pointer`[](#pointer)

定义一个包含任何 mlirtype 地址的 Pointer 结构。

**Parameters：**

* **type** ( `AnyType`)：基础数据的类型。

**别名：**

* `pointer_type = pointer<*"type">`

**领域：**

* **地址**（`pointer<*"type">`）：指向的地址。

**函数：**

### `__init__`[](#init__)

`__init__() -> Self`

从 pop.pointer 类型的值构造一个空指针。

**返回：**

构造的指针对象。

`__init__(address: Self) -> Self`

从地址构造一个指针。

**参数：**

* **地址**( `Self`)：输入指针。

**返回：**

构造的指针对象。

`__init__(address: pointer<*"type">) -> Self`

从地址构造一个指针。

**参数：**

* **地址**( `pointer<*"type">`)：输入指针地址。

**返回：**

构造的指针对象。

`__init__(value: SIMD[address, 1]) -> Self`

从标量地址的值构造一个指针。

**参数：**

* **value** ( `SIMD[address, 1]`)：输入指针索引。

**返回：**

构造的指针对象。

### `__bool__`[](#bool__)

`__bool__(self: Self) -> Bool`

检查指针是否为空。

**返回：**

如果指针为空则返回 False，否则返回 True。

### `__getitem__`[](#getitem__)

`__getitem__(self: Self, offset: Int) -> *"type"`

加载 Pointer 对象以给定偏移量指向的值。

**参数：**

* **offset** ( `Int`): 加载的偏移量。

**返回：**

加载的值。

### `__eq__`[](#eq__)

`__eq__(self: Self, rhs: Self) -> Bool`

如果两个指针相等则返回 True。

**参数：**

* **rhs** ( `Self`)：另一个指针的值。

**返回：**

如果两个指针相等则为 True，否则为 False。

### `__ne__`[](#ne__)

`__ne__(self: Self, rhs: Self) -> Bool`

如果两个指针不相等，则返回 True。

**参数：**

* **rhs** ( `Self`)：另一个指针的值。

**返回：**

如果两个指针不相等则为 True，否则为 False。

### `__add__`[](#add__)

`__add__(self: Self, rhs: Int) -> Self`

返回移动指定偏移量的新指针。

**参数：**

* **rhs** ( `Int`)：偏移量。

**返回：**

新指针移动了偏移量。

### `__sub__`[](#sub__)

`__sub__(self: Self, rhs: Int) -> Self`

返回向后移动指定偏移量的新指针。

**参数：**

* **rhs** ( `Int`)：偏移量。

**返回：**

新指针向后移动了偏移量。

### `__iadd__`[](#iadd__)

`__iadd__(inout self: Self, rhs: Int)`

将当前指针移动指定的偏移量。

**参数：**

* **rhs** ( `Int`)：偏移量。

### `__isub__`[](#isub__)

`__isub__(inout self: Self, rhs: Int)`

将当前指针向后移动指定的偏移量。

**参数：**

* **rhs** ( `Int`)：偏移量。

### `get_null`[](#get_null)

`get_null() -> Self`

构造一个代表 nullptr 的指针。

**返回：**

构造了 nullptr 指针对象。

### `address_of`[](#address_of)

`address_of(inout *arg: "type") -> Self`

获取参数的地址。

**参数：**

* **arg** ( `*"type"`)：要获取地址的值。

**返回：**

包含参数地址的指针结构。

### `load`[](#load)

`load(self: Self, offset: Int) -> *"type"`

加载 Pointer 对象以给定偏移量指向的值。

**参数：**

* **offset** ( `Int`): 加载的偏移量。

**返回：**

加载的值。

`load(self: Self) -> *"type"`

加载 Pointer 对象指向的值。

**返回：**

加载的值。

### `store`[](#store)

`store(self: Self, offset: Int, *value: "type")`

将指定值存储到 Pointer 对象以给定偏移量指向的位置。

**参数：**

* **offset** ( `Int`): 加载的偏移量。
* **value** ( `*"type"`)：要存储的值。

`store(self: Self, *value: "type")`

将指定值存储到 Pointer 对象指向的位置。

**参数：**

* **value** ( `*"type"`)：要存储的值。

### `alloc`[](#alloc)

`alloc(count: Int) -> Self`

堆分配多个指定类型的元素。

**参数：**

* **count** ( `Int`)：要分配的元素数量（请注意，这不是字节计数）。

**返回：**

已在堆上分配的新指针对象。

### `aligned_alloc`[](#aligned_alloc)

`aligned_alloc(alignment: Int, count: Int) -> Self`

使用指定的对齐方式在堆上分配指定类型的多个元素。

**参数：**

* **alignment** ( `Int`): 用于分配的对齐方式。
* **count** ( `Int`)：要分配的元素数量（请注意，这不是字节计数）。

**返回：**

已在堆上分配的新指针对象。

### `free`[](#free)

`free(self: Self)`

释放堆分配的内存。

### `bitcast`[](#bitcast)

`bitcast[new_type: AnyType](self: Self) -> Pointer[new_type]`

将指针位广播为不同类型。

**Parameters：**

* **new\_type** ( `AnyType`)：目标类型。

**返回：**

具有指定类型和与原始 Pointer 相同地址的新 Pointer 对象。

### `offset`[](#offset)

`offset(self: Self, idx: Int) -> Self`

返回移动指定偏移量的新指针。

**参数：**

* **idx** ( `Int`)：偏移量。

**返回：**

新指针移动了偏移量。

## `DTypePointer`[](#dtypepointer)

定义一个`DTypePointer`包含给定数据类型地址的结构体。

**Parameters：**

* **type** ( `DType`)：基础数据的 DType。

**别名：**

* `element_type = scalar<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> type, "value">>`

<!---->

* `pointer_type = pointer<scalar<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> type, "value">>>`

**领域：**

* **地址**（`pointer<scalar<#lit.struct.extract<:!kgen.declref<@"$builtin"::@"$dtype"::@DType> type, "value">>>`）：指向的地址。

**函数：**

### `__init__`[](#init__-1)

`__init__() -> Self`

`DTypePointer`从给定类型构造一个 null 。

**返回：**

构造的`DTypePointer`对象。

`__init__(address: Self) -> Self`

从地址构造一个 DTypePointer。

**参数：**

* **地址**( `Self`)：输入指针。

**返回：**

构造的指针对象。

`__init__(address: pointer<scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>>) -> Self`

`DTypePointer`从给定地址构造 a 。

**参数：**

* **地址**( `pointer<scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>>`)：输入指针。

**返回：**

构造的`DTypePointer`对象。

`__init__(value: Pointer[SIMD[type, 1]]) -> Self`

`DTypePointer`从相同类型的标量指针构造 a 。

**参数：**

* **value** ( `Pointer[SIMD[type, 1]]`)：标量指针。

**返回：**

已建成`DTypePointer`。

`__init__(value: SIMD[address, 1]) -> Self`

`DTypePointer`从标量地址的值构造 a 。

**参数：**

* **value** ( `SIMD[address, 1]`)：输入指针索引。

**返回：**

构造的`DTypePointer`对象。

### `__bool__`[](#bool__-1)

`__bool__(self: Self) -> Bool`

检查指针是否为_null_。

**返回：**

如果指针为_空_则返回 False ，否则返回 True。

### `__lt__`[](#lt__)

`__lt__(self: Self, rhs: Self) -> Bool`

如果该指针表示的地址低于 rhs，则返回 True。

**参数：**

* **rhs** ( `Self`)：另一个指针的值。

**返回：**

如果该指针代表低地址则为 True，否则为 False。

### `__eq__`[](#eq__-1)

`__eq__(self: Self, rhs: Self) -> Bool`

如果两个指针相等则返回 True。

**参数：**

* **rhs** ( `Self`)：另一个指针的值。

**返回：**

如果两个指针相等则为 True，否则为 False。

### `__ne__`[](#ne__-1)

`__ne__(self: Self, rhs: Self) -> Bool`

如果两个指针不相等，则返回 True。

**参数：**

* **rhs** ( `Self`)：另一个指针的值。

**返回：**

如果两个指针不相等则为 True，否则为 False。

### `__add__`[](#add__-1)

`__add__(self: Self, rhs: Int) -> Self`

返回移动指定偏移量的新指针。

**参数：**

* **rhs** ( `Int`)：偏移量。

**返回：**

新的 DTypePointer 移动了偏移量。

### `__sub__`[](#sub__-1)

`__sub__(self: Self, rhs: Int) -> Self`

返回向后移动指定偏移量的新指针。

**参数：**

* **rhs** ( `Int`)：偏移量。

**返回：**

新的 DTypePointer 移动了偏移量。

### `__iadd__`[](#iadd__-1)

`__iadd__(inout self: Self, rhs: Int)`

将当前指针移动指定的偏移量。

**参数：**

* **rhs** ( `Int`)：偏移量。

### `__isub__`[](#isub__-1)

`__isub__(inout self: Self, rhs: Int)`

将当前指针向后移动指定的偏移量。

**参数：**

* **rhs** ( `Int`)：偏移量。

### `get_null`[](#get_null-1)

`get_null() -> Self`

构造一个`DTypePointer`代表_nullptr_。

**返回：**

构造了_nullptr_ `DTypePointer`对象。

### `address_of`[](#address_of-1)

`address_of(inout arg: scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>) -> Self`

获取参数的地址。

**参数：**

* **arg** ( `scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>`)：要获取地址的值。

**返回：**

包含参数地址的指针结构。

### `alloc`[](#alloc-1)

`alloc(count: Int) -> Self`

堆分配多个指定类型的元素。

**参数：**

* **count** ( `Int`)：要分配的元素数量（请注意，这不是字节计数）。

**返回：**

`DTypePointer`已在堆上分配的新对象。

### `aligned_alloc`[](#aligned_alloc-1)

`aligned_alloc(alignment: Int, count: Int) -> Self`

使用指定的对齐方式在堆上分配指定类型的多个元素。

**参数：**

* **alignment** ( `Int`): 用于分配的对齐方式。
* **count** ( `Int`)：要分配的元素数量（请注意，这不是字节计数）。

**返回：**

`DTypePointer`已在堆上分配的新对象。

### `free`[](#free-1)

`free(self: Self)`

释放堆分配内存。

### `bitcast`[](#bitcast-1)

`bitcast[new_type: DType](self: Self) -> DTypePointer[new_type]`

位广播`DTypePointer`为不同的数据类型。

**Parameters：**

* **new\_type** ( `DType`)：目标数据类型。

**返回：**

`DTypePointer`具有指定 dtype 和与原始 相同地址的新对象`DTypePointer`。

### `as_scalar_pointer`[](#as_scalar_pointer)

`as_scalar_pointer(self: Self) -> Pointer[SIMD[type, 1]]`

将 转换`DTypePointer`为相同数据类型的标量指针。

**返回：**

A`Pointer`为相同数据类型的标量。

### `load`[](#load-1)

`load(self: Self, offset: Int) -> SIMD[type, 1]`

从指定索引处的指针加载单个元素（大小为 1 的 SIMD）。

**参数：**

* **offset** ( `Int`): 加载的偏移量。

**返回：**

加载的值。

`load(self: Self) -> SIMD[type, 1]`

从指针加载单个元素（大小为 1 的 SIMD）。

**返回：**

加载的值。

### `prefetch`[](#prefetch)

`prefetch[params: PrefetchOptions](self: Self)`

预取底层地址处的内存。

**Parameters：**

* **params** ( `PrefetchOptions`)：预取选项（`PrefetchOptions`详细信息请参见）。

### `simd_load`[](#simd_load)

`simd_load[width: Int](self: Self, offset: Int) -> SIMD[type, width]`

从指定偏移处的指针加载元素的 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **offset** ( `Int`): 加载的偏移量。

**返回：**

加载的值。

`simd_load[width: Int](self: Self) -> SIMD[type, width]`

从指针加载元素的 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**返回：**

加载的 SIMD 值。

### `aligned_simd_load`[](#aligned_simd_load)

`aligned_simd_load[width: Int, alignment: Int](self: Self, offset: Int) -> SIMD[type, width]`

从指定偏移处的指针加载元素的 SIMD 向量，并保证指定的对齐方式。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。
* **alignment**( `Int`)：地址的最小对齐方式。

**参数：**

* **offset** ( `Int`): 加载的偏移量。

**返回：**

加载的 SIMD 值。

`aligned_simd_load[width: Int, alignment: Int](self: Self) -> SIMD[type, width]`

从具有保证的指定对齐方式的指针加载元素的 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。
* **alignment**( `Int`)：地址的最小对齐方式。

**返回：**

加载的 SIMD 值。

### `store`[](#store-1)

`store(self: Self, offset: Int, val: SIMD[type, 1])`

在给定偏移处存储单个元素值。

**参数：**

* **offset** ( `Int`)：要存储的偏移量。
* **val** ( `SIMD[type, 1]`)：要存储的值。

`store(self: Self, val: SIMD[type, 1])`

存储单个元素值。

**参数：**

* **val** ( `SIMD[type, 1]`)：要存储的值。

### `simd_store`[](#simd_store)

`simd_store[width: Int](self: Self, offset: Int, val: SIMD[type, width])`

在给定偏移处存储 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **offset** ( `Int`)：要存储的偏移量。
* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

`simd_store[width: Int](self: Self, val: SIMD[type, width])`

存储 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

### `simd_nt_store`[](#simd_nt_store)

`simd_nt_store[width: Int](self: Self, offset: Int, val: SIMD[type, width])`

使用非时间存储来存储 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **offset** ( `Int`)：要存储的偏移量。
* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

`simd_nt_store[width: Int](self: Self, val: SIMD[type, width])`

使用非时间存储来存储 SIMD 向量。

地址必须正确对齐，avx512 为 64B，avx2 为 32B，avx 为 16B。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

### `simd_strided_load`[](#simd_strided_load)

`simd_strided_load[width: Int](self: Self, stride: Int) -> SIMD[type, width]`

执行 SIMD 向量的跨步加载。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **步幅**( `Int`)：负载之间的步幅。

**返回：**

跨步加载的向量。

### `simd_strided_store`[](#simd_strided_store)

`simd_strided_store[width: Int](self: Self, val: SIMD[type, width], stride: Int)`

执行 SIMD 向量的跨步存储。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。

**参数：**

* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。
* **stride** ( `Int`)：商店之间的步幅。

### `aligned_simd_store`[](#aligned_simd_store)

`aligned_simd_store[width: Int, alignment: Int](self: Self, offset: Int, val: SIMD[type, width])`

在给定偏移处存储 SIMD 向量并保证对齐。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。
* **alignment**( `Int`)：地址的最小对齐方式。

**参数：**

* **offset** ( `Int`)：要存储的偏移量。
* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

`aligned_simd_store[width: Int, alignment: Int](self: Self, val: SIMD[type, width])`

存储具有保证对齐的 SIMD 向量。

**Parameters：**

* **width**( `Int`)：SIMD 宽度。
* **alignment**( `Int`)：地址的最小对齐方式。

**参数：**

* **val** ( `SIMD[type, width]`)：要存储的 SIMD 值。

### `is_aligned`[](#is_aligned)

`is_aligned[alignment: Int](self: Self) -> Bool`

检查指针是否对齐。

**参数：**

* **alignment**( `Int`)：所需的最小对齐方式。

**返回：**

`True`如果指针至少是`alignment`对齐的，`False`否则。

### `offset`[](#offset-1)

`offset(self: Self, idx: Int) -> Self`

返回移动指定偏移量的新指针。

**参数：**

* **idx** ( `Int`)：新指针的偏移量。

**返回：**

新构造的 DTypePointer。

## `bitcast`[](#bitcast-2)

`bitcast[new_type: AnyType, src_type: AnyType](ptr: Pointer[src_type]) -> Pointer[new_type]`

将指针位广播为不同类型。

**Parameters：**

* **new\_type** ( `AnyType`)：目标类型。
* **src\_type** ( `AnyType`)：源类型。

**参数：**

* **ptr** ( `Pointer[src_type]`)：源指针。

**返回：**

具有指定类型和与原始指针相同的地址的新指针。

`bitcast[new_type: DType, src_type: DType](ptr: DTypePointer[src_type]) -> DTypePointer[new_type]`

将 DTypePointer 位转换为不同的类型。

**Parameters：**

* **new\_type** ( `DType`)：目标类型。
* **src\_type** ( `DType`)：源类型。

**参数：**

* **ptr** ( `DTypePointer[src_type]`)：源指针。

**返回：**

具有指定类型和与原始 DTypePointer 相同的地址的新 DTypePointer。

`bitcast[new_type: DType, new_width: Int, src_type: DType, src_width: Int](val: SIMD[src_type, src_width]) -> SIMD[new_type, new_width]`

将一个 SIMD 值位转换为另一个 SIMD 值。

**限制条件：**

两种类型的位宽必须相同。

**Parameters：**

* **new\_type** ( `DType`)：目标类型。
* **new\_width** ( `Int`)：目标宽度。
* **src\_type** ( `DType`)：源类型。
* **src\_width** ( `Int`)：源宽度。

**参数：**

* **val** ( `SIMD[src_type, src_width]`)：源值。

**返回：**

具有指定类型和宽度的新 SIMD 值以及源 SIMD 值的位副本。

[__记忆](https://docs.modular.com/mojo/stdlib/memory/memory.html)

[原子__](https://docs.modular.com/mojo/stdlib/os/atomic.html)

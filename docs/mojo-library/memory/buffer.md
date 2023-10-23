# buffer

实现 Buffer 类。

您可以从 `memory`包中导入这些 API。例如：

```
from memory.buffer import Buffer
```

## `Buffer`[](#buffer)

定义一个可以根据静态大小和 Dtype 进行参数化的 Buffer。

 Buffer 不拥有其底层指针。

**Parameters：**

* **size** ( `Dim`)：缓冲区的静态大小（如果已知）。
* **type** ( `DType`): Buffer 的元素类型。

**域：**

* **data** ( `DTypePointer[type]`)：数据的底层数据指针。

<!---->

* **dynamic\_size** ( `Int`)：缓冲区的动态大小。

<!---->

* **dtype** ( `DType`)：缓冲区的动态数据类型。

**函数：**

### `__init__`[](#init__)

`__init__() -> Self`

Buffer 的默认初始值设定项。默认情况下，这些字段都初始化为 0。

**返回：**

NDBuffer 对象。

`__init__(ptr: Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]) -> Self`

构造一个具有静态已知大小和类型的 Buffer。

**限制条件：**

尺寸已知。

**参数：**

* **ptr** ( `Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]`)：指向数据的指针。

**返回：**

缓冲区对象。

`__init__(ptr: DTypePointer[type]) -> Self`

构造一个具有静态已知大小和类型的 Buffer。

**限制条件：**

尺寸已知。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向数据的指针。

**返回：**

缓冲区对象。

`__init__(ptr: Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>], in_size: Int) -> Self`

构造一个具有静态已知类型的 Buffer。

**限制条件：**

尺寸未知。

**参数：**

* **ptr** ( `Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]`)：指向数据的指针。
* **in\_size** ( `Int`)：缓冲区的动态大小。

**返回：**

缓冲区对象。

`__init__(ptr: DTypePointer[type], in_size: Int) -> Self`

构造一个具有静态已知类型的 Buffer。

**限制条件：**

尺寸未知。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向数据的指针。
* **in\_size** ( `Int`)：缓冲区的动态大小。

**返回：**

缓冲区对象。

`__init__(data: DTypePointer[type], dynamic_size: Int, dtype: DType) -> Self`

### `__copyinit__`[](#copyinit__)

`__copyinit__(existing: Self) -> Self`

### `__getitem__`[](#getitem__)

`__getitem__(self: Self, idx: Int) -> SIMD[type, 1]`

从指定索引处的缓冲区加载单个元素（大小为 1 的 SIMD）。

**参数：**

* **idx** ( `Int`): Buffer 的索引。

**返回：**

该位置的值`idx`。

### `__setitem__`[](#setitem__)

`__setitem__(self: Self, idx: Int, val: scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>)`

将单个值存储到缓冲区的指定索引处。

**参数：**

* **idx** ( `Int`): Buffer 的索引。
* **val** ( `scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>`)：要存储的值。

`__setitem__(self: Self, idx: Int, val: SIMD[type, 1])`

将单个值存储到缓冲区的指定索引处。

**参数：**

* **idx** ( `Int`): Buffer 的索引。
* **val** ( `SIMD[type, 1]`)：要存储的值。

### `__len__`[](#len__)

`__len__(self: Self) -> Int`

如果它是已知常量，则获取大小，否则获取动态大小。

该方法用于`Buffer.__len__`获取缓冲区的大小。如果缓冲区大小是已知常量，则返回该大小。否则，返回dynamic\_size。

**返回：**

如果是静态大小，则为动态大小。

### `simd_load`[](#simd_load)

`simd_load[width: Int](self: Self, idx: Int) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。

**参数：**

* **idx** ( `Int`): Buffer 的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

### `aligned_simd_load`[](#aligned_simd_load)

`aligned_simd_load[width: Int, alignment: Int](self: Self, idx: Int) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `Int`): Buffer 的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

### `simd_store`[](#simd_store)

`simd_store[width: Int](self: Self, idx: Int, val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `Int`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `aligned_simd_store`[](#aligned_simd_store)

`aligned_simd_store[width: Int, alignment: Int](self: Self, idx: Int, val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `Int`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `simd_nt_store`[](#simd_nt_store)

`simd_nt_store[width: Int](self: Self, idx: Int, val: SIMD[type, width])`

使用非临时存储来存储 simd 值。

**限制条件：**

地址必须正确对齐，avx512 为 64B，avx2 为 32B，avx 为 16B。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `Int`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `prefetch`[](#prefetch)

`prefetch[params: PrefetchOptions](self: Self, idx: Int)`

预取给定索引处的数据。

**Parameters：**

* **params** ( `PrefetchOptions`): 预取配置。

**参数：**

* **idx** ( `Int`)：预取位置的索引。

### `bytecount`[](#bytecount)

`bytecount(self: Self) -> Int`

返回缓冲区的大小（以字节为单位）。

**返回：**

缓冲区的大小（以字节为单位）。

### `zero`[](#zero)

`zero(self: Self)`

将 Buffer 的所有字节设置为 0。

### `simd_fill`[](#simd_fill)

`simd_fill[simd_width: Int](self: Self, val: SIMD[type, 1])`

将 val 分配给大小为 simd\_width 的块中的所有元素。

**Parameters：**

* **simd\_width** ( `Int`)：填充的 simd\_width。

**参数：**

* **val** ( `SIMD[type, 1]`)：要存储的值。

### `fill`[](#fill)

`fill(self: Self, val: SIMD[type, 1])`

将 val 分配给 Buffer 中的所有元素。

填充以大小为 N 的块执行，其中 N 是系统上类型的本机 SIMD 宽度。

**参数：**

* **val** ( `SIMD[type, 1]`)：要存储的值。

### `write_file`[](#write_file)

`write_file(self: Self, path: Path)`

将值写入文件。

**参数：**

* **path** ( `Path`): 输出文件的路径。

### `aligned_stack_allocation`[](#aligned_stack_allocation)

`aligned_stack_allocation[alignment: Int]() -> Self`

构造一个由堆栈分配的内存空间支持的缓冲区实例。

**参数：**

* **alignment**( `Int`)：地址分配的对齐要求。

**返回：**

使用分配的空间构造缓冲区。

### `stack_allocation`[](#stack_allocation)

`stack_allocation() -> Self`

构造一个由堆栈分配的内存空间支持的缓冲区实例。

**返回：**

使用分配的空间构造缓冲区。

## `NDBuffer`[](#ndbuffer)

N 维缓冲区。

NDBuffer 可以根据等级、静态维度和 Dtype 进行参数化。它不拥有其底层指针。

**Parameters：**

* **rank**( `Int`)：缓冲区的等级。
* **shape** ( `DimList`)：缓冲区的静态大小（如果已知）。
* **type** ( `DType`)：缓冲区的元素类型。

**领域：**

* **data** ( `DTypePointer[type]`)：缓冲区的基础数据。该指针不属于 NDBuffer。

<!---->

* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：形状的动态值。

<!---->

* **Dynamic\_stride** ( `StaticIntTuple[rank]`)：缓冲区的动态步幅。

<!---->

* **is\_contigious** ( `Bool`)：如果缓冲区的内容在内存中是连续的，则为 True。

**函数：**

### `__init__`[](#init__-1)

`__init__() -> Self`

NDBuffer 的默认初始值设定项。默认情况下，这些字段都初始化为 0。

**返回：**

NDBuffer 对象。

`__init__(ptr: Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]) -> Self`

构造一个具有静态已知等级、形状和类型的 NDBuffer。

**限制条件：**

等级、形状和类型是已知的。

**参数：**

* **ptr** ( `Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]`)：指向数据的指针。

**返回：**

NDBuffer 对象。

`__init__(ptr: DTypePointer[type]) -> Self`

构造一个具有静态已知等级、形状和类型的 NDBuffer。

**限制条件：**

等级、形状和类型是已知的。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向数据的指针。

**返回：**

NDBuffer 对象。

`__init__(ptr: pointer<scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>>, dynamic_shape: StaticIntTuple[rank]) -> Self`

构造一个具有静态已知等级但动态形状和类型的 NDBuffer。

**限制条件：**

等级已知。

**参数：**

* **ptr** ( `pointer<scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>>`)：指向数据的指针。
* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：表示形状的大小为“rank”的静态元组。

**返回：**

NDBuffer 对象。

`__init__(ptr: Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>], dynamic_shape: StaticIntTuple[rank]) -> Self`

构造一个具有静态已知等级但动态形状和类型的 NDBuffer。

**限制条件：**

等级已知。

**参数：**

* **ptr** ( `Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]`)：指向数据的指针。
* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：表示形状的大小为“rank”的静态元组。

**返回：**

NDBuffer 对象。

`__init__(ptr: DTypePointer[type], dynamic_shape: StaticIntTuple[rank]) -> Self`

构造一个具有静态已知等级但动态形状和类型的 NDBuffer。

**限制条件：**

等级已知。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向数据的指针。
* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：表示形状的大小为“rank”的静态元组。

**返回：**

NDBuffer 对象。

`__init__(ptr: Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>], dynamic_shape: StaticIntTuple[rank], dynamic_stride: StaticIntTuple[rank]) -> Self`

构造一个具有静态已知等级但动态形状和类型的跨步 NDBuffer。

**限制条件：**

等级已知。

**参数：**

* **ptr** ( `Pointer[scalar<#lit.struct.extract<:!kgen.declref<_"$builtin"::_"$dtype"::_DType> type, "value">>]`)：指向数据的指针。
* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：表示形状的大小为“rank”的静态元组。
* **Dynamic\_stride** ( `StaticIntTuple[rank]`)：表示步幅的大小为“rank”的静态元组。

**返回：**

NDBuffer 对象。

`__init__(ptr: DTypePointer[type], dynamic_shape: StaticIntTuple[rank], dynamic_stride: StaticIntTuple[rank]) -> Self`

构造一个具有静态已知等级但动态形状和类型的跨步 NDBuffer。

**限制条件：**

等级已知。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向数据的指针。
* **Dynamic\_shape** ( `StaticIntTuple[rank]`)：表示形状的大小为“rank”的静态元组。
* **Dynamic\_stride** ( `StaticIntTuple[rank]`)：表示步幅的大小为“rank”的静态元组。

**返回：**

NDBuffer 对象。

`__init__(data: DTypePointer[type], dynamic_shape: StaticIntTuple[rank], dynamic_stride: StaticIntTuple[rank], is_contiguous: Bool) -> Self`

### `__getitem__`[](#getitem__-1)

`__getitem__(self: Self, *idx: Int) -> SIMD[type, 1]`

从缓冲区中指定索引处获取元素。

**参数：**

* **idx** ( `*Int`)：要检索的元素的索引。

**返回：**

元素的值。

`__getitem__(self: Self, idx: StaticIntTuple[rank]) -> SIMD[type, 1]`

从缓冲区中指定索引处获取元素。

**参数：**

* **idx** ( `StaticIntTuple[rank]`)：要检索的元素的索引。

**返回：**

元素的值。

### `__setitem__`[](#setitem__-1)

`__setitem__(self: Self, idx: StaticIntTuple[rank], val: SIMD[type, 1])`

将单个值存储到缓冲区的指定索引处。

**参数：**

* **idx** ( `StaticIntTuple[rank]`): Buffer 的索引。
* **val** ( `SIMD[type, 1]`)：要存储的值。

### `get_rank`[](#get_rank)

`get_rank(self: Self) -> Int`

返回缓冲区的排名。

**返回：**

NDBuffer 的等级。

### `get_shape`[](#get_shape)

`get_shape(self: Self) -> StaticIntTuple[rank]`

返回缓冲区的形状。

**返回：**

大小为“rank”的静态元组，表示 NDBuffer 的形状。

### `get_nd_index`[](#get_nd_index)

`get_nd_index(self: Self, idx: Int) -> StaticIntTuple[rank]`

根据平面索引计算 NDBuffer 的 ND 索引。

**参数：**

* **idx** ( `Int`)：索引。

**返回：**

索引位置。

### `__len__`[](#len__-1)

`__len__(self: Self) -> Int`

计算 NDBuffer 的元素数量。

**返回：**

NDBuffer 中的元素总数。

### `num_elements`[](#num_elements)

`num_elements(self: Self) -> Int`

计算 NDBuffer 的元素数量。

**返回：**

NDBuffer 中的元素总数。

### `size`[](#size)

`size(self: Self) -> Int`

计算 NDBuffer 的元素数量。

**返回：**

NDBuffer 中的元素总数。

### `simd_load`[](#simd_load-1)

`simd_load[width: Int](self: Self, *idx: Int) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。

**参数：**

* **idx** ( `*Int`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`simd_load[width: Int](self: Self, idx: VariadicList[Int]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。

**参数：**

* **idx** ( `VariadicList[Int]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`simd_load[width: Int](self: Self, idx: StaticIntTuple[rank]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。

**参数：**

* **idx** ( `StaticIntTuple[rank]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`simd_load[width: Int](self: Self, idx: StaticTuple[rank, Int]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。

**参数：**

* **idx** ( `StaticTuple[rank, Int]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

### `aligned_simd_load`[](#aligned_simd_load-1)

`aligned_simd_load[width: Int, alignment: Int](self: Self, *idx: Int) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `*Int`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`aligned_simd_load[width: Int, alignment: Int](self: Self, idx: VariadicList[Int]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `VariadicList[Int]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`aligned_simd_load[width: Int, alignment: Int](self: Self, idx: StaticIntTuple[rank]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `StaticIntTuple[rank]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

`aligned_simd_load[width: Int, alignment: Int](self: Self, idx: StaticTuple[rank, Int]) -> SIMD[type, width]`

从指定索引处的缓冲区加载 simd 值。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：负载的 simd\_width。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `StaticTuple[rank, Int]`)：NDBuffer 中的索引。

**返回：**

`idx`从位置开始到 结束的simd 值`idx+width`。

### `simd_store`[](#simd_store-1)

`simd_store[width: Int](self: Self, idx: StaticIntTuple[rank], val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `StaticIntTuple[rank]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

`simd_store[width: Int](self: Self, idx: StaticTuple[rank, Int], val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `StaticTuple[rank, Int]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `aligned_simd_store`[](#aligned_simd_store-1)

`aligned_simd_store[width: Int, alignment: Int](self: Self, idx: StaticIntTuple[rank], val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `StaticIntTuple[rank]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

`aligned_simd_store[width: Int, alignment: Int](self: Self, idx: StaticTuple[rank, Int], val: SIMD[type, width])`

将 simd 值存储到缓冲区的指定索引处。

**限制条件：**

缓冲区必须是连续的或宽度必须为 1。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。
* **alignment**( `Int`)：对齐值。

**参数：**

* **idx** ( `StaticTuple[rank, Int]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `simd_nt_store`[](#simd_nt_store-1)

`simd_nt_store[width: Int](self: Self, idx: StaticIntTuple[rank], val: SIMD[type, width])`

使用非临时存储来存储 simd 值。

**限制条件：**

缓冲区必须是连续的。地址必须正确对齐，avx512 为 64B，avx2 为 32B，avx 为 16B。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `StaticIntTuple[rank]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

`simd_nt_store[width: Int](self: Self, idx: StaticTuple[rank, Int], val: SIMD[type, width])`

使用非临时存储来存储 simd 值。

**限制条件：**

缓冲区必须是连续的。地址必须正确对齐，avx512 为 64B，avx2 为 32B，avx 为 16B。

**Parameters：**

* **width** ( `Int`)：simd 向量的宽度。

**参数：**

* **idx** ( `StaticTuple[rank, Int]`): Buffer 的索引。
* **val** ( `SIMD[type, width]`)：要存储的值。

### `dim`[](#dim)

`dim[index: Int](self: Self) -> Int`

获取给定索引处的缓冲区维度。

**参数：**

* **index** ( `Int`)：要获取的维度数。

**返回：**

给定维度的缓冲区大小。

`dim(self: Self, index: Int) -> Int`

获取给定索引处的缓冲区维度。

**参数：**

* **index** ( `Int`)：要获取的维度数。

**返回：**

给定维度的缓冲区大小。

### `stride`[](#stride)

`stride(self: Self, index: Int) -> Int`

获取给定索引处的缓冲区步幅。

**参数：**

* **index** ( `Int`)：要获取步幅的维度数。

**返回：**

给定维度的步幅。

### `flatten`[](#flatten)

`flatten(self: Self) -> Buffer[#pop.variant<:i1 0, 0>, type]`

构造此 NDBuffer 的展平 Buffer 对应项。

**限制条件：**

缓冲区必须是连续的。

**返回：**

构造的 Buffer 对象。

### `make_dims_unknown`[](#make_dims_unknown)

`make_dims_unknown(self: Self) -> NDBuffer[rank, create_unknown[$builtin::$int::Int][rank](), type]`

将 NDBuffer 重新绑定到形状未知的缓冲区。

**返回：**

形状未知的反弹 NDBuffer。

### `bytecount`[](#bytecount-1)

`bytecount(self: Self) -> Int`

返回 NDBuffer 的大小（以字节为单位）。

**返回：**

NDBuffer 的大小（以字节为单位）。

### `zero`[](#zero-1)

`zero(self: Self)`

将 NDBuffer 的所有字节设置为 0。

**限制条件：**

缓冲区必须是连续的。

### `simd_fill`[](#simd_fill-1)

`simd_fill[simd_width: Int](self: Self, val: SIMD[type, 1])`

将 val 分配给大小为 simd\_width 的块中的所有元素。

**Parameters：**

* **simd\_width** ( `Int`)：填充的 simd\_width。

**参数：**

* **val** ( `SIMD[type, 1]`)：要存储的值。

### `write_file`[](#write_file-1)

`write_file(self: Self, path: Path)`

将值写入文件。

**参数：**

* **path** ( `Path`): 输出文件的路径。

### `fill`[](#fill-1)

`fill(self: Self, val: SIMD[type, 1])`

将 val 分配给 Buffer 中的所有元素。

填充以大小为 N 的块执行，其中 N 是系统上类型的本机 SIMD 宽度。

**参数：**

* **val** ( `SIMD[type, 1]`)：要存储的值。

### `aligned_stack_allocation`[](#aligned_stack_allocation-1)

`aligned_stack_allocation[alignment: Int]() -> Self`

构造一个由堆栈分配的内存空间支持的 NDBuffer 实例。

**参数：**

* **alignment**( `Int`)：地址分配的对齐要求。

**返回：**

使用分配的空间构造 NDBuffer。

### `stack_allocation`[](#stack_allocation-1)

`stack_allocation() -> Self`

构造一个由堆栈分配的内存空间支持的 NDBuffer 实例。

**返回：**

使用分配的空间构造 NDBuffer。

### `prefetch`[](#prefetch-1)

`prefetch[params: PrefetchOptions](self: Self, *idx: Int)`

预取给定索引处的数据。

**Parameters：**

* **params** ( `PrefetchOptions`): 预取配置。

**参数：**

* **idx** ( `*Int`)：预取位置的ND索引。

`prefetch[params: PrefetchOptions](self: Self, indices: StaticIntTuple[rank])`

预取给定索引处的数据。

**Parameters：**

* **params** ( `PrefetchOptions`): 预取配置。

**参数：**

* **indexs** ( `StaticIntTuple[rank]`)：预取位置的ND索引。

## `DynamicRankBuffer`[](#dynamicrankbuffer)

DynamicRankBuffer 表示具有未知等级、形状和数据类型的缓冲区。

它不如静态排名缓冲区高效，但在与外部函数交互时很有用。特别是，形状被表示为固定（即 \_MAX\_RANK）维度数组以简化 ABI。

**领域：**

* **data** ( `DTypePointer[invalid]`)：指向缓冲区的指针。

<!---->

* **rank**( `Int`)：缓冲区等级。最大值为`_MAX_RANK`.

<!---->

* **shape** ( `StaticIntTuple[8]`)：缓冲区的动态形状。

<!---->

* **type** ( `DType`)：缓冲区的动态数据类型。

**函数：**

### `__init__`[](#init__-2)

`__init__(data: DTypePointer[invalid], rank: Int, shape: StaticIntTuple[8], type: DType) -> Self`

构造 DynamicRankBuffer。

**参数：**

* **data** ( `DTypePointer[invalid]`)：指向底层数据的指针。
* **rank** ( `Int`): 缓冲区的等级。
* **shape** ( `StaticIntTuple[8]`)：缓冲区的形状。
* **type** ( `DType`)：`dtype`缓冲区的类型。

**返回：**

构造了DynamicRankBuffer。

### `to_buffer`[](#to_buffer)

`to_buffer[type: DType](self: Self) -> Buffer[#pop.variant<:i1 0, 0>, type]`

将 DynamicRankBuffer 转换为 Buffer。

**参数：**

* **type** ( `DType`)：`dtype`缓冲区的类型。

**返回：**

构造的缓冲区。

### `to_ndbuffer`[](#to_ndbuffer)

`to_ndbuffer[rank: Int, type: DType](self: Self) -> NDBuffer[rank, create_unknown[$builtin::$int::Int][rank](), type]`

将缓冲区转换为 NDBuffer。

**限制条件：**

DynamicRankBuffer 的等级必须等于 NDBuffer 的等级。

**Parameters：**

* **rank** ( `Int`): 缓冲区的等级。
* **type** ( `DType`)：`dtype`缓冲区的类型。

**返回：**

构造的 NDBuffer。

`to_ndbuffer[rank: Int, type: DType](self: Self, stride: StaticIntTuple[rank]) -> NDBuffer[rank, create_unknown[$builtin::$int::Int][rank](), type]`

将缓冲区转换为 NDBuffer。

**限制条件：**

DynamicRankBuffer 的等级必须等于 NDBuffer 的等级。

**Parameters：**

* **rank** ( `Int`): 缓冲区的等级。
* **type** ( `DType`)：`dtype`缓冲区的类型。

**参数：**

* **stride** ( `StaticIntTuple[rank]`)：缓冲区的步长。

**返回：**

构造的 NDBuffer。

### `rank_dispatch`[](#rank_dispatch)

`rank_dispatch[func: fn[Int]() capturing -> None](self: Self)`

根据缓冲区等级调度函数调用。

**限制条件：**

排名必须为正且小于或等于 8。

**Parameters：**

* **func** ( `fn[Int]() capturing -> None`)：要调度的函数。该函数应该在索引参数上进行参数化，该参数将在调用该函数时用于排名。

`rank_dispatch[func: fn[Int]() capturing -> None](self: Self, out_chain: OutputChainPtr)`

根据缓冲区等级调度函数调用。

**限制条件：**

排名必须为正且小于或等于 8。

**Parameters：**

* **func** ( `fn[Int]() capturing -> None`)：要调度的函数。该函数应该在索引参数上进行参数化，该参数将在调用该函数时用于排名。

**参数：**

* **out\_chain** ( `OutputChainPtr`)：输出链。

### `num_elements`[](#num_elements-1)

`num_elements(self: Self) -> Int`

获取缓冲区中的元素数量。

**返回：**

缓冲区中的元素数量。

### `get_shape`[](#get_shape-1)

`get_shape[rank: Int](self: Self) -> StaticIntTuple[rank]`

获取表示缓冲区形状的静态元组。

**Parameters：**

* **rank** ( `Int`): 缓冲区的等级。

**返回：**

大小为“Rank”的静态元组，填充有缓冲区形状。

### `dim`[](#dim-1)

`dim(self: Self, idx: Int) -> Int`

获取给定维度。

**参数：**

* **idx** ( `Int`)：维度索引。

**返回：**

给定维度上的缓冲区大小。

## `partial_simd_load`[](#partial_simd_load)

`partial_simd_load[type: DType, width: Int](storage: DTypePointer[type], lbound: Int, rbound: Int, pad_value: SIMD[type, 1]) -> SIMD[type, width]`

加载具有动态边界的向量。

超出范围的数据将用填充值填充。如果 idx 从 0 到 (simd\_width-1) 时 lbound <= idx < rbound，则数据有效。例如：

```
addr 0  1  2  3
data x 42 43  x

partial_simd_load[4](addr0,1,3) #gives [0 42 43 0]
```

**Parameters：**

* **type** ( `DType`)：计算的基础数据类型。
* **width** ( `Int`)：系统 simd 矢量大小。

**参数：**

* **storage** ( `DTypePointer[type]`)：指向要执行加载的地址的指针。
* **lbound** ( `Int`)：simd 内有效索引的下限（含）。
* **rbound** ( `Int`)：simd 内有效索引的上限（不包含）。
* **pad\_value** ( `SIMD[type, 1]`)：为越界索引填充的值。

**返回：**

SIMD 向量已加载并用零填充。

## `partial_simd_store`[](#partial_simd_store)

`partial_simd_store[type: DType, width: Int](storage: DTypePointer[type], lbound: Int, rbound: Int, data: SIMD[type, width])`

存储具有动态边界的向量。

超出范围的数据将被忽略。如果 idx 从 0 到 (simd\_width-1) 时 lbound <= idx < rbound，则数据有效。

例如地址 0 1 2 3 数据 0 0 0 0

```
partial_simd_load[4](addr0,1,3, [-1, 42,43, -1]) #gives [0 42 43 0]
```

**Parameters：**

* **type** ( `DType`)：计算的基础数据类型。
* **width** ( `Int`)：系统 simd 矢量大小。

**参数：**

* **storage** ( `DTypePointer[type]`)：指向要执行加载的地址的指针。
* **lbound** ( `Int`)：simd 内有效索引的下限（含）。
* **rbound** ( `Int`)：simd 内有效索引的上限（不包含）。
* **data** ( `SIMD[type, width]`)：要存储的向量值。

## `prod_dims`[](#prod_dims)

`prod_dims[start_dim: Int, end_dim: Int, rank: Int, shape: DimList, type: DType](x: NDBuffer[rank, shape, type]) -> Int`

计算给定缓冲区维度的切片的乘积。

**Parameters：**

* **start\_dim** ( `Int`)：开始计算乘积的索引。
* **end\_dim** ( `Int`)：停止计算乘积的索引。
* **等级**( `Int`)：NDBuffer 的等级。
* **shape** ( `DimList`)：NDBuffer 的形状。
* **type** ( `DType`)：NDBuffer 的元素类型。

**参数：**

* **x** ( `NDBuffer[rank, shape, type]`): 其维度将被相乘的 NDBuffer。

**返回：**

缓冲区尺寸的指定切片的乘积。

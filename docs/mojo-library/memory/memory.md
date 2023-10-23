# memory

定义内存操作的函数。

您可以从 `memory`包中导入这些 API。例如：

```
from memory import memcmp
```

## `memcmp`[](#memcmp)

`memcmp[type: DType](s1: DTypePointer[type], s2: DTypePointer[type], count: Int) -> Int`

比较两个缓冲区。假定两个字符串的长度相同。

**Parameters：**

* **type** ( `DType`)：元素数据类型。

**参数：**

* **s1** ( `DTypePointer[type]`)：第一个缓冲区地址。
* **s2** ( `DTypePointer[type]`)：第二个缓冲区地址。
* **count** ( `Int`)：缓冲区中元素的数量。

**返回：**

如果字节缓冲区相同，则返回 0；如果 s1 > s2，则返回 1；如果 s1 < s2，则返回 -1。比较是通过缓冲区中的第一个不同字节来执行的。

`memcmp[type: AnyType](s1: Pointer[*"type"], s2: Pointer[*"type"], count: Int) -> Int`

比较两个缓冲区。假定两个字符串的长度相同。

**Parameters：**

* **type** ( `AnyType`)：元素类型。

**参数：**

* **s1** ( `Pointer[*"type"]`)：第一个缓冲区地址。
* **s2** ( `Pointer[*"type"]`)：第二个缓冲区地址。
* **count** ( `Int`)：缓冲区中元素的数量。

**返回：**

如果字节字符串相同，则返回 0；如果 s1 > s2，则返回 1；如果 s1 < s2，则返回 -1。比较是通过字节字符串中的第一个不同字节来执行的。

## `memcpy`[](#memcpy)

`memcpy[type: AnyType](dest: Pointer[*"type"], src: Pointer[*"type"], count: Int)`

复制内存区域。

**Parameters：**

* **type** ( `AnyType`)：元素类型。

**参数：**

* **dest** ( `Pointer[*"type"]`)：目标指针。
* **src** ( `Pointer[*"type"]`)：源指针。
* **count** ( `Int`)：要复制的元素数量。

`memcpy[type: DType](dest: DTypePointer[type], src: DTypePointer[type], count: Int)`

复制内存区域。

**Parameters：**

* **type** ( `DType`)：元素数据类型。

**参数：**

* **dest** ( `DTypePointer[type]`)：目标指针。
* **src** ( `DTypePointer[type]`)：源指针。
* **count** ( `Int`)：要复制的元素数量（不是字节！）。

`memcpy[type: DType, size: Dim](dest: Buffer[size, type], src: Buffer[size, type])`

将内存缓冲区从 复制`src`到`dest`。

**Parameters：**

* **type** ( `DType`)：元素数据类型。
* **size** ( `Dim`)：缓冲区中元素的数量。

**参数：**

* **dest** ( `Buffer[size, type]`)：目标缓冲区。
* **src** ( `Buffer[size, type]`): 源缓冲区。

## `memset`[](#memset)

`memset[type: DType](ptr: DTypePointer[type], value: SIMD[ui8, 1], count: Int)`

用给定值填充内存。

**Parameters：**

* **type** ( `DType`)：元素数据类型。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向要填充的内存块开头的指针。
* **value** ( `SIMD[ui8, 1]`)：要填充的值。
* **count** ( `Int`)：要填充的元素数（以元素为单位，而不是字节）。

## `memset_zero`[](#memset_zero)

`memset_zero[type: DType](ptr: DTypePointer[type], count: Int)`

用零填充内存。

**Parameters：**

* **type** ( `DType`)：元素数据类型。

**参数：**

* **ptr** ( `DTypePointer[type]`)：指向要填充的内存块开头的指针。
* **count** ( `Int`)：要设置的元素数量（以元素为单位，而不是字节）。

`memset_zero[type: AnyType](ptr: Pointer[*"type"], count: Int)`

用零填充内存。

**Parameters：**

* **type** ( `AnyType`)：元素类型。

**参数：**

* **ptr** ( `Pointer[*"type"]`)：指向要填充的内存块开头的指针。
* **count** ( `Int`)：要填充的元素数（以元素为单位，而不是字节）。

## `stack_allocation`[](#stack_allocation)

`stack_allocation[count: Int, type: DType]() -> DTypePointer[type]`

在给定数据类型和元素数量的情况下在堆栈上分配数据缓冲区空间。

**参数：**

* **count** ( `Int`)：要为其分配内存的元素数量。
* **type** ( `DType`)：每个元素的数据类型。

**返回：**

指向分配空间的给定类型的数据指针。

`stack_allocation[count: Int, type: DType, alignment: Int]() -> DTypePointer[type]`

在给定数据类型和元素数量的情况下在堆栈上分配数据缓冲区空间。

**参数：**

* **count** ( `Int`)：要为其分配内存的元素数量。
* **type** ( `DType`)：每个元素的数据类型。
* **alignment** ( `Int`)：分配数据的地址对齐。

**返回：**

指向分配空间的给定类型的数据指针。

`stack_allocation[count: Int, type: AnyType]() -> Pointer[*"type"]`

在给定数据类型和元素数量的情况下在堆栈上分配数据缓冲区空间。

**参数：**

* **count** ( `Int`)：要为其分配内存的元素数量。
* **type** ( `AnyType`)：每个元素的数据类型。

**返回：**

指向分配空间的给定类型的数据指针。

`stack_allocation[count: Int, type: AnyType, alignment: Int]() -> Pointer[*"type"]`

在给定数据类型和元素数量的情况下在堆栈上分配数据缓冲区空间。

**参数：**

* **count** ( `Int`)：要为其分配内存的元素数量。
* **type** ( `AnyType`)：每个元素的数据类型。
* **alignment** ( `Int`)：分配数据的地址对齐。

**返回：**

指向分配空间的给定类型的数据指针。

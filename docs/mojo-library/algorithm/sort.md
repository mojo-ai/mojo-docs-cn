# sort

实现排序函数。

你可以从 `algorithm` 包中导入这些 API。例如：

```python
from algorithm.sort import sort
```

## `partition`

```python
partition[type: AnyType, cmp_fn: fn[AnyType]($0, $0) capturing -> Bool](buff: Pointer[*"type"], k: Int, size: Int)
```

就地分割输入向量，使前 k 个元素成为最大的（如果 cmp_fn 是 <= 运算符，则为最小的）元素。

前 k 个元素的顺序是未定义的。

**Parameters**：

- **type** (`AnyType`)：底层数据的数据类型。

- **cmp_fn** (`fn[AnyType]($0, $0) capturing -> Bool`)：比较函数

**Args**：

- **buff** (`Pointer[*"type"]`)：输入缓存区。

- **k** (`Int`)：分区元素的索引。

- **size** (`Int`)：缓存区的长度。

## `sort`

```python
sort(inout buff: Pointer[Int], len: Int)
```

对向量进行排序。

该函数不返回任何内容，向量在原地更新。

**Args**：

- **buff** (`Pointer[Int]`)：输入缓冲区。

- **len** (`Int`)：缓冲区的长度。

```python
sort[type: DType](inout buff: Pointer[SIMD[type, 1]], len: Int)
```

对向量进行排序。

该函数不返回任何内容，向量在原地更新。

**Parameters**：

- **type** (`DType`)：底层数据的数据类型。

**Args**：

- **buff** (`Pointer[SIMD[type, 1]]`)：输入缓冲区。

- **len** (`Int`)：缓冲区的长度。

```python
sort(inout v: DynamicVector[Int])
```

对向量进行排序。

该函数不返回任何内容，向量在原地更新。

**Args**：

- **v** (`DynamicVector[Int]`)：输入，要排序的整数向量。

```python
sort[type: DType](inout v: DynamicVector[SIMD[type, 1]])
```

对向量进行排序。

该函数不返回任何内容，向量在原地更新。

**Parameters**：

- **type** (`DType`)：底层数据的数据类型。

**Args**：

- **v** (`DynamicVector[SIMD[type, 1]]`)：输入，要排序的整数向量。

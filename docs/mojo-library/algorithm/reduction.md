# reduction

实现 SIMD 归约。

你可以从 algorithm 包中导入这些 API。例如：

```python
from algorithm import map_reduce
```

## `map_reduce`

```python
map_reduce[simd_width: Int, size: Dim, type: DType, acc_type: DType, input_gen_fn: fn[DType, Int](Int) capturing -> SIMD[*(0,0), *(0,1)], reduce_vec_to_vec_fn: fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)], reduce_vec_to_scalar_fn: fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]](dst: Buffer[size, type], init: SIMD[acc_type, 1]) -> SIMD[acc_type, 1]
```

将调用 input_gen_fn 的结果存储在 dst 中，并同时使用自定义的归约函数对结果进行归约操作。

**Parameters**：

- **simd_width** (`Int`)：计算的向量宽度。

- **size** (`Dim`)：buffer 大小。
  
- **type** (`DType`)：buffer 元素的数据类型。

- **acc_type** (`DType`)：归约累加器的数据类型。

- **input_gen_fn** (`fn[DType, Int](Int) capturing -> SIMD[*(0,0), *(0,1)]`)：一个生成输入以进行归约操作的函数。

- **reduce_vec_to_vec_fn** (`fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)]`)：一个映射函数，用于将两个输入数据块组合（累加）起来。例如：将两个 8 x float32 的向量归约为一个 8 x float32 的向量。

- **reduce_vec_to_scalar_fn** (`fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]`)：一个归约函数，用于将一个向量归约为一个标量。 例如：将一个 8 x float32 的向量归约为一个 float32 的标量。

**Args**：

- **dst** (`Buffer[size, type]`)：输出 buffer。

- **init** (`SIMD[acc_type, 1]`)：在累加器中使用的初始值。

**Returns**：

计算得到的归约值。

## `reduce`

```python
reduce[simd_width: Int, size: Dim, type: DType, acc_type: DType, map_fn: fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)], reduce_fn: fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]](src: Buffer[size, type], init: SIMD[acc_type, 1]) -> SIMD[acc_type, 1]
```

计算缓冲区元素的自定义归约。

**Parameters**：

- **simd_width** (`Int`)：计算的向量宽度。

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

- **acc_type** (`DType`)：归约累加器的数据类型。

- **map_fn** (`fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)]`)：一个映射函数，用于将两个输入数据块组合（累加）在一起使用。例如：将两个 8 x float32 的向量归约为一个单独的 8 x float32 的向量。

- **reduce_fn** (`fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]`)：一个归约函数，用于将一个向量归约为一个标量。 例如：将一个 8 x float32 的向量归约为一个 1 x float32 的标量。
  
**Args**：

- **src** (`Buffer[size, type]`)：输入 buffer。

- **init** (`SIMD[acc_type, 1]`)：在累加器中使用的初始值。

**Returns**：

计算得到的归约值。

```python
reduce[simd_width: Int, rank: Int, input_shape: DimList, output_shape: DimList, type: DType, acc_type: DType, map_fn: fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)], reduce_fn: fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1], reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, acc_type], init: SIMD[acc_type, 1])
```

执行对 NDBuffer（src）的 reduce_axis 进行归约，并将结果存储在 NDBuffer（dst）中。

首先，将 src 重塑为一个 3D 张量。不失一般性，三个轴将被称为 [H, W, C]，其中要归约的轴是 W，归约之前的轴被打包到 H 中，归约之后的轴被打包到 C 中。即在轴 i 上减少的维度为 [D1, D2, …, Di, …, Dn] 的张量被打包成一个维度为 [H, W, C] 的 3D 张量，其中 H=prod(D1, …, Di-1), W=Di, C=prod(Di+1, …, Dn)。

**Parameters**：

- **simd_width** (`Int`)：计算的向量宽度。

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **acc_type** (`DType`)：归约累加器的数据类型。

- **map_fn** (`fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)]`)：一个映射函数，用于将两个输入数据块组合（累加）在一起使用。例如：将两个 8 x float32 的向量归约为一个单独的 8 x float32 的向量。

- **reduce_fn** (`fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]`)：一个归约函数，用于将一个向量归约为一个标量。 例如：将一个 8 x float32 的向量归约为一个 1 x float32 的标量。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**：

- **src** (`NDBuffer[rank, input_shape, type]`)：输入 buffer。

- **dst** (`NDBuffer[rank, output_shape, acc_type]`)：输出 buffer。

- **init** (`SIMD[acc_type, 1]`)：在累加器中使用的初始值。

## `reduce_boolean`

```python
reduce_boolean[simd_width: Int, size: Dim, type: DType, reduce_fn: fn[DType, Int](SIMD[*(0,0), *(0,1)]) capturing -> Bool, continue_fn: fn(Bool) capturing -> Bool](src: Buffer[size, type], init: Bool) -> Bool
```

计算缓冲区元素的布尔归约。
 
如果 continue_fn 返回 False，则归约操作提前退出。

**Parameters**：

- **simd_width** (`Int`)：计算的向量宽度。

- **size** (`Dim`)：buffer 大小。
  
- **type** (`DType`)：buffer 元素的数据类型。
  
- **reduce_fn** (`fn[DType, Int](SIMD[*(0,0), *(0,1)]) capturing -> Bool`)：一个布尔归约函数，用于将向量归约为标量。例如：将一个 8 x float32 向量归约为布尔值。

- **continue_fn** (`fn(Bool) capturing -> Bool`)：一个用于指示是否继续处理剩余迭代的函数，这个函数接收 reduce_fn 的结果，返回 True 则继续处理，返回 False 则提前退出。

**Args**：

- **src** (`Buffer[size, type]`)：输入buffer。

- **init** (`Bool`): 要使用的初始值。

**Returns**：

计算得到的归约值。

## `max`

```python
max[size: Dim, type: DType](src: Buffer[size, type]) -> SIMD[type, 1]
```

计算缓冲区中最大的元素。

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区中最大的元素。

```python
max[rank: Int, input_shape: DimList, output_shape: DimList, type: DType, reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, type])
```

计算 NDBuffer 在 reduce_axis 轴上的最大值。

**Parameters**：

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**:

- **src** (`NDBuffer[rank, input_shape, type]`)：The input buffer.
- **dst** (`NDBuffer[rank, output_shape, type]`)：The output buffer.

## `min`

```python
min[size: Dim, type: DType](src: Buffer[size, type]) -> SIMD[type, 1]
```

计算缓冲区中最小的元素。

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区中最小的元素。

```python
min[rank: Int, input_shape: DimList, output_shape: DimList, type: DType, reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, type])
```

计算 NDBuffer 在 reduce_axis 轴上的最小值。

**Parameters**：

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**：

- **src** (`NDBuffer[rank, input_shape, type]`)：输入 buffer。

- **dst** (`NDBuffer[rank, output_shape, type]`)：输出 buffer。

## `sum`

```python
sum[size: Dim, type: DType](src: Buffer[size, type]) -> SIMD[type, 1]
```

计算缓冲区元素的和。

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区元素的和。

示例：

```python
from algorithm import sum
from memory.buffer import Buffer

fn main():
    alias numElem = 10

    # allocate a buffer, use stackalloc 
    # var A = Buffer[size, DType.float32].stack_allocation()
    # allocate a buffer, use heapalloc
    var B = DTypePointer[DType.float32].alloc(numElem)
    var A = Buffer[numElem, DType.float32](B)

    # initialize buffer
    for i in range(numElem):
       A[i] = Float32(i)
       # print(A[i])
    
    var mySum: Float32 = 0.0
    mySum = sum[numElem, DType.float32](A)
    
    print("sum = ", mySum)

main()
```

> sum =  45.0

```python
sum[rank: Int, input_shape: DimList, output_shape: DimList, type: DType, reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, type])
```

计算 NDBuffer 在 reduce_axis 轴上的和。

**Parameters**：

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**：

- **src** (`NDBuffer[rank, input_shape, type]`)：输入 buffer。

- **dst** (`NDBuffer[rank, output_shape, type]`)：输出 buffer。

## `product`

```python
product[size: Dim, type: DType](src: Buffer[size, type]) -> SIMD[type, 1]
```

计算缓冲区元素的乘积。

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**:

- **src** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区元素的乘积。

```python
product[rank: Int, input_shape: DimList, output_shape: DimList, type: DType, reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, type])
```

计算 NDBuffer 在 reduce_axis 轴上的乘积。

**Parameters**：

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**：

- **src** (`NDBuffer[rank, input_shape, type]`)：输入 buffer。

- **dst** (`NDBuffer[rank, output_shape, type]`)：输出 buffer。

## `mean`

```python
mean[size: Dim, type: DType](src: Buffer[size, type]) -> SIMD[type, 1]
```

计算缓冲区元素的平均值。

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

**Returns**：

缓冲区元素的平均值。

```python
mean[rank: Int, input_shape: DimList, output_shape: DimList, type: DType, reduce_axis: Int](src: NDBuffer[rank, input_shape, type], dst: NDBuffer[rank, output_shape, type])
```

计算 NDBuffer 在 reduce_axis 轴上的平均值。

**Parameters**：

- **rank** (`Int`)：输入/输出 buffers 的 rank。

- **input_shape** (`DimList`)：输入 buffer 维度。

- **output_shape** (`DimList`)：输出 buffer 维度。

- **type** (`DType`)：buffer 元素的数据类型。

- **reduce_axis** (`Int`)：要归约的坐标轴。

**Args**：

- **src** (`NDBuffer[rank, input_shape, type]`)：输入 buffer。

- **dst** (`NDBuffer[rank, output_shape, type]`)：输出 buffer。

## `variance`

```python
variance[size: Dim, type: DType](src: Buffer[size, type], mean_value: SIMD[type, 1], correction: Int) -> SIMD[type, 1]
```

 给定均值，计算缓冲区中元素的方差。

均值用于避免对数据进行第二次遍历：

`variance(src) = sum((x - E(x))^2) / (size - correction)`

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

- **mean_value** (`SIMD[type, 1]`)：缓冲区元素的平均值。

- **correction** (`Int`)：修正（修正方差的因子，默认为1）。

**Returns**:

缓冲区中元素的方差。

```python
variance[size: Dim, type: DType](src: Buffer[size, type], correction: Int) -> SIMD[type, 1]
```

计算缓冲区中元素的方差。

`variance(src) = sum((x - E(x))^2) / (size - correction)`

**Parameters**：

- **size** (`Dim`)：buffer 大小。

- **type** (`DType`)：buffer 元素的数据类型。

**Args**：

- **src** (`Buffer[size, type]`)：缓冲区。

- **correction** (`Int`)：修正（修正方差的因子，默认为1）。

**Returns**：

缓冲区中元素的方差。


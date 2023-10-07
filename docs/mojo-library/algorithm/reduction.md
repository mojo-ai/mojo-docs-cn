# reduction

实现 SIMD 归约。

你可以从 algorithm 包中导入这些API。例如：

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

- **size** (`Dim`)：buffer大小。
  
- **type** (`DType`)：buffer元素的数据类型。

- **acc_type** (`DType`)：归约累加器的数据类型。

- **input_gen_fn** (`fn[DType, Int](Int) capturing -> SIMD[*(0,0), *(0,1)]`)：一个生成输入以进行归约操作的函数。

- **reduce_vec_to_vec_fn** (`fn[DType, DType, Int](SIMD[*(0,0), *(0,2)], SIMD[*(0,1), *(0,2)]) capturing -> SIMD[*(0,0), *(0,2)]`)：一个映射函数，用于将两个输入数据块组合（累加）起来。 例如：将两个 8xfloat32 的向量归约为一个 8xfloat32 的向量。

- **reduce_vec_to_scalar_fn** (`fn[DType, Int](SIMD[*(0,0), *(0,1)]) -> SIMD[*(0,0), 1]`)：一个归约函数，用于将一个向量归约为一个标量。 例如：将一个 8xfloat32 的向量归约为一个 float32 的标量。

**Args**：

- **dst** (`Buffer[size, type]`)：输出buffer。

- **init** (`SIMD[acc_type, 1]`)：在累加器中使用的初始值。

**Returns**:

计算得到的归约值。

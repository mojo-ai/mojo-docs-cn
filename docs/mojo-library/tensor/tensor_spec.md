# tensor_spec

实现 `TensorSpec` 类型。

您可以从 `tensor`（张量）包中导入这些 API。例如：

```python
from tensor import TensorSpec
```

## `TensorSpec`

张量形状和 dtype 的空间高效表示。此结构体实现值语义并拥有其基础数据。

**Fields**：

- **shape** (`TensorShape`)：规范的基础形状。
  

# testing

用于各类测试的基础工具集（包）。

您可以从 `testing` 包中导入以下 API。例如：

```python
from testing import assert_true
```

## `assert_true`

```python
assert_true(val: Bool, msg: String) -> Bool
```

断言期望值为 True。若不是 True，则打印一条包含输入内容的消息。

**Args**：

- **val** (`Bool`)：期望为 True 的值。
- **msg** (`String`)：断言失败时打印的消息。

**Returns**：

若断言成功，则为 True，否则为 False。

## `assert_false`

```python
assert_false(val: Bool, msg: String) -> Bool
```

断言期望值为 False。若不是 False，则打印一条包含输入内容的消息。

**Args**：

- **val** (`Bool`)：期望为 False 的值。
- **msg** (`String`)：断言失败时打印的消息。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_false(val: Bool) -> Bool
```

断言期望值为 False。若不是 False，则打印一条包含输入内容的消息。

**Args**：

- **val** (`Bool`)：期望为 False 的值。

**Returns**：

若断言成功，则为 True，否则为 False。

## `assert_equal`

```python
assert_equal(lhs: Int, rhs: Int) -> Bool
```

断言期望 `lhs` 与 `rhs` 相等。若不相等，则打印一条包含输入内容的消息。

**Args**：

- **lhs** (`Int`)：输入 lhs。
- **rhs** (`Int`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_equal(lhs: String, rhs: String) -> Bool
```

断言期望 `lhs` 与 `rhs` 相等。若不相等，则打印一条包含输入内容的消息。

**Args**：

- **lhs** (`String`)：输入 lhs。
- **rhs** (`String`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_equal[type: DType, size: Int](lhs: SIMD[type, size], rhs: SIMD[type, size]) -> Bool
```

断言期望 `lhs` 与 `rhs` 相等。若不相等，则打印一条包含输入内容的消息。

**Parameters**：

- **type** (`DType`)：左右两侧 SIMD 矢量的 dtype。
- **size** (`Int`)：左右两侧 SIMD 矢量的宽度。

**Args**：

- **lhs** (`SIMD[type, size]`)：输入 lhs。
- **rhs** (`SIMD[type, size]`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

## `assert_not_equal`

```python
assert_not_equal(lhs: Int, rhs: Int) -> Bool
```

断言期望 `lhs` 和 `rhs` 不相等。若相等，则打印一条包含输入内容的消息。

**Args**：

- **lhs** (`Int`)：输入 lhs。
- **rhs** (`Int`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_not_equal(lhs: String, rhs: String) -> Bool
```

断言期望 `lhs` 和 `rhs` 不相等。若相等，则打印一条包含输入内容的消息。

**Args**：

- **lhs** (`String`)：输入 lhs。
- **rhs** (`String`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_not_equal[type: DType, size: Int](lhs: SIMD[type, size], rhs: SIMD[type, size]) -> Bool
```

断言期望 `lhs` 和 `rhs` 不相等。若相等，则打印一条包含输入内容的消息。

**Parameters**：

- **type** (`DType`)：左右两侧 SIMD 矢量的 dtype。
- **size** (`Int`)：左右两侧 SIMD 矢量的宽度。

**Args**：

- **lhs** (`SIMD[type, size]`)：输入 lhs。
- **rhs** (`SIMD[type, size]`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

## `assert_almost_equal`

```python
assert_almost_equal[type: DType, size: Int](lhs: SIMD[type, size], rhs: SIMD[type, size]) -> Bool
```

断言期望输入值等于 `tolerance`（容差）。若不相等，则打印一条包含输入内容的消息。

**Parameters**：

- **type** (`DType`)：左右两侧 SIMD 矢量的 dtype。
- **size** (`Int`)：左右两侧 SIMD 矢量的宽度。

**Args**：

- **lhs** (`SIMD[type, size]`)：输入 lhs。
- **rhs** (`SIMD[type, size]`)：输入 rhs。

**Returns**：

若断言成功，则为 True，否则为 False。

```python
assert_almost_equal[type: DType, size: Int](lhs: SIMD[type, size], rhs: SIMD[type, size], absolute_tolerance: SIMD[type, 1], relative_tolerance: SIMD[type, 1]) -> Bool
```

断言期望输入值等于 `tolerance`（容差）。若不相等，则打印一条包含输入内容的消息。

**Parameters**：

- **type** (`DType`)：左右两侧 SIMD 矢量的 dtype。
- **size** (`Int`)：左右两侧 SIMD 矢量的宽度。

**Args**：

- **lhs** (`SIMD[type, size]`)：输入 lhs。
- **rhs** (`SIMD[type, size]`)：输入 rhs。
- **absolute_tolerance** (`SIMD[type, 1]`)：`tolerance` 绝对值。
- **relative_tolerance** (`SIMD[type, 1]`)：`tolerance` 相对值。

**Returns**：

若断言成功，则为 True，否则为 False。

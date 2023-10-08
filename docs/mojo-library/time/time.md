# time

用于时间处理的基础工具集（包）。

您可以从 `time` 包中导入以下 API。例如：

```python
from time import now
```

## `now`

```python
now() -> Int
```

返回当前单调时间（ns 为单位）。此函数查询当前平台的单调时钟，使其可用于时差测量，但是返回值因依赖系统底层实现而存在差异性。

**Returns**：

以 ns 为单位的当前时间。

## `time_function`

```python
time_function[func: fn() capturing -> None]() -> Int
```

测量函数执行的耗时。

**Parameters**：

- **func** (`fn() capturing -> None`)：计时功能。

**Returns**：

函数执行的耗时（ns 为单位）。

## `sleep`

```python
sleep(sec: SIMD[f64, 1])
```

设定当前线程挂起的秒数。

**Args**：

- **sec** (`SIMD[f64, 1]`)：休眠的秒数。

```python
sleep(sec: Int)
```

设定当前线程挂起的秒数。

**Args**：

- **sec** (`Int`)：休眠的秒数。

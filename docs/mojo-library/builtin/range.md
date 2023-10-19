# range

实现区间（range）调用。

这些为 Mojo 内置，因此您无需导入它们。

## `range`

```python
range(end: Int) -> _ZeroStartingRange
```

构造 [0; end) 区间。

**Args**：

- **end** (`Int`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(end: PythonObject) -> _ZeroStartingRange
```

构造 [0; end) 区间。

**Args**：

- **end** (`PythonObject`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(length: object) -> _ZeroStartingRange
```

构造 [0; length) 区间。

**Args**：

- **length** (`object`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(start: Int, end: Int) -> _SequentialRange
```

构造 [start; end) 区间。

**Args**：

- **start** (`Int`)：区间的起始。
- **end** (`Int`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(start: object, end: object) -> _SequentialRange
```

构造 [start; end) 区间。

**Args**：

- **start** (`object`)：区间的起始。
- **end** (`object`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(start: PythonObject, end: PythonObject) -> _SequentialRange
```

构造 [start; end) 区间。

**Args**：

- **start** (`PythonObject`)：区间的起始。
- **end** (`PythonObject`)：区间的末端（长度）。

**Returns**：

构造的区间。

```python
range(start: Int, end: Int, step: Int) -> _StridedRange
```

构造具有给定步长的 [start; end) 区间。

**Args**：

- **start** (`Int`)：区间的起始。
- **end** (`Int`)：区间的末端（长度）。
- **step** (`Int`)：区间的步长。

**Returns**：

构造的区间。

```python
range(start: object, end: object, step: object) -> _StridedRange
```

构造具有给定步长的 [start; end) 区间。

**Args**：

- **start** (`object`)：区间的起始。
- **end** (`object`)：区间的末端（长度）。
- **step** (`object`)：区间的步长。

**Returns**：

构造的区间。

```python
range(start: PythonObject, end: PythonObject, step: PythonObject) -> _StridedRange
```

构造具有给定步长的 [start; end) 区间。

**Args**：

- **start** (`PythonObject`)：区间的起始。
- **end** (`PythonObject`)：区间的末端（长度）。
- **step** (`PythonObject`)：区间的步长。

**Returns**：

构造的区间。

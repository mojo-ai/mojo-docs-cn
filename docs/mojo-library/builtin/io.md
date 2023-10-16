# io

处理输入/输出的工具集。

这些均为 Mojo 内置，因此您无需导入它们。

## `put_new_line`

```python
put_new_line()
```

打印换行符。

## `print`

```python
print()
```

打印换行符。

```python
print(t: DType)
```

打印 DType。

**Args**：

- **t** (`DType`)：要打印的 DType。

```python
print(x: String)
```

打印字符串。

**Args**：

- **x** (`String`)：要打印的字符串。

```python
print(x: StringRef)
```

打印字符串。

**Args**：

- **x** (`StringRef`)：要打印的字符串。

```python
print(x: StringLiteral)
```

打印字符串。

**Args**：

- **x** (`StringLiteral`)：要打印的字符串。

```python
print(x: Bool)
```

打印布尔值。

**Args**：

- **x** (`Bool`)：要打印的值。

```python
print(x: FloatLiteral)
```

打印浮点数。

**Args**：

- **x** (`FloatLiteral`)：要打印的值。

```python
print(x: FloatLiteral)
```

打印浮点数。

**Args**：

- **x** (`FloatLiteral`)：要打印的值。

```python
print(x: Int)
```

打印整型数。

**Args**：

- **x** (`Int`)：要打印的值。

```python
print[simd_width: Int, type: DType](vec: SIMD[type, simd_width])
```

打印 SIMD 数。

**Parameters**：

- **simd_width** (`Int`)：SIMD 矢量宽度。
- **type** (`DType`)：值的 DType。

**Args**：

- **vec** (`SIMD[type, simd_width]`)：要打印的 SIMD 值。

```python
print[simd_width: Int, type: DType](vec: ComplexSIMD[type, simd_width])
```

打印 SIMD 数。

**Parameters**：

- **simd_width** (`Int`)：SIMD 矢量宽度。
- **type** (`DType`)：值的 DType。

**Args**：

- **vec** (`ComplexSIMD[type, simd_width]`)：要打印的 complex 值。

```python
print[type: DType](x: Atomic[type])
```

打印原子值。

**Parameters**：

- **type** (`DType`)：原子值的 DType。

**Args**：

- **x** (`Atomic[type]`)：要打印的值。

```python
print[length: Int](shape: DimList)
```

打印 DimList 对象。

**Parameters**：

- **length** (`Int`)：DimList 长度。

**Args**：

- **shape** (`DimList`)：要打印的 DimList 对象。

```python
print(obj: object)
```

打印对象。

**Args**：

- **obj** (`object`)：要打印的对象。

```python
print(err: Error)
```

打印 Error 类型。

**Args**：

- **err** (`Error`)：要打印的 Error 类型。

```python
print(*elements: _Printable)
```

打印一系列元素（采用空格连接，后跟换行符）。

**Args**：

- **elements** (`*_Printable`)：要打印的元素。

## `print_no_newline`

```python
print_no_newline(*elements: _Printable)
```

打印由空格连接的元素序列。

**Args**：

- **elements** (`*_Printable`)：要打印的元素。

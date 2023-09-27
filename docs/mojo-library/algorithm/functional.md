# functional

实现高阶函数。

你可以从 `algorithm` 包中导入这些API。例如：

```python
from algorithm import map
```

## 别名（Aliases）：

- `Static1DTileUnitFunc = fn[Int](Int) capturing -> None`：一个 1D 平铺函数（tiled function）的签名，它使用固定的平铺大小和偏移量执行某些工作。例如：func<tile_size: Int> (offset: Int)

- `Dynamic1DTileUnitFunc = fn(Int, Int) capturing -> None`：一个 1D 平铺函数（tiled function）的签名，它使用动态的平铺大小和偏移量执行某些工作。例如：func(offset: Int, tile_size: Int)

- `BinaryTile1DTileUnitFunc = fn[Int](Int, Int) capturing -> None`：一个平铺函数（tiled function）的签名，它使用动态的平铺大小和一个次要的静态平铺大小来执行一些工作。

- `Static2DTileUnitFunc = fn[Int, Int](Int, Int) capturing -> None`：一个2D 平铺函数（tiled function）的签名，它使用静态的平铺大小和偏移量来执行某些工作。例如：func<tile_size_x: Int, tile_size_y: Int> (offset_x: Int, offset_y: Int)

- `SwitchedFunction = fn[Bool]() capturing -> None`

- `SwitchedFunction2 = fn[Bool, Bool]() capturing -> None`

- `Static1DTileUnswitchUnitFunc = fn[Int, Bool](Int, Int) capturing -> None`：一个平铺函数（tiled function）的签名，它使用静态的平铺大小和偏移量来执行某些工作。例如：func<tile_size: Int> (offset: Int)

- `Dynamic1DTileUnswitchUnitFunc = fn[Bool](Int, Int, Int) capturing -> None`

## `map`

```python
map[func: fn(Int) capturing -> None](size: Int)
```

将一个函数映射到从0到size的范围上。

**Parameters**：

- **func**（`fn(Int) capturing -> None`）: 映射函数。

**Args**：

- **size**（`Int`）: 元素的数量。

## `unroll`

```python
unroll[count: Int, func: fn[Int]() capturing -> None]()
```

重复计算一个函数 count 次。

**Parameters**：

- **count**（`Int`）：重复次数。

- **func**（`fn[Int]() capturing -> None`）：要计算的函数。该函数应该接受一个整数参数。

```python
unroll[dim0: Int, dim1: Int, func: fn[Int, Int]() capturing -> None]()
```


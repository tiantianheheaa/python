在 Python 中，**迭代器（Iterator）** 和 **`yield`** 是用于处理可迭代对象和生成器的重要概念。它们允许你高效地处理大量数据或无限序列，而无需一次性将所有数据加载到内存中。

### 迭代器（Iterator）

#### 定义

- **迭代器** 是一个对象，它实现了迭代器协议，即定义了 `__iter__()` 和 `__next__()` 方法。
- `__iter__()` 方法返回迭代器对象本身。
- `__next__()` 方法返回下一个值，如果没有更多值可返回，则抛出 `StopIteration` 异常。

#### 特点

- 迭代器是惰性计算的，即只在需要时生成下一个值。
- 迭代器只能迭代一次，遍历完成后无法再次使用。

#### 示例

```python
class MyIterator:
    def __init__(self, max_value):
        self.max_value = max_value
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.max_value:
            self.current += 1
            return self.current
        else:
            raise StopIteration

# 使用迭代器
my_iterator = MyIterator(3)
for item in my_iterator:
    print(item)
```

输出：
```
1
2
3
```

### `yield`

#### 定义

- **`yield`** 关键字用于定义生成器函数。生成器函数在被调用时返回一个生成器对象，而不是立即执行函数体。
- 生成器对象是一个迭代器，支持迭代器协议。

#### 特点

- `yield` 语句暂停函数的执行，并返回一个值给调用者。
- 每次调用生成器的 `__next__()` 方法时，函数从上次暂停的地方继续执行，直到遇到下一个 `yield` 语句或函数结束。
- 生成器是惰性计算的，可以节省内存，因为它们不会一次性生成所有值。

#### 示例

```python
def my_generator(max_value):
    current = 0
    while current < max_value:
        current += 1
        yield current

# 使用生成器
gen = my_generator(3)
for item in gen:
    print(item)
```

输出：
```
1
2
3
```

### 迭代器与生成器的关系

- **生成器** 是一种特殊的迭代器，通过 `yield` 关键字实现。
- 生成器函数在被调用时返回一个生成器对象，该对象实现了迭代器协议。
- 生成器提供了更简洁的语法来创建迭代器，而不需要手动实现 `__iter__()` 和 `__next__()` 方法。

### 总结

- **迭代器** 是一个实现了 `__iter__()` 和 `__next__()` 方法的对象，用于遍历集合中的元素。
- **`yield`** 关键字用于定义生成器函数，生成器函数在被调用时返回一个生成器对象，该对象是一个迭代器。
- 生成器是惰性计算的，适合处理大数据集或无限序列，可以显著减少内存使用。

理解迭代器和生成器的概念，可以帮助你更高效地处理数据流，尤其是在需要逐个处理大量数据时。

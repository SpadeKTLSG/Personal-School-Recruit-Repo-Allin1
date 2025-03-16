‍

# PY

‍

### 特性

‍

#### 深浅拷贝

‍

1. **浅拷贝**：

    * 浅拷贝创建一个新的对象，但不复制嵌套对象。新对象中的嵌套对象仍然是原始对象中的引用。
    * 可以使用`copy`​模块中的`copy`​函数或对象的`copy`​方法来创建浅拷贝。
2. **深拷贝**：

    * 深拷贝创建一个新的对象，并**递归地复制所有嵌套对象**。新对象中的嵌套对象是原始对象中嵌套对象的副本。
    * 可以使用`copy`​模块中的`deepcopy`​函数来创建深拷贝。

‍

‍

‍

### 语法API

‍

#### python有哪些数据类型，元组和list有什么区别

Python 中的常见数据类型包括：

1. **整数（int）** ：如 1, 2, 3
2. **浮点数（float）** ：如 1.0, 2.5, 3.14
3. **字符串（str）** ：如 "hello", "world"
4. **布尔值（bool）** ：如 True, False
5. **列表（list）** ：如 [1, 2, 3], ["a", "b", "c"]
6. **元组（tuple）** ：如 (1, 2, 3), ("a", "b", "c")
7. **字典（dict）** ：如 {"key1": "value1", "key2": "value2"}
8. **集合（set）** ：如 {1, 2, 3}, {"a", "b", "c"}

‍

‍

#### python怎么实现AOP

装饰器来实现AOP（面向切面编程）。装饰器允许你在函数执行前后添加额外的行为

```python
import functools

# 定义一个装饰器，用于在函数执行前后添加行为
def aop_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        # 在函数执行前添加行为
        print("Before function execution")
        result = func(*args, **kwargs)
        # 在函数执行后添加行为
        print("After function execution")
        return result
    return wrapper

# 使用装饰器
@aop_decorator
def example_function():
    print("Function is executing")

# 调用函数
example_function()
```

‍

‍

#### Python 生成器？

generator

‍

有两种产生生成器对象的方式：一种是列表生成式加括号：

​`g1 = (x for x in range(10))`​

‍

一种是在函数定义中包含`yield`​关键字：

```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

g2 = fib(8)
```

对于generator对象g1和g2，可以通过`next(g1)`​不断获得下一个元素的值，如果没有更多的元素，就会报错`StopIteration`​

也可以通过for循环获得元素的值。

生成器的好处是不用占用很多内存，只需要在用的时候计算元素的值就行了。

‍

‍

#### Python 迭代器?

Python中可以用于for循环的，叫做可迭代`Iterable`​，包括list/set/tuple/str/dict等数据结构以及生成器；可以用以下语句判断一个对象是否是可迭代的：

```python
from collections import Iterable
isinstance(x, Iterable)
```

迭代器`Iterator`​，是指可以被`next()`​函数调用并不断返回下一个值，直到`StopIteration`​；生成器都是Iterator，而列表等数据结构不是；可以通过以下语句将list变为Iterator：

​`iter([1,2,3,4,5])`​

生成器都是Iterator，但迭代器不一定是生成器

‍

‍

#### list 和 tuple 有什么区别？

* list 长度可变，tuple不可变；
* list 中元素的值可以改变，tuple 不能改变；
* list 支持`append`​; `insert`​; `remove`​; `pop`​等方法，tuple 都不支持

‍

‍

### 并发

‍

#### Python 中使用多线程可以达到多核CPU一起使用吗？

Python中有一个被称为Global Interpreter Lock（GIL）的东西，它会确保任何时候你的多个线程中，只有一个被执行。线程的执行速度非常之快，会让你误以为线程是并行执行的，但是实际上都是轮流执行。经过GIL这一道关卡处理，会增加执行的开销。

可以通过多进程实现多核任务。

‍

‍

### 双等于和 is 有什么区别？

‍

​`==`​比较的是两个变量的 value，只要值相等就会返回True

​`is`​比较的是两个变量的 id，即`id(a) == id(b)`​，只有两个变量指向同一个对象的时候，才会返回True

但是需要注意的是，比如以下代码：

```notranslate
a = 2
b = 2
print(a is b)
```

按照上面的解释，应该会输出False，但是事实上会输出True，这是因为Python中对小数据有缓存机制，-5\~256之间的数据都会被缓存。

‍

‍

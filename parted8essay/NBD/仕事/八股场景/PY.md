‍

# 概念

‍

‍

## 零碎

‍

### python有哪些数据类型，元祖和list有什么区别

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

### 装饰器是什么

Python装饰器是一种用于修改或增强函数或方法行为的高级函数。装饰器本质上是一个函数，它接受另一个函数作为参数，并返回一个新的函数。装饰器通常用于在不修改原始函数代码的情况下，添加额外的功能或行为。

‍

‍

### Py断言是什么

在Python中，断言（assert）是一种用于调试的工具。它允许你在代码中插入检查点，以确保某些条件为真。如果条件为假，程序会抛出一个`AssertionError`​异常，并且可以选择性地提供一个错误消息。

‍

```python
def divide(a, b):
    assert b != 0, "The divisor 'b' must not be zero"
    return a / b

# 调用函数
result = divide(10, 2)  # 正常执行
print(result)

result = divide(10, 0)  # 触发断言错误
print(result)
```

‍

‍

### python怎么实现AOP

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

‍

‍

# 大块

‍

## 深浅拷贝

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

# 高级

‍

---
title: 【Python进阶_03】可迭代对象(Iterable)、迭代器(Iterator)、迭代(Iteration)、生成器(Generators)
date: 2018-06-26 21:46:56
tags: Python
categories: Python
copyright: true
---

根据维基百科， 迭代器是一个可以遍历一个容器（特别是列表）的对象。 然而，一个迭代器在遍历并读取一个容器的数据元素时， 并不会执行一个迭代。换句话说这有三个部分：
- 可迭代对象(Iterable)
- 迭代器(Iterator)
- 迭代(Iteration)

<!--more-->

### 可迭代对象(Iterable)
一个可迭代对象是Python中任意的对象， 只要它定义了可以返回一个迭代器的 **`__iter__方法`**， 或者定义了可以支持下标索引的 **`__getitem__方法`**。 简单说， 一个可迭代对象， 就是任意的对象， 只要它能给我们提供一个迭代器。

### 迭代器(Iterator)
一个迭代器是任意一个对象， 只要它定义了一个**`next(Python2)`** 或者**`__next__方法`**。

### 迭代(Iteration)
就是从某个地方（比如一个列表） 取出一个元素的过程。 当我们使用一个循环来遍历某个东西时， 这就叫一个个迭代，它是这个过程本身的名字。 

### 生成器(Generators)
生成器也是一种迭代器， 但是你只能对其迭代一次。 这是因为他们并没有把所有的值存在内存中， 而是在运行时生成值。 你通过遍历来使用它们， 要么用一个**`“for”循环`**， 要么将它们传递给任意可以进行迭代的函数和结构。 大多数时候生成器是以函数来实现的。 然而，它们并不返回一个值，而是yield(暂且译作“生出”)一个值。 

```
def generator_function():
    """
    生成器函数
    :return:
    """
    for i in range(10):
        yield i


def print_generator_function():
    for item in generator_function():
        print(item)


print_generator_function()
# output:
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
```

生成器最佳应用场景是： 你不想同一时间将所有计算出来的大量结果集分配到内存当中， 特别是结果集里还包含循环。

#### 计算斐波那契数列的生成器

**使用生成器计算斐波那契数列的生成器**

```
def fibon(n):
    """
    斐波那契数列生成器
    :param n: 生成数列长度
    :return:
    """
    a = b = 1
    for i in range(n):
        yield a
        a, b = b, a + b


def fibonacci():
    """
    调用fibon(n) 斐波那契数列生成函数
    :return:
    """
    for x in fibon(100000):  # 传入生成长度
        print(x)

        
fibonacci()
```

用这种方式式， 我们可以不用担心会使用大量的资源。

**不使用生成器计算斐波那契数列的生成器**

如果使用如下方式来实现的话会在计算很大的输入参数时， 用尽所有的资源。

```
def fibon(n):
    """
    使用列表实现斐波那契数列
    :param n: 生成数列个数
    :return: 返回存储生成数列的列表
    这样会消耗大量资源，尤其是在生成一个很大的数列长度时
    """
    a = b = 1
    result = []
    for i in range(n):
        result.append(i)
        a, b = b, a + b
    return result

fibon(100000)
```

### 生成器Code 

Python内置函数：**` next()`**， 它允许我们获取一个序列的下一个元素。

```
def generator_function_next():
    """
    输出需要用到ython内置函数： next()
    它允许我们获取一个序列的下一个元素。
    :return:
    """
    for i in range(5):
        yield i


def print_generator_function_next():
    generator = generator_function_next()
    print(next(generator))
    print(next(generator))
    print(next(generator))
    print(next(generator))
    print(next(generator))

    print(next(generator))  # 异常报错
    # Traceback(most recent call last):
    # StopIteration

print_generator_function_next()

```

在yield掉所有的值后， **next()**触发了一个 **`StopIteration的异常`**，这个异常说明所有的值都已经被yield完了。 

而在使用**`for循环`**时没有这个异常？？？ **`因为for循环会自动捕捉到这个异常并停止调用 next()。`**


#### 内置函数iter

```
my_string = "huangkeke"
next(my_string)
# Output: Traceback (most recent call last):
# File "<stdin>", line 1, in <module>
# TypeError: str object is not an iterator
```

这个异常说明**`str对象`**不是一个迭代器，但是**`str对象是一个可迭代对象`**。 这意味着它支持迭代， 但不能直接对其进行迭代操作。需要用到一个内置函数--**`内置函数iter`**。

**`内置函数iter`**， 将根据一个可迭代对象返回一个迭代器对象。

```
def iter_function():
    """
    Python内置函数 iter()
    根据一个可迭代对象返回一个迭代器
    :return:
    """
    my_string = "huangkeke"
    # print(next(my_string))  # 直接迭代输出 报错  str对象是一个可迭代对象，但不是一个迭代器
    # 需要使用内置函数iter 根据一个可迭代对象返回一个迭代器对象
    my_iter = iter(my_string)
    for item in my_iter:
        print(item)

iter_function()

```

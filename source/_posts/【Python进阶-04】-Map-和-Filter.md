---
title: 【Python进阶-04】-Map 和 Filter
date: 2018-07-11 22:33:56
tags: Python
categories: Python
copyright: true
---

### Map

Map会将一个函数映射到一个输入列表的所有元素上。

```
map(function_to_apply, list_of_inputs)
```

把列表中所有元素一个个地传递给一起个函数， 并收集输出。

```
# 把列表中所有元素一个个地传递给一个函数， 并收集输出。
items = [1, 2, 3, 4, 5]
squared = []
for i in items:
    squared.append(i ** 2)

# Map用一种简单的方式来实现
items = [1, 2, 3, 4, 5]
squared = map(lambda x: x ** 2, items)
print(squared)  
# <map object at 0x000001B91099B710>

print(type(squared))  
# <class 'map'>
```
<!--more-->

大多数时候， 使用匿名函数(lambda)来配合map
```
# 需要转换为list
squared = list(map(lambda x: x ** 2, items))
print(squared)
# [1, 4, 9, 16, 25]
```

不仅用于一列表的输入， 我们甚至可以用于一列表的函数：
```
def multiply(x):
    """
    乘法函数
    :param x: 需要做乘法的数据
    :return:  完成乘法运算后结果
    """
    return x * x


def add(x):
    """
    加法运算函数
    :param x: 需要做加法的数据
    :return:  完成加法运算后的结果
    """
    return x + x


# 列表的函数
funcs = [multiply, add]
# print(type(funcs[1]))  # <class 'function'> 列表中元素类型是function
for i in range(5):
    value = list(map(lambda x: x(i), funcs))
print(value)


# [16, 8]  1*2*3*4  1+2+3+4
```


### Filter

Python内建的filter()函数用于过滤序列。

filter能创建一个列表， 其中每个元素都是对一个函数能返回True.

和map()类似，filter()也接收一个函数和一个序列。
和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

```
def less_zero(x):
    """
    判断一个元素是否符合条件 小于0
    :param x: 需要判断元素
    :return: 返回判断结果
    """
    return x < 0


number_list = range(-5, 5)
# print(type(number_list))  # <class 'range'>
# less_than_zero = list(filter(lambda x: x < 0, number_list))  # 与下面同样功能

less_than_zero = list(filter(lambda x: less_zero(x), number_list))  # 为了更好的演示【每个元素都是对⼀个函数能返回True.】
print(less_than_zero)
# Output: [-5, -4, -3, -2, -1]
```

> [**GitHub-code 04_map_filter.py **](https://github.com/hkkhuang/PythonDev/blob/master/interPy-Python%E8%BF%9B%E9%98%B6%5B3.x%5D/04_map_filter.py)
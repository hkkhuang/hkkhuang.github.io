---
title: 【Python进阶-05】-05_set_datastruct
date: 2018-07-18 22:03:32
tags: Python
categories: Python
copyright: true
---

### Set集合

set(集合)是一个非常有用的数据结构。 它与**`列表(list)`**的特性类似， 区别在于**set不能包含重复的值**。

例如你可能想检查列表中是否包含重复的元素， 你有两个选择， 第一个需要使用for循环：

```
def check_list_elements():
    """
    使用普通方法，遍历列表，一次判断列表元素是否重复
    :return:
    """
    some_list = ['a', 'b', 'c', 'b', 'd', 'm', 'n', 'n']  # 待检查列表
    repeats = []  # 结果存放列表
    for value in some_list:  # 依次遍历some_list中的元素
        if some_list.count(value) > 1:  # 判断该元素在some_list的个数，count>1 说明重复
            if value not in repeats:  # 再判断value是否已经在duplicates中（some_list中某个元素多次重复），duplicates只记录一次
                repeats.append(value)  # 将some_list中重复的元素并且尚未添加到duplicates中的，添加进duplicates
    print(repeats)  # 输出结果


def main():
    check_list_elements()


if __name__ == '__main__':
    main()
```
<!--more-->

还有一种更简单更优雅的解决方案， 那就是使用集合(sets)：

```
def duplicates(some_list):
    """
    使用set检查列表中是否包含重复的元素
    :param some_list:
    :return:
    """
    return set([x for x in some_list if some_list.count(x) > 1])


def main():
    check_list_elements()
    print(duplicates(some_list))



if __name__ == '__main__':
    main()

```


#### 交集
对比两个集合的交集（两个集合中都有的数据）， 如下：
```
def intersect():
    """
    两个集合的交集
    :return:
    """
    valid = set(['yellow', 'red', 'blue', 'green', 'black'])
    input_set = set(['red', 'brown'])
    print(input_set.intersection(valid))  # 交集运算
    print(valid & input_set)   # 交集运算


def main():
    some_list = ['a', 'b', 'c', 'b', 'd', 'm', 'n', 'n']
    intersect()   # 集合交集


if __name__ == '__main__':
    main()
```

#### 并集

```
def union():
    """
    两个集合的并集
    :return:
    """
    valid = set(['yellow', 'red', 'blue', 'green', 'black'])
    input_set = set(['red', 'brown'])
    print(input_set.union(valid))  # 并集运算
    print(valid | input_set)   # 并集运算


def main():
    union()       # 集合并集


if __name__ == '__main__':
    main()
```


#### 差集
你可以用差集(difference)找出无效的数据， 相当于用一个集合减去另一个集合的数据：

```
def difference():
    """"
    两个集合的差集
    """
    valid = set(['yellow', 'red', 'blue', 'green', 'black'])
    input_set = set(['red', 'brown'])
    print(input_set.difference(valid))  # 差集运算
    print(input_set - valid)  # 差集运算


def main():
    difference()  # 集合差集


if __name__ == '__main__':
    main()
```

> [**GitHub-code 05_set_datastruct.py **](https://github.com/hkkhuang/PythonDev/blob/master/interPy-Python%E8%BF%9B%E9%98%B6%5B3.x%5D/05_set_datastruct.py)
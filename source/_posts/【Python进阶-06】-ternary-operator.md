---
title: 【Python进阶-06】-ternary_operator 三元运算符（条件表达式）
date: 2018-07-21 22:23:51
tags: Python
categories: Python
copyright: true
---

### 三元运算符

三元运算符通常在Python里被称为条件表达式， 这些表达式基于真(true)/假(not)的条件判断， 在Python 2.4以上才有了三元操作。


下面是一个伪代码和例子：
伪代码:
```
#如果条件为真， 返回真 否则返回假
condition_is_true if condition else condition_is_false
```

例子：
```

def ternary_operator_one():
    """
    三元运算符-条件表达式（1）
    :return:
    """
    is_fat = True
    state = "fat" if is_fat else "not fat"
    print(state)

    a, b = 1, 2
    result = a > b
    print("a > b") if result else print("a <= b")


def main():
    ternary_operator_one()


if __name__ == '__main__':
    main()
```
它允许用简单的一行快速判断， 而不是使用复杂的多行if语句。 这在大多数时候非常有用， 而且可以使代码简单可维护。
<!--more-->

另一个晦涩一点的用法比较少见， 它使用了元组：
伪代码:
```
#(返回假， 返回真)[真或假]
(if_test_is_false, if_test_is_true)[test]
```

例子：


```
def ternary_operator_two():
    fat = True
    fitness = ("skinny", "fat")[fat]
    print(fitness)


def main():
    ternary_operator_two()


if __name__ == '__main__':
    main()
```
**能够使用元组，是因为在Python中， True等于1， 而False等于0， 这就相当于在元组中使用0和1来选取数据。**

但是这样的用法很容易把真正的数据与true/false弄混，不建议使用。


另外一个不使用元组条件表达式的缘故是因为在元组中会把两个条件都执行，而**`if-else `**的条件表达式不会是两个条件都执行。

```
condition = True
print(2 if condition else 1/0)
#输出: 2

print((1/0, 2)[condition])
#输出ZeroDivisionError异常
```

在元组中是先建数据， 然后用`True(1)/False(0)`来索引到数据。
 而`if-else条件表达式`遵循普通的**if-else逻辑树**， 因此， 如果逻辑中的条件异常， 或者是重计算型（计算较久） 的情况下， 最好尽量避免使用元组条件表达式。

> [**GitHub-code 06_ternary_operator.py **](https://github.com/hkkhuang/PythonDev/blob/master/interPy-Python%E8%BF%9B%E9%98%B6%5B3.x%5D/06_ternary_operator.py)
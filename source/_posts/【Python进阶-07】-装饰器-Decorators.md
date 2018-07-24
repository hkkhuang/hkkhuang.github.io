---
title: 【Python进阶-07】-装饰器(Decorators).md
date: 2018-07-24 22:11:43
tags: Python
categories: Python
copyright: true
---


### 装饰器

装饰器(Decorators)是Python的一个重要部分。 简单地说： 他们是修改其他函数的功能的函数。 

### 一切皆对象
首先理解下Python中的函数
```
def hi(name='hkkhuang'):
    return 'hi,' + name


print(hi())
# Output: hi,hkkhuang

# 可以将一个函数赋值给一个变量，比如
my_hi = hi
# 这里没有在使用小括号， 因为并不是在调用hi函数,而是将它放在greet变量中
print(my_hi())
# Output: hi,hkkhuang

# 如果删掉旧的hi函数
del hi
# print(hi())
# outputs: NameError: name 'hi' is not defined
print(my_hi())
# Output: hi,hkkhuang
```

### 在函数中定义函数

```
# 【2 在函数中定义函数】
def hi(name='hkkhuang'):
    print('now you are inside the hi() function')

    def greet():
        return 'now you are in the greet() function'

    def welcome():
        return 'now you are in the welcome() function'

    print(greet())
    print(welcome())
    print('now you are back in the hi() function')


hi()
# Output:
# now you are inside the hi() function
# now you are in the greet() function
# now you are in the welcome() function
# now you are back in the hi() function

# 无论何时调⽤hi(), greet()和welcome()将会同时被调⽤。
# 注意：greet()和welcome()函数在hi()函数之外是不能访问的：
# greet()
# Outputs: NameError: name 'greet' is not defined
```
### 从函数中返回函数

```
# 【3-从函数中返回函数】
# 不需要在一个函数里去执行另一个函数， 我们也可以将其作为输出返回出来
def hi2(name='hkkhuang'):
    def greet():
        return 'now you are in the greet() function'

    def welcome():
        return 'now you are in the welcome() function'

    if name == 'hkkhuang':
        return greet
    else:
        return welcome
        # 注意：
        # 在if/else语句中我们返回greet和welcome， 而不是greet()和welcome()。
        # 为什么那样？ 这是因为当你把一对小括号放在后面， 这个函数就会执行；
        # 然而如果你不放括号在它后面， 那它可以被到处传递， 并且可以赋值给别的变量而不去执行它。


a = hi2()
print(a)  # a现在指向到hi2()函数中的greet()函数
# <function hi2.<locals>.greet at 0x0000021C10623950>

# 当我们写下a = hi2()， hi2()会被执行， 而由于name参数默认是yasoob， 所以函数greet被返回了。
# 如果我们把语句改为a = hi(name = "ali")， 那么welcome函数将被返回。
# 我们还可以打印出hi()()， 这会输出now you are in the greet() function。
a = hi2(name='hkk')
print(a)
# <function hi2.<locals>.welcome at 0x0000022B0B8A3F28>

print(a())  # now you are in the welcome() function

print(hi2()())  # now you are in the greet() function
print(hi2(name='hkk')())  # now you are in the welcome() function
```
### 将函数作为参数传给另一个函数

```
# 【4-将函数作为参数传给一个函数】
def hi3():
    return 'hi,hkkhuang!'


def doSomethingBeforeHi(func):
    """
    将函数作为参数传给另一个函数
    :param func: 参数是一个函数
    :return:
    """
    print('I am doing some boring work before executing hi3()')
    print(func())


doSomethingBeforeHi(hi3)
# I am doing some boring work before executing hi3()
# hi,hkkhuang!
```

### 第一个装饰器

**简单地说： 装饰器是修改其他函数的功能的函数。**

装饰器是一个函数，其主要用途是包装另一个函数或类。这种包装的首要目的是透明地修改或增强被包装对象的行为。

装饰器本质上是一个Python函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对象。

它经常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等场景。装饰器是解决这类问题的绝佳设计，有了装饰器，就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。

**概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能。**

```
def a_new_decorator(a_func):
    """
    定义装饰器
    :param a_func: 传递参数 函数
    :return:
    """
    def wrap_the_function():
        print('I am doing some boring work before executing a_func()')
        a_func()
        print('I am doing some boring work after executing a_func()')

    return wrap_the_function

def a_function_requiring_decoration():
    """Hey you! Decorate me!"""
    print('I am the function which needs some decoration to remove my foul smell')


a_function_requiring_decoration()
# output
# I am the function which needs some decoration to remove my foul smell


a_function_requiring_decoration = a_new_decorator(a_function_requiring_decoration)
a_function_requiring_decoration()
# output
# I am doing some boring work before executing a_func()
# I am the function which needs some decoration to remove my foul smell
# I am doing some boring work after executing a_func()

print(a_function_requiring_decoration.__name__)
# output
# wrap_the_function
"""
这并不是我们想要的！Ouput输出应该是“a_function_requiring_decoration”。 
这⾥的函数被warpTheFunction替代了。 
它重写了我们函数的名字和注释⽂档(docstring)。 
Python提供给我们⼀个简单的函数来解决这个问题， 那就是functools.wraps。
07_decorators_first-2.py 示例代码
"""
```

**拓展示例：**
>注:整理于: [https://www.zhihu.com/question/26930016](https://www.zhihu.com/question/26930016) 刘志军老师回答

#### 1、简单函数
开始我们有一个函数
```
def fun1():
    print("this is fun")
```

现在有新的需求，对这个函数增加一个记录日志功能,最直接方法在原来函数代码中添加记录日志功能的相应代码:
```
def fun1():
    print("This is fun")
    # 添加记录日志代码
    logging.info("fun is running")


fun1()
```

如果其他函数具有同样的需求，在每个函数中添加logging,则造成大量的代码冗余,为了减少重复代码，可以重新定义一个函数，专门进行日志处理，日志处理完成再执行业务代码
```
def use_logging(fun):
    logging.warning("%s is running" % fun.__name__)
    fun()


def fun2():
    print("this is fun2")


use_logging(fun2)
```
这样做，每次都要将一个参数传递给**`use_logging函数`**, 这样新定义日志处理函数，破坏了原有的代码逻辑结构，之前执行业务逻辑时，直接执行gun2()，现在需要执行use_logging(fun2), 在不破坏原来代码的业务逻辑，同时完成需求功能就要使用装饰器了。

#### 2、简单装饰器
```
def use_logging(func):
    """
    函数use_logging就是装饰器
    :param func:
    :return:
    """
    def wrapper(*args, **kwargs):
        logging.warning("%s is running" % func.__name__)
        return func(*args, **kwargs)

    return wrapper


def fun():
    print("This is fun")


fun = use_logging(fun)
fun()
# output:
# WARNING:root:fun is running
# This is fun
```


函数use_logging就是装饰器，它把执行真正业务方法的func包裹在函数里面，看起来像bar被use_logging装饰了。

在这个例子中，函数进入和退出时 ，被称为一个横切面(Aspect)，这种编程方式被称为面向切面的编程(Aspect-Oriented Programming)。

```
# @符号是装饰器的语法糖，在定义函数的时候使用，避免再一次赋值操作
def use_logging(func):
    """
    函数use_logging就是装饰器
    :param func:
    :return:
    """

    def wrapper(*args, **kwargs):
        logging.warning("%s is running" % func.__name__)
        return func(*args, **kwargs)

    return wrapper


@use_logging
def foo():
    print("I am foo")


@use_logging
def bar():
    print("I am bar")


foo()
# output
# I am foo
# WARNING:root:foo is running

# bar()
# output
# I am foo
# WARNING:root:bar is running
```
#### 3、带参数的装饰器

装饰器还有更大的灵活性，例如带参数的装饰器：在上面的装饰器调用中，比如@use_logging，该装饰器唯一的参数就是执行业务的函数。

装饰器的语法允许我们在调用时，提供其它参数，比如@decorator(a)。这样，就为装饰器的编写和使用提供了更大的灵活性。

```
def use_logging(level):
    """
    use_logging是允许带参数的装饰器。
    :param level:
    :return: 实际上是对原有装饰器的一个函数封装，并返回一个装饰器。
    """

    def decorator(func):
        def wrapper(*args, **kwargs):
            if level == "warn":
                logging.warning("%s is running" % func.__name__)
            return func(*args, **kwargs)

        return wrapper

    return decorator


@use_logging(level="warn")
def foo(name="foo"):
    print("I am %s" % name)


# foo()
# output
# I am foo
# WARNING:root:foo is running

```
上面的`use_logging`是允许带参数的装饰器。实际上是对原有装饰器的一个函数封装，并返回一个装饰器。可以将它理解为一个含有参数的闭包。

使用`@use_logging(level="warn")`调用的时候，Python能够发现这一层的封装，并把参数传递到装饰器的环境中。装饰器在Python使用如此方便都要归因于Python的函数能像普通的对象一样能作为参数传递给其他函数，可以被赋值给其他变量，可以作为返回值，可以被定义在另外一个函数内。

#### 4、类装饰器
类装饰器，相比函数装饰器，类装饰器具有灵活度大、高内聚、封装性等优点。

使用类装饰器还可以依靠类内部的**`__call__方法`**，当使用@形式将装饰器附加到函数上时，就会调用此方法。

```
class Foo(object):
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("class decorator running")
        self.func()
        print("class decorator ending")


@Foo
def bar():
    print("this is bar")


# bar()
# output
# class decorator running
# this is bar
# class decorator ending
```

#### 5、functools.wraps

使用装饰器极大地复用了代码，但是他有一个缺点就是原函数的元信息不见了，比如函数的docstring、__name__、参数列表.
```
def logged(func):
    def with_logging(*args, **kwargs):
        print(func.__name__ + " was called")
        return func(*args, **kwargs)

    return with_logging


@logged
def foo(x):
    """does some math"""
    return x + x * x


print(foo.__name__)  # with_logging
print(foo.__doc__)  # None

```
不难发现，**函数foo被with_logging取代了**，当然它的`docstring，__name__`就是变成了with_logging函数的信息了。这个问题就比较严重的，此时需要借助**`functools.wraps`**，**wraps本身也是一个装饰器**，**它能把原函数的元信息拷贝到装饰器函数中，这使得装饰器函数也有和原函数一样的元信息了。**

```
def logged(func):
    @wraps(func)
    def with_logging(*args, **kwargs):
        print(func.__name__ + "was called")
        return func(*args, **kwargs)

    return with_logging


@logged
def bar(x):
    """dose some math"""
    return x ** 2 + x


print(bar.__name__)  # bar
print(bar.__doc__)  # dose some math
```

#### 6、内置装饰器
**@staticmathod、@classmethod、@property**

```
# 装饰器的顺序
@a
@b
@c
def f():
    pass

# 等效于:
f = a(b(c(f)))

```


> [**GitHub-code 07_decorators_pre.py **](https://github.com/hkkhuang/PythonDev/blob/master/interPy-Python%E8%BF%9B%E9%98%B6%5B3.x%5D/07_decorators_pre.py)
> [**GitHub-code 07_decorators_first_hkk.py **](https://github.com/hkkhuang/PythonDev/blob/master/interPy-Python%E8%BF%9B%E9%98%B6%5B3.x%5D/07_decorators_first_hkk.py)

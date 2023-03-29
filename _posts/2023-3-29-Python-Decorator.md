---
layout: post
title: Python Decorator
categories: [Course]
---
## Python 装饰器（Decorator）
一句话解释清楚：

Python Decorator本质上是一个定义的函数，该函数的参数是函数对象，能让其他函数在不需要进行任何代码改动的前提下增加额外的功能，Python装饰器的返回值也是一个函数对象。

例子：
假如说要统计一个函数compute1()的执行时间，一般会这么写：

```
def TimeRecord1():
    start = time.time()
    compute1()
    end = time.time()
    print(end-start)
```
但是又要统计另外一个函数compute2()的执行时间，我们就需要再写一个TimeRecord函数，命名为TimeRecord2()
```
def TimeRecord2():
    start = time.time()
    compute2()
    end = time.time()
    print(end-start)
```
如果我们再统计一个函数的执行时间呢？那么还要继续定义新的TimeRecord函数，代码冗余不优雅

因此Python装饰器出现，我们只需要定义一个装饰器函数即可。
```
def TimeRecord(func):
    def wrapper(*args, **kargs):
        start = time.time()
        f = func(*args, **kargs)
        end = time.time()
        return f
    return wrpper

@TimeRecord
def compute1():
    xxx

@TimeRecord
def compute2():
    xxx
```

Python Decorator的本质即为在原先的函数执行栈外面再包一层，类似于包洋葱的方式，多重的函数装饰器也是如此。因此执行的时候也是从洋葱的一面切到另外一面，即可快速的得出执行的结果。
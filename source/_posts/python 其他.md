---
title: python 其他
tags:  	
    - python
    - PROGRAMMING
---
几个知识点：装饰器，\*用法，\*\*用法。
<!--more-->
装饰器实质上是一个函数。它把一个函数作为输入并且返回另外一个函数，可以看做是在不改变源代码的情况下修改已经存在的函数。


```
def document_it(func):
    def new_fun(*arg,**kwargs):
        print('fun',func.__name__)
        re=func(*arg,**kwargs)
        print('re',re)
        return re
    return new_fun
@document_it
def add_int(a=0,b=0):
    return a+b

add_int(5,3)
```

\*用法
\*在Python\*中不用于C/C++的指针。在用作参数时，可以将一组可变数量的位置参数集合成参数值的元组。

```
def add_ints(a=0,b=0,*args):
    print('a',a)
    print('b',b)
    print('*args',args)
add_ints(1,2,3,4,5,6)
# a 1
# b 2
# *args (3, 4, 5, 6)
```


\*\*用法
在参数使用中双星号是将参数接受为一个字典，参数的名字是字典的键，对应参数的值是字典的值。这个用法需要注意是后面的参数必须赋值。

```
def add_ints(a=0,b=0,**kwargs):
    print('kwargs',kwargs)
add_ints(a=1,b=2,d=3,e=4,f=5)
# kwargs {'d': 3, 'e': 4, 'f': 5}   #!!!注意输出的内容
```
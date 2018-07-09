---
title: python 教程六-面向对象
tags:  	
    - python
    - PROGRAMMING
---
Python面向对象的用法简析。这里面向对象的概念不在赘述只说Python面向对象的用法。
<!--more-->
## 定义类和初始化
Python定义类很简单，简单如

```
class Person():
    pass
```

的代码就可以定义一个类，不过这个类是类的最简形式——空类。Python用__init__(self)函数初始化一个类。

```
class Person():
    def __init__(self):
        print('Person')
```

现在创建的是具有初始化函数的类。实例化的时候话输出‘Person’。 __init__() 方法第一个参数一般为 self。虽然算是约定俗成的但是 self 并不是一个 Python 保留字（用其他的变量替代也是可以的）。

```
class Person():
    def __init__(args,name):
        args.name=name
        print('Person',args.name)
Tom=Person('Tom.krose')
print(Tom.name)
# Person Tom.krose
# Tom.krose
```

整个过程可以理解为调用对象的__init__方法，将这个新创建的对象作为self传入，并将另一个参数作为 name 传入。即类内函数的第一个参数是表示类对象本身的。

```

```


## 继承
继承是为了继承前面类实现的功能不必再重复工作还能保证代码简介修改方便。

```
class Person():
    def __init__(self,name):
        self.name=name
        print('Person',name)
class Asian(Person):
    def hometown(self):
        print('Asia')
cha=Asian('Tang')
print(cha.name)
cha.hometown()
# Person Tang
# Tang
# Asia
```

子类不光可以继承父类还可以覆盖父类的内容

```
class Chinese(Asian):
    def hometown(self):
        print('China')
    def food(self):
        print('Rice')
cha=Chinese('Tang')
print(cha.name)
cha.hometown()
cha.food()
# Person Tang
# Tang
# China
# Rice
```

上例覆盖了Asian的hometown方法，创建了Asian没有的food方法。
当然，有时候需要在子类中使用父类的方法。python中使用super来重父类参数或方法。

```
class Chinese(Asian):
    def hometown(self,home):
        super().hometown(home)
        print('China',home)
    def food(self):
        print('Rice')
cha=Chinese('Tang')
print(cha.name)
cha.hometown('Beijing')
cha.food()
# Person Tang
# Tang
# Asia Beijing
# China Beijing
# Rice
```

上例super重用父类的hometown。
python中没有像C/C++中pravite这种机制，所有属性都是公开的。如果想要使用类似于保护机制不直接访问对象属性的策略时，可以使用property方式定义类。如下：

```
class Chinese():
    def __init__(self,name):
        self.name=name
        print('Person',name)
    def get_name(self):
        print('get_name')
        return self.name
    def set_name(self,name):
        print('set_name')
        self.name=name
    pro_name=property(get_name,set_name)
cha=Chinese('Tang')
cha.pro_name
# Person Tang
# get_name
```

也可以调用刚才定义的set_name方法：

```
cha.pro_name='Tangdun'
# set_name
```

上述实现可以用装饰器实现。输出结果和上面的例子相同。

```
class Chinese():
    def __init__(self,name):
        self.name=name
        print('Person',name)
    @property
    def get_name(self):
        print('get_name')
        return self.name
    @get_name.setter
    def set_name(self,name):
        print('set_name')
        self.name=name
cha=Chinese('Tang')
cha.get_name
cha.set_name='Tangdun'
```

类方法是作用于整个类的方法，对类作出的任何改变会对它的所有实例对象产生影响。用@classmethod指定某个方法为类方法。类方法的第一个参数是类本身常写作cls

```
class Chinese():
    count=0
    def __init__(self,name):
        Chinese.count += 1
        self.name=name
        print('Person',name)
    @classmethod
    def person_count(cls):
        return cls.count
cha=Chinese('Tang')
ha=Chinese('Hai')
wang=Chinese('Wang')
print(Chinese.count)
print(Chinese.person_count())
# Person Tang
# Person Hai
# Person Wang
# 3
# 3
```

静态方法（static method），用 @staticmethod 修饰，既不会影响类也不会影响类的对象。

python多态（空着）
python magic method（空着）


注：self参在调用机制中是对象参数。
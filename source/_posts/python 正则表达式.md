---
title: python 正则表达式
tags:  	
    - python
    - PROGRAMMING
---
故事从一句话说起~~
<!--more-->
小明：“这是我的邮箱：9421@qq.com，欢迎来信。”
我想提取这个qq号怎么办，我想看邮箱怎么办，我想看他用的是什么邮箱怎么办，我只想看汉字怎么办？怎么办？？
# (⊙_⊙?)

N大问题一个对策——正则表达式，正则表达式的作用是把标准字母表用于通用文本，对文本进行处理和搜索。或者说用某些特定字符表示一类字符的集合，比如：\\d 表示 一个十进制的数字，通过\\d结合一些函数就可以找出句子中所有的数字。现在来看看这些用法。

这里我们主要讲compile，match，findall，search，sub的用法。

## 正则表达式常见符号和表示方法 

|表示法|描述|例子|
|:---|:---|:---|
|\\b|匹配单词的边界||
|\\d|匹配一个十进制数字|0|
|\\D|匹配非数字字符|他|
|\\w|匹配一个任意字符或数字字符|他|
|\\s|匹配一个空格||
|\\N|匹配已保存的子组N||
|\\c|逐字匹配任何特殊字符c|\\*|
|\.|匹配除了\\n之外的任意字符|！|
|^|限定字符起始字符|^A|
|$|限定字符的终止字符|$Z|
|*|匹配0 次或者多次前面出现的正则表达式|A*|
|+|匹配1 次或者多次前面出现的正则表达式|A+|
|?|匹配0 次或者1次前面出现的正则表达式|A?|
|{N}|匹配N次前面出现的正则表达式|A{3}|
|{M,N}|匹配M到N次前面出现的正则表达式|A{2,3}|
|[...]|匹配来自字符集的任意单一字符 |[A,B,C,D]|
|[..x−y..]|匹配x～y 范围中的任意单一字符 |[A-Za-z]|

注：符号还有些不太常用就不列举了。
## compile
compile 将符号编译成正则表达式的模式，然后返回一个正则表达式对象。函数根据一个模式字符串和可选的标志参数生成一个正则表达式对象。该对象拥有一系列方法用于正则表达式匹配和替换。

```
import re
pattern =re.compile('\d')

```

compile类似制作了一把一个类型的万能钥匙，有了钥匙才能打开相同类型的锁。

## match

从字符串的<b>起始位置</b>匹配一个模式，如果不是就返回none。

```
match(pattern, string, flags=0)
```

pattern	匹配的正则表达式。
string	要匹配的字符串。
flags	可选参数，用于控制正则表达式的匹配方式。
```
import re
string='我的英文名是：xiaoming，这是我的邮箱：9421@qq.com，欢迎来信。'
pattern =re.compile('\d')
restring=re.match(pattern,string)
if restring:
   print ("restring.group() : ", restring.group())
else:
   print ("No match!!")
# 结果为：No match!!
# \d 改为\w则为我
```
可以使用group(num) 或 groups() 匹配对象函数来获取匹配表达式。

```
import re
string='我的英文名是：xiaoming，这是我的邮箱：9421@qq.com，欢迎来信。'
pattern =re.compile('(\w+)：(\w+)')
restring=re.match(pattern,string)
if restring:
   print ("restring.groups() : ", restring.group(2))
else:
   print ("No match!!")
#输出结果：restring.groups() :  xiaoming
```

## findall
findall 在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果没有找到匹配的，则返回空列表。

```
import re
string='我的英文名是：xiaoming，这是我的邮箱：9421@qq.com，欢迎来信。'
pattern =re.compile('(\w+)')
restring=re.findall(pattern,string)
if restring:
   print ("restring : ", restring)
#输出结果：restring :  ['我的英文名是', 'xiaoming', '这是我的邮箱', '9421', 'qq', 'com', '欢迎来信']
```

## search
search 扫描整个字符串并返回第一个成功的匹配。否则返回None。

```
search(pattern, string, flags=0)
```

pattern	匹配的正则表达式。
string	要匹配的字符串。
flags	可选参数，用于控制正则表达式的匹配方式.

```
import re
string='我的英文名是：xiaoming，这是我的邮箱：9421@qq.com，欢迎来信。'
pattern =re.compile('(\w+)：(\w+)')
restring=re.search(pattern,string)
if restring:
   print ("restring.groups() : ", restring.group(2))
else:
   print ("No match!!")
#输出结果：restring.groups() :  xiaoming
```

也可以使用group(num) 或 groups() 匹配对象函数来获取匹配表达式。
## sub
sub用于替换字符串中的匹配项。

```
sub(pattern, repl, string, count=0)
```

pattern  正则中的模式字符串。
repl 	 替换的字符串，也可为一个函数。
string 	 要被查找替换的原始字符串。
count 	 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。

```
import re
string='我的英文名是：xiaoming，这是我的邮箱：9421@qq.com，欢迎来信。'
pattern =re.compile('(\D+)')
restring=re.sub(pattern,'',string)
if restring:
   print ("restring : ", restring)
# 结果是：9421
```

实例参考：[爬取猫眼电影100排行榜](https://frfy.github.io/2018/05/10/20180510/)
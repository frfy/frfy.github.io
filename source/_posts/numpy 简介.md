---
title: numpy简介
tags:
	- MACHINELEARNING
	- DEEPLEARNING
---
numpy是python中科学计算的库，提供矩阵运算。本文将概述numpy的基本使用方法。
<!--more-->
## 创建矩阵
通过array 赋值创建numpy的矩阵。示例：

```
import numpy as np

test_array_a=np.array([1,2,3])
print(type(test_array_a))					#<class'numpy.ndarray'>
print(test_array_a.shape)					#(3,)
print(test_array_a)							#[1,2,3]

test_array_b=np.array([[1,2,3],[2,3,4]])	
print(test_array_b.shape)					#(2,3)
print(test_array_b[1])						#[2,3,4]
```

zeros创建值为零的矩阵，示例：

```
test_zeros = np.zeros((2,2))
```

ones创建值为全为1的矩阵

```
test_ones = np.ones((2,2))
```

full创建自定义值的全值矩阵

```
test_full = np.full((2,2),3)
```

eye创建单位阵

```
test_eye = np.eye(2)
```

random 创建随机值矩阵

```
test_random = np.random.random((2,2))
```

arrange 创建某个单位的矩阵

```
test_arrange = np.arrage(10)
np.arange(2, 10, dtype=float)
np.arange(2, 3, 0.1)
```

linspace在某个范围创建特定个数矩阵元素的矩阵

```
test_linspace = np.linspace(1,5,5) # array([1,2,3,4,5])
```

indices不太好描述啊……[参考英文官方文档](https://docs.scipy.org/doc/numpy/user/basics.creation.html#arrays-creation)

## 访问矩阵

访问矩阵的方式有多种，但是原理上都是按照矩阵（数组）的行列访问。
* 整数组合地址
numpy允许构造数据对的形式访问矩阵形式如下：

```
a = np.array([[1,2], [3, 4], [5, 6]])
print (a[[0, 1, 2], [0, 1, 0]])  				# [1 4 5]
print (np.array([a[0, 0], a[1, 1], a[2, 0]]))  	# [1 4 5]
print (a[[0, 0], [1, 1]])  						# [2 2]
print (np.array([a[0, 1], a[0, 1]]))  			# [2 2]
```

上面代码中内部的[a,b,c][d,e,f]是按照[a,d][b,e][c,f]形式组成的，跟直观感觉可能不太一样需要注意。
* 整数序列访问
类似于arange函数产生整数序列，按照这个整数序列访问矩阵


```
print (a[np.arange(4), np.arange(4)])
```

代码实际效果等价

```
print (a[[0,1,2,3], [0,1,2,3]])
```

* 布尔形式访问

```
a = np.array([[1,2], [3, 4], [5, 6]])
bool_idx = (a > 2) 
print (bool_idx)
print (a[bool_idx])
print (a[a > 2])
```

* 切片
numpy可以使用与Python相似的切片功能，不过需要注意维度问题。虽然重要但是是Python的基础内容不想展开，参考一个格式a:b:c意思是范围从a到b的半闭半开区间用步长c取值。下面附代码片段做参考


```
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
row_r1 = a[1, :]    			
row_r2 = a[1:2, :]  			
print （row_r1）			# [5 6 7 8] 
print （row_r1.shape）  	# (4,)
print （row_r2）			# [[5 6 7 8]] 
print （row_r2.shape）  	# (1, 4)
```

更多内容可以参考[官方文档](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html)
## 矩阵运算
\+ 	对应函数	np.add       元素对应相加
\-	对应函数	np.subtract  元素对应相减
\*	对应函数	np.multiply  元素对应相乘
/	对应函数	np.divide    元素对应相除
dot函数进行矩阵乘法

```
print （v.dot(w)）
print （np.dot(v, w)）
```

sum矩阵求和，用axis参数制定维度，默认全部元素求和。
T表示转置，是矩阵的属性参数。
## 广播机制
此处参考一份资料中的解释（出处忘记了）
对两个数组使用广播机制要遵守下列规则：
如果数组的秩不同，使用1来将秩较小的数组进行扩展，直到两个数组的尺寸的长度都一样。
如果两个数组在某个维度上的长度是一样的，或者其中一个数组在该维度上长度为1，那么我们就说这两个数组在该维度上是相容的。
如果两个数组在所有维度上都是相容的，他们就能使用广播。
如果两个输入数组的尺寸不同，那么注意其中较大的那个尺寸。因为广播之后，两个数组的尺寸将和那个较大的尺寸一样。
在任何一个维度上，如果一个数组的长度为1，另一个数组长度大于1，那么在该维度上，就好像是对第一个数组进行了复制。



注：上述函数都可以加dtype参数设定矩阵中的数值类型如float
数据类型直接贴官网的

|Data type|Description|
|:---|:---|
|bool_			|Boolean (True or False) stored as a byte|
|int_			|Default integer type (same as C long; normally either int64 or int32)|
|intc			|Identical to C int (normally int32 or int64)|
|intp			|Integer used for indexing (same as C ssize_t; normally either int32 or int64)|
|int8			|Byte (-128 to 127)|
|int16			|Integer (-32768 to 32767)|
|int32			|Integer (-2147483648 to 2147483647)|
|int64			|Integer (-9223372036854775808 to 9223372036854775807)|
|uint8			|Unsigned integer (0 to 255)|
|uint16			|Unsigned integer (0 to 65535)|
|uint32			|Unsigned integer (0 to 4294967295)|
|uint64			|Unsigned integer (0 to 18446744073709551615)|
|float_			|Shorthand for float64.|
|float16		|Half precision float: sign bit, 5 bits exponent, 10 bits mantissa|
|float32		|Single precision float: sign bit, 8 bits exponent, 23 bits mantissa|
|float64		|Double precision float: sign bit, 11 bits exponent, 52 bits mantissa|
|complex_		|Shorthand for complex128.|
|complex64		|Complex number, represented by two 32-bit floats (real and imaginary components)|
|complex128		|Complex number, represented by two 64-bit floats (real and imaginary components)|


至此numpy中常用功能算是简要介绍完了，有需要可以查看[numpy官方文档](https://docs.scipy.org/doc/numpy/reference/)
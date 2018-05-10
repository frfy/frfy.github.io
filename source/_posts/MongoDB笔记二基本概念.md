---
title: MongoDB笔记二基本概念 		
tags:  	
    - DATABASE
    - PROGRAMMING
---
mongodb中基本的概念是文档、集合、数据库
<!--more-->

* MongoDB概念与SQL属于比较

|SQL术语概念|MongoDB术语概念|解释说明|
|----|:----|:----|
|database		|database			|数据库|
|table			|collection			|数据库表集合|
|row			|document			|数据记录行文档|
|column			|field				|数据字段域|
|index			|index				|索引|
|table 			|joins	 			|表连接,MongoDB不支持|
|primary key	|primary key		|主键,MongoDB自动将_id字段设置为主键|

* 数据库

显示所有数据的列表
show dbs 
显示当前数据库对象或集合
db
连接到一个指定的数据库
use
use local
switched to db local


* 文档
文档是一组键值(key-value)对。
注：
1.文档中的键/值对是有序的。
2.文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
3.MongoDB区分类型和大小写。
4.MongoDB的文档不能有重复的键。
5.文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。


* 集合
集合就是 MongoDB 文档组，类似于关系数据库的表格。
集合没有固定的结构，对集合可以插入不同格式和类型的数据。


* 数据类型

|数据类型|描述|
|:---|:---|
|String				|字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。|
|Integer			|整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。|
|Boolean			|布尔值。用于存储布尔值（真、假）。|
|Double				|双精度浮点值。用于存储浮点值。|
|Min/Max keys		|将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。|
|Array				|用于将数组或列表或多个值存储为一个键。|
|Timestamp			|时间戳。记录文档修改或添加的具体时间。|
|Object				|用于内嵌文档。|
|Null				|用于创建空值。|
|Symbol				|符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。|
|Date				|日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date象，传入年月日信息。|
|Object ID			|对象 ID。用于创建文档的 ID。|
|Binary Data		|二进制数据。用于存储二进制数据。|
|Code				|代码类型。用于在文档中存储 JavaScript 代码。|
|Regular expression	|正则表达式类型。用于存储正则表达式。|

ObjectId类似唯一主键，可以很快的去生成和排序，包含 12 bytes，含义是：
前 4 个字节表示创建 unix时间戳,格林尼治时间 UTC 时间，比北京时间晚了 8 个小时
接下来的 3 个字节是机器标识码
紧接的两个字节由进程 id 组成 PID
最后三个字节是随机数
MongoDB 中存储的文档必须有一个 _id 键。这个键的值可以是任何类型的，默认是个 ObjectId 对象
由于 ObjectId 中保存了创建的时间戳，所以不需要为文档保存时间戳字段，可以通过 getTimestamp 函数来获取文档的创建时间:
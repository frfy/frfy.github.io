---
title: MongoDB笔记三基本操作 		
tags:  	
    - DATABASE
    - PROGRAMMING
---
MongoDB基本操作：增、删、改、查等。
<!--more-->

## 创建数据库
use DATABASE_NAME 数据库存在就切换到指定数据库，不存在则创建数据库
db 显示当前数据库对象或集合
show dbs 显示所有数据的列表

## 删除数据库
db.dropDatabase()

## 显示集合
show collections
show tables

## 创建集合
db.createCollection(name, options)

options 可以是如下参数：

|字段|类型|描述|
|:---|:---|:---|
|capped			|布尔		|（可选）如果为 true，则创建固定集合。固定集合是指有着固定大小的集合，当达到最大值时，它会自动覆盖最早的文档。当该值为 true 时，必须指定 size 参数。|
|autoIndexId	|布尔		|（可选）如为 true，自动在 _id 字段创建索引。默认为 false。|
|max			|数值		|（可选）指定固定集合中包含文档的最大数量。|
|size			|数值		|（可选）为固定集合指定一个最大值（以字节计）。如果 capped 为 true，也需要指定该字段。|



MongoDB 也可以在插入文档时自动创建集合。
db.COLLECTION_NAME.insert(document)

## 删除集合
db.collection_name.drop()

## 插入文档
使用 insert() 或 save() 方法向集合中插入文档
db.COLLECTION_NAME.insert(document)

也可以使用 db.col.save(document) 命令。如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id 的数据。


## 更新文档

在3.2版本，MongoDB提供更新集合文档的方法：
db.collection.updateOne() 向指定集合更新单个文档
db.collection.updateMany() 向指定集合更新多个文档

原先使用 update() 和 save() 方法来更新集合中的文档

```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

* query : update的查询条件，类似sql update查询内where后面的。
* update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
* upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
* multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
* writeConcern :可选，抛出异常的级别。

save() 方法通过传入的文档来替换已有文档。

```
db.collection.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

```
只更新第一条记录：
db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } );
全部更新：
db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true );
只添加第一条：
db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false );

db.test_collection.updateOne({"name":"abc"},{$set:{"age":"28"}})
db.test_collection.updateMany({"age":{$gt:"10"}},{$set:{"status":"xyz"}})
```

## 删除文档
使用 deleteOne() 和 deleteMany() 方法，还有remove()函数

## 查询文档
db.collection.find(query, projection)
* query ：可选，使用查询操作符指定查询条件
* projection ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。
{key1:1,key2:1}  inclusion模式 指定返回的键，不返回其他键
{key1:0,key2:0}  exclusion模式 指定不返回的键,返回其他键
两种模式不能混用，只能全1或全0，除了在inclusion模式时可以指定_id为0
_id 键默认返回，需要主动指定 _id:0 才会隐藏


db.col.find().pretty()
pretty() 方法以格式化的方式来显示所有文档。

|操作|格式|范例|
|:---|:---|:---|
|等于		|{<key>:<value>}			|db.col.find({"by":"菜鸟教程"}).pretty()|
|小于		|{<key>:{$lt:<value>}}		|db.col.find({"likes":{$lt:50}}).pretty()|
|小于或等于	|{<key>:{$lte:<value>}}		|db.col.find({"likes":{$lte:50}}).pretty()|
|大于		|{<key>:{$gt:<value>}}		|db.col.find({"likes":{$gt:50}}).pretty()|
|大于或等于	|{<key>:{$gte:<value>}}		|db.col.find({"likes":{$gte:50}}).pretty()|
|不等于		|{<key>:{$ne:<value>}}		|db.col.find({"likes":{$ne:50}}).pretty()|

* AND 条件
find() 方法可以传入多个键(key)，每个键(key)以逗号隔开

* OR 条件
OR 条件语句使用了关键字 $or

* $type 操作符

|类型|数字|备注|
|:---|:---|:---|
|Double					|1	 	||
|String					|2	 	||
|Object					|3	 	||
|Array					|4	 	||
|Binary data				|5	 	||
|Undefined				|6		|已废弃。|
|Object id				|7	 	||
|Boolean					|8	 	||
|Date					|9	 	||
|Null					|10	 	||
|Regular Expression		|11	 	||
|JavaScript				|13	 	||
|Symbol					|14	 	||
|JavaScript (with scope)	|15	 	||
|32-bit integer			|16	 	||
|Timestamp				|17	 	||
|64-bit integer			|18	 	||
|Min key					|255	|Query with -1.|
|Max key					|127	| |



* Limit与Skip方法
limit()方法基本语法
db.COLLECTION_NAME.find().limit(NUMBER)

skip() 方法语法
db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)

* sort()方法排序
sort()方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列。
db.COLLECTION_NAME.find().sort({KEY:1})

##### 注：skip(), limilt(), sort()三个放在一起执行的时候，执行的顺序是先 sort(), 然后是 skip()，最后是显示的 limit()。
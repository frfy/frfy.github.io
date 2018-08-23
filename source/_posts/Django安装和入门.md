---
title: Django 安装和入门
tags:
	- python
    - PROGRAMMING
---
Django 安装和入门。
<!--more-->
[Django原网](https://www.djangoproject.com)
## 安装
* pip安装直接执行：

```
pip install django
```

* [下载文件](https://www.djangoproject.com/download/2.0.7/tarball/)解压后进入到文件目录，执行：

```
python setup.py install
```

* 检查安装是否成功输入：

```
python -m django --version #显示版本号
```

## 创建项目和应用

* 创建项目
切换在目标目录下，创建项目，通过命令行输入

```
django-admin startproject testweb
```

目录下会出现testweb的文件夹。目录结构如下：
testweb
-manage.py
-testweb
\-\-\_\_init\_\_.py
\-\-settings.py
\-\-urls.py
\-\-wsgi.py
<b> manage.py:</b>项目管理器，与Python交互的入口 如：

```
python manage.py runserver
```

<b> -testweb：</b>项目容器目录，包含项目基本配置。（目录下包含：\_\_init\_\_.py，wsgi.py，settings.py，urls.py）
<b> \-\-\_\_init\_\_.py:</b>Python模块声明文件
<b> \-\-settings.py:</b>核心配置文件（数据库，web应用，时间等）
<b> \-\-urls.py:url配置文件</b>
<b> \-\-wsgi.py:</b>python web server gateway interface 应用与服务器之间的接口

* 创建应用
创建应用指的是：
执行：

```
python manage.py startapp testblog
```

添加应用名（testblog）到settings.py中的INSTALLED_APPS里
在同级目录下会生成testblog目录，目录结构如下：
\-migrations
\-\-\_\_init\_\_
\-\_\_init\_\_
\-admin.py
\-apps.py
\-models.py
\-tests.py
\-views.py
<b>migrations:</b>目录数据模块（迁移）
<b>admin.py:</b>应用后台管理系统配置文件
<b>apps.py:</b>当前应用的配置
<b>models.py:</b>数据模型模块（ORM框架）
<b>tests.py:</b>测试模块
<b>views.py:</b>执行响应的模块，主要代码编辑区

在views.py中编写网页响应函数，url加入urls.py，启动服务即可访问
1、每个响应对应一个函数，函数返回响应
2、函数参数一般为request
3、每个响应函数对应一个URL
4、url配置有三种方法

## Templates
使用Django模板语言DTL，类似的模板引擎还有（jinja2）
1、APP目录下创建Templates目录
2、在Templates目录中创建HTML文件
3、由views.py中的render函数返回HTML

<b>注：Django按照INSTALLED_APPS中添加顺序查找Templates，不同APP下Templates目录中的同名HTML文件会冲突。
解决方案：在APP的templates目录中创建以APP名为名称的目录。将HTML文件放到目录下。<b>

## Models
Django中数据库处理类。可以以对象的形式操作数据库。隐藏数据库访问。
在models.py中引入models.Model，这个类与数据表对应，通过manage.py映射成数据表。
通过类方法创建字段，如models.CharField(max_length=100),具体数据类型可以通过models查看。

将models映射到数据表


```
python manage.py makemigrations app_name(optinal)   #形成映射
```

```
python manage.py migrate							#完成映射动作，后台生成数据表
```

完成后会在app/migrations/目录下生成移植文件(file_name)

查看映射对应的sql语句，执行：

```
python manage.py sqlmigrate app_name file_name 
```

后台在views.py 中,执行：

```
import models
object=model.Article.objects.get(primary_key=int_tpye)
render(request,'page',{'obj':object})
```

前段的HTML可以接受到对象直接使用{{object.attribute}}引用。

## Admin
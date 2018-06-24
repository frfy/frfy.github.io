---
title: Git使用笔记
tags:
	- Tricks
	- Git
---
曾经修改论文名列表<font face="verdana" color="red">[论文1……论文100,论文终稿1……终稿100,不改稿……不改稿100,………坚决不改100]</font>
现在妈妈再也不用担心我的论文名了。
<!--more-->
本文只记录Git命令行的使用，不讲解原理、概念和安装等。
## 本地创建和管理仓库
* 创建版本库
要在本地管理多版本最重要的是本地创建版本库。命令很简单，新建存储目录切换到该目录下，执行：

```
	git init
```

接下来就可以添加文件进行版本控制了。
* 添加文件
通过命令将文件添加到仓库，如将A.txt添加到仓库。

```
git add A.txt
```

可以通过 git add .添加当前目录下所有文件
* 提交文件
接下来，还需要告诉Git你添加文件的信息，把文件提交到仓库。

```
git commit -m '201806241700update'
```

-m后面跟的就是更改的信息，可以不添加信息，用 git help commit 命令自己查看吧（强烈不建议！！）。
* 查看当前状态
多次修改文件，添加和提交后。通过命令查看当前仓库的状态

```
git status
```

* 查看更改内容
通过命令查文件被更改的具体内容:

```
git diff
```

diff 跟具体文件查看特定文件的更改内容。

* 查看提交记录
通过命令可以查看由近到远的提交记录：

```
git log
```

命令会给出 commit 、 Author 、 Date 和提交-m中的信息。commit后面跟的是id版本号。这个id非常重要，版本的控制会用到。
* 版本控制
多此修改提交后，想退回某个版本怎么办呢？
上面 log中的id就可以帮我们了。
退回到某个版本的命令是：

```
git reset --hard id  
```

id不需要像log中的那么长，前几位id代码就可以确定了。
当然跳回上一版本或者上面的有限版本可以使用 <font color="blue"> ^ </font> 和 <font color="blue"> ~100 </font> 。
* 撤销修改

```
git checkout -- A.txt
```

可以撤销当前对A.txt的修改。<font color="bule">checkout</font>还有一个用法是切换分支

## 本地与远程仓库同步
主要指与GitHub的同步。
* 关联远程仓库

```
git remote add origin git@username:path/repo-name.git
```

* 内容推送
将本地内容上传到远程仓库。

```
git push 
```

* 克隆远程仓库
从远程克隆仓库到本地

```
git clone git@github.com:*****.git
```


注：第一次同步最好加上<font color="bule">-u</font>参数，实现远程和本地关联，方便以后版本更新和回退。


## 其余
* 历史命令列表
查看使用过的命令，同时记录了当时提交的id，这样产看记录的同时也可以找到误删的版本。

```
git reflog
```


* 注：
版本控制工具只能跟踪文本文件的改动。
[使用 git revert <commit_id>操作实现以退为进，git revert 不同于 git reset  它不会擦除"回退"之后的 commit_id ，而是正常的当做一次"commit"，产生一次新的操作记录，所以可以push，不会让你再pull。](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)
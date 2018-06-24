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

可以通过 <font color="blue">git add . </font>添加当前目录下所有文件
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

注：第一次同步最好加上<font color="bule">-u</font>参数，实现远程和本地关联，方便以后版本更新和回退。（存疑）
## 创建和合并分支
前面说到的Git是按照时间顺序作为线索的，而且只有一条master的主分支。可以理解为时间线上的一个指针。创建分支可以理解为在时间线上新建一个指针。分支之间的合并就是指针之间的合并。
* 创建分支

```
git branch branch-name
```

```
git branch 
```

可以查看创建的所有分支，并在当前分支上加\*显示。
* 切换分支

```
git checkout branch-name
```
* 创建和切换分支
可以通过 checkout的 -b 参数创建并切换到创建的分支。

```
git checkout -b branch-name
```

* 合并分支
将branch-name合并到当前分支中：

```
git merge branch-name
```

注：合并分支时，加上<font color="bule">--no-ff</font>参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
* 删除分支

```
git branch -d branch-name
```

* 分支冲突
[待详细了解。](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840202368c74be33fbd884e71b570f2cc3c0d1dcf000)
* 分支的暂存
分支没有提交但是需要切换到其他分支中工作，可以通过将分支暂存然后恢复的策略。(比如临时修复bug)
分支暂存

```
git stash
```

恢复分支
恢复分支的策略有两个：一是用<font color="bule">git stash apply</font>恢复，但是恢复后，stash内容并不删除，你需要用<font color="bule">git stash drop</font>来删除；另一种方式是用<font color="bule">git stash pop</font>恢复的同时把stash内容也删了。

```
git stash apply
git stash drop
```

```
git stash pop
```

注：可以多次 <font color="bule">stash</font>通过git stash list查看，然后用git stash apply stash@{0}恢复指定stash。
* 多人协作分支冲突
[待详细了解。](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013760174128707b935b0be6fc4fc6ace66c4f15618f8d000)
## 标签管理
相当于vi,v2这种版本的记录。
* 创建tag

```
git tag <name>
```

注： 省略<name>表示查看tag列表
默认标签是打在最新提交的commit上,想要补充未tag的commit可以通过如下命令补充:

```
git tag v0.9 commit_id
```

可以用git show tagname查看标签信息
还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：

```
$ git tag -a v0.1 -m "version 0.1 released" commit_id
```

* 推送整个版本的内容:

```
git push origin <tagname>
```

* 删除tag

```
git tag -d tag_name
```

如果已经提交到远程<font color="bule">git push origin :refs/tags/tagname</font>可以删除一个远程标签


## 其余
* 搭建Git服务器
[资料](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)
* 历史命令列表
查看使用过的命令，同时记录了当时提交的id，这样产看记录的同时也可以找到误删的版本。

```
git reflog
```

* git fork
fork 别人的代码,提交到自己的github 然后发起<font color="bule">pull request</font>提交给原作者
* git自定义功能
<font color="bule">git config --global ....</font>的组合命令.
* 注：
版本控制工具只能跟踪文本文件的改动。
[使用 git revert <commit_id>操作实现以退为进，git revert 不同于 git reset  它不会擦除"回退"之后的 commit_id ，而是正常的当做一次"commit"，产生一次新的操作记录，所以可以push，不会让你再pull。](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)
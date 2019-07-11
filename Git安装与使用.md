# Git安装与使用

> 本步骤参考 [Git安装和使用教程](https://www.cnblogs.com/smuxiaolei/p/7484678.html) 及 [廖雪峰git教程](https://www.liaoxuefeng.com/wiki/896043488029600) 进行
>

## 1.安装

从[官网](https://git-scm.com/downloads/)下载git客户端，可参考前述教程进行，安装时选择的命令行工具为Git Bash，随后打开Git Bash设置用户名与邮箱。

代码如下：

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```



## 2.建立本地新仓库

在D盘新建一个**"学习笔记"**文件夹并将其变为git可以管理的仓库

代码如下：

~~~bash
79862@DESKTOP-G1C5J5S MINGW64 ~
$ cd d: #转入D盘

79862@DESKTOP-G1C5J5S MINGW64 /d
$ mkdir 学习笔记 #创建文件夹

79862@DESKTOP-G1C5J5S MINGW64 /d
$ cd 学习笔记 #进入文件夹

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记
$ git init #将改文件夹变为git可管理的仓库
Initialized empty Git repository in D:/学习笔记/.git/
~~~

## 3.将本地文件提交至库中

将**"Git安装与使用.md"**加入暂缓区中，并提交入库

```bash
79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git add Git安装与使用.md #添加文件

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git commit #上传文件
[master (root-commit) 45115c1] test
 1 file changed, 41 insertions(+)
 create mode 100644 "Git\345\256\211\350\243\205\344\270\216\344\275\277\347\224\250.md"

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git status #查看状态
On branch master
nothing to commit, working tree clean
```

## 4.对文件进行修改后重新提交及返回至原版本

对文件修改后可用 `git status`进行修改查看，重复**步骤3.**中过程即可储存更改。注意`git commit`后须对更改进行说明才可继续commit，可用`git commit -m <messge>`完成

```bash
79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git status #查看状态
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   "Git\345\256\211\350\243\205\344\270\216\344\275\277\347\224\250.md"

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git add Git安装与使用.md #添加文件

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git commit #上传文件
[master 0888441] test 1
 1 file changed, 22 insertions(+)
```

改回原版本相关代码

~~~bash
$ git log #显示由最近到最远排列的全部提交
$ git log –pretty=oneline #显示由最近到最远排列的全部提交,并显示在一行中
$ git reset  --hard HEAD~n #回到前n个版本 
$ git reset  --hard 版本号 #回到对应版本号的版本
$ git reflog #显示所有commit及对应版本号
$ git checkout  -- 文件名 #放弃对该文件的更改，回到上一个版本,若文件已删除则可以恢复
~~~

## 5.远程仓库（github）

- 创建SSH秘钥

```
ssh-keygen  -t rsa –C “youremail@example.com”
```

将邮箱地址换为自己的邮箱地址，输入后按enter，完成后再本地用户目录下找到两个文件，**id_rsa**是私钥，不能泄露出去，**id_rsa.pub**是公钥，可以放心地告诉任何人。

![截图](http://pic.yuntu.ru/2019/07/11/git1400cec31cadcd228.png)

登录github,打开” settings”中的SSH Keys页面，然后点击“Add SSH Key”,填上任意title，在Key文本框里黏贴id_rsa.pub文件的内容，并add key。

- 创建远程仓库并更新

首先，登录github上，然后在右上角找到“create a new repo”创建一个新的仓库，随后按网页中的提示代码进行操作。

```bash
$ git remote add origin #仓库地址可为https，也可为ssh，ssh更快且不用输密码
$ git push -u origin master
```




![1](http://pic.yuntu.ru/2019/07/11/git226ad97cfe4f2b86f.png)

完成后可用`git remote -v`查看设置

第一次推送master分支时，加上了 –u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，后续可直接使用`git push origin master`来推送

- 从远程库clone

```bash
$ git clone (仓库地址) #在当前位置新建一个仓库文件夹，并clone远程库中的文件
```

## 6.分支管理

- 分支创建与合并

可通过创建分支，从而在不直接改变master主分支的情况下，对代码进行修改，修改完成后再合并。

首先，我们创建`dev`分支，然后切换到`dev`分支：

```bash
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```bash
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后，用`git branch`命令查看当前分支：

```bash
$ git branch
* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

随后可以对该分支进行修改，和add以及commit，push操作。

利用`git checkout 分支名`来切换分支

现在，我们把`dev`分支的工作成果合并到`master`分支上：

```bash
$ git checkout master
Switched to branch 'master'
$ git merge dev
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

删除分支使用`git branch -d 分支名`即可

- 从远程库中更新分支

若从远程库中回`origin`主机的`next`分支，与本地的`master`分支合并，需要写成下面这样 

```shell
$ git pull origin next:master
```

若不填写本地分支名，则与当前分支合并

若希望比对后再合并，按以下思路进行：

```bash
$ git branch tmp #新建tmp分支
$ git fetch origin master:tmp #从远程库中取回master分支并与tmp分支合并
$ git diff tmp #将当前分支与tmp分支比对，显示差别
$ git merge tmp #将当前分支与tmp合并
```

- 将本地更改上传至远程库

```bash
$ git push origin '本地分支名':'远程分支名'
$ git push origin :'远程分支' #用空分支替代远程分支，即删除该远程分支
```

若不填写本地分支名则默认为当前分支，不填写远程分支则上传至本地分支**建立连接**的远程分支

默认情况下执行过 git remote add命令后，同名字的本地库和远程库将建立连接，也可以通过以下命令建立或修改连接。

```bash
$ git branch --set-upstream '本地分支名' origin/'远程分支名'
```

## 7.其他命令

　git还可以隐藏工作，对某一个commit设置标签，具体可参考[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/896043488029600) **分支管理及标签管理部分**

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

Git基本常用命令如下：

　　mkdir：         **XX (创建一个空目录 XX指目录名)**

　　pwd：          **显示当前目录的路径。**

　　git init          **把当前的目录变成可以管理的git仓库，生成隐藏.git文件。**

　　git add XX       **把xx文件添加到暂存区去。**

　　git commit –m **“XX”  提交文件 –m 后面的是注释。**

　　git status        **查看仓库状态**

　　git diff  XX      **查看XX文件修改了那些内容**

　　git log          **查看历史记录**

　　git reset  --hard HEAD^ **或者 git reset  --hard HEAD~ 回退到上一个版本**

　　**(如果想回退到100个版本，使用git reset –hard HEAD~100 )**

　　cat XX         **查看XX文件内容**

　　git reflog       **查看历史记录的版本号id**

　　git checkout -- XX  **把XX文件在工作区的修改全部撤销。**

　　git rm XX          **删除XX文件**

　　git remote add origin *‘远程库地址’*     **关联一个远程库**

　　git push –u**(第一次要用-u 以后不需要)** origin master **把当前master分支推送到远程库**

　　git clone *’仓库地址‘*     **从远程库中克隆**

　　git checkout –b dev  **创建dev分支 并切换到dev分支上**

　　git branch  **查看当前所有的分支**

　　git checkout master **切换回master分支**

　　git merge dev    **在当前的分支上合并dev分支**

　　git branch –d dev **删除dev分支**

　　git branch name  **创建分支**

　　git stash **把当前的工作隐藏起来 等以后恢复现场后继续工作**

　　git stash list **查看所有被隐藏的文件列表**

　　git stash apply **恢复被隐藏的文件，但是内容不删除**

　　git stash drop **删除文件**

　　git stash pop **恢复文件的同时 也删除文件**

　　git remote **查看远程库的信息**

　　git remote –v **查看远程库的详细信息**

　　git push origin master  **Git会把master分支推送到远程库对应的远程分支上**


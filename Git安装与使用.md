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



## 7.其他命令




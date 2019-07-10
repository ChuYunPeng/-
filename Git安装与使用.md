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

![截图](C:\Users\79862\Desktop\M{KU}2REXMOYUEPO[0A$ZVG.png)

登录github,打开” settings”中的SSH Keys页面，然后点击“Add SSH Key”,填上任意title，在Key文本框里黏贴id_rsa.pub文件的内容，并add key。

- 创建


# Git安装与使用

> 本步骤参考 [Git安装和使用教程](https://www.cnblogs.com/smuxiaolei/p/7484678.html)进行
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
$ cd d:

79862@DESKTOP-G1C5J5S MINGW64 /d
$ mkdir 学习笔记

79862@DESKTOP-G1C5J5S MINGW64 /d
$ cd 学习笔记

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记
$ git init
Initialized empty Git repository in D:/学习笔记/.git/
~~~

## 3.将本地文件提交至库中

将**"Git安装与使用.md"**加入暂缓区中，并提交入库

```bash
79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git add Git安装与使用.md

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git commit
[master (root-commit) 45115c1] test
 1 file changed, 41 insertions(+)
 create mode 100644 "Git\345\256\211\350\243\205\344\270\216\344\275\277\347\224\250.md"

79862@DESKTOP-G1C5J5S MINGW64 /d/学习笔记 (master)
$ git status
On branch master
nothing to commit, working tree clean
```

## 4.对文件进行修改后重新提交及返回至原版本




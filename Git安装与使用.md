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




---
title: Git基础学习笔记
date: 2021-03-01
author: 四川的小熊猫
toc: true
categories: GIT学习
tags:
  - git
---

# GIT教程（一）

> 根据菜鸟教程学习：[git](https://www.runoob.com/git/git-tutorial.html)
>
> 还有B站的UP：[遇见狂神说的讲解](https://www.bilibili.com/video/BV1FE411P7B3)、[他的文档](https://mp.weixin.qq.com/s/Bf7uVhGiu47uOELjmC5uXQ)
>
> 有一篇实例的讲解挺好的：[实例讲解](https://blog.csdn.net/u013005791/article/details/75043443)
>
> 学习的过程：看菜鸟教程——》git简明教学——》遇见狂神说

​			采用分布式版本库的方式。

## git简明教学

> 作者：罗杰·杜德勒
>
> 摘自git简明教学

1. 安装git
2. 新建文件夹，并在`cmd`中切换到文件夹，执行`git init`

显示：

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git.png)

3. 克隆：
   1. 创建一个本地仓库的克隆版本`git clone /path/to/repository`
   2. 远端服务器上的仓库：`git clone username@host:/path/to/repository`

#### 本地仓库：

- 工作目录
  - 持有实际的文件

- 暂缓区（index）
  - 临时保存你的改动

- HEAD
  - 它指向你最后一次提交的结果

#### 添加和提交

​			提出改动（把它们添加到暂缓区）

​			`git add <fielname>`

​			`git add *`

​			使用命令以实际提交改动

​			`git commit -m "代码提交信息"`

#### 推送改动

​			执行如下命令以将这些改动提交到远端仓库

​			`git push origin master`

​			可以把master换成你想要推送的任何分支



​			如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，

​			`git remote add origin <server>`

#### 分支

​			分支是用来将开发绝缘开来的，在你创建仓库的时候，master是默认的分支，在其他分支上进行开发，完成后再将他们合并到主分支上

​			创建一个叫做`feature_x`的分支，并切换过去：

​			`git checkout -b feature_x`

​			切换回主分支`git checkout master`

​			再把新建的分支删掉`git branch -d feature_x`

#### 更新与合并

​			要更新你的本地仓库至最新改动，执行`push pull`

​			以在你的工作目录中 获取（fetch）并合并（merge）远端的改动，要合并其他分支到你的当前分支（例如master）`git merge <branch>`

> 后面还有：标签、替换本地改动等，但是我认为用的不多就没写入，想看的话到原文就可以了

## 实例

> 学的半知半解，需要实际的操作，正好有我需要做的

### 说明：

​			在马云上创建一个私有的库用来存放我需要定期发布的md文件，我会在一个台式机和一个笔记本上写md，两个之间的同步很麻烦，所以建立仓库，就可以直接使用git上传和同步下载。

 			创建一个私有的仓库

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blogmd.png)

​			在本地创建仓库

​			初始化仓库

​			`git init`

​			通过`git status`查看仓库中文件的状态

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git1.png)

​			将所有的文件提交到暂缓区，`git add .`然后查看文件的情况`git status`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git2.png)

​			我们修改某个文件的内容，然后查看文件的情况

​			`git status Git`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git3.png)

​			把代码提交到本地的仓库：`git commit -m "我的md"`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git4.png)

​			我们把修改的文件提交到暂缓区`git add Git`上传到本地仓库`git commit -m "我修改了"`

> commit：是注释信息

​			查看git日志：`git log`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git5.png)

​			要上传到远程的仓库

​			显示所有的远程仓库：`git remote -v`我还没有写进去，所以没有

​			添加远程仓库：`git remote add origin https://gitee.com/xxxxxx/xxxxxx`

> origin:是设置仓库的别名

​			输入密码			

​			提交代码：`git push origin master`

​			==**出现问题：**==

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git6.png)

​			解决：`git pull --rebase origin master`

​			再次上传：`git push origin master`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/git7.png)

​				成功

下面是我第一次上传的远程仓库的截图：

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/gitee.png)

我修改了git学习文件，再次上传。

```bash
git add Git学习.md#上传到暂缓区
git commit -m ”第二次修改“
#上传到本地仓库
git push origin	master
#上传到远程仓库
```

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/gitee1.png)

### 克隆远端仓库

`git clone [url]`

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/gitee2.png)

## 免密码上传

> 每次都要输入密码。很麻烦，所以使用密钥。

​			生成密钥：`ssh-keygen -t rsa`

​			回车、回车、回车

​			找到电脑中的C:\Users\s'w'l\.ssh的密钥文件，一个是私有的一个是公有的

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/ssh.png)

​			在码云上，设置，我的公钥，添加即可。

​			上传的时候选择SSH

​	![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/ssh1.png)

​		就可以了

#### 从远端更新到本地

`git pull`

## 操作的步骤

情景：我在台式机上新建了一个text文件，然后上传到远端仓库

本地的工作区——》暂缓区——》本地仓库——》远端仓库——》本地仓库——》？

```bash
git add text
git commit -m "首次"
git push markdown master
git pull #拉取远程仓库到本地
```

在网上找的一张图：

![img](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/4428238-fcad08ebe26933a6.png)

这张图很好的解释了工作流程。

常用指令：

```bash
git init : 初始化git
git add . : 将本地项目保存到暂缓区
git commit -m "注释”:将项目从暂缓区提交到本地仓库
git remote add 仓库别名 仓库地址：配置远程仓库地址
git push -u[别名] master :将本地仓库提交到远程仓库
git pull : 同步远程仓库的最新版本到本地
git clone 仓库地址:克隆远程仓库的代码到本地
```


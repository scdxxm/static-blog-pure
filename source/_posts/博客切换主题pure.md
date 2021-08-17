---
title: 博客切换pure主题（乱七八糟）
date: 2021-08-11
author: 四川的小熊猫
toc: true
categories: 博客搭建
tags:
  - HEXO-blog
---

## 回顾

- 大概了解一下之前的情况

```
项目主要文件目录介绍：
.
├── .deploy       # 需要部署的文件
├── node_modules  # 项目所有的依赖包和插件
├── public        # 生成的静态网页文件
├── scaffolds     # 文章模板
├── source        # 博客正文和其他源文件等都应该放在这里
|   ├── _drafts   # 草稿
|   └── _posts    # 文章
├── themes        # 主题
├── _config.yml   # 全局配置文件
└── package.json  # 项目依赖信息
```

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog仓库目录.png)

- 由于电脑的环境已经变了，要在本地重新编辑博客的样式，需要重新安装环境，所以：安装`node.js`和`hexo`

安装环境的途中出现了如下问题：

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog错误1.png)

原因未知：大概率是系统的故障，安装的`win11`有许多的bug

卸载重新安装`node.js`

这次在安装界面，我多点了一个安装必要的工具选项。

本来想`win11`上有这么多的`BUG`,我都不想弄了，想着我还有一个固态硬盘，里面有`Ubuntu`的系统，可以用来做，但是好久没弄了，出现`Boot failed`的错误。（主引导有问题，之后在弄吧，装新版的系统玩一玩）

----

解决问题：安装本地博客环境

- 先卸载之前的安装
- 安装`node.js`

我尝试更换安装位置，但是出现如下错误，还是默认吧。

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog错误2.png)

- 解决办法：以**管理员身份运行cmd**

到如下这里都没有问题

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog错误3.png)

尝试“开飞机”。问题解决。

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog错误3解决.png)

运行成功。

![](https://scdxxm.oss-cn-shanghai.aliyuncs.com/img/blog初步展示.png)

把之前编辑的文件替换到这个里面。

- 直接替换，总是出错，所以这次小心，重新一个一个的设置。
- 还是找不出原因，因为要重新设置跟之前一样的博客太难了，所以这次做简单一点。

## 重新开始部署主题

因为之前的主题，我懒得在搞了，为了方便快捷，我换了个简单的主题。

### 前期的准备：
[博客主题教程1](https://blog.cofess.com/2017/04/09/hexo-builds-a-personal-blog-and-deploys-to-github.html)
[博客主题教程2](https://blog.cofess.com/2017/11/01/hexo-blog-theme-pure-usage-description.html)

#### RSS订阅

> 简易信息聚合是“Really Simple Syndication”或“Richsite summary”(网站内容摘要)的中文名字。是站点用来和其他站点之间共享内容的一种简易方式。

```
cnpm install hexo-generator-feed --save

在博客目录的_config.yml中添加如下代码
## feed   
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
```

#### sitemap站点地图

>网站地图，又叫站点地图，它就是一个列出了你网站上所有页面地址的清单文件，一般来说分为2种，一种是给搜索引擎看的，一种是给用户看的，前者帮助搜索引擎更好地收录你的网站，后者帮助用户更好的了解你的网站整体结构、更快的找到他们想要找的内容。

```
cnpm install hexo-generator-baidu-sitemap --save
cnpm install hexo-generator-sitemap --save
```

#### 替换主题

```
git clone https://github.com/cofess/hexo-theme-pure.git themes/pure
```

#### 安装插件

```
cnpm install hexo-wordcount --save
cnpm install hexo-generator-json-content --save
cnpm install hexo-generator-feed --save
cnpm install hexo-generator-sitemap --save
cnpm install hexo-generator-baidu-sitemap --save
```

#### 主题配置

- 这里都是根据主题的作者，改的，个人喜欢，没啥说的

#### 博客优化

```
cnpm install hexo-neat --save
====
在博客配置文件_config.yml中添加

# hexo-neat
neat_enable: true
neat_html:
  enable: true
  exclude:  
neat_css:
  enable: true
  exclude:
    - '*.min.css'
neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '*.min.js'
=======
cnpm install hexo-baidu-url-submit --save
cnpm install hexo-translate-title --save
```

### 安装hexo-renderer-markdown-it-plus插件

```
cnpm un hexo-renderer-marked --save
cnpm i hexo-renderer-markdown-it-plus --save
```

----

中间省略了，很多。上午的工作就到这吧，下午接着优化。

#### 优化

加入豆瓣书单和电影

解决办法：
先通过`node --version`查看一下当前nodejs的版本，
我使用的版本比较高，在github的issue中发现，采用12.18.x的版本或许可以，然后我重新安装了一下nodejs，然后重新`hexo douban -bgm`就ok了。

问题解决。



`hexo-autonofollow`
Github：https://github.com/liuzc/hexo-autonofollow

简介：自动为站外链接添加nofollow属性

安装：

`cnpm install hexo-autonofollow --save`
配置：

在站点配置文件`_config.yml`中添加

```
nofollow:
  enable: true
  exclude:
    - exclude1.com
    - exclude2.com
```



垃圾coding，部署不了，也没有解决办法

换github上了。在github上也不行。

我决定换到gitee上，把之前的博客删了，把位置腾出来

在上传gitee的时候，遇到一个问题记录一下：

```
问题：
提交后报如下异常:
$ git add .　　　　　　　　　　　　
warning: adding embedded git repository:xxxxxxxxxx
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint: git submodule add <url>xxxxxxxxxx
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint: git rm --cached   xxxx
hint:
hint: See "git help submodule" for more information.
原因：
即在本地初始化的仓库(使用 git init的文件夹) 中的某一个文件夹，也含有 .git 文件 。
```


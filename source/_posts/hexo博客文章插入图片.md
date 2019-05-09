---
title: hexo博客文章插入图片
date: 2019-04-29 15:15:29
categories: 折腾记录
copyright: true
tags:
  - hexo
---

# 前言

在撰写博客文章时，我们会向文章插入一些图片，但是hexo本身要插入图片比较麻烦，这边就可以使用hexo的一款插件，它可以让我们插入图片非常简单。

<!--more-->

# 如何安装

安装此插件很简单，你只需要在你的hexo目录下执行如下命令:

~~~shell
$ npm install hexo-asset-image --save
~~~

如果安装速度很慢可以把npm源改为国内源。

[点击打开npm源改为国内源的方法](https://evanmeek.github.io/2019/04/23/ManjaroLinux%E7%9A%84%E5%AE%89%E8%A3%85%E8%BF%87%E7%A8%8B/)

在设置镜像源->npm国内源下

# 如何使用

## 第一步
首先，我们得先设置主目录(博客目录)下的 **_config.yml** 文件.

找到 **post_asset_folder:** 项，将其修改为 **true**

## 第二步

使用也十分简单，hexo-asset-image可以时hexo在创建文章时自动在文章保存目录下创建一个同名的目录。

然后我们就可以把要插入的图片放入其目录，在文章中使用Markdown的插入图片语法即可。

# 栗子

~~~shell
$ hexo n "test"
$ mv test.jpg source/_posts/test
~~~

插入图片

~~~
![图片alt](图片地址)

# ![test](./test/test.jpng)
~~~

---
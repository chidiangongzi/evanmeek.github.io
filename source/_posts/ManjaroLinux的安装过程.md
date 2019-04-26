---
title: 'ManjaroLinux的安装过程'
date: 2019-04-23 16:37:18
categories: 学习笔记
tags:
  - Linux
  - 折腾
  - 软件使用
---

## 获取镜像
ManjaroLinux官方提供了多个桌面环境的镜像，分别是:
- XFCE 

特点

> 系统资源低耗，快速

- KDE

特点

> 高可定制化，消耗系统资源相比XFCE要大，开机时内存占用大概500MB+

- GNOME

特点

> 简单易用，可定制化，美化较为简单，内存占用大

并且ManjaroLinux在国内有4个镜像源可选，分别是:
- [清华大学](https://mirrors.tuna.tsinghua.edu.cn/manjaro-cd/)
- [中科大](http://mirrors.ustc.edu.cn/manjaro-cd/)
- [华为](https://mirrors.huaweicloud.com/manjaro-cd/)
- [浙江大学](http://mirrors.zju.edu.cn/manjaro/)

我们也可以直接使用官方的镜像源获取镜像[Manjaro](https://manjaro.org/get-manjaro/)

选择好自己要使用的桌面环境就可以开始制作启动盘了。

## 制作启动盘

**Windows:**

推荐使用[Rufus](https://github.com/pbatard/rufus/releases/download/v3.5/rufus-3.5.exe)进行制作启动盘。

下载好后直接选择镜像和要进行制作的U盘，选择开始。

**开始时会让你勾选制作方式请选择dd模式**

---

**Linux:**

只需要执行这几条命令

~~~shell
$ sudo lsblk #列出系统上的所有磁盘
~~~

找到大小磁盘大小跟你U盘差不多的那个磁盘名，一般来说都是**sdb或sda**

如果看到你的U盘对应的MOUNTPOINT有内容，就代表目前磁盘是被挂在了的，你就需要先取消挂载.

~~~shell
$ sudo umount /dev/sda* #这里的sda是你U盘的磁盘名，
~~~

取消挂载之后就可以进行格式化了.

~~~shell
$ sudo mkfs.vfat /dev/sda #注意这里没有*，并且同上一样sda是你的磁盘名.
~~~

格式化完成后，进入到你下载的镜像目录下，开始进行制作启动盘.

~~~shell
$ sudo dd bs=4M if=你的iso镜像路径 of=/dev/sda
~~~

如果终端内有一些返回信息，大概是xxMB/s这样的，就代表制作完成，可以关机已U盘启动了。

## 开始安装

## 系统美化

## 安装环境

## 使用体验总结

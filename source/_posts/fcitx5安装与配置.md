---
title: fctix5安装与配置
copyright: true
date: 2019-06-14 02:11:41
categories: 折腾日记
tags:
  - fcitx5
---

某天下午，我在Telegram群组里受人安利Fcitx5,今晚正好有空，所以就安装了个试试，还挺好的。

<!--more-->

![演示](fcitx5安装与配置/输入.gif)

所需安装的软件包:
  - fcitx5-git 输入法基础框架主程序
  - fcitx5-chinese-addons-git 简体中文输入的支持，云拼音
  - fcitx5-gtk-git gtk 程序的支持
  - fcitx5-qt4-git qt4 的支持
  - fcitx5-qt5-git qt5 的支持
可能还需要：
  - kcm-fcitx5-git 如果你用的是 KDE ，请装这个
  - fcitx5-rime-git 繁體中文輸入 RIME 中州韻輸入法引擎

如果你是KDE桌面环境可以直接使用kcm-fcitx5-git配置输入法:

![kcm](fcitx5安装与配置/kcm.png)

否则将改配置文件`~/.config/fcitx5/profile`

~~~
[Groups/0]
# Group Name
Name=Default
# Layout
Default Layout=us
# Default Input Method
DefaultIM=pinyin

[Groups/0/Items/0]
# Name
Name=keyboard-us
# Layout
Layout=

[Groups/0/Items/1]
# Name
Name=pinyin
# Layout
Layout=

[GroupOrder]
0=Default
~~~

__若没有`fcitx5`这个目录，则先打开一次fcitx5，再关闭，因为fcitx5关闭时会覆盖此文件。__

由于fcitx5不能自动启动，我们需要添加环境变量

将如下内容添加到`~/.xprofile`

~~~
fcitx5 &
~~~

然后再将如下内容添加到~/.pam_environment`，没有则创建

~~~
GTK_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx
QT_IM_MODULE=fcitx5
~~~

KDE用户可以直接在`系统设置模块-自动启动`设置

默认的皮肤很丑，我们可以使用这个[fcitx5-simple-theme](https://github.com/iovxw/fcitx5-simple-theme)

然后你就可以把fcitx4给删了...




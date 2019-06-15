---
title: 解决KDE下部分应用不能使用fcitx中文输入法的问题
copyright: true
date: 2019-05-19 15:56:33
categories: 学习笔记
tags:
 - Linux
 - KDE
---

我有两台设备，都是KDE5-Plasma桌面，但是其中一台可以完美使用中文输入法，另外一台则不可以，为了解决这个问题，便有这篇文章。

<!--more-->

*********** 本教程使用fcitx输入法框架。**************

# 第一步

首先安装一些必要的软件:

~~~shell
$ sudo pacman -S fcitx fcitx-im fcitx-configtool fcitx-googlepinyin
~~~

# 第二步

安装完成后编辑:**/etc/environment**文件，加上如下内容:

~~~shell
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
~~~

# 第三步

注销当前会话，配置输入法为googlepinyin即可使用。


> [本文参考](https://code-insight.xyz/manjaro%E6%96%B0%E6%89%8B%E5%BF%AB%E9%80%9F%E8%A3%85%E9%85%8D%E6%8C%87%E5%8D%97/)

---

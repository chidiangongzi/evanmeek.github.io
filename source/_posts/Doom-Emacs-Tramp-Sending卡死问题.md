---
title: Doom Emacs Tramp Sending卡死问题
copyright: true
date: 2020-01-22 10:13:12
categories: 折腾日记
tags: Emacs
---

在使用DoomEmacshttps://github.com/bbatsov/prelude/issues/594的 sudo-thin-file函数时出现不能输入密码的解决方案。
<!--more-->

# 遇到的问题 

> 使用 sudo-this-file函数出现:

``` emacs-lisp
Tramp: Sending Password
```


# 原因

原因是因为projectile占用了minibuffer，当Tramp试图请求输入密码时就会出现问题。

# 解决方案

我在这个Issue找到的[解决方案](https://github.com/bbatsov/prelude/issues/594 "外
部链接->Github")

我是在`Domm Emacs`的`config.el`里加上下面代码:

``` emacs-lisp
(projectile-global-mode)
(set projectile-mode-line " Projectile")
```

> TG群里的Citreu还说可以设置~/.authinfo解决，这样好像更加安全。

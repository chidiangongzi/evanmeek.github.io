---
title: Mac下安装Rust
copyright: true
date: 2019-08-20 02:30:40
categories: 学习笔记
tags: Rust
---

本篇文章记录了我是如何在Mac下安装rust的过程.

<!--more-->

首先在你Shell的配置文件内加入下面两行:

~~~
export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
~~~

然后打开终端，输入:

~~~
curl https://sh.rustup.rs -sSf | sh
~~~

中间稍微等待一下，选择安装的方式即可。

安装好后记得执行:

~~~
source $HOME/.cargo/env
~~~

最后再编辑$HOME/.cargo/config文件

~~~
[registry]
index = "https://mirrors.ustc.edu.cn/crates.io-index/"
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "https://mirrors.ustc.edu.cn/crates.io-index/"
~~~
就大功告成啦，赶快写一个HelloWorld吧!

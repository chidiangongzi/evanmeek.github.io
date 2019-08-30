---
title: 终端多窗口神器——Screen
date: 2019-05-09 16:56:08
categories: 折腾日记
tags:
  - Linux
  - 软件折腾
copyright: true
---

曾几何时，在你使用ssh登录到服务器时要做某个需要点时间的操作时感到烦恼。

曾几何时，在你想要在终端进行多窗口控制时，感到十分麻烦。

有了Screen,你就可以获得更好的使用终端多窗口的体验。

<!--more-->

我想你肯定遇到以下几种情况:

- ftp传输

- 系统备份

- 长时间运行任务

好的，以上的这几种情况在你关掉窗口或断开链接时，任务将会被杀死，一切都没了...只能重新来过。

# 凶手 SIGHUP 信号

> 以下资料来自维基百科 
>> SIGHUP又称为Unix信号，它是Unix、类Unix以及其他POSIX兼容的操作系统种进程间通讯的一种有限制的方式。它是一种异步的通知机制，用来提醒进程一个事件已经发生。当一个信号发送给一个进程，操作系统中断了进程正常的控制流程，此时，任何非原子操作都将被终端。如果进程定义了信号的处理函数，那么它将被执行，否则就执行默认的处理函数。

简单来说呢，这个SIGHUP信号就是Unix信号，它可以通过控制终端以一些特殊的按键发送某些特定的信号，这些信号有特定的功能，不过都是用来处理进程的。

## 发送信号

在一个已运行程序的终端可键入以下组合键从而实现发送某些信号。

- Ctrl-C发送INT信号(SIGINT); 缺省情况下，会导致进程终止。

- Ctrl-Z发送TSTP信号(SIGTSTP); 缺省情况下，会导致进程挂起。

- Ctrl-\发送QUIT信号(SIGQUIT); 缺省情况下，会导致进程终止并且将内存中的信息存储到硬盘。

## 前因后果

相信大家每次要终止当前正在运行的进程都是键入组合键Ctrl-C，也就是说触发了一个SIGHUP信号————SIGINT，也就导致了进程终止。

**更多有关SIGHUP信号的资料，我会在后面的文章进行更新。**

---

# 开始使用Screen

先简单说说什么是Screen:

Screen是一个可以在多个进程之间多路复用一个物理终端的窗口管理器。(吃不吃惊，居然是个窗口管理器)。

Screen就像tty一样，可以创建多个会话，然而会话还可以创建多个screen窗口，并且每个screen都跟真实SSH/Telnet连接窗口一样。

**1.创建一个screen窗口**

~~~shell
[evanmeek@Evan-PC]# screen
~~~

这样就创建了一个可执行shell程序的窗口，若在该窗口种键入exit则退出该窗口，又倘若该窗口是当前会话的唯一窗口，screen则会退出该会话，否则screen将会自动切换到前一个窗口。

**2.创建窗口+执行命令**

~~~shell
[evanmeek@Evan-PC]# screen vim 
~~~

screen会先创建一个窗口，并且执行vim命令，若你退出vim，则该窗口也会退出。

**3.一个窗口中再有一个窗口中再有一个窗口中...**

你可以打开一个窗口后再输入命令打开一个窗口，也可以通过组合键C-a c(CTRL+a再按c)，screen会和段话所描述的功能一样。

**4.screen的暂时断开(detach)和重新链接(attach)**

比如在screen窗口下用vim编辑C++源文件

~~~shell
[evanmeek@Evan-PC]# screen vim test.cpp 
~~~

但写到一半，你发现要修改点东西，但是又不想退出vim编辑器，那么直接键入C-a d，Screen会提示你已挂起(detached).

![挂起提示](终端多窗口神器——Screen/detachedInfo.png)

当你做完其他事你就可以找回该会话，进行重新连接:

找到会话

~~~shell
[evanmeek@Evan-PC]# screen -ls
There are screens on:
        17944.pts-4.EvanLinux   (Detached)
        14290.server    (Detached)
2 Sockets in /run/screens/S-evanmeek.
~~~

重新连接

~~~shell
[evanmeek＠Evan-PC]# screen- r 17944
~~~

这样就可以恢复pts这个会话的窗口了．

---

# 配置你的Screen

前面的几个组合键操作，可以 ，我们总是通过C-a来做开始触发的命令.screen中这个叫做按键绑定，而被绑定的C-a叫做命令字符.

可通过如下键绑定查看所有键绑定．

**C-a ?**

常用的键绑定有：

|键绑定|描述|
|:---:|:---:|---|
|C-a ?|显示所有键绑定信息|
|C-a w|显示所有窗口列表|
|C-a C-a|切换到之前显示的窗口|
|C-a c|创建一个新的运行shell的窗口并切换到该窗口|
|C-a n|切换到下一个窗口|
|C-a p|切换到前一个窗口|
|C-a 0~9|切换到0~9窗口|
|C-a a|发送C-a到当前窗口|
|C-a d|暂时断开screen会话|
|C-a k|杀掉当前窗口|
|C-a [|进入拷贝/回滚模式

我们可以自己设置命令字符，使用C-a ?命令可见， 缺省的命令字符为C-a，而转义字符为a;

![默认的命令字符](终端多窗口神器——Screen/DefalutCommandKey.png);

我们可以修改它，通过如下格式:

**-exy**

x:命令字符

y:转义字符

~~~shell
[evanmeek@Evan-PC]# screen -e^oo
~~~

这样原本需要使用Ｃ-a a 执行的操作就需要使用C-o o来执行．

---
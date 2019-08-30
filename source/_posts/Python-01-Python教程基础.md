---
title: '[Python-01]Python教程基础'
copyright: true
date: 2019-08-29 00:25:46
categories: Python
tags:
 - Python系列
---

Python系列第一章笔记，查看Python系列所有文章,请点击 [💿](https://evanmeek.github.io/Python/)
<!--more-->

# 编程语言是什么

编程语言中的每个结构，都有固定的使用格式（称之为`语法`)以及精确的含义（称之为`语义`）。

编程语言也分等级，例如C、C++、Java、Ruby等可以称为高级语言，而计算机`硬件`只能理解一种非常低级的编程语言，`机器语言`。

# 解释型语言和编译型语言（两者区别）

> 编译型语言

编译型语言是指使用专门的编译器，对特定的操作系统（平台）将源代码一次性“翻译”为可被该操作系统（平台）硬件所执行的机器语言。

优点：
 - 编译好后的可执行文件，可以在没有编译器的机器上独立运行。
 - 程序执行速度快

缺点：
 - 跨平台不友好(如果是不同的平台，需要将源代码在特定的平台重新编译，甚至需要修改代码)

> 解释型语言

解释型语言由解释器完成将源代码转换成机器语言，在任何平台上必须安装解释器才可以运行，而不同的平台只需要安装解释器，代码不需要修改也可以被解释。

优点：

 - 跨平台友好

缺点：

 - 执行速度慢

# Python是什么，Python简介

> Python历史

1989年，荷兰人`Guido van Rossum` 创造了Python.

`Python`最初基于`ABC`教学语言.

> Python简介

`Python`可以和其他语言，如C、C++、Java的模块（方法/函数）轻松的结合在一起，因此`Python`又被称为“胶水”语言。

> Python的设计哲学

优雅、明确、简单。

有些人说：“人生苦短，我用Python”

# Python的特点（优点和缺点）

> 简单易学

Python虽然语法格式要求严格，但是语法却很简洁。

> 开源

Python是开源的，使用Python编写的程序可以做商业用途也不用付费，并且可以让第三方开发者为Python开发提供优秀的功能。

> 高级语言

在使用Python编写程序时，开发者无需考虑底层细节问题，而专注于编写程序。

> 解释型语言

可移植性优秀

> 面向对象

Python既支持面向过程编程，也支持面向对象编程。

> 强大的功能

Python可以从简单的字符串处理到复杂的3D图形编程，这些借助Python的扩展模块可以轻松完成。

> 可扩展性

Python具有脚本语言中最丰富和强大的类库，不管是I/O、GUI、网络编程、数据库编程等绝大部应用场景，都可以使用Python内置的类库完成。

Python可以使用C或C++编写的代码，这样可以一定程度上的弥补执行速度慢的缺点。

> 缺点

速度慢，相比Java、C、C++编写的程序，运行效率都要慢。
源代码加密困难，由于是解释型语言，不像编译型语言那样会被编译成各种目标程序，所以加密困难。

# 学Python，不需要有编程基础

Python语法简明易懂，不像C++或C语言等语法复杂，并且在学习Python中也不需要太过于专注底层的细节，很多事情解释器都已经帮忙做好了。所以对于零基础的初学者来说，Python非常合适。

# Python能干什么，Python的应用领域

> Web应用开发

Python可以通过一些模块，使Python具备HTTP服务器与Python的Web程序之间的通信。

全球最大的搜索引擎`Google`，在其搜索系统中就大量的使用Python。

`豆瓣`也是由Python编写的。

> 操作系统管理、自动化运维开发

大部分操作系统中，Python都作为标准的系统组件，例如大多数Linux发行版，BSD系、Mac OS X都集成了Python。

并且相对于Shell脚本来说，无论是可读性、性能、代码重用度以及扩展性方面都要优秀很多。

> 游戏开发

虽说Python的运行效率不算快，但很多游戏可以用C++编写高性能模块，而用Pyton编写游戏的逻辑。

例如，`文明`这款游戏就是使用Python实现的。

> 编写服务器软件

由于Python对各种网络协议的支持完善，所以经常被用于编写服务器软件以及网络爬虫。

> 科学计算

Python内置了很多工具，可以让科研人员编写科学计算程序。

# 怎样学习Python，才能成为Python高手？

> 编程语言都是相通的

如果你具备一定的编程基础，接触一门新的编程语言时会发现，不同的编程语言其实是相通的，大多数不同的地方在于语法规则。

> Python对初学者友好

- 多实践、积累代码量

  任何编程语言知识都是大量的，如果不在学习编程时就开始练习，那么可能当你学完素有的语法后，却把前面的知识忘得一干二净。

  所以，学习编程，需要多写代码，没有途径可走。

- 时刻注意代码规范

  在我们学习时，一定要养成良好的编程习惯，例如适当的编写注释，定义变量名称时不要随意使用无意义的字符。

- 开发经验必不可少

当你熟练的掌握一门编程语言的语法时，你还需要大中型产品的开发经验，它会让你学得更多，简而言之站得更高，看得更远。

![Python知识体系图](Python-01-Python教程基础/Python知识体系框架.png)

# Python 2.x和Python 3.x，初学者应该如何选择？

推荐选择Python 3.x，因为Python将在2020不再更新Python 2.x，并且Python 3.x比Python 2.x 具有更多的特性与功能。

这里只是推荐，详细看Python3和Python2的区别可以看这本:[📖《Python3和Python2的区别》](http://c.biancheng.net/view/4147.html)

# Python版本区别，Python3和Python2区别详解

学习完基础再来...暂时未编写😅

不过可以知道的是，Python3相比与Python2在`语句输出、编码、运算和异常等`方面做出了调整。

# Python2to3 自动将Python2.x代码转换成Python3.x代码

学习完基础再来...暂时未编写😅

学完完基础再来...暂时未编写

# Python PEP 及时追踪Python最新变化

为了追踪Python的更新动态，我们需要借助Python PEP 文档

> Python PEP文档

Python语法修改方案是由`邮件列表`的形式进行讨论，但Python的PEP文档发布了，新的变化才会生效。

`PEP(Python Enhancement Proposal)`，中译为`Python改进方案`。它主要由三个用途

- 通知: 汇总Python核心开发者重要信息

- 标准化: 提供代码风格，文档或者其他指导意见

- 设计: 对提交的新功能进行说明

如果想要查看提交的`PEP`历史，可以点击这里:[PEP0文档](https://www.python.org/dev/peps/)

# Python底层是用什么语言实现的

大多数讨论的Python，所指的是CPython，它是用C语言编写的。

不仅有用C语言编写的Python也有用其他语法编写的Python。

不同语言实现Python的的原因，大部分是为了解决某些实际问题而创建的，例如：

- 在嵌入式系统中运行Python代码

- 在运行框架(Java/.NET)或其他语言做代码集成。

- 在Web浏览器中运行Python代码

以上所述使用CPython需要花费开发者大量精力也很难实现，所以才有了各种实现方式的Python.

> Stackless Python

`Stackless Python`自称为Python增强版，它没有依赖C语言的调用栈。

其新添加的功能最重要的是:解释器管理的微线程

支持版本是2.7.9和3.3.5，Stackless Python的所有额外功能都是内置stackiess模块内的框架。

> JPython

由Java实现的Python。它将代码编译为Java字节码，开发者可以在Pyton模块中无缝使用Java类

JPython与CPython的主要区别:

- 真正的Java垃圾回收机制

- 没有`全局解释器锁(GlobalInterpreter Lock,GIL)`，在多线程应用中可以充分利用多个内核

支持版本: 2.7

缺点: 缺少对C/Python扩展API的支持，预计JPython3.x支持C/Python扩展API

> IronPython

IronPython将Python引入至.NET框架中。

支持版本: 2.7.5

缺点: 类似JPython

相比于CPython的优点:

- 没有全局解释器锁

- 用.NET语言家族编写的代码可以轻松集成到IronPython中，反之亦然。

- 通过`Silverlight`，在所有主流Web浏览器中都可运行。

> PyPy

社区内呼声最高的Python实现，它是由Python重写的Python。

支持版本: 2.7完全兼容,PyPy3与3.25完全兼容

PyPy与CPython实现的主要区别:

- 使用垃圾回收

- 集成跟踪JIT编译器，可以提高性能

- 借鉴Stackless Python在应用层的无栈特性。

缺点: 对C/Python扩展API不完善，但为CPyExt子系统C扩展提供了某种程度的支持。

# 了解Jupyter Notebook，你已然超越了90%的Python程序员

简单介绍下，Jupyter Notebook就是个整合了代码、计算输出、解释文档、多媒体资源的多功能科学运行平台。

去看原文吧，这个知道有这个东西，以后再去学习。

[💿原文传送门](http://c.biancheng.net/view/5279.html)

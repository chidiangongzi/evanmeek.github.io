---
title: '[Python-06]Python流程控制'
copyright: true
date: 2019-09-28 14:14:26
categories: Python
tags:
  - Python系列
---

Python中的流程结构也就是选择语句，选择语句又分为3种语法形式，分别是if、if else、if elif else。

if 语句语法格式:

```
if 表达式:
  代码块
```
if else 语句语法格式:

```
if 表达式:
  代码块 1
else:
  代码块 2
```

if elif else 语句语法格式:

```
if 表达式1:
  代码块 1
elif 表达式2:
  代码块 2
elif 表达式3:
  代码块 3
...
else:
  代码块 n
```

以上三种选择结构的语法形式差别不大，它们有个共性，就是**当表达式的值为True时会执行代码块内的代码** 。

选择语句的表达式相当于条件，当表达式的条件满足后，就会执行代码块内的代码啦。

**注意:Python的代码块是通过缩进标记的，具有相同缩进的多行代码属于同一个代码块** .

**if表达式真假值得判断方法** 

表达式可以是任意类型，不过下面的几种类型将会被Python解释器当做False处理:

`Flase、None、0、""、()、[]、{}` 

# Python if else语句用法范例(注意事项_)



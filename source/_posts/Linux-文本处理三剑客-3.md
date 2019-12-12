---
title: Linux-文本处理三剑客-3
copyright: true
date: 2019-12-12 17:07:28
categories: Linux系列
tags:
  - Linux
---

# 4.1 grep: 文本过滤工具

## 命令详解

功能说明

grep命令可以从文本文件或管道数据流中筛选匹配的行或数据，还可以配合正则表达式一起
使用。

语法格式

```shell
grep [参数] [匹配模式] [需要查找的文件]
```

选项说明

| 参数选项     | 解释说明                         |
|--------------|----------------------------------|
| -v           | 排除某行                         |
| -n           | 显示匹配行及行号                 |
| -i           | 不区分大小写                     |
| -c           | 统计匹配行数                     |
| -E           | 使用egrep命令替代grep            |
| --color=auto | 为grep过滤后匹配的字符串添加颜色 |
| -w           | 只匹配过滤的单词                 |
| -o           | 只输出匹配的内容                 |

## 使用范例

1. 基础范例

使用grep过滤不包括evanmeek字符串的行(-v参数实践)

```shell
➜   cat test.txt 
China
Japan
root
EvanMeek
MyBlog
evanmeek

➜   grep -v "evanmeek" test.txt
China
Japan
root
EvanMeek
MyBlog
```

*提示:* grep命令-v参数正如刚刚输出所示，会将过滤参数后的内容。

使用grep过滤包括evanmeek字符串的行，并显示其所在行行号(-n实践)

```shell
# 文本内容相同，我们使用下面这条命令，看看会发生什么
➜   grep -n "evanmeek" test.txt 
# 我们得到了test.txt中包含evanmeek的行且行号。

# 我们也可以使用.匹配任意内容，相当于看test.txt文件内容加上行号
➜   grep -n "." test.txt 
1:China
2:Japan
3:root
4:EvanMeek
5:MyBlog
6:evanmeek
6:evanmeek
```

不区分大小写参数实践

```shell
# grep在过滤时可以选择忽略区分大小写，默认是区分的
# 文件内容相同,使用-i参数忽略大小写，-n参数选择要筛选的内容并有行号
➜   grep -i -n "evanmeek" test.txt
4:EvanMeek
6:evanmeek
```

计算匹配的字符串的数量(-c参数实践)

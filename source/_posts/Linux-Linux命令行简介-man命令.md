---
title: Linux-Linux命令行简介-man命令
copyright: true
date: 2019-06-15 18:31:17
categories: Linux系列
tags:
 - Linux
---

本篇文章为Linux系列的第1章 Linux命令行简介 1.2小节的外部展示。

<!--more-->

# 1.2.1 使用man获取命令帮助信息

man命令的作用:
  
  - 查看命令的使用帮助

  - 查看软件服务配置文件

  - 查看系统调用信息

  - 查看C库函数帮助信息

man命令的使用:
  
  ~~~Shell
  man 参数选项 命令/文件
  ~~~

man命令可选参数:

  |参数|英文说明|中文说明|
  |:--:|:------:|:------:|
  |1|User Commands|用户命令相关|
  |2|System Calls|系统调用相关|
  |3|C Library Functions|C的库函数相关|
  |4|Devices and Special Files|设备与特殊文件相关|
  |5|File Formats and Conventions|文件格式和规则|
  |6|Games et. Al.|游戏及其他|
  |7|Miscellanea|宏，包及其他杂项|
  |8|System Admin tools and Deamons|系统管理员命令和进程|

  例子:
  
  ~~~Shell
  # 查看cp命令的使用帮助
  man cp
  # 查看C语言printf函数的使用帮助
  man 3 printf
  ~~~

man命令信息的格式

  |标签|说明(`!`表示重点)|
  |:--:|:---------------:|
  |NAME|命令说明及介绍`!`|
  |SYNOPSIS|命令的基本使用语法`!`|
  |DESCRIPTION|命令的详细描述，有的命令会单独使用标签介绍COMMANDS LINE OPTION或OPTIONS`!`|
  |OPTIONS|命令参数选项说明|
  |COMMANDS|执行某个软件时可附加的软件的命令|
  |FILES|程序涉及的相关文件|
  |EXAMPLES|命令的例子`!`|
  |SEE ALSO|命令相关信息的说明|
  |BUGS(REPORTING BUGS)|命令对应缺陷问题的描述|
  |COPYRIGHT|版权信息相关声明|
  |AUTHOR|作者介绍|

man命令信息操作键

  |操作键|功能说明|
  |:----:|:------:|
  |Page Down|向下翻页|
  |Page Up|向上翻页|
  |Home|跳转到第一页|
  |End|跳转到最后一页|
  |/|向下查找某个字符|
  |?|向上查找某个字符|
  |n,N|当使用向上查找，那么n则为下一个，N为上一个。当使用向下查找，那么则取反|
  |q|结束本次man帮助|


---
title: Linux-文件和目录操作命令-1
copyright: true
date: 2019-06-16 15:56:11
categories: Linux系列
tags:
  - Linux
---

# 2.1 pwd命令

  `print working diretory`

  查看当前路径使用`pwd`命令

  例子:

  ~~~shell
  [evanmeek@EvanLinux ~]$ pwd
  ~~~

  输出结果

  ~~~Shell
  /home/evanmeek
  ~~~

  |选项|说明|
  |:------:|:--:|
  |-L|显示当前目录的逻辑路径(忽略软链接文件)|
  |-P|显示当前目录的物理路径(若有软链接则显示源文件地址)|

  所谓的软链接相当于快捷方式，例如`~/test.txt`是`/test.txt`的软链接，那么我们操作`~/test.txt`等同于操作`/test.txt`，详细的软链接将会在后面的`ln`命令讲解。

# 2.2 cd 切换目录

  `change directory`

  进入某个目录使用`cd`命令

  例子:

  ~~~shell
  [evanmeek@EvanLinux ~]$ pwd
  [evanmeek@EvanLinux ~]$ cd /etc/sysctl.d/
  [evanmeek@EvanLinux /etc/sysctl.d/]$ pwd
  ~~~

  输出结果

  ~~~
  /home/evanmeek/
  /etc/sysctl.d/
  ~~~
  
  |选项|说明|
  |:------:|:--:|
  |-P|进入目录的物理路径|
  |-L|进入目录的逻辑路径|
  |-|进入上次的目录|
  |~|进入系统环境变量的`HOME`目录路径，即当前登录用户的家目录`|
  |..|进入父目录|

  `cd` 命令如果不带任何选项和路径的话，会进入当前登录用户的家目录.

  例子:

  ~~~Shell
  [evanmeek@EvanLinux ~]$ cd Desktop
  [evanmeek@EvanLinux ~/Desktop]$ pwd
  [evanmeek@EvanLinux ~]$ cd -
  [evanmeek@EvanLinux ~]$ pwd
  [evanmeek@EvanLinux ~]$ cd /etc/systemd/
  [evanmeek@EvanLinux /etc/systemd/]$ pwd
  [evanmeek@EvanLinux /etc/systemd/]$ cd ..
  [evanmeek@EvanLinux /etc/]$ pwd
  ~~~

  输出结果

  ~~~shell
  ~/Desktop/
  ~
  /etc/systemd/
  /etc/
  ~~~

# 2.3 tree以树形结构显示目录下的内容

  树形结构可以很清晰的显示出目录的父子级关系。

  例子:

  ~~~
  [evanmeek@EvanLinux ~/test]$ tree -L 1
  ~~~

  输出结果

  ~~~
  .
  ├── dir1
  │   ├── dir1_1
  │   └── dir2_2
  └── dir2
      ├── dir1_1
      └── dir2_2

  6 directories, 0 files
  ~~~

  |选项|说明|
  |:--:|:--:|
  |-a|显示所有文件包括隐藏文件|
  |-d|只显示目录`!`|
  |-f|显示每个文件的绝对路径|
  |-i|不显示树枝|
  |-L levelNum|显示遍历目录的层级，levelNum为层级(数字)|
  |-F|显示时根据不同文件类型在文件名结尾处显示不同的符号|

  例子:

  显示隐藏文件 
  ~~~
  #假设此目录下有隐藏文件
  [evanmeek@EvanLinux ~/tmp]$ tree -a
  ~~~

  输出结果

  ~~~
  .
  ├── dir1
  │   ├── dir1_1
  │   └── dir2_2
  ├── dir2
  │   ├── dir1_1
  │   └── dir2_2
  ├── .file1
  └── .file2

  6 directories, 2 files
  ~~~

  例子:

  显示1级层文件完整路径，并不显示树枝
  ~~~
  [evanmeek@EvanLinux ~/tmp]$ tree -L 1 -fi .
  ~~~

  输出结果

  ~~~
  .
  ./dir1
  ./dir2
  ~~~

# 2.4 mkdir创建目录

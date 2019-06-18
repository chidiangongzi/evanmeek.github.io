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

  __查看当前路径使用`pwd`命令__

  例子:

  ~~~shell
  [evanmeek@EvanLinux ~]$ pwd
  ~~~

  输出信息

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

  __进入某个目录使用`cd`命令__

  例子:

  ~~~shell
  [evanmeek@EvanLinux ~]$ pwd
  [evanmeek@EvanLinux ~]$ cd /etc/sysctl.d/
  [evanmeek@EvanLinux /etc/sysctl.d/]$ pwd
  ~~~

  输出信息

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

  输出信息

  ~~~shell
  ~/Desktop/
  ~
  /etc/systemd/
  /etc/
  ~~~

# 2.3 tree以树形结构显示目录下的内容

  __树形结构可以很清晰的显示出目录的父子级关系__

  例子:

  ~~~
  [evanmeek@EvanLinux ~/test]$ tree -L 1
  ~~~

  输出信息

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

  输出信息

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

  输出信息

  ~~~
  .
  ./dir1
  ./dir2
  ~~~

# 2.4 mkdir创建目录

  `make directory`

  __创建目录使用`mkdir`命令__

  |选项|说明|
  |:--:|:--:|
  |-p|递归创建目录，若目录已存在不会报错|
  |-m|创建时指定目录的权限|
  |-v|创建时显示过程信息|

  例子:

  创建目录时显示信息
  ~~~
  [evanmeek@EvanLinux ~]$ mkdir -v testDir
  [evanmeek@EvanLinux ~]$ cd testDir
  [evanmeek@EvanLinux ~/testDir]$ pwd
  ~~~

  输出信息:

  ~~~
  mkdir: 已创建目录 'testDir'
  ~~~

  递归创建目录并且显示信息

  ~~~
  [evanmeek@EvanLinux ~]$ mkdir -pv father/son/test
  ~~~

  输出信息:

  ~~~
  mkdir: 已创建目录 'father'
  mkdir: 已创建目录 'father/son'
  mkdir: 已创建目录 'father/son/test'
  ~~~

  创建目录并且指定目录权限

  ~~~
  [evanmeek@EvanLinux ~]$ mkdir -m 333 -v testDir
  [evanmeek@EvanLinux ~]$ ls -ld testDir
  ~~~

  输出信息:

  ~~~
  mkdir: 已创建目录 'testDir'
  d-wx-wx-wx 2 evanmeek evanmeek 4096  6月 17 20:15 testDir
  ~~~

  利用特殊符号“{}”同时创建多目录及多子目录

  ~~~
  [evanmeek@EvanLinux ~]$ mkdir -pv father/{son1/{a1,a2},son2/{b1,b2},son3/{c1,c2}}
  [evanmeek@EvanLinux ~]$ tree father
  ~~~

  输出信息:

  ~~~
  mkdir: 已创建目录 'father'
  mkdir: 已创建目录 'father/son1'
  mkdir: 已创建目录 'father/son1/a1'
  mkdir: 已创建目录 'father/son1/a2'
  mkdir: 已创建目录 'father/son2'
  mkdir: 已创建目录 'father/son2/b1'
  mkdir: 已创建目录 'father/son2/b2'
  mkdir: 已创建目录 'father/son3'
  mkdir: 已创建目录 'father/son3/c1'
  mkdir: 已创建目录 'father/son3/c2'

  father
  ├── son1
  │   ├── a1
  │   └── a2
  ├── son2
  │   ├── b1
  │   └── b2
  └── son3
      ├── c1
      └── c2

  9 directories, 0 files
  ~~~

# 2.5 touch创建空文件或改变文件的时间戳属性

  __创建新的空文件，改变文件的时间戳属性，需要用到touch__

  |选项|说明|
  |:--:|:--:|
  |-a|更改指定文件的最新访问时间|
  |-d STRING|用字符串的方式指定一个模板作为指定文件的时间属性|
  |-m|更改指定文件的最新修改时间|
  |-r file|将指定文件的时间属性设置为file的时间属性|
  |-t STAMP|使用时间格式设置文件的时间属性|

  例子:

  创建文件

  ~~~
  [evanmeek@EvanLinux ~]$ touch test.txt
  ~~~

  同时创建多个文件

  ~~~
  [evanmeek@EvanLinux ~]$ touch test1.txt test2.txt
  ~~~

  利用{}批量创建文件

  ~~~
  [evanmeek@EvanLinux ~]$ touch t{01..05}.txt
  ~~~

  利用`stat`命令查看时间戳

  ~~~
  [evanmeek@EvanLinux ~]$ stat t01.txt
  ~~~

  输出信息

  ~~~
  File: t01.txt
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
  Device: 10305h/66309d   Inode: 18352077    Links: 1
  Access: (0644/-rw-r--r--)  Uid: ( 1000/evanmeek)   Gid: ( 1000/evanmeek)
  Access: 2019-06-17 21:36:42.380004039 +0800
  Modify: 2019-06-17 21:36:42.380004039 +0800
  Change: 2019-06-17 21:36:42.380004039 +0800
  Birth: 2019-06-17 21:36:42.380004039 +0800
  ~~~

  __时间戳属性说明:__

  - Access 访问属性

  - Modify 修改属性

  - Birth 状态改变属性

  利用-a选项修改文件最后访问属性

  ~~~
  [evanmeek@EvanLinux ~]$ touch -a t01.txt
  [evanmeek@EvanLinux ~]$ stat t01.txt
  ~~~

  输出信息

  ~~~
  File: t01.txt
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
  Device: 10305h/66309d   Inode: 18352077    Links: 1
  Access: (0644/-rw-r--r--)  Uid: ( 1000/evanmeek)   Gid: ( 1000/evanmeek)
  Access: 2019-06-17 21:44:27.210736590 +0800
  Modify: 2019-06-17 21:36:42.380004039 +0800
  Change: 2019-06-17 21:44:27.210736590 +0800
  Birth: 2019-06-17 21:36:42.380004039 +0800
  ~~~

  修改文件的修改时间

  ~~~
  [evanmeek@EvanLinux ~]$ touch -d 20010101 t01.txt
  [evanmeek@EvanLinux ~]$ stat t01.txt
  ~~~

  输出信息

  ~~~
  File: t01.txt
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
  Device: 10305h/66309d   Inode: 18352077    Links: 1
  Access: (0644/-rw-r--r--)  Uid: ( 1000/evanmeek)   Gid: ( 1000/evanmeek)
  Access: 2001-01-01 00:00:00.000000000 +0800
  Modify: 2001-01-01 00:00:00.000000000 +0800
  Change: 2019-06-17 21:48:26.700992172 +0800
  Birth: 2019-06-17 21:36:42.380004039 +0800
  ~~~

  修改指定文件为某文件的时间属性

  ~~~
  [evanmeek@EvanLinux ~]$ stat t02.txt
  [evanmeek@EvanLinux ~]$ touch -r t02.txt t01.txt
  [evanmeek@EvanLinux ~]$ stat t01.txt
  ~~~$ stat t01.txt

  输出结果

  ~~~
  File: t01.txt
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
  Device: 10305h/66309d   Inode: 18352077    Links: 1
  Access: (0644/-rw-r--r--)  Uid: ( 1000/evanmeek)   Gid: ( 1000/evanmeek)
  Access: 2019-06-17 21:36:42.380004039 +0800
  Modify: 2019-06-17 21:36:42.380004039 +0800
  Change: 2019-06-17 21:51:35.907031392 +0800
  Birth: 2019-06-17 21:36:42.380004039 +0800
  ~~~

# 2.6 ls显示目录下的内容及相关属性信息

  `list directory contents`

  例子:

  查看当前目录下的文件信息

  ~~~
  [evanmeek@EvanLinux ~]$ ls
  ~~~

  输出结果

  ~~~
  Applications  Desktop  Downloads  GameDir  index.html  Music  Pictures  temp  WorkDir
  ~~~

  每个人的目录里面的内容不同，所以可能不一样。

  |选项|说明|
  |:--:|:--:|
  |-l|使用长格式列出目录下的文件和信息|
  |-a|显示目录下的所有文件，包括隐藏文件`!`|
  |-t|根据最新的修改时间排序，不加此参数默认是根据文件名排序`!`|
  |-r|反向排序|
  |-F|在显示的条目后加上特殊符号用以区别文件类型`!`|
  |-p|目录后面加上“/”|
  |-i|显示inode节点信息|
  |-d|遇到目录时，只列出目录本身，并且不跟随符号链接`!`|
  |-h|以人类可读的信息显示文件或目录大小|
  |-A|列出所有文件，包括隐藏文件夹，但不包括.和..|
  |-S|根据文件大小排序|
  |-R|递归列出所有子目录|
  |-x|逐行列出项目而不是逐栏列出|
  |-X|根据扩展名排序|
  |-c|根据状态改变时间排序|
  |-u|根据最后访问时间排序|
  |--color={never,always,auto}|根据文件类型显示不同颜色，never:不显示，always:总是显示，auto:表示自动显示|
  |--full-time|以完整的时间格式进行显示|
  |--time-style={full-iso,long-iso,iso,locale}|以不同的时间格式输出，long-iso最常用
  |--time={atime,ctimeA}|按不同的时间属性输出,atime:访问时间，ctime:改变权限属性时间，默认:最后修改时间

  例子:

  环境准备

  ~~~
  [evanmeek@EvanLinux ~]$ mkdir temp
  [evanmeek@EvanLinux ~]$ cd temp
  [evanmeek@EvanLinux ~]$ mkdir dir/{dir1..dir3}
  [evanmeek@EvanLinux ~]$ touch dir/{dir1..dir3/{txt1..txt3}}
  ~~~

  利用-a显示所有文件并显示详细信息

  ~~~
  [evanmeek@EvanLinux ~/WorkDir/MyBlog/]$ ls -a 
  ~~~

  输出信息
  
  ~~~
  ~~~

   

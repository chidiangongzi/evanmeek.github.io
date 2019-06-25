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
  |----|----------------------------------------------------|
  | -L | 显示当前目录的逻辑路径(忽略软链接文件)             |
  | -P | 显示当前目录的物理路径(若有软链接则显示源文件地址) |

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
  
  | 选项 | 说明                                                      |
  |------|-----------------------------------------------------------|
  | -P   | 进入目录的物理路径                                        |
  | -L   | 进入目录的逻辑路径                                        |
  | -    | 进入上次的目录                                            |
  | ~    | 进入系统环境变量的`HOME`目录路径，即当前登录用户的家目录` |
  | \.\. | 进入父目录                                                |

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
  |-------------|----------------------------------------------------|
  | -a          | 显示所有文件包括隐藏文件                           |
  | -d          | 只显示目录`!`                                      |
  | -f          | 显示每个文件的绝对路径                             |
  | -i          | 不显示树枝                                         |
  | -L levelNum | 显示遍历目录的层级，levelNum为层级(数字)           |
  | -F          | 显示时根据不同文件类型在文件名结尾处显示不同的符号 |

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
  |----|------------------------------------|
  | -p | 递归创建目录，若目录已存在不会报错 |
  | -m | 创建时指定目录的权限               |
  | -v | 创建时显示过程信息                 |

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
  |-----------|--------------------------------------------------|
  | -a        | 更改指定文件的最新访问时间                       |
  | -d STRING | 用字符串的方式指定一个模板作为指定文件的时间属性 |
  | -m        | 更改指定文件的最新修改时间                       |
  | -r file   | 将指定文件的时间属性设置为file的时间属性         |
  | -t STAMP  | 使用时间格式设置文件的时间属性                   |

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
  ~~~

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

  | 选项                                        | 说明                                                                           |
  |---------------------------------------------|--------------------------------------------------------------------------------|
  | -l                                          | 使用长格式列出目录下的文件和信息                                               |
  | -a                                          | 显示目录下的所有文件，包括隐藏文件`!`                                          |
  | -t                                          | 根据最新的修改时间排序，不加此参数默认是根据文件名排序`!`                      |
  | -r                                          | 反向排序                                                                       |
  | -F                                          | 在显示的条目后加上特殊符号用以区别文件类型`!`                                  |
  | -p                                          | 目录后面加上“/”                                                                |
  | -i                                          | 显示inode节点信息                                                              |
  | -d                                          | 遇到目录时，只列出目录本身，并且不跟随符号链接`!`                              |
  | -h                                          | 以人类可读的信息显示文件或目录大小                                             |
  | -A                                          | 列出所有文件，包括隐藏文件夹，但不包括.和..                                    |
  | -S                                          | 根据文件大小排序                                                               |
  | -R                                          | 递归列出所有子目录                                                             |
  | -x                                          | 逐行列出项目而不是逐栏列出                                                     |
  | -X                                          | 根据扩展名排序                                                                 |
  | -c                                          | 根据状态改变时间排序                                                           |
  | -u                                          | 根据最后访问时间排序                                                           |
  | --color={never,always,auto}                 | 根据文件类型显示不同颜色，never:不显示，always:总是显示，auto:表示自动显示     |
  | --full-time                                 | 以完整的时间格式进行显示                                                       |
  | --time-style={full-iso,long-iso,iso,locale} | 以不同的时间格式输出，long-iso最常用                                           |
  | --time={atime,ctimeA}                       | 按不同的时间属性输出,atime:访问时间，ctime:改变权限属性时间，默认:最后修改时间 |

  例子:

  环境准备

  ~~~
  [evanmeek@EvanLinux ~]$ mkdir temp
  [evanmeek@EvanLinux ~]$ cd temp
  [evanmeek@EvanLinux ~]$ mkdir -p father/dir{01..02}
  [evanmeek@EvanLinux ~]$ touch father/dir{01..02}/txt{01..02}
  [evanmeek@EvanLinux ~]$ touch father/dir{01..02}/.txt{01..02}
  [evanmeek@EvanLinux ~]$ tree -a
  ~~~

  输出结果

  ~~~
  .
  └── father
      ├── dir01
      │   ├── .txt01
      │   ├── txt01
      │   ├── .txt02
      │   └── txt02
      └── dir02
          ├── .txt01
          ├── txt01
          ├── .txt02
          └── txt02

3 directories, 8 files
  ~~~

  递归显示所有文件

  ~~~
  [evanmeek@EvanLinux ~/WorkDir/MyBlog/]$ ls -Ra
  ~~~

  输出信息
  
  ~~~
  .:
  .  ..  father

  ./father:
  .  ..  dir01  dir02

  ./father/dir01:
  .  ..  .txt01  txt01  .txt02  txt02

  ./father/dir02:
  .  ..  .txt01  txt01  .txt02  txt02
  ~~~
  
 __ls命令输出属性解释__

  目录内容如下：

  ~~~
  .
  ├── dir01
  ├── dir02
  ├── file01.txt
  └── file02.txt

  2 directories, 2 files
  ~~~

  长格式列出人类可读信息并显示inode信息

  ~~~
  [evanmeek@EvanLinux ~]$ ls -lhi
  ~~~

  输出信息

  ~~~
  total 8.0K
  18219052 drwxr-xr-x 2 evanmeek evanmeek 4.0K  6月 18 19:27 dir01
  18219053 drwxr-xr-x 2 evanmeek evanmeek 4.0K  6月 18 19:27 dir02
  18219054 -rw-r--r-- 1 evanmeek evanmeek    0  6月 18 19:28 file01.txt
  18219055 -rw-r--r-- 1 evanmeek evanmeek    0  6月 18 19:28 file02.txt
  ~~~

  从第一列依次往后排，分别含义为:

  1. inode索引节点编号
  2. 文件类型以及属性(第一字符标注类型，后9个代表权限)
  3. 硬链接个数
  4. 文件或目录所属用户
  5. 文件或目录所属的组
  6. 文件或目录的大小
  7. 修改时间
  10. 文件名或目录名

# 2.7 cp复制文件或目录
  
  `copy`

  | 选项 | 说明                                                                                       |
  |------|--------------------------------------------------------------------------------------------|
  | -p   | 复制文件时保存源文件的所有者、权限信息及时间属性                                           |
  | -d   | 如果复制的源文件是符号链接，那么仅复制符号链接本身，并且保留符号链接所只想的目标文件或目录 |
  | -r   | 递归复制目录，即目录下所有的子目录及文件                                                   |
  | -a   | 等同于上面的p、d、r这3个选项功能的总和                                                     |
  | -i   | 覆盖已有文件前提示用户确认                                                                 |
  | -t   | 调换命令格式，默认格式是"cp 源文件 目标文件"，将目标文件和源文件进行位置调换               |
  
  例子:

  环境准备

  ~~~
  .
  └── fatherDir
      ├── sonDir1
      │   └── test.txt
      ├── sonDir2
      │   └── test.txt
      └── sonDir3
          └── test.txt

  4 directories, 3 files
  ~~~

  拷贝`fatherDir`为`father2Dir`并保留源文件的所有者，权限信息及时间属性
  
  ~~~
  [evanmeek@EvanLinux ~/temp]cp -rp fatherDir father2Dir
  ~~~
  
  再次拷贝`fatherDir`为`father2Dir`从而覆盖上个例子的`father2Dir`
  
  ~~~
  [evanmeek@EvanLinux ~etemp]$ cp -ri fatherDir father2Dir
  ~~~
  
  输出信息

  ~~~
  cp：是否覆盖'father2Dir/fatherDir/sonDir1/test.txt'？ y
  cp：是否覆盖'father2Dir/fatherDir/sonDir2/test.txt'？ y
  cp：是否覆盖'father2Dir/fatherDir/sonDir3/test.txt'？ y
  ~~~

# 2.8 mv移动或重命名文件
  
  `move`
  | 选项 | 说明                                                       |
  |------|------------------------------------------------------------|
  | -f   | 若目标文件已存在，不询问直接覆盖                           |
  | -i   | 若目标文件已存在，询问是否覆盖                             |
  | -n   | 不覆盖已存在的文件                                         |
  | -t   | 交换目标文件和源文件的参数位置，常用于有多个目标目录的情况 |
  | -u   | 源文件比目标文件新，或目标文件不存在时再移动               |

  例子:

  环境准备

  ~~~
  总用量 4
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test0.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test1.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test2.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test3.txt
  drwxr-xr-x 2 evanmeek evanmeek 4096 2019-06-20 19:11:55.618528975 +0800 testTxt
  ~~~
  
  更换文件名

  ~~~
  [evanmeek@EvanMeek ~]$mv test0.txt test-1.txt
  [evanmeek@EvanMeek ~]$ls -l --full-time
  ~~~
  
  输出信息

  ~~~
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test-1.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test1.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test2.txt
  -rw-r--r-- 1 evanmeek evanmeek    0 2019-06-20 19:11:36.807398116 +0800 test3.txt
  drwxr-xr-x 2 evanmeek evanmeek 4096 2019-06-20 19:11:55.618528975 +0800 testTxt
  ~~~
  
  __移动文件__

  ~~~
  [evanmeek@EvanLinux ~]$ mv test-1.txt testTxt
  ~~~

  __移动多个文件至一个目录__

  ~~~
  [evanmeek@EvanLinux ~]$ mv -t testTxt test1.txt test2.txt test3.txt
  ~~~
  
# 2.9 rm删除文件或目录

  __前排提示:使用rm命令时最好知道自己在干什么!__

  `remove`

  | 选项 | 说明                                   |
  |------|----------------------------------------|
  | -f | 强制删除并且忽略不存在文件的提示       |
  | -i | 删除时需要确认                         |
  | -I | 删除三个以上文件或者递归删除前需要确认 |
  | -r | 递归删除目录以及其内容`!`                |

  例子:

  __再次提醒，使用此命令时最好知道自己在做什么并且检查是否写错，一旦删除无法恢复(大多数情况下可以恢复，可以通过ext3grep实现)__

  环境准备
  ~~~
  .
  ├── test2Txt
  │   ├── test1.txt
  │   ├── test2.txt
  │   └── testTxt
  │       └── test-1.txt
  └── test3.txt
  ~~~

  __删除文件__
  
  ~~~
  [evanmeek@EvanLinux ~]$ rm test3.txt
  ~~~

  __强制删除并且删除时需要确认__

  ~~~
  [evanmeek@EvanLinux ~]$ rm -fi test2Txt/test2.txt
  ~~~
  
  输出信息

  ~~~
  rm：是否删除普通空文件 'test2Txt/test2.txt'？
  ~~~

  __删除目录并且删除时需要确认__
  
  ~~~
  [evanmeek@EvanLinux ~]$ rm -ri test2Txt/testTxt
  ~~~
  
  __强制删除+递归删除目录__
  
  ~~~
  [evanmeek@EvanLinux ~]$ rm -rf test2Txt
  ~~~

  __最后再提醒一下，如果网上有人叫你输入如下命令，请千万不要输入__

  ~~~
  sudo rm -rf /*
  ~~~
  
  __这行命令的意思是:以管理员的权限强制+递归删除根目录下的所有文件,此行命令不在我们学习范围之内.__

## 删除时的小技巧

  - 使用`mv`命令代替`rm`命令，可以将要删除的文件暂时保存在`/tmp`目录下，需要清理空间时再去删除

  - 删除前先备份，并且最好是不同机器备份，Linux可以做到若出现问题随时还原

  - 若非要用删除命令清理空间可以选择用`find`代替`rm`

  - 删除时尽量不要使用系统通配符

# 2.10 rmdir删除空目录

  `remove dirctory`

  此命令只能删除空目录

  | 选项 | 说明                                                                                                                  |
  |------|-----------------------------------------------------------------------------------------------------------------------|
  | -p   | 递归删除目录，若发现子目录被删除后父目录也为空时，则一并删除。若由于部分原因，部分目录被保留，那么则会显示相应的信息 |
  | -v   | 删除时显示执行过程                                                                                                    |

# 2.11 ln硬链接与软链接

  `link`

  链接分为两种，分别是硬链接与软链接

  硬链接(hard link):
  
  - 不能将硬链接链接到不同文件系统的文件

  - 硬链接不能链接目录

  - 删除硬链接或者源文件之一并不能完全删除实体

  - 删除实体需要删除硬链接以及起对应的源文件

  - 硬链接相当与源文件的另外一个入口

  - 对于静态文件来说，对应的硬链接连接的个数为0时，则代表被删除

  - 硬链接的文件类型是普通文件(字符型)

  - 硬链接通过索引节点进行链接

  例子:

  创建硬链接

  ~~~
  [evanmeek@EvanLinux ~]$ ln test.txt testHardFile.txt
  ~~~

  软链接(Symbolic Link):

  - 类似于Windows的快捷方式

  - 文件内存放的是源文件的路径

  - 即使删除源文件，软链接仍然存在，但无法访问源文件

  - 源文件被删除后，软链接则失效，失效后将会有白字红底闪烁提示

  - 软链接可以用rm命令删除

  例子:

  __创建软链接__

  ~~~
  [evanmeek@EvanLinux ~]$ ln -s test.txt testSyumbolicLink.txt
  ~~~

## 文件链接案例

  通过一个案例演示软链接和硬链接的区别。
  
  ~~~
  [evanmeek@EvanLinux ~]$ cat testFile
  123
  # 创建硬链接
  [evanmeek@EvanLinux ~]$ ln testFile testFileHardLink
  # 创建软链接
  [evanmeek@EvanLinux ~]$ ln -s testFile testFileSymbolicLink
  [evanmeek@EvanLinux ~]$ cat testFile testHardLink testFileSymbolicLink
  123
  123
  123
  # 删除软链接
  [evanmeek@EvanLinux ~]$ rm -f testFileSymbolicLink
  [evanmeek@EvanLinux ~]$ cat testFile testHardLink
  123
  123
  # 复原
  [evanmeek@EvanLinux ~]$ ln -s testFile testFileSymbolicLink
  # 删除硬链接
  [evanmeek@EvanLinux ~]$ rm -f testFileHardLink
  [evanmeek@EvanLinux ~]$ cat testFile testFileHardLink
  123
  123
  # 复原
  [evanmeek@EvanLinux ~]$ ln testFile testFileHardLink
  # 删除源文件
  [evanmeek@EvanLinux ~]$ rm -f testFile
  [evanmeek@EvanLinux ~]$ cat testFileHardLink testFileSymbolicLink
  123
  cat: testFileSymbolicLink: 没有那个文件或目录
  ~~~
  
  - 硬链接可以没有源文件

  - 软链接不行

# 2.12 readlink 查看符号链接文件的内容

  此命令可查看链接指向的源文件的地址

  | 选项 | 说明                                                           |
  |------|----------------------------------------------------------------|
  | -f   | 一直跟随符号链接，直到遇到一个非符号链接的文件，若不存在则不行 |

  例子：
  
  ~~~
  [evanmeek@EvanLinux ~]$ readlink testFileSymbolicLink
  ~~~

# 2.13 find 查找目录下的文件

  由于本篇篇幅较大，请点击下方超链接进行访问。

  [点击访问](/2019/6/21/Linux-文件和目录操作命令-find命令)

# 2.14 xargs将标准输入转换成命令行参数

  | 选项 | 说明                                                           |
  |------|----------------------------------------------------------------|
  | -n   | 指定每行命令的最大参数数量，每个参数由空格隔开                 |
  | -d   | 自定义分割符                                                   |
  | -i   | 以{}替代xargs命令之前的结果                                    |
  | -I   | 指定一个符号替代前面的结果，而不是使用默认的{}                 |
  | -P   | 提示让用户确认是否执行后面的命令，y执行，n不执行               |
  | -0   | 用null替代空格作为分割符，配合find命令的-printf0选项的输出使用 |

## 2.14.2使用范例

  __多行输入变单行__

  ~~~
  > cat test.txt
  1 2 3 4 
  5 6 7
  8 9
  1 
  > xargs < test.txt
  1 2 3 4 5 6 7 8 9 1
  ~~~

  __通过-n指定每行的输出个数__

  ~~~
  > xargs -n 2 < test.txt
  1 2
  3 4
  5 6
  7 8
  9 1
  ~~~

  __自定义分隔符(使用-d功能)__
  ~~~
  > echo 123I321I809I098
  123I321I809I098

  > echo 123I321I809I098|xargs -d I -n 2
  123 321
  890 098
  ~~~

  __指定一个替换字符串__
  ~~~
  # 将查找出来的结果删除
  # 先将结果传给{}
  # 再会被删除
  > find . -name "*.log"|xargs -i rm -rf {}
  # 自定义替换字符串
  > find . -name "*.log"|xargs -I [] rm -rf []
  ~~~

# 2.15 rename重命名

  rename通过替换字符串的方式批量修改文件名

  语法格式

  ~~~
  rename from to file
  ~~~

  例子:

  __批量修改文件名__

  ~~~
  > ls
  test_demo_0  test_demo_1  test_demo_2  test_demo_3  test_demo_4  test_demo_5
  > rename "_demo" "" *
  > ls
  test_0  test_1  test_2  test_3  test_4  test_5
  ~~~

  __批量修改文件扩展名__

  ~~~
  > ls
  test0.txt  test1.txt  test2.txt  test3.txt  test4.txt  test5.txt
  > rename .txt .demo *
  > ls
  test0.demo  test1.demo  test2.demo  test3.demo  test4.demo  test5.demo
  ~~~

# 2.16 basename显示文件名或目录名

  basename命令用于显示去除路径和文件后缀的文件名或目录名

  语法格式

  ~~~
  basename [<文件或目录>] [后缀]
  ~~~
  
  其中的后缀为可选

  例子:

  __只显示文件名和后缀，不显示完整路径__

  ~~~
  > mkdir -p dir1/dir2/
  > touch dir1/dir2/test.txt
  > basename dir1/dir2/test.txt
  test.txt
  ~~~

  只显示文件名，不显示完整路径制定不显示某个后缀

  ~~~
  > touch dir1/dir2/test.demo.txt
  > basename dir1/dir2/test.demo.txt .txt
  test.demo
  ~~~
# 2.17 dirname显示文件或目录的路径

  dirname命令用于只显示文件或目录的路径

  语法格式

  ~~~
  dirname [<文件或目录>]
  ~~~

  例子:

  ~~~
  > dirname dir1/dir2/test.txt
  dir1/dir2
  ~~~

# 2.18 chattr改变文件的扩展属性
  charttr命令用户改变文件的扩展属性，相比chmod命令不同的是，chmod只是改变文件的读写执行权限，而更底层的权限属性控制是由charttr来改变的．

  语法格式

  ~~~
  chattr [选项] [模式] [<文件或目录>]
  ~~~

  提示:`lsattr`命令可以查看文件的属性

  | 选项 | 说明                                       |
  |------|--------------------------------------------|
  | -R   | 递归更改目录属性                           |
  | -V   | 显示执行过程                               |
  | mode |                                            |
  | +    | 增加参数                                   |
  | -    | 移除参数                                   |
  | =    | 更新为指定参数                             |
  | A    | 指定文件的最后访问时间不可修改             |
  | a    | 指定文件只能添加数据，无法删除数据`!`      |
  | !    | 指定文件不能被删除，重命名，写入或新增内容 |

  例子：

  __给文件加锁，使其只能为只读__

  ~~~
  > chattr +i test.txt
  > lsattr test.txt
  ----i---------e----- test.txt
  > echo a1111 > test.txt
  zsh: 不允许的操作: test.txt
  > echo b2222 >> test.txt 
  zsh: 不允许的操作: test.txt
  ~~~

  __给文件解锁__

  ~~~
  > charttr -i test.txt
  > lsattr test.txt
  --------------e----- test.txt
  > eco 111 > test.txt
  > cat test.txt
  111
  ~~~

# 2.19 lsattr查看文件扩展属性

  lsattr命令用于查看文件扩展属

  语法格式

  ~~~
  lsattr [选项] [<文件或目录>]
  ~~~

  | 选项 | 说明                   |
  |------|------------------------|
  | -R   | 递归查看目录的扩展属性 |
  | -a   | 显示所有文件的扩展属性 |
  | -d   | 显示目录的扩展属性     |

  例子:

  __查看文件的扩展属性__

  ~~~
  > lsattr test.txt
  --------------e----- test.txt
  > chattr +i test.txt
  > lsattr test.txt
  ----i---------e----- test.txt
  ~~~

  __查看目录的扩展属性__

  ~~~
  > lsattr -d testDir
  --------------e----- testDir
  > chattr +i testDir
  > lsattr -d testDir
  ----i---------e----- testDir
  ~~~

# 2.20 file显示文件的类型

  file命令用于显示文件的类型

  语法格式

  ~~~
  file [选项] [<文件或目录>]
  ~~~

  | 选项 | 说明                 |
  |------|----------------------|
  | -b   | 输出信息使用精简格式 |

  例子:

  __查看文件类型__

  ~~~
  > file test.txt
  test.txt: empty
  > file *
  test.txt:      empty
  test.txt.link: symbolic link to test.txt
  ~~~

# 2.21 md5sum计算和校验文件的MD5值

  md5sum命令用于计算和校验文件的MD5值.

  语法格式

  ~~~
  md5sum [选项] [文件]
  ~~~

  | 选项     | 说明                                                 |
  |----------|------------------------------------------------------|
  | -b       | 二进制模式读取文件                                   |
  | -c       | 从指定文件中读取MD5校验值，并进行校验                |
  | -t       | 文本模式读取文件，默认                               |
  | --quiet  | 校验文件时，若通过不输出OK                           |
  | --status | 校验文件时，不输出任何信息，但可通过命令的返回值判断 |

  例子:

  __生成一个文件的MD5值__

  ~~~
  > md5sum test.txt
  d41d8cd98f00b204e9800998ecf8427e  test.txt
  ~~~

  __校验文件MD5值是否发生改变__

  ~~~
  > md5sum test.txt > md5.log
  > cat md5.log
  d41d8cd98f00b204e9800998ecf8427e  test.txt
  > md5sum -c md5.log
  test.txt: 成功
  > echo "update" >> test.txt
  > md5sum -c md5.log
  test.txt: 失败
  md5sum: 警告：1 个校验和不匹配
  > md5sum --status -c md5.log
  > echo $?
  1
  ~~~

# 2.22 chown改变文件或目录的用户和用户组

  chown命令用于改变文件或目录的用户和用户组

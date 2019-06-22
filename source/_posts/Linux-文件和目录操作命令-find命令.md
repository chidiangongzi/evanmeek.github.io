---
title: Linux-文件和目录操作命令-find命令
copyright: true
date: 2019-06-21 01:04:56
categories: Linux系列
tags:
 - Linux
---

本篇文章为Linux系列的第2章 文件和目录操作名 2.13小节的外部展示

<!--more-->

# 2.13.1 命令详解

find命令参数较多，并且不同的参数所在的子模块不同.

~~~
    如何处理符号链接
        |
        |  需要查找的路径
        |     |
        |     |
find -H-L-P path expression
                /    |     \
              /      |       \
            |        |         |
            options tests actions
            参数      |       |
                限定的条件     |
                          执行的动作
~~~

| 选项               | 说明                                                                  |
|--------------------|-----------------------------------------------------------------------|
| pathname           | 需要查找的路径                                                        |
| Options模块        |                                                                       |
| -depth             | 从指定目录下最深层的子目录开始查找                                    |
| -maxdepth levels   | 查找的最大目录层级数，levels为自然数`!`                               |
| -regextype type    | 改变正则表达式的模式，默认为emacs，还有posix-awk/basic/egrep/extended |
| Tests模块          |                                                                       |
| -mtime [-n\|n\|+n] | 按照修改时间进行查找.后面会将，这几种n分别代表的是时间，单位为天`!`   |
| -atime[-n\|n\|+n]  | 同上，只不过是按照访问时间进行查找，单位为天                          |
| -ctime             | 按照文件的状态改变时间来查找文件，单位为天                            |
| -amin              | 按照文件的访问时间查找，单位为分钟                                    |
| -cmin              | 按照文件的状态改变时间查找，单位为分钟                                |
| -mmin              | 按照文件的修改时间来查找文件，单位为分钟                              |
| -group             | 按照文件所属的组来查找文件                                            |
| -name              | 按照文件名查找文件，只支持\*,?,[]等特殊通配符`!`                      |
| -newer             | 查找更改时间比指定文件新的文件                                        |
| -nogroup           | 查找没有有效用户组的文件，即文件所属组在/etc/groups中不存在           |
| -nouser            | 查找没有有效属主的文件，即该文件的属主在/etc/passwd中不存在           |
| -path pattern      | 指定路径样式，配合-prune参数排除指定目录                              |
| -perm              | 按照文件权限来查找文件                                                |
| -regex             | 接正则表达式                                                          |
| -iregex            | 不区分大小写接正则表达式                                              |
| -size n[cwbkMG]    | 查找文件长度为n块的文件，带有cwbkMG时表示文件长度以字节计             |
| -user              | 按照文件属主来查找文件                                                |
| -type              | 查找某一类型的文件:`!`，后面会讲                                      |
| -Actions模块       |                                                                       |
| -delete            | 将查找出的文件删除                                                    |
| -exec              | 对匹配文件执行该参数给出的Shell命令`!`                                |
| -ok                | 和-exec作用相同，但在执行每个命令之前，都会让用户先确定是否执行       |
| -prune             | 使fint命令不再指定的目录中查找                                        |
| -print             | 将匹配的文件输出到标准输出(默认可用                                   |
| OPERATORS          | find支持逻辑运算符                                                    |
| !                  | 取反`!                                                                |
| -a                 | 取交集，全拼为and`！`                                                 |
| -o                 | 取并集，全拼为or`!`                                                   |

-type 查找某一类型的文件:

  - b(块设备文件)

  - c(字符设备文件)

  - d(目录)

  - p(管道文件)

  - l(符号链接文件)

  - f(普通文件)

  - s(socket文件)

  - D(door)


# 2.13.2 使用范例

__查找指定时间内访问过的文件__

~~~
> find . -atime -2

./Linux-文件和目录操作命令-1.md
./Linux-文件和目录操作命令-find命令.md
./我的VIM配置详解.md
./我的VIM配置详解
~~~

__查找指定时间内修改过的文件__

~~~
> find . -mtime -5
.
./Linux-Linux命令行简介-0.md
./Linux-文件和目录操作命令-1.md
./C-内存四区之栈区.md
./Linux-文件和目录操作命令-find命令.md
./我的VIM配置详解.md
./Linux-Linux命令行简介-man命令.md
./我的VIM配置详解
~~~

时间关系字符图如下:

~~~
------------+4  4 -4---------------
8   7   6   5   4   3   2   1   now
~~~

`-n`代表从第四天到现在之内

`n`代表具体某一天

`+n`代表某一天之前

__根据文件名查找指定时间的文件__

~~~
> find . -mtime -1 -name '*.md'
./Linux-文件和目录操作命令-find命令.md
~~~

__根据文件类型查找目录__

~~~
> find . -type d
.
./Linux-Linux命令行简介-0
./终端多窗口神器——Screen
./Qt5
./2008年5月12日14时28分04秒
./如何自学编程
./Learn-Qt5-自定义信号槽
./C-内存四区之代码区与全局区
./Linux
./C-友元
./Learn-Qt5-Qt模块简介
./ManjaroLinux的安装过程
./C-的命名空间与作用域
./Learn-Qt5-信号槽
./我儿子的博客
./C-内存四区之堆区
./fcitx5安装与配置
./hexo-next插入网易云音乐
./Linux-文件和目录操作命令-1
./C-读写文件
./Linux-Linux命令行简介-man命令
./C-指针-基础02
./Learn-Qt5-HelloWorld
./常用算法-1
./C-内存四区之栈区
./我的VIM配置详解
./解决KDE下部分应用不能使用fctix中文输入法的问题
./如何用hexo-github-pages搭建博客
~~~

__根据文件类型查找非目录的文件__

~~~
> find . ! -type d
./Linux-Linux命令行简介-0/1.1.2-0
./fcitx5安装与配置.md
./终端多窗口神器——Screen/DefalutCommandKey.png
./终端多窗口神器——Screen/detachedInfo.png
./Linux中的解压与压缩.md
./Linux-Linux命令行简介-0.md
./终端多窗口神器——Screen.md
./C-内存四区之代码区与全局区.md
./C-内存四区之堆区.md
./2008年5月12日14时28分04秒/空降.webp
./2008年5月12日14时28分04秒/操场.webp
./2008年5月12日14时28分04秒/流量图.webp
./hexo-next插入网易云音乐.md
./如何自学编程/群组.png
./Linux-文件和目录操作命令-1.md
./我儿子的博客.md
./解决KDE下部分应用不能使用fctix中文输入法的问题.md
./C-内存四区之代码区与全局区/代码区示意图.png
./C-内存四区之栈区.md
./Learn-Qt5-信号槽.md
./Linux-文件和目录操作命令-find命令.md
./Learn-Qt5-Qt模块简介.md
./C-读写文件.md
./ManjaroLinux的安装过程/编辑文章时截图.png
./ManjaroLinux的安装过程/分区.png
./ManjaroLinux的安装过程/开始安装.png
./ManjaroLinux的安装过程/安装选择界面.png
./ManjaroLinux的安装过程/摘要.png
./ManjaroLinux的安装过程/分区标识.png
./ManjaroLinux的安装过程/桌面.png
./Learn-Qt5-自定义信号槽.md
./我儿子的博客/预览.png
./hexo博客文章插入图片.md
./C-函数探幽.md
./C-内存四区之堆区/test.png
./如何自学编程.md
./深拷贝和浅拷贝的区别.md
./ManjaroLinux的安装过程.md
./fcitx5安装与配置/kcm.png
./fcitx5安装与配置/输入.gif
./hexo-next插入网易云音乐/01.png
./hexo-next插入网易云音乐/插哪.png
./2008年5月12日14时28分04秒.md
./C-读写文件/二进制文件.png
./C-指针-基础02/指针位偏移.png
./Learn-Qt5-HelloWorld.md
./ManjaroLinuxTG讨论群组.md
./Learn-Qt5-HelloWorld/newProject.gif
./我的VIM配置详解.md
./C-友元.md
./如何用hexo-github-pages搭建博客.md
./Linux-Linux命令行简介-man命令.md
./常用算法-1.md
./C-的命名空间与作用域.md
./我的Linux之路.md
./2019年的规划.md
./C-指针-基础01.md
./C-指针-基础02.md
./如何用hexo-github-pages搭建博客/创建仓库.png
./如何用hexo-github-pages搭建博客/deploy.png
./如何用hexo-github-pages搭建博客/逆光.jpg
./如何用hexo-github-pages搭建博客/本地部署.png
./如何用hexo-github-pages搭建博客/hexoinit.png
./如何用hexo-github-pages搭建博客/导入密钥.png
./如何用hexo-github-pages搭建博客/打开设置.png
./如何用hexo-github-pages搭建博客/ssh目录.png
./如何用hexo-github-pages搭建博客/设置SSH.png
~~~

__根据文件或目录的权限查找文件__

~~~
> find . -perm 755
.
./Linux-Linux命令行简介-0
./终端多窗口神器——Screen
./Qt5
./2008年5月12日14时28分04秒
./如何自学编程
./Learn-Qt5-自定义信号槽
./C-内存四区之代码区与全局区
./Linux
./C-友元
./Learn-Qt5-Qt模块简介
./ManjaroLinux的安装过程
./C-的命名空间与作用域
./Learn-Qt5-信号槽
./我儿子的博客
./C-内存四区之堆区
./fcitx5安装与配置
./hexo-next插入网易云音乐
./Linux-文件和目录操作命令-1
./C-读写文件
./Linux-Linux命令行简介-man命令
./C-指针-基础02
./Learn-Qt5-HelloWorld
./常用算法-1
./C-内存四区之栈区
./我的VIM配置详解
./解决KDE下部分应用不能使用fctix中文输入法的问题
./如何用hexo-github-pages搭建博客
~~~

__根据文件大小查找文件__

~~~
> find . -size +1M
./ManjaroLinux的安装过程/桌面.png
~~~

__查找时忽略某个目录__

~~~
> find . -path "*Linux*" -prune -o -type d -print
.
./终端多窗口神器——Screen
./Qt5
./2008年5月12日14时28分04秒
./如何自学编程
./Learn-Qt5-自定义信号槽
./C-内存四区之代码区与全局区
./C-友元
./Learn-Qt5-Qt模块简介
./C-的命名空间与作用域
./Learn-Qt5-信号槽
./我儿子的博客
./C-内存四区之堆区
./fcitx5安装与配置
./hexo-next插入网易云音乐
./C-读写文件
./C-指针-基础02
./Learn-Qt5-HelloWorld
./常用算法-1
./C-内存四区之栈区
./我的VIM配置详解
./解决KDE下部分应用不能使用fctix中文输入法的问题
./如何用hexo-github-pages搭建博客
~~~

__查找比某个文件新，但比某个文件旧__

~~~
# 其中的!不代表取反，代表逻辑运算符非
> find . -newer new.txt ! -newer old.txt
./verynew.txt
~~~

__查找文件时使用正则表达式__

~~~
> ls
txt0.txt  txt1.txt  txt2.txt  txt3.txt  txt4.txt
> find . -regex ".*xt"
./txt0.txt
./txt4.txt
./txt1.txt
./txt2.txt
./txt3.txt
~~~

__对查找到的文件执行Shell命令操作__

~~~
> ls
txt0.txt  txt1.txt  txt2.txt  txt3.txt  txt4.txt

# 其中的{}代表查找到的内容，使用-exec必须在后面加上;，并且分好前要使用\，因为需要转义
> find . -regext ".*txt" -exec mv {} {}.demo \;
txt0.txt.demo  txt1.txt.demo  txt2.txt.demo  txt3.txt.demo  txt4.txt.demo
~~~

__对查找到的文件使用Shell命令并且使用安全模式-ok

~~~
> find . -type f -ok rm {} \;
< rm ... ./txt1.txt.demo > ? n
< rm ... ./txt2.txt.demo > ? n
< rm ... ./txt4.txt.demo > ? n
< rm ... ./txt0.txt.demo > ? y
< rm ... ./txt3.txt.demo > ? n
~~~

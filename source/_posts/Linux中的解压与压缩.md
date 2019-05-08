---
title: Linux中的解压与压缩
date: 2019-05-08 20:54:19
categories: 学习笔记
tags:
  - Linux
---

当我们需要传输数据时，如果是直接对文件进行传输，若数据较大，则传输时间会很长。我们可以将文件进行压缩，减少文件的体积，从而减少传输耗时。

<!--more-->

在Windows下我们通常使用rar或zip进行压缩解压的操作，但是像rar这种软件实际是收费的，所以在Linux下使用有些不太实际。


Linux下有三种主流常用的解压压缩软件可选:

- gzip (GNUzip)

- bz2 (bzip2)

- xz (xzutils)

三个软件的参数相同，只是命令不同:

~~~shell
$ gzip [参数] <文件名>
~~~

~~~shell
$ bzip2 [参数] <文件名>
~~~

~~~shell
$ xz [参数] <文件名>
~~~

> 可选参数

|参数名|作用|
---|:---:|---
|-d|解压|
|-k|压缩时不删除源文件|
|-r|递归查找目录下的文件，并且压缩|
|-v|显示详细信息|
|-t|测试压缩包是否完整|
|-l|显示压缩包信息|
|-c|写入标准输出，保持原始文件不变|
|-1~9|压缩等级|

**示例:**

> 压缩test.txt，并删除.

~~~shell
$ gzip test.txt
~~~

> 压缩test.txt，不删除原文件，并且显示信息.

~~~shell
$ gzip -vk test.txt
~~~

> 以最高压缩test.txt和test2.txt，不删除原文件，显示信息，并把压缩文件写为test.gz

~~~shell
$ gzip -9cvk test.txt test2.txt > test.gz
~~~

> 解压test.gz

~~~shell
$ gzip -d test.gz
~~~

---

介绍完上面的几种压缩软件，下面介绍一个打包软件**tar**

我们常常可以看见**.tar.xz这种文件，它就是用tar打包，再用xz进行压缩的文件了，下面直接看示例你就会了。


## 压缩

这里注意第一个参数，它们分别代表使用什么压缩软件。

> bz2
~~~shell
$ tar -jcvf test.tar.bz test/ 
~~~

>xz
~~~shell
$ tar -Jcvf test.tar.xz test/
~~~

>gzip
~~~shell
$ tar -zcvf test.tar.gz test/
~~~

## 解压

只需要看文件名的后缀，然后把参数c改为x即可.x代表解压.


~~~shell
$ tar -Jxvf test.tar.xz test/
~~~


---

完.
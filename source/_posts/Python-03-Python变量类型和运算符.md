---
title: '[Python-03]Python变量类型和运算符'
copyright: true
date: 2019-08-31 15:03:13
categories: Python
tags:
  - Python系列
---
Python系列第三章笔记，查看Python系列所有文章，请点击[💿](https://evanmeek.github.io/Python/)
<!--more-->

__本章重点:Python变量数据类型、运算符。__

Python是弱类型语言。

弱类型含义:

- 所有变量无需声明即可使用。

- 变量的数据类型随时可变。

# Python变量及其使用

变量:

- 数据可发生无数次变化。

- 数据类型可发生变化。


常量: 一旦保存数据，则不可修改。


赋值运算符: `=`

__type()作用:__查看变量的数据类型

# Python数值类型（整型、浮点型和复数）及其用法

Python中的数值类型都是不可变的。

有些人可能会问，不是不可变么，为什么我定义的int类型变量的值仍然可以变化，那是因为底层实现将新的值存放到新的一块内存中，然后将修改变量指针的指向。

> Python整型

整型是用来表示没有小数部分的数，整数包括：正整数、0、负整数


Python整型的四种表示形式：

- 十进制(0-9)

- 二进制(0-1)

- 八进制(0-7)

- 十六进制(0-9-A-F/a-f)

> Python浮点型

浮点型是用来保存带小数的数值，浮点数包括:十进制形式、科学计数形式。

十进制形式的写法:

~~~
float_dex = 1.100111
~~~

科学计数形式

~~~
float2 = 2e3
~~~

> Python复数

我跳过了本节，如果读者想看，可以点击进行访问[💿Python复数](http://c.biancheng.net/view/2173.html)

# Python字符串详解(包含长字符串和原始字符串)

Python字符串必须使用引号括起来，可以是单引号也可以是双引号，但必须成对。

如果字符串内仍然包含引号，可以使用以下两种方法解决:

__用另一种成对的引号包括起来__

~~~
str1 = "I'm EvanMeek."

str2 = 'Evan:"Hello World."'
~~~

__用转义字符进行转义__

~~~
str1 = 'I\'m EvanMeek'
~~~

转义字符还可以用来转义换行符，应用场景通常是:

__字符串过长，转义换行符，使其不换行__

~~~
print("mac mac macmac mac macmac mac mac \
mac mac macmac mac mac")
~~~

> Python长字符串

长字符串常用场景是:

__定义大段文本内容为字符串时__

~~~
str1 = ''' "Fuck you ! Bitch!",said he.
"Mother fuck!",said she.
~~~

> Python原始字符串

在Windows下,路径是使用反斜杠作为路径区分的，如果需要将反斜杠转义，那必须再加一个反斜杠，这样非常麻烦，就可以使用下面的案例来解决:

__转义反斜杠写路径__

~~~
path = 'C:\\User\\Admin\\Desktop'
~~~

__使用原始字符串写反斜杠__

~~~
path = r'C:\User\Admin\Desktop'
~~~

注意: 原始字符串中的引号同样需要使用`\`进行转义

# Python bytes类型及用法

bytes类型代表了字节串。

字节串与字符串不同的是:

- 字节串是以字节为单位进行操作

- 字节串可直接用于网络通信数据互联

字节串是由多个字节组成的，每个字节由8个bit位组成。

字节串保存的数据都是二进制格式的数据。

字节串可以转换成字符串，而字符串也能恢复成字节串。

> 字节串转换为字符串

__创建字节串__

~~~
# 创建一个空的bytes
b1 = bytes()
# 创建一个空的bytes值
b2 = b''
# 创建一个非空的字节串
b3 = b'hello'
~~~

__字符串转换为字节串__

~~~
# 使用encode方法将字符串以utf-8字符集转换为字节串
b4 = "I love Python".encode('utf-8')

# 创建bytes对象时将字符串的字符集指定为'utf-8'，自动转换为字节串
b5 = bytes('I love Python', encoding='utf-8')
~~~

> 字节串转换为字符串

~~~
# 使用字节串对象的方法decode，指定字符集转化字节串
str1 = b'I love Python'.decode('utf-8')
~~~

# Python bool布尔类型

bool变量只有两个值分别是: True,False。它们都是Python的关键字。

True代表真

False代表假

例如表达式:

~~~
3 > 5
~~~

结果是False

Python中所有对象都可以进行真假值的测试。

# Python len()函数详解：获取字符串长度或字节数

len()函数是Python内置函数，用于获取字符串或字节串的长度（数量）。

例子:

__统计字符串的长度__

~~~
print(len("Hello World"))
~~~

输出结果: 11

__统计字节串的长度__

~~~
print(len("你好世界".encode()))
~~~

输出结果: 12

不同的语言所占的字节数不同，并且不同的编码格式所占的字节数也不同。

例如，汉字使用utf-8编码格式，占用3个字节，中文标点符号使用GBK编码格式占用2个字节。

# Python input()函数：获取用户输入的字符串

input()是Python的内置函数，其作用是输出一段信息然后请求用户输入，并且将获取的值传入接收的对象。

input()函数将会把用户输入的任何字符都作为字符串读入。

例子:

~~~
a = input("Please input something:")
print(type(a))
~~~

运行:

~~~
Please input something > 19
<class 'str'>
~~~

__注意: Python2.x中，要求input()函数读入的内容必须是符合Python语法表达式的。__

例如: 输入字符串时，必须带双引号，否则将会报错。

# Python print()函数的高级用法


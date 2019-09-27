---
title: '[Python-05]Python字符串常用方法详解'
copyright: true
date: 2019-09-23 19:40:09
categories: Python
tags:
  - Python系列
---

Python系列第五章笔记，查看Python系列所有文章，请点击[💿](http://c.biancheng.net/python/str_method/)

<!--more-->

# Python字符串拼接(包含字符串拼接数字)

先说一个Python中书写字符串的一种特殊方式，如果我们将两个字符串紧挨着写，那么Python则会自动拼接它们。

```
str1 = "Hello"',World'
print(str1)
```

输出结果:`Hello,World` 

**Python字符串拼接数字** 

某些场景下，我们需要将字符串与其他数据类型进行拼接，例如数字，但Python是不支持直接将数字与字符串拼接的，所以我们得先将数字转换成字符串，再进行拼接。

```
str1 = "This number is:"
number = 1.1001
# 使用str()方法将数值类型的变量转化成字符串
print(str1+str(number))
# 使用repr()方法将数值类型的变量转化成字符串
print(str1+repr(number))
# 直接将字符串类型与数值类型进行拼接
print(str1+number)
```

输出结果:

```
This number is:1.1001
This number is:1.1001
Traceback (most recent call last):
  File "test.py", line 8, in <module>
  │ print(str1+number)
TypeError: can only concatenate str (not "float") to str
```

可以看到，我们必须先将数值类型的变量转换成字符串类型才能进行拼接，否则将会引发`TypeError`的错误。

**str()与repr()的区别** 

str()与repr()都可以将数值转换成字符串，但其中**str是Python内置的类型，和int、float一样** ，然而repr()则只是一个函数。

repr()方法还可以以Python表达式的形式来表示值:

```
str1 = "This number is:"
print(str1)
print(repr(str1))
```

输出结果:

```
This number is:
'This number is:'
```

# Python截取字符串(字符串切片)方法详解

Python的字符串实际上是由多个字符组成的，并且允许通过索引访问字符串的某个字符，其语法格式为:

`str[index]` 

str代表要获取的字符串，index代表字符串的某个下标。

Python中字符串的第一个字符默认从0开始访问，依次推进则是0,1,2,n...，并且Python还允许使用负数作为索引下标，负数从-1开始，依次推进。

例子:

```
str1 = "HelloWorld"
# 获取'H'
print(str1[0])
# 获取'o'
print(str1[-6])
```

输出结果:

```
H
o
```

除了通过索引单次获取单个字符外，Python还可以使用中括号对字符串以范围的方式获取，被获取的字符串称为"子串"，其语法格式为:

`string[start:end:step]` 

- string代表要截取的字符串
- start代表要截取子串的开始位置
- end代表要截取子串的结束位置(不包括该字符)
- step代表从start开始，每step个距离获取一个字符。默认为1，可忽略该值。

例子:

```
str1 = "HelloWorld"
# 截取'Hello'
print(str1[0:6])
# 截取'Hold'
print(str1[0:len(str1):3])
```

输出结果:

```
HelloW
Hlod
```

Python还支持使用`in`运算符判断是否包含某个子串.

例子:

```
str1="HelloWorld"
print('Hello' in str1)
print("World" in str1)
print("Test" in str1)
```

输出结果:

```
True
True
False
```

# Python len()函数详解:获取字符串长度或字节数

len()函数用于获取字符串的长度，或字符串占用的字节。

例子:

```
str1="HelloWorld"
print(len(str1))
```

输出结果:`10` 

如果想知道字符串所占用的字节数，可以先将字符串编码后，再获取。

例子:

```
str1="你好世界"
print(len(str1))
print(len(str1.encode()))
```

输出结果:

```
4
10
```

`encode()`方法可以将字符串转换成不同编码格式的字符。

例如:

```
str1="你好世界"
print(len(str1.encode()))
# 将字符串转换成gbk编码格式
print(len(str1.encode('gbk')))
```

输出结果:

```
8
12
```

# Python split()方法详解: 分割字符串


split()方法可以实现将一个字符串按照指定的分隔符分成多个子串，这些子串会被保存至列表中，其语法格式为:

`string.split(sep,maxsplit)` 

- string代表要分割的字符串

- sep代表指定的分隔符，默认为None，也就是任何空字符，例如空格，\n，\t等

- maxsplit代表最大分割次数，如果不指定或者指定为-1，则表示分割次数无限制。

**如果不指定sep，那么maxsplit也不能指定** 

例子:

``` 
str1 = "192.168.0.0.1"
# 指定分隔符为'.'，最大分割数为3次
list1 = str1.split('.',3)
print(list1)
# 指定分割符为'0.'，最大分割数为-1
list1 = str1.split('0.',-1)
print(list1)
# 不指定split()参数
list1 = str1.split()
print(list1)
```

输出结果:

```
['192', '168', '0', '0.1']
['192.168.', '', '1']
['192.168.0.0.1']
```

# Python join()方法: 合并字符串

join()方法算是split()方法的逆方法，它可以将列表(或元素)中多个字符串元素采用固定的连接负连接在一起，其语法格式为:

`newstr = str.join(iterable)` 

- newstr代表合并后产生的新字符串.

- str代表连接符

- iterable代表合并操作的源字符串数据。

例子:

```
path = ['usr','bin','python3.7']
str1 = '/'.join(path)
print(str1)
```

输出结果:

```
/usr/bin/python3.7
```

# Python count()方法，统计字符串出现的次数

count()方法用于统计字符串在另一个字符串出现的次数，若不存在则返回0，否则返回统计的次数，其语法格式如下:

`string.count(sub[,start[,end]])` 

- string代表字符串源

- sub代表要检索的字符串

- start代表检索字符串的起始位置，若不指定则默认为0开始

- end指定检索的终止位置，若不指定则默认为字符串长度

例子:

```
str1 = "叽里呱啦，嘻嘻哈哈，高高兴兴"
print(str1.count('嘻嘻哈哈',0,len(str1)))
```

# Python find()方法：检测字符串中是否包含某个子串

find()方法用于检索字符串中是否包含目标字符串，若包含则返回第一次出现该字符串的索引，否则返回-1。其语法格式为:

`string.find(sub,start,end)` 

- string要检索的字符串源

- sub要检索的子串

- start检索的起始位置

- end检索的终止位置

例子:

```
str1 = "叽里呱啦，嘻嘻哈哈，高高兴兴"
print(str1.find("嘻嘻哈哈"))
print(str1.find("嘻嘻哈哈",6,len(str1)))
```

输出结果:

```
5
-1
```

**Python还提供了rfind()方法，与find()方法不同的是，其实从字符串的右侧开始检索**

# Python index()方法: 检测字符串中是否包含某个字符串

index()方法与find()方法类似，唯一不同的是，index()方法检索子串若没找到，则会抛出异常。

同理，Python也提供了个rindex()方法，作用于rfind()方法类似。

# Python字符串对齐方法ljust()、rjust()和center()详解

Python 的`str`类提供了3种可以用来进行文本对齐的方法，分别是ljust()，rjust()，center()

## Python ljust()方法

ljust()是向指定字符串的右侧填充指定字符，从而达到左对齐文本的目的。语法格式如下:

```
string.ljust(width,fillchar)
```

- string 表示被填充的字符串
- width 表示包括string长度在内，字符串要占的总长度
- fillchar 表示填充时占位的字符，默认为空格

例子:

```
string = 'HelloWorld'
string2 = "你好世界"
print(string.ljust(15,'*'),string2)
```

输出结果:

```
HelloWorld***** 你好世界
```

## Python rjust()方法

rjust()方法与ljust()方法类似，唯一不同的是rjust()方法是向字符串左侧填充字符以右对齐的目的。语法格式:

`str.rjust(width,fillchar)` 

例子:

```
string = "HelloWorld"
print(string.rjust(15,'*'))
```

输出结果:

```
*****HelloWorld
```

## Python center()方法

center()方法与rjust()、ljust()方法类似，其作用是在字符串两边填充字符以进行居中对齐。语法格式:

`str.center(width,fillchar)` 

例子:

```
string = "HelloWorld"
print(string.center(20,'*'))
```

输出结果:

`*****HelloWorld*****` 

# Python startswith()和endswith()方法

startswith()方法与endswith()方法都是用来检索指定字符串是否为字符串源的开头或结尾。

## startswith()方法

startswith()方法用于检索指定字符串是否为字符串源的开头。如果是返回True，否则反之。语法格式:

`str.startswith(sub,start,end)` 

- str: 字符串源

- sub: 指定的字符串（子串)

- start: 指定开始检索的索引位置，可选参数，默认为开头。

- end: 指定结束检索的索引位置，可选参数，默认为字符串源结尾。

例子:

```
string = "HelloWorld"
print(string.startswith("He",2))
print(string.startswith("Wo",5))
```

输出结果:

```
False
True
```

## endswith()方法

endswith()方法用于检索字符串是否以指定字符串结尾

语法格式:

`str.endswith(sub,start,end)` 

例子:

```
string = "HelloWorld"
print(string.endswith('ld'))
print(string.endswith('rl',0,len(string)-1))
```

输出结果:

```
True
True
```

# Pyhton大小写转换(3种)函数及用法

Python提供了三种函数，方便用于转换字符串大小写，分别是title(),lower(),upper().

## title()方法

title()方法用于将字符串的字符转换为大写，其他字符转换为小写，并返回。

**若不需要进行转换，则会直接返回** 

语法格式:

`str.title()` 

例子:

```
string = "HelloWorld"
print(string.title())
```

输出结果:

```
Helloworld
```

## lower()方法

lower()方法用于将字符串中大写的字符转换为小写字符，并返回。

语法格式:

`str.lower()` 

例子:

```
string = "HelloWorld"
print(string.lower())
```

输出结果:`helloworld` 

## upper()方法

upper()方法用于将字符串中小写的字符转换为大写字符，并返回。

语法格式:

`str.upper()` 

例子:

```
string = "HelloWorld"
print(string.upper())
```

输出结果:

`HELLOWORLD` 

# Python去除字符串中空格

Python提供了三种方法，用于去除字符串中的特殊符号或指定字符，例如**换行符(\n)，回车符(\r)，制表符(\t)**，它们分别是strip(),ltrip(),rtrip().

## strip()方法

strip()用于去除字符串前后(左右侧)的特殊符号或指定字符。

语法格式:

`str.strip(char)` 

- str: 字符串源

- char: 指定删除的字符，可选参数，默认为空格、换行符、回车符、制表符

例子:

```
string = "\r   排山倒海\t\n\r"
print(repr(string))
print(repr(string.strip()))
print(repr(string.strip('\r')))
```

输出结果:

```
'\r   排山倒海\t\n\r'
'排山倒海'
'   排山倒海\t\n'
```

## lstrip()方法

lstrip方法用于去除字符串前(左侧)的特殊符号或指定字符。

语法格式:

`str.lstrip(char)` 

例子:

```
string = "\t\n\r排山倒海"
print(repr(string))
print(repr(string.lstrip()))
```

输出结果:

```
'\t\n\r排山倒海'
'排山倒海'
```

## rstrip()方法

rstrip()方法与lstrip()方法以及strip()方法很类似，只不过其作用是去除字符串后(右侧)的特殊符号或指定字符。

语法格式:

`str.rstrip(char)` 

例子:

```
string = "排山倒海\t\n\r"
print(repr(string))
print(repr(string.rstrip()))
```

输出结果:

```
'排山倒海\t\n\r'
'排山倒海'
```

# Python format()方法格式化输出方法详解

语法格式:

`str.format(args)` 

- str: 字符串源

- args: 参数列表，使用逗号进行分割

format()方法的重点在于搞清楚str显示样式的格式。在差UN感觉爱你显示样式模板时，需要使用`{}`和`:`来指定占位符，其完整的语法格式为:

`{[index][:[[fill] align] [sign] [#] [width] [.precision] [type]]}` 

**注意,语法格式中的`[]`括起来的都是可选参数** 

参数含义如下:

- index : 指定后面设置的格式要作用到args中第n个数据，数据的索引值从0开始，默认值为args中数据的先后顺序自动分配排列。

- fill : 指定空白处填充的字符。注意，当填充字符为逗号`,`切作用于整数或浮点数时，该整数(或浮点数)会以逗号分隔的形式输出，例如(1000会输出1,000)。

- align : 指定数据的对齐方式

align 参数及含义

| align | 含义                                                                  |
|-------|-----------------------------------------------------------------------|
| <     | 数据左对齐                                                            |
| >     | 数据右对齐                                                            |
| =     | 数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对 数据类型有效 |
| ^     | 数据居中，此选项续和width参数一起使用                                 |

- sign : 指定有无符号数

| sign | 含义                                                 |
|------|------------------------------------------------------|
| +    | 正数加正号，负数加负号                               |
| -    | 正数不加正好，负数加负号                             |
| 空格 | 正数前加空格，负数前加负号                           |
| #    | 对于二、八、十六进制数，使用此参数，会显示对应的前缀 |

- width : 指定输出数据时所占的宽度。

- .precision : 指定保留的小数位数。

- type : 指定输出数据的具体类型

| type类型值 | 含义                                           |
|------------|------------------------------------------------|
| s          | 对字符串类型格式化                             |
| d          | 十进制整数                                     |
| c          | 将十进制整数自动转换成对应的 Unicode字符       |
| e或者E     | 转换成科计数法后，再格式化输出                 |
| g或G       | 自动在e和f中切换                               |
| b          | 将十进制数自动转换成二进制表示，再格式化       |
| o          | 将十进制数自动转换成八进制表示，再格式化       |
| x或X       | 将十进制数自动转换成十六进制表示，再格式化     |
| f或F       | 转换为浮点数(默认小数点后保留6位),再格式化输出 |
| %          | 显示百分比(默认显示小数点后6位)                |

例子:

```
string = "姓名:{:>5s}\n工资:{:>10.2F}\n"
print(string.format("张三",1001.223))
```

输出结果:

```

姓名:   张三
工资:   1001.22
```

例子2:

```
# 货币形式显示
print("$:{:,d}".format(1000009922399))

# 科学计数法显示
print("科学计数法:{:e}".format(1000.123))

# 十六进制显示
print("1016的十六进制:{:x}".format(1016))

# 百分比形式显示
print("百分比显示:{:.0%}".format(0.99))
```

输出结果:

```
$:1,000,009,922,399
科学计数法:1.000123e+03
1016的十六进制:3f8
百分比显示:99%
```

# Python encode()和decode()方法: 字符串编码转换

前言: 世界最早的字符编码时ASCII编码，它最多表示256个符号，每个符号占用1个字节，随着技术的发展，多国的文字都需要进行编码，所以出现了很多种编码格式，例如UTF-8也就是最通用的编码格式，Python3.x默认也是使用UTF-8编码格式。

Python中有两种常用的字符串类型: `str`与`bytes`类型，`str`用来表示Unicode字符,`bytes`用来表示二进制数据。

所以我们就需要使用`encode()`和`decode()`方法进行转换。

## Phthon encode()方法

encode()方法是str提供的功法，其作用是将str类型转换成bytes类型，这个操作也被称为编码。

语法格式如下:

`str.encode([encode="utf-8"],[errors="strict"])` 

- encoding : 指定在编码时采用的字符编码，默认采用utf-8。当只有这个参数时，可以省略`=`直接写`str.encode("UTF-8")`

- errors : 指定错误处理方式，默认为strict，其可选项有:

| errors            | 含义                   |
|-------------------|------------------------|
| strict            | 遇到非法字符就抛出异常 |
| ignore            | 忽略非法字符           |
| replace           | 用`?`替代非法字符      |
| xmlcharrefreplace | 使用xml的字符引用      |

例子:

```
string = "HelloWorld"
print(string.encode())
```

输出结果:

`b'HelloWorld'` 

## Python decode()方法

decode()可以将bytes类型的二进制数据转换成str类型，这个过程被称为解码

语法格式:

`bytes.decode([encoding="utf-8"],[errors="strict"])` 

例子:

```
string = "HelloWorld"
print(string.encode())
print(bytes.decode(string.encode()))
```

输出结果:

```
b'HelloWorld'
HelloWorld
```

**注意:解码时必须使用与编码时相同的编码格式，否则将会抛出异常** 

# Python dir()和help()帮助函数

Python提供了两个函数，用于帮助程序员查询文档，掌握这两个函数则可以查看所有函数(方法)的用法及功能.

**dir()** 列出指定类或模块包含的全部内容，包括函数、方法、类、变量etc.

**help()** 查看某个函数或方法的帮助文档。

例子:

查看字符串能调用的全部内容

```
print(dir(str))
```

输出结果:

```
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '_
_eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs
__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__'
, '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__',
'__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__'
, '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'e
ncode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isal
num', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', '
isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lo
wer', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust',
 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip',
 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

**注意:其中以`_`结尾的方法为私有方法，不希望被外界直接调用。** 


**help()** 

想要查看某个方法或函数的帮助文档，就使用help()函数

`print(help(str.format))` 

输出结果:

```
Help on method_descriptor:

format(...)
    S.format(*args, **kwargs) -> str

    Return a formatted version of S, using substitutions from args and kwargs.
    The substitutions are identified by braces ('{' and '}').
(END)
```



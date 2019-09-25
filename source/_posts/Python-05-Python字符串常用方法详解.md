---title: '[Python-05]Python字符串常用方法详解'
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

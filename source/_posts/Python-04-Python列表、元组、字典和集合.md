---
title: '[Python-04]Python列表、元组、字典和集合'
copyright: true
date: 2019-09-08 15:00:28
categories: Python
tags:
 - Python系列
---

# 什么是序列，Python序列详解（包括序列类型和常用操作）

序列：一块可存放多个且连续的内存空间，并且这些值有顺序，可通过索引进行访问。

常见的序列有: 字符串、列表、元组、集合和字典。

这些常见的序列，除了集合和字典不支持索引、切片、相加和相乘的操作，其余的都可以。

## 序列索引

索引就是一个序列中每个元素的编号。第一个元素的索引是0，也就是说想要访问某个序列的第一个元素，那么它的索引就是0，而想要访问最后一个元素，那么它的索引就是序列长度-1

索引还分为正索引值和负索引值，它们的区别仅仅在于访问方式不同。

__注意:__

- 正索引值的起始位置是0，结束位置是序列长度-1

- 负索引值的起始位置是-1,结束位置是-(序列长度-1)

例子:

__根据索引访问序列元素__

~~~
str = "Hello World"
print("str 的第一个字符是:%s，最后一个字符是:%s" % (str[0],str[len(str)-1]))
~~~

输出结果:
~~~
str 的第一个字符是:H，最后一个字符是:d
~~~

## 序列切片

刚刚我们通过索引值进行访问序列元素，那么序列切片也是可以做到的，它可以访问某个范围内的元素。

语法格式:

~~~
sname[start:end:step]
~~~

- sname:序列名称

- start:切片开始的索引位置（包括该位置），此参数可不指定，默认为0。

- end:切片结束的索引位置(不包括该位置)，此参数可不指定，默认为序列的长度。

- step:切片的范围，也就是每次取元素时，要隔多少个位置，此参数可不指定，可以直接忽略最后一个冒号

例子:

~~~
str = "Hello World"
# 获取整个字符串
print(str[:])
# 从索引4开始，一直到最后一个，没隔2个字符取一次。
print(str[4::2])
~~~

输出结果:

~~~
Hello World
oWrd
~~~

## 序列相加

序列可以使用`+`运算符，进行相加操作，他会将两个序列进行连接，但不会去除重复的元素。

例子:

~~~
str1="hello"
str2="world"
print(str1+str2)
~~~

输出结果:`helloworld`

## 序列相乘

使用`*`运算符，可以将序列的元素进行重复。

例子:

~~~
str1 = "hello\t"
print(str1*3)
~~~

输出结果:`hello	hello	hello	`

__tips:可以使用序列相乘，创建指定长度空列表__

~~~
test_list = [None]*5
~~~

## 检查元素是否包含在序列中

使用`in`关键字可以检查序列中的元素是否存在。 

语法格式:

~~~
value in sequence
~~~

例子:

~~~
str1="Hello"
print('o' in str1)
~~~

输出结果: `True`

__tips:使用`not in`关键字可以检查是否不存在__


## 和序列相关的内置函数

Python提供了几个用于操作序列的内置函数，可以很方便的操作序列。

![Python序列内置函数](Python-04-Python列表、元组、字典和集合/Python序列内置函数.png)

# Python list列表详解

Python提供了一种数据结构————`list`(列表)

__列表可以存储多个不同数据类型的元素。__


## Python创建列表

创建列表分为两种方式

使用`=`运算符创建列表

语法格式:

~~~
listname = [element1,element2...elementn]
~~~

listname: 列表的名称

element1: 列表的元素

例子:

~~~
# 创建一个列表
test_list1 =["one",1,True,1.0]
print(test_list1)
# 创建一个空列表
empty_list = []
print(empty_list)
~~~

输出结果:

~~~
['one', 1, True, 1.0]
[]
~~~

__使用list()函数创建列表__

例子:

~~~
str1="HelloWorld"
test_list = list(str1)
print(test_list)
~~~

输出结果:

~~~
['H', 'e', 'l', 'l', 'o', 'W', 'o', 'r', 'l', 'd']
~~~

## 访问列表元素

两种方式：通过索引访问和通过切片访问。

## 删除列表

不常用，因为Python具有垃圾回收机制，有些不需要再使用的列表将会自动回收。

使用`del`关键字进行删除

语法格式:

~~~
del listname
~~~

__注意:删除后的列表不能再次使用__

# Python list列表添加元素的3种方法

## Python append()方法添加元素

`append()`方法在列表的末尾追加元素。

语法格式:

~~~
listname.append(obj)
~~~

listname代表要添加元素的列表;obj代表要添加到列表末尾的数据。

obj可以是单个元素，也可以是其他序列。

例子:

~~~
# 追加单个元素
list1 = [0,1,2,3]
print(list1)
list1.append(4)
print(list1)
# 追加一个列表
list2 = [5,6,7,8]
print(list2)
list1.append(list2)
print(list1)
~~~

输出结果:
~~~
[0, 1, 2, 3]
[0, 1, 2, 3, 4]
[5, 6, 7, 8]
[0, 1, 2, 3, 4, [5, 6, 7, 8]]
~~~

__注意:使用append()函数时，如果是传递的单个数据，将会直接追加到列表后，但是如果传入的是个列表（序列），那么则会追加一个列表形式的元素。__

想要访问刚刚追加的列表元素的其中一个可以这样：

~~~
list1 = [0,1,2]
list2 = [3,4,5]
list1.append(list2)
print(list1[3][2])
~~~

输出结果:`5`

## Python extend()方法添加元素

刚刚我们使用`append()`函数追加了个列表元素，但是并没有像添加单个字符一样作为一个整体添加，而我们只需要使用`extend()`方法就可以将列表以整体的方式添加进去。

例子:

~~~
list1 = [0,1,2,3]
print(list1)
list2 = [5,6,7,8]
print(list2)
list1.extend(list2)
print(list1)
~~~

输出结果:

~~~
[0, 1, 2, 3]
[5, 6, 7, 8]
[0, 1, 2, 3, 5, 6, 7, 8]
~~~

## Python insert()方法插入元素

需要指定插入列表元素的位置时，可以使用insert()方法。

语法格式:

~~~
listname.insert(index,obj)
~~~

index: 将obj插入到listname列表的索引

例子:

~~~
test_list1 = list(range(1,11))
print(test_list1)

print(len(test_list1))
test_list1.insert(len(test_list1),11)
print(test_list1)
~~~

输出结果:

~~~
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
10
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
~~~

## Pyhton list列表删除元素(3种方法)

> del删除

__del语句在Python中可以删除变量、列表的元素__

~~~
test_list = list(range(1, 11))
print(test_list)
del test_list[1::2]
print(test_list)
~~~

输出结果:

~~~
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[1, 3, 5, 7, 9]
~~~

> 根据元素值进行删除

可以使用remove()方法来删除列表元素。

删除第一个被查找到的元素。

__注意:remove()方法不是根据索引来删除元素的，而是查找元素本身，再进行删除，所以如果找不到元素，则会报错__

例子:

~~~
test_list = ['test', 30, 'test2', 10, 30]
test_list.remove('test')
test_list.remove(30)
print(test_list)
~~~

输出结果:

~~~
['test2', 10, 30]
~~~

> 删除列表所有元素

使用clear()方法可以删除列表的所有元素。

例子:

~~~
test_list = ['test', 30, 'test2', 10, 30]
test_list.clear()
print(test_list)
~~~

输出结果:

~~~
[]
~~~

# Python list列表修改元素

修改列表元素，可以通过列表索引获取元素进行赋值。

~~~
testlist = list(range(1,10))
print(testlist)
testlist[len(testlist)-1] = 100
print(testlist)
~~~

输出结果:

~~~
[1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 2, 3, 4, 5, 6, 7, 8, 100]

[Process exited 0]
~~~

使用slice语法对列表部分进行赋值。

slice语法，不要求新赋值的元素个数与原来的元素个数相等。也就是说使用slice剩余法既可以为列表增加元素，也可以为列表删除元素。

~~~
b_list = list(range(1,5))
print(b_list)

b_list[1:3] = ['a','b']
print(b_list)
~~~

输出结果:

~~~
[1, 2, 3, 4]
[1, 'a', 'b', 4]
~~~

# Pyhthon list常用方法(count、index、pop、reverse和sort)快速攻略

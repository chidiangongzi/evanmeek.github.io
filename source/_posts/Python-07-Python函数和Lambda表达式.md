---
title: '[Python-07]Python函数和Lambda表达式'
copyright: true
date: 2019-10-09 15:34:55
categories: Python
tags:
  - Python系列
---

Python系列第七章笔记，查看Python系列所有文章，请点击[💿](http://c.biancheng.net/python/str_method/)

<!--more-->

本章记录定义函数、调用函数以及大量有关Python的高级内容。

还会记录Lambda表达式，学习完Lambda表达式后可以让源代码更加简洁。

# Python函数（函数定义、函数调用）用法详解

我们之前以及用到过很多的函数，例如:`print() range() len()` 等等，不过这些都是Python的内置函数，Python还允许我们自定义函数，也就是将一段代码定义成函数，从而达到`一次编写、多次调用的目的` 。

## Python函数的定义

想要定义函数需要使用def关键字实现，语法格式如下:

```
def function_name([params]):
    code_space
    [return [value]]
```

其中由`[]` 括起来的为可选部分。

语法格式解释:

- function_name: 函数名，需要符合合法的标识符。

- params: 形式参数列表，也就是定义该函数可以接受的参数。可以有多个，多个之间使用英文逗号(`,` )隔开。

- code_space: 代码块，也就是调用函数时需要执行的代码，记得缩进。

**注意: 在创建函数时，即使函数不需要参数，也必须保留括号。** 

例子:

```
# 求最大值
def my_max(x,y):
    return  x if x > y else y
```

## Python函数的调用

调用函数也就是执行定义过的函数。

函数调用语法格式:

`function_name([params])`

**注意:函数定义时有多少个参数，我们调用时就必须传入相同数量的参数个数。并且如果调用的函数原型没有参数，调用时也不能省略括号。** 

例子:

```
print(my_max(10,20))
```

运行过程:

```
20

[Process exited 0]
```

## 为函数提供说明文档

前目提到过可以使用`help()` 命令查看指定函数的帮助文档。

想要为函数添加说明文档可以在函数声明后，代码块之前插入字符串以作为函数的说明文档。

例子:

```
def say_helloworld():
    "输出HelloWorld"
    print("HelloWorld")

print(help(say_helloworld))
print(say_helloworld.__doc__)
```

运行过程:

```
Help on function say_helloworld in module __main__:

say_helloworld()
    输出HelloWorld
(END)

None
输出HelloWorld

[Process exited 0]
```

# Python函数值传递和引用传递(包括形式参数和实际参数的区别)

## 形参实参的区别

形参又被称为形式参数，也就是指：在定义函数时，函数列表中的参数，叫做形参。

实参又被称作实际参数，也就是指：在调用函数时，向函数列表中传递的参数，叫做实际参数。

## 值传递与引用传递

值传递使用场景: 不可变类型(字符串，数字，元组)
引用传递: 可变类型（列表、字典）

两者区别: **值传递的时候，实参传递给形参后，如果形参被修改，实参不收影响。引用传递时，则会改变。** 

例子:

```
def change_param(x):
    x+=[4] if isinstance(x,list) else 1
    print(x)
a = 10
change_param(a)
print(a)
b = [1,2,3]
change_param(b)
print(b)
```

运行过程:

```
11
10
[1, 2, 3, 4]
[1, 2, 3, 4]

[Process exited 0]
```

# Python函数参数传递机制(超级详细)

本笔记不讨论，想要了解[查看原文](http://c.biancheng.net/view/2258.html) 

# Python位置参数

一句话解释:`调用函数时传入的实参的数量和位置必须和定义函数时的形参保持一致` 

# Python关键字参数

如果不想要记住参数的位置，我们可以使用关键字参数特性，在调用函数时为实际参数指定一个参数名。

例子:

```
def test(x,y,z):
    return x*y+z
print(test(10,20,10))
print(test(z=10,y=20,x=10))
```

运行结果:

```
210
210

[Process exited 0]
```

**注意:如果要在传递实参时混用关键字参数与位置参数，必须确保关键字参数置于位置参数之前。**

# Python默认参数

我们可以给形参指定默认参数，这样在调用时，可以省略传入实参。

例子:

```
def user_name(name="未命名"):
    print("你的姓名:",name)

user_name()
user_name("EvanMeek")
```

输出结果:

```
你的姓名: 未命名
你的姓名: EvanMeek

[Process exited 0]
```

# Python 函数可变参数

如果在编写函数时，不确定需要使用多少个参数，我们就可以使用可变参数这个特性。

可变参数有两种形式，分别是在形参之前添加个**一**`*` 与在形参之前添加个**两**`*` 。

# 可变参数:形参前添加一个`*`

例子:

```
# 忽略这个反斜杠，因为markdown的缘故
def test(x,\*y):
    print(type(x),"\n",x)
    print(type(y),"\n",y)
test(10,"你好","世界",9.09,0xa)
```

输出结果:

```
<class 'int'>
 10
<class 'tuple'>
 ('你好', '世界', 9.09, 10)

[Process exited 0]
```

可以看到，实际上可变参数是将多个参数包含在一个元组内，然后将其输出。

## 可变参数:形参前添加两个`*` 

前面的第一种可变参数形式，是往形参前添加一个\*，并且我们知道它其实就是个元组，那么第二种形式提前透露一下，它其实就是个字典

例子:

```
def test(x,**y):
    print(type(x),"\n",x)
    print(type(y),"\n",y)
test(10,语文=100,数学=9.99,英语=8.88)
```

输出结果:

```
<class 'int'>
 10
<class 'dict'>
 {'语文': 100, '数学': 9.99, '英语': 8.88}

[Process exited 0]
```

## 可变参数：形参前添加两个`*`  

语法格式如下:

`**kwargs` 

- \*kw表示创建一个名为kwargs的空字典，该字典可以接收任意多个以关键字参数赋值的实际参数。

例子:

```
def test(x,**y):
    print(type(x),"\n",x)
    print(type(y),"\n",y)
test(10,语文=100,数学=9.99,英语=8.88)
```

运行结果:

```
<class 'int'>
 10
<class 'dict'>
 {'语文': 100, '数学': 9.99, '英语': 8.88}

[Process exited 0]
```

# Python逆向参数收集详解

逆向参数也就是说将程序中定义的列表、元组、字典等对象的元素拆开后传递给函数的参数。

**逆向参数收集需要在传入的列表、元组参数之前添加一个星号，在字典参数之前添加两个星号** 

例子:

```
def get_sum(*x):
    sum = 0
    for ele in x:
        sum += ele
    return sum

num_list = range(1,101)

print(get_sum(*num_list))
```

运行结果:

```
5050

[Process exited 0]

```

字典也支持逆向收集，字典会以关键字参数的形式传入。

例子:

```
def get_student(stu_id,stu_name,**x):
    print("学号:"+str(stu_id))
    print("姓名:"+str(stu_name))
    print("其他:"+str(x))

stu_info = {"stu_id":0,"stu_name":"张三","stu_age":18,"stu_address":"广州市"}
get_student(**stu_info)
```

输出结果:

```
学号:0
姓名:张三
其他:{'stu_age': 18, 'stu_address': '广州市'}

[Process exited 0]
```

# Python None(空值)及用法

Python中有一个特殊的常量`None`，其表示为空值，它不等于空列表，也不等于空字符串。

`None` 具有自己的数据类型，通过`type()` 可以查看它的类型。

```
<class 'NoneType'>

[Process exited 0]

```

`None` 为`NoneType` 数据类型的唯一值，不能创建其他NoneType类型的变量，但是可以为任何变量赋值为`None` 。


`None` 常用场景是:**assert断言，判断，以及函数无返回值。** 

# Python return函数返回值详解

语法格式:

`return [返回值]` 

return 语句是用于给函数的调用处返回一个值。

**return 语句可以在同一函数中出现多次，但只要有一个得到执行，就会结束函数的执行。** 

例子:

```
def sum(x,y):
    return x+y

print(sum(10,20))
```

输出结果:

```
30

[Process exited 0]
```

**return 的返回值可以为任意类型。** 

# Python函数返回多个值的方法

Python允许函数同时返回多个值，它会将多个返回值封装成元组。

例子:

```
def multi_return():
    return 10,20,30,40
# 序列解包
a,b,c,d = multi_return()
# 序列解包
test_list = multi_return()
print(a,b,c,d)
print(test_list)
print(multi_return())
```

输出结果:

```
10 20 30 40
(10, 20, 30, 40)
(10, 20, 30, 40)

[Process exited 0]
```

# Python partial偏函数及用法

[见原文](http://c.biancheng.net/view/5674.html) 

# Python函数递归

当一个函数体内调用自身，就被称为`函数递归` 


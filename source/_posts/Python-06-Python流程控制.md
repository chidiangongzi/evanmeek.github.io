---
title: '[Python-06]Python流程控制'
copyright: true
date: 2019-09-28 14:14:26
categories: Python
tags:
  - Python系列
---

Python中的流程结构也就是选择语句，选择语句又分为3种语法形式，分别是if、if else、if elif else。

if 语句语法格式:

```
if 表达式:
  代码块
```
if else 语句语法格式:

```
if 表达式:
  代码块 1
else:
  代码块 2
```

if elif else 语句语法格式:

```
if 表达式1:
  代码块 1
elif 表达式2:
  代码块 2
elif 表达式3:
  代码块 3
...
else:
  代码块 n
```

以上三种选择结构的语法形式差别不大，它们有个共性，就是**当表达式的值为True时会执行代码块内的代码** 。

选择语句的表达式相当于条件，当表达式的条件满足后，就会执行代码块内的代码啦。

**注意:Python的代码块是通过缩进标记的，具有相同缩进的多行代码属于同一个代码块** .

**if表达式真假值得判断方法** 

表达式可以是任意类型，不过下面的几种类型将会被Python解释器当做False处理:

`Flase、None、0、""、()、[]、{}` 

# Python if else语句用法范例(注意事项_)

**1)代码块不要忘记缩进** 

每一个缩进就代表了一个代码块，如果没有没有缩进程序可能会出现各种问题。

```
s_age = input("请输入您的年龄:")
age = int(s_age)
if age >= 18:
print("你成年了.")
```

输出结果:

```
File "test.py", line 4
  print("你成年了.")
      ^
IndentationError: expected an indented block
```

有时没有缩进不代表程序没有错误。

```
s_age = input("请输入您的年龄:")
age = int(s_age)
if age >= 18:
    print("你成年了.")
print("成年了，就要修身养性.")
print("你未成年.")
```

运行过程:

```
请输入您的年龄:10
成年了，就要修身养性.
你未成年.

[Process exited 0]
```

虽然程序没有报错，但是确是不符合逻辑的，应该是当输入的年龄大于等于18岁才输出成年了，就要修身养性，但是由于没有将其缩进，所以造成了代码的运行结果不如人意。

**2)语句不要随意缩进** 

我们必须保证同一个代码块内的代码必须保持相同的缩进，如果多一个缩进或少一个缩进都会出现不可预料的错误。

```
int a = 10
if a > 9:
    print("a > 9")
        print("====")
```

运行结果:

```
  File "test.py", line 1
    int a = 10
        ^
SyntaxError: invalid syntax
```

Python解释器抛出了一个SyntaxError错误

**3)if表达式不要遗忘冒号** 

Python解释器将冒号表示为代码块的开始，如果遗忘冒号也会引发一些错误，因为Python解释器无法识别代码块的开始。

```
if 10 > 9
    print("9 > 10")
else:
    print("10 < 9")
```

输出结果:

```
  File "test.py", line 1
    if 10 > 9
            ^
SyntaxError: invalid syntax

[Process exited 1]
```

以冒号作为代码块的开始在其他语句结构也是如此，例如循环、类等。

# Python if语句嵌套

此笔记不讨论此内容，如需了解，请点击此处[查看原文](https://evanmeek.github.io/2019/09/23/Python-05-Python字符串常用方法详解/) 

# Python pass语句及其作用

如果你想要一个代码块内什么都不做，但是没有这个代码块语法又不通过，你可以使用`pass` ，其是Python中的空语句，它什么也不做，唯一的功能就是占位了。

```
if 10 > 9:
    print("xxx")
else:
    pass
print("xxxx")
```

# Python assert断言函数及用法

`assert断言函数` 与if分支类似，不过它的特点是:**当它的表达式条件为False时将会抛出异常，程序崩溃** 。

```
num = int(input("请输入大于10且小于100的数字:"))
assert 10 < num < 100
print(num)
```

当我们输入非大于10且小于100的数字将会抛出异常:

```
请输入大于10且小于100的数字:1000
Traceback (most recent call last):
  File "test.py", line 2, in <module>
    assert 10 < num < 100
AssertionError

[Process exited 1]
```

# Python 如何合理使用assert

本小节通过一些实际应用的例子，演示assert在Python中的用法。

某商场促销活动，对商进行打折销售，现在需要做到如果折后价大于0或小于原价，那么输出折后价，否则报错。

```
# 原价
price = float(input("请输入原价:"))
# 折扣力度
discount = float(input("请输入打几折:"))
# 折后价
update_price = price * (discount * 0.1)
assert 0 < update_price < price
print("折后价为:{:.2f}¥".format(update_price))
```

正常结果:

```
请输入原价:100
请输入打几折:8
折后价为:80.00¥

[Process exited 0]
```

错误结果:

```
请输入原价:100
请输入打几折:18
Traceback (most recent call last):
  File "test.py", line 7, in <module>
    assert 0 < update_price < price
AssertionError

[Process exited 1]
```

在实际工作中，assert可以提前预防一些问题。

# Python while循环语句详解

本笔记不讨论`while` 循环语句的使用，想要了解的同学，可以点击[查看原文](http://c.biancheng.net/view/4427.html) 

# Python for循环及用法详解

本笔记不讨论`for` 循环语句的使用，想要了解的同学，可以点击[查看原文](http://c.biancheng.net/view/2225.html) 

# Python循环结构中else用法(入门必读)

Python中，循环语句后可以跟着一个else语句块。其作用是，当循环条件为Fale时，会直接执行紧跟着循环语句块后的else语句块内的代码。 

例子:

```
count_i = 0
while count_i < 5:
    print("count_i小于5:",count_i)
    count_i+=1
else:
    print("count_i大于或等于5:",count_i)
```

输出结果:

```
count_i小于5: 0
count_i小于5: 1
count_i小于5: 2
count_i小于5: 3
count_i小于5: 4
count_i大于或等于5: 5

[Process exited 0]
```

读者可能会想，这样做其实也没什么，就算没有else程序也照样会执行else内的代码。

其实这种语法是Python中一个为了让代码更加具有可读性、美观而有的一个语法。

for循环也是可以紧跟else的。

例子:

```
for i in range(1,6):
    print(i)
else:
    print("输出完毕")
```

输出结果:

```
1
2
3
4
5
输出完毕

[Process exited 0]
```

# Python(for和while)循环嵌套及用法

如果将一个循环语句放入一个循环体内，就会形成循环嵌套。

当程序遇到循环嵌套时，如果外层循环的循环条件允许，则会执行外层循环的循环体，而内层循环将会被外层循环的循环体来执行(只是内层循环需要反复执行自己的循环体而已)。只有当内层循环执行结束且外层循环的循环体也执行结束时，才会再次通过判断外层循环的条件，决定是否再次开始执行外层循环的循环体。

居上所述，假设外层循环的循环次数为n次，那么内层循环的循环次数为m次，那么可得出内层循环的循环体实际上需要执行`n x m` 次。

例子:

```
for i in range(0,3):
    j = 0
    while j < 3:
        print("i:{}\tj:{}".format(i,j))
        j += 1
```

输出结果:

```
i:0     j:0
i:0     j:1
i:0     j:2
i:1     j:0
i:1     j:1
i:1     j:2
i:2     j:0
i:2     j:1
i:2     j:2

[Process exited 0]
```

i 为外层循环的数，j为内层循环的数，可以看到每次内层循环结束后外层循环的i才会发生改变，当时每次外层循环结束后，再次进入循环体后，将会重置内层循环j的值。

嵌套循环可以无限嵌套，但开发者最好不要超过三层循环，不然逻辑很容易混乱。

# Python嵌套循环实现冒泡排序

冒泡排序算法的实现思想:

- 比较相邻元素大小，若前一个比后一个大则交换位置。

- 从第一对相邻元素到结尾的最后一对相邻元素，对每一对相邻元素做上一步骤的比较工作，并将最大的元素放在后面。

- 将循环缩短，除去最后一个数，再重复第二步骤操作。

- 持续做步骤三操作，将每次循环缩短一位。

实现:

```
test_list = [10,23,4522,55,13,5123,5,1321235.33,42.123]

for i in range(len(test_list)-1):
    # 每次得到最大值后循环缩短，因为最大值已经在最后
    for j in range(len(test_list)-i-1):
        # 如果相邻元素的第一个元素比第二元素大则:
        if(test_list[j]>test_list[j+1]):
            test_list[j],test_list[j+1]=test_list[j+1],test_list[j]
print("排序后:",test_list)
```

输出结果:

```
排序后: [5, 10, 13, 23, 42.123, 55, 4522, 5123, 1321235.33]
```

# Pyton break用法详解

在我们使用循环时，当条件满足那么循环体内的代码将会一路执行，直到循环体结束为止，如果我们想在执行循环体时直接终止循环或跳出本次循环，则可以使用`coontinue`或`break` 语句。


**break用于完全结束一个循环，杀死循环。** 

例子:

```
sum = 0
for i in range(0,100000):
    print("i的值为:",i)
    sum += i
    if sum == 5050:
        break
```

输出结果:

```
i的值为: 0
i的值为: 1
i的值为: 2
i的值为: 3
i的值为: 4
...
...
i的值为: 94
i的值为: 95
i的值为: 96
i的值为: 97
i的值为: 98
i的值为: 99
i的值为: 100
```

可以看到，当sum值为5050时，循环将会被杀死，不再执行。


如果循环体外带上了else块，那么如果循环体内执行了break语句，则else语句块内的代码不会被执行。

```
for i in range(1,4):
    print(i)
    if i > 2:
        break
else:
    print("else")
```

输出结果:

```
1
2
3

[Process exited 0]
```

可以看到，当for循环体内执行了break语句后，else内的代码也不会执行。

**break语句只能结束当前执行的循环，而不能结束被嵌套循环的外层循环。**

# Python continue用法

continue与break类似，但不同点在于continue只能跳出本次循环，并不能终止循环。

例子:

```
for i in range(1,5):
    if i == 2:
        continue
    print(i)
```

输出结果:

```
1
3
4

[Process exited 0]
```

可以看到，当循环内部执行continue之后，下面的代码将不会被执行。

# 如何避免Python出现死循环 

为了避免Python程序出现死循环，所以**必须确保循环结构中至少有能让循环条件为False或让break语句得以执行的语句。** 

# Python推导式详解

Python推导式，是Python独有的一种特性。使用推导式可以快速生成列表、元素、字典以及集合类型的数据。

列表推导式利用range区间、元组、列表、字典和集合等数据类型、快速生成一个满足指定需求的列表。

语法格式:

`[表达式 for 迭代变量 in 可迭代对象 [if 条件表达式]]` 

**if条件表达式为非必须的。**

## 列表推导式

例子:

求0-10的平方

```
test_list = [x * x for x in range(11)]
print(test_list)
```

输出结果:`[0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]`

例子2:

求0-10的平方，并且满足可以整除2

```
test_list = [x * x for x in range(11) if x % 2 == 0]
print(test_list)
```

输出结果:

`[0, 4, 16, 36, 64, 100]` 

上面的列表推导式都只有一个循环，但实际上它可以使用多个循环。

例子:

```
test_list = [(x,y)for x in range(5) for y in range(4)]
print(test_list)
```

输出结果:

```
[(0, 0), (0, 1), (0, 2), (0, 3), (1, 0), (1, 1), (1, 2), (1, 3), (2, 0), (2, 1)
, (2, 2), (2, 3), (3, 0), (3, 1), (3, 2), (3, 3), (4, 0), (4, 1), (4, 2), (4, 3
)]

[Process exited 0]
```

其实Python的列表推导式可以使用循环语句重写:

```
test_list2 = []
for x in range(5):
    for y in range(4):
        test_list2.append((x,y))
print(test_list2)
```

输出结果同上

当然，也支持多层循环嵌套的推导式。

## 元组推导式

元组推导式同列表推导式一样，可以使用range区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的元组。

语法格式:

`(表达式 for 迭代变量 in 可迭代对象 [if条件表达式])` 

**if条件表达式为可选** 

首先将元组推导式与列表推导式做一个对比。

例子:

```
test_list = [x for x in range(10)]
print(test_list)
test_tuple = (x for x in range(10))
print(test_tuple)
```

输出结果:

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
<generator object <genexpr> at 0x106f3d450>

[Process exited 0]
```

可以看到，除了元组推导式是使用`()` 圆括号而列表推导式是使用`[]` 方括号之外，还有就是元组推导式生成的结果并不是一个元组，而是一个`生成器对象` 。

我们可以通过`tuple()` 函数将生成器对象转换为元组或使用循环遍历生成器对象，获取各元素。

```
x =  (x for x in range(10))
for ele in x:
\    print(ele,end=" ")
print(tuple(x))
```

输出结果:

`0 1 2 3 4 5 6 7 8 9 ()` 

**注意:当我们遍历了生成器对象后，原生成器对象将不复存在，这就是为什么我们遍历了生成器对象后再将原生成器对象转换却得到空元组的原因** 

我们还可以使用`__next__()` 方法遍历，但很不方便。

```
x =  (x for x in range(10))
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(tuple(x))
print(x.__next__())
```

输出结果:

```
0
1
2
3
4
5
6
7
8
9
()
Traceback (most recent call last):
  File "test.py", line 13, in <module>
    print(x.__next__())
StopIteration

[Process exited 1]
```

可以看到被遍历后的生成器将会被清空，并且需要注意的是**__next__方法需要不能越界** 

## Python 字典推导式

同前两个推导式一样，都可以接住多种数据类型生成符合需求的字典。

语法格式:

`{表达式 for 迭代变量 in 可迭代对象 [if 条件表达式]}` 

例子:

将列表内元素作为键，其元素长度为值

```
test_list = ['Hello',"World"]
test_map = {key:len(key) for key in test_list}
print(test_map)
```

输出结果:

`{'Hello': 5, 'World': 5}` 

例子2:

调换键值对

```
test_list = ["语文","数学","英语"]
test_dict = dict.fromkeys(test_list,100)
print(test_dict)
test_dict2 = {v:x for x,v in test_dict.items()}
print(test_dict2)
```

输出结果:

```
{'语文': 100, '数学': 100, '英语': 100}
{100: '英语'}

[Process exited 0]
```

## Python集合推导式

同上，可以使用常用数据类型快速生成符合需求的集合。

语法格式:

`{表达式 for 迭代变量 in 可迭代对象 [if 条件表达式]}` 

**注意：集合推导式的语法格式与字典推导式的语法格式相同，为了区分它们，同时看表达式的形式，如果是以键值对(key:value)的形式，那么就是字典，否则反之** 

例子:

```
newset = {i**2 for i in range(3)}
print(newset)
print(type(newset))
```

输出结果:

```
{0, 1, 4}
<class 'set'>

```

# Python zip函数及用法

`zip()` 函数可以将多个列表转化一个zip对象(可迭代对象)。

例子:

```
list1 = list(range(1,10))
list2 = list(range(-10,0))
print([x for x in zip(list1,list2)])
```

输出结果:

```
[(1, -10), (2, -9), (3, -8), (4, -7), (5, -6), (6, -5), (7, -4), (8, -3), (9, -
2)]

[Process exited 0]
```

# Python reversed函数及用法

reversed()函数用于将各种序列进行**逆序排序** ，但不会影响序列本身。

例子:

```
string = "HelloWorld"
print([x for x in reversed(string)])
```

输出结果:

`['d', 'l', 'r', 'o', 'W', 'o', 'l', 'l', 'e', 'H']` 


# Python sorted函数及用法

sorted函数用于将各种序列进行排序。

例子:


```
string = "123456789"
re_string = [x for x in reversed(string)]
print(re_string)
sort_string = sorted(re_string)
print(sort_string)
```

输出结果:

```
['9', '8', '7', '6', '5', '4', '3', '2', '1']
['1', '2', '3', '4', '5', '6', '7', '8', '9']

[Process exited 0]
```

# Python项目实战之猜数字游戏

代码如下:

```
# 随机数模块
import random

print("{0:=^20s}{1:s}{0:=^20s}\n".format("==========","欢迎游玩猜数字游戏"))

# 随机数(1-20之间)
randomNum = random.randint(1,20)

# 只给用户5次机会

for count in range(1,6):
    print("\n算上这次，你还有{:d}次机会!\n".format(5-count))
    num = int(input("请输入猜测的数(范围1~20):"))
    if num>randomNum:
        print("\n系统>> 大了点!!!")
    elif num < randomNum:
        print("\n系统>> 小了点!!!")
    else:
        print("\n系统>> 恭喜你猜中了数字!!!")
        break
else:
    print("\n系统>> 很遗憾，你没有猜到正确答案，答案为:{:d}".format(randomNum))
```

猜中运行实例:

```
====================欢迎游玩猜数字游戏====================


算上这次，你还有4次机会!

请输入猜测的数(范围1~20):10

系统>> 小了点!!!

算上这次，你还有3次机会!

请输入猜测的数(范围1~20):15

系统>> 大了点!!!

算上这次，你还有2次机会!

请输入猜测的数(范围1~20):14

系统>> 大了点!!!

算上这次，你还有1次机会!

请输入猜测的数(范围1~20):13

系统>> 恭喜你猜中了数字!!!

[Process exited 0]
```

猜错运行实例:

```
====================欢迎游玩猜数字游戏====================


算上这次，你还有4次机会!

请输入猜测的数(范围1~20):1

系统>> 小了点!!!

算上这次，你还有3次机会!

请输入猜测的数(范围1~20):1

系统>> 小了点!!!

算上这次，你还有2次机会!

请输入猜测的数(范围1~20):1

系统>> 小了点!!!

算上这次，你还有1次机会!

请输入猜测的数(范围1~20):1

系统>> 小了点!!!

算上这次，你还有0次机会!

请输入猜测的数(范围1~20):1

系统>> 小了点!!!

系统>> 很遗憾，你没有猜到正确答案，答案为:3

[Process exited 0]
```
# Python项目实战: 绕圈圈面试题

```
SIZE = 7

array = [[0] * SIZE]

# 创建一个长度SIZE * SIZE的二维列表
for i in range(SIZE - 1):
    array += [[0] * SIZE]

# 绕圈的方向(0:下 1:右 2：左 3:上)
orient = 0

# l 控制行索引 c控制列索引
l = 0
c = 0

for i in range(1,SIZE * SIZE + 1):
    array[l][c] = i

    # 如果位于1号转弯线上
    if l+c == SIZE - 1:
        # l > c，位于左下角
        if l > c:
            orient = 1
        else :
            orient = 2
    elif (c == l) and (c >= SIZE / 2):
        orient = 3
    elif (l == c - 1) and (c <= SIZE / 2):
        orient = 0
    if orient == 0:
        l += 1
    elif orient == 1:
        c += 1
    elif orient == 2:
        c -= 1
    elif orient == 3:
        l -= 1
for i in range(SIZE):
    for j in range(SIZE):
        print("%02d" % array[i][j],end = "")
    print("")
```





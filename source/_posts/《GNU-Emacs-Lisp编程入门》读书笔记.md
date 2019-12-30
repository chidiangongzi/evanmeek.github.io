---
title: 《GNU Emacs Lisp编程入门》读书笔记
copyright: true
date: 2019-12-21 16:17:25
categories: Lisp
tags:
 - EmacsLisp
---

借了本Elisp的书，不厚，200多页，大概一周(两周)就能看完吧!

<!--more-->

# 第一章 列表处理 #

列表是Lisp的基础。

## Lisp列表 ##
### 介绍 ###

简单的Lisp列表书写形式:

``` emacs-lisp
'(rose violet daisy buttercup) ;; => (rose violet daisy buttercup)
```

这个简单的列表中的四个元素时四种不同花的名称。**元素之间用空格隔开，并且被括号包住。**

另有一种在elisp中常用到的写法:

 
```emacs-lisp
(+ 2 2) ;; => 4
```

这种写法是Lisp的一个特性————**数据和代码都用相同的方式表示**。

**列表还允许嵌套列表，也就是说列表的元素也可以是列表**。

### Lisp原子 ###


原子意味着"不可再分"。例如刚刚列表内的'2'或者是'rose'等等，这些都是原子。

而列表却不是原子，因为**列表是由CAR和CDR与CONS构成的**。

技术上说，Lisp的列表有三种组合方式:
  * 括号和括号中由空格分隔的原子
  * 括号和括号中的其他列表
  * 括号和括号中的其他列表和原子

**一个列表可以仅有一个原子或完全没有原子**

无任何原子的列表称作空列表: `()`。你可以把空列表看为原子或列表。

*原子和列表可以被称为**符号表达式**(symbolic expression)，又可称为**S-表达式** *。

Lisp编程几乎都是关于列表中的符号的(且有时是关于数字的).

**双引号中的文本，都是单个原子**:`'(Info "Name:EvanMeek Age:18 Sex:Men**)`

这种被双引号括起来的文本叫做**字符串(string)**。

### 列表中的空格 ###

Lisp中括号的数量无关紧要。下面两个的列表是完全相同的。

括号多
``` emacs-lisp
'(1 2 3 4      5       6) ;; => (1 2 3 4 5 6)
```

括号少
``` emacs-lisp
'(1 2 3 4 5 6) ;; => (1 2 3 4 5 6)
```

适当的在列表中加入一些空格以及换行符可以提高可读性。


### GNU Emacs帮助你输入列表 ###

在Emacs中使用Emacs Lisp模式或Lisp交互模式输入Lisp表达式时可以用`Tab`按键使光标所在行自动缩排到适当的位置。要使某个区域的表达式都自动缩排的快捷键是`C-M-\`

并且Emacs会具有括号匹配的功能，以防你迷失在Lisp的括号海洋中。

有兴趣的可以看下这个知乎提问。<https://www.zhihu.com/question/356026550>

## 运行一个程序 ##

如果你想运行一段Lisp程序，那么计算机可能会做三种事:
* 只返回列表本身;
* 提示出错信息;
* 将列表中第一个符号作为要执行的命令;
大多数情况，我们希望计算机做的是第三件事

前面我们看到过一些列表的前面有一个单引号"'"，它其实是Lisp中的一个引用(quote)。它的作用是告诉Lisp不要做对这个列表做任何操作，只返回列表本身即可。

``` emacs-lisp
'(只是返回本身 即可) ;; => (只是返回本身 即可)
```

而如果列表前没有quote，那么列表的第一个符号就会称为Lisp要执行的命令(函数)，后面的则是函数的参数。

``` emacs-lisp
(+ 1 2 3 4) ;; => 10
```

Emacs中可以将光标放置一对S-表达式后按 `C-x C-e`就会将表达式读入至Lisp解释器中，进行解释，将结果输出至回显区，英文叫 `mini buffer`。

也可以对原子(没有被括号括起来)求值

## 产生错误消息 ##

编写Lisp代码时难免遇到错误，而Lisp解释器会在程序出错时输出报错信息。与其说是报错信息，不如说是有助的信息(书上这么说)。

下面，我们对一个没有引用并且第一个元素不是一个有意义的符号的列表进行求值。

``` emacs-lisp
(Just Error!) ;; => Symbol's function definition is void: Just
```
这个输出结果就像是出错了一样，它告诉我们Just符号命令没有定义。也就是说Lisp解释器视图将`(Just Error!)`当成类似`(+ 1 2)`这种列表进行求值，但由于后者的第一个元素"+"是有意义的(已定义)，不会有任何问题，而我们编写的列表中第一个元素"Just"是没有任何意义(未定义)的，Lisp解释器不知道怎么办了，只好告诉我们一些有用的信息。


 ##

我们已经讨论过一些符号或函数，例如"+"。就以"+"为例子，当我们对`(+ 2 2)`表达式求值时，计算机并不是执行的"+"这个命令，而是执行其对应的指令。我们甚至可以随意改变，例如我把"+"改为"Plus"。





## Lisp解释器 ##

下面，简单解释下Lisp解释器在对一个列表求值时做了些什么。
* 首先，检查列表前是否有单引号(quote)，如果有则直接返回这个列表的输出形式。
* 若没有单引号则查看列表的第一个元素，是否有相对应的函数定义，如果有则执行对应的指令。
* 若没有则提示错误消息。
以上就是Lisp解释器的工作方式。但都比较简单，下面将会介绍几种比较复杂的工作方式。

* 第一种。Lisp解释器还可以对符号求值(并不是只能对列表)，但这个符号前不能有单引号和被括号括起。
* 第二种，Lisp解释器在遇到一些特殊函数时。这些特殊的函数以特殊的方式运行着，这些特殊函数通常被称为特殊表(special form)。见名知意，它用于一些特殊的工作，例如定义函数之类的。
* 第三种，Lisp解释器在遇到一些不是特殊表，而是列表的一部分时。这可能意味着是一个嵌套列表，Lisp解释器首先查看列表中是否有另外一个列表，如果有则先解释内部列表，如果内部列表仍然具有一个列表，那么就再次解释更深的列表层级中的列表，最终以此返回结果。

否则Lisp解释器将会从左往右依次执行。

### 字节编译 ###

Lisp解释器还可以将Lisp代码编译成字节。这样的好处是可以让程序的执行速度更快，缺点是可读性几乎为零。

被编译成字节码后的源码叫做elc，可以通过命令`(byte-compile-file)`进行编译。


## 求值 ##

前面我们所得到的一些结果，都是由Lisp解释器求值得到的。求值也就是Lisp解释器处理表达式时进行的操作。

解释器对表达式求值时几乎总是会返回值，如果没有返回值，通常是会提示一些错误信息。

解释器对表达式求值不仅会返回值，还可能会有一些附加效果，可能是移动光标或拷贝文件、刷新Buffer之类的动作。

### 对一个内部列表求值

上一节我们讨论过嵌套列表，这一小节解释了为什么内层列表总是首先被求值。首先给出答案:因为内层列表的返回值要被外层列表所使用。

下面通过一个例子了解这个求值的过程。

``` emacs-lisp
(+ 1 (+ 2 3))
```

我们知道使用快捷键`C-x C-e`可以对一个表达式求值，那么我们将光标放置`(+ 2 3)`表达式之后，然后按下这个快捷键，看看会发生什么。很显然，我们得到返回值`5`，那么再将光标放置整个表达式之后，按下快捷键得到返回值`6`。这就很好的解释了Lisp解释器对嵌套列表的求值过程。

我们可以通过快捷键`C-h k`然后键入`C-x C-e`查看这个快捷键所对应的符号(命令\函数)，也就是`eval-last-sexp`。 这个函数的作用是**对最近的一个表达式进行求值，并且将结果打印至输出区域**。





## 变量 ##

其他语言中，我们经常将某值赋值给一个变量，但你有见过可以将一个函数赋值给一个变量的语言吗(Python)?

**在Lisp中，我们可以把值赋值给符号，并且这个符号的值可以使Lisp中任意表达式(符号、数字、列表、字符串)**，并且符号的值是可变的，我们把一个有值的符号称为变量。

前面提到的将一个函数定义赋值给一个符号就是通过Lisp中变量的特性。**Lisp的符号可以同时具有一个函数定义和一个值。**我们可以把这种概念想象成具有多个抽屉的柜子。

例如变量`fill-column`是一个有值的符号，对它求值可以获取自动换行的字符数。

任何值都可以赋给符号，这个操作是:变量与一个值进行绑定。

`fill-column`只是一个很普通的值而已，如果我们对其求值时加上括号，将会发生一些错误。

``` emacs-lisp
(fill-column) ;; => Symbol's function definition is void: fill-column
```
这个错误被打印在回显区，很容易可以理解为什么会出现这个错误。因为Lisp解释器将这个列表读入后试图寻找第一个元素与之相联系的函数定义，让而fill-column只是一个值为数字的变量罢了，所以就会引发这个错误。

### 符号无值时的错误信息 ###

下面我对一个没有赋值的符号进行求值。
``` emacs-lisp
(+ 2 2) ;; => 4
```
很显然，如果是在这个表达式右括号后执行`eval-last-sexp`将不会有任何问题，但我们现在将光标移动至`+`后，执行`eval-last-sexp`，会引发这个报错提示:`Symbol's value as variable void: +`。

这是因为Lisp解释器将无值的符号当成一个变量处理了，而Lisp解释器却没有找到任何关于`+`的变量，只找到了函数定义，因为就报错了。

## 参量 ##

参量对应着`argument`，也就是其他语言中参数的意思。例如`(+ 2 3**`这个列表的参数就是`2`和`3`，而这个`+`则是函数，`+`允许由多个参量。

**不同的函数需要不同数目的参量，有些函数甚至不需要参量。**

### 参量的数据类型 ###

函数所接收的参量也是有数据类型的限制的，例如`+`函数就规定其参量的值必须是数字。

有些函数允许有任意数量个参量，例如`concat`函数，它将任意多个字符串类型的参量合并为一个字符串。

``` emacs-lisp
(concat "My name is:" "EvanMeek") ;; => "My name is: EvanMeek"
```

**请注意，`concat`函数的参量类型需要字符串并不意味着参量就必须写上字符串，这里指的是参量的值必须是字符串，请不要混淆。**

例如我们可以在`concat`的参量中写上`substring`函数。

``` emacs-lisp
(concat "Nice to meet " (substring "fuck you" 5 8))
```
上面的`concat`是一个参量必须都为字符串类型且任意数量的函数，而`substring`是一个可变数量参量且有多种参量类型的函数。
`substring`是可以对字符串这种单原子抽取出子字符串的，而这种操作可以取个好玩的名称`原子分裂机`。





### 作为变量和列表的值的参量 ###

> 上一小节提到————有些函数允许有任意数量个参量，且参量数据类型不同，我们可以理解为有些函数的参量可以是任意任意数量个符号。

这一节，我们将谈谈函数的参量还支持那些。

函数参量还支持列表和变量，当参量为变量时，Lisp解释器就会寻找是否有有值的变量，如果有就返回值，例如:

``` emacs-lisp
;; 结果可能不同，取决于你的Emacs配置。
(+ 2 fill-column) ;; => 82
```

并且参量还可以是一个列表，例如:

``` emacs-lisp
(+ 2 (+ 3 (+ 4))) ;; =>  9
```


### 数目可变的参量 ###
前面提到过的函数已经具有这个规则了，参量的数目可变，例如我们已经知道的`+`函数:

``` emacs-lisp
(+) ;; => 0
(+ 2) ;; => 2
```
又或是`\*`函数:

``` emacs-lisp
(*) ;; => 1
(* 2) ;; => 2
```

所以它们都具有一个特性————参量数量可变。

``` emacs-lisp
(* 1 2 3) ;; => 66
(+ 1 2 3) ;; => 6
```



### 用一个错误类型的数据对象作为参量 ###

试想下，如果我们对函数提供了错误类型的参量会发生什么？

``` emacs-lisp
(+ 2 'hello) ;; => Wrong type argument: number-or-marker-p,hello
```
我们知道`+`函数的参量必须是数字，而我们传入的参量2的`'hello`被Lisp解释器操作时会试图将`2`和`'hello`的返回值相加，但是`'hello`的返回值不是一个数字，所以就会引发这个错误。

让我们来试着解读下Lisp解释器提示的错误信息。首先Lisp解释器明确的告诉了我们————Wrong type argument(参量类型错误)，再是一段我们看不懂的符号`number-or-marker-p`这个符号意味着:Lisp解释器提示我们`+`函数的参量所需的数据类型，`number`也就是数字，而`marker`是一个标记(Elisp的一个特性，缓冲区的位置是由标记决定的，我们可以通过快捷键C-@C-SPC命令设置标记)， 而`p`则是Lisp的一个历史问题(早期Lisp程序员中用"p"替代"predicate"用于表示是否为真)，类似的有`zerop`用于判断参量值是否为零。最后的`hello`则是我们传给`+`函数出错的参量的值。

### message函数 ###
`message`函数用于给用户发送消息。这些消息是被打印在回显区的，它的第一个参量要求为一个`FORMAT STRING`(可格式化字符串)。

``` emacs-lisp
(message "Should you sleep now?") ;; => Should you sleep now?
```
双引号中的文本被打印在回显区(我们看到的是表达式的返回值，而打印只是一个附加效果)，这显得没什么新奇的，我们直接写一个字符串原子并且对其求值貌似也有同样的结果，下面将会介绍格式化字符串。

``` emacs-lisp
(message "The name of this buffer is: %s" (buffer-name)) ;; => "The name of this buffer is: 《GNU-Emacs-Lisp编程入门》读书笔记.md"
```
这输出了我当前buffer的名称。重点在于第一个参量中存在一段特殊的子串`%s`，`message`函数的第二个参量的值将用于它，这个`%s`代表了接收一段字符传，类似的还有`%d`用于接收一个十进制数。

``` emacs-lisp
(message "The value of fill-column is %d" fill-column) ;; => "The value of fill-column is 80"
```

这些特殊子串都支持变量、列表或符号，例如：

``` emacs-lisp
(message "我想吃%s，各来%d斤!" (concat "苹果、" "梨子、" "葡萄") (+ 1 1)) ;; => "我想吃苹果、梨子、葡萄，各来2斤!"
```

从第二个参量开始将会一次取代第一个参量中特殊子串的位置。
## 给一个变量赋值 ##

这一小节学习为一个变量赋值，常用的操作有`set`、`setq`、`let`，在这节主要将`set`和`setq`。并且描述这两个函数是如何工作的。

### 使用set函数 ###

我们要为`flowers`符号附上一个列表值，那么可以这么写 
```emacs-lisp
(set 'flowers '(菊花 百合 玫瑰)) ;; => (菊花 百合 玫瑰)
```
这意味着我们将列表`菊花 百合...`绑定给了`flowers`符号。

两个参量的引用是为了让其不要求值，所以你可以知道`set`函数的第一个参量最好要加上引用，这大概是很常用的搭配。

### 使用setq函数 ###

`setq`函数与`set`函数很相似，它们只有一个区别，就是`setq`函数会自动给第一个参量加上引用，例如用`setq`完成上一小节的例子:

``` emacs-lisp
(setq flowers '(菊花 百合 玫瑰)) ;; => (菊花 百合 玫瑰)
```

并且它们俩都是可以为多个变量绑定多个值的，例如:

``` emacs-lisp
(setq 学生 '(学号 地址 姓名 电话)
      老师 '(教师号 地址 姓名 电话))
学生 ;; => (学号 地址 姓名 电话)
老师 ;; => (教师号 地址 姓名 电话)
```

其中参量二绑定给参量一，参量四绑定给参量三，以此类推。




### 计数 ###

就是用`setq`函数完成了一个递增的操作。

首先生成一个初始化器，再生成一个递增器，再进行输出数值。

``` emacs-lisp
(setq count 0) ;; 初始器
(setq count (1+ count)) ;; 递增器
count ;;输出
```

## 小结 ##
记录一下，加油努力，毕竟书中都说了，我已经跨过了最陡峭的那段山路。

  * Lisp程序由表达式组成，表达式是列表或单个原子。
  * 列表由0个或更多的原子或内部列表组成，原子或列表之间由空格隔开，并由括号括起来，列表可为空。
  * 原子是多字符的符号(如fill-column)，单字符的符号(如+号)，双引号之间的字符串或者数字。
  * 对数字求值就是其本身
  * 对双引号之间的字符串求值也是其本身
  * 当对一个符号求值时，将返回它的值。
  * 当对一个列表求值时，Lisp解释器查看列表首符号绑定在其上的函数定义，并执行其指令。
  * 单引号告诉Lisp解释器返回后续表达式的书写形式，而不是像没有单引号时那样对其求值。
  * 参量是传递给函数的信息。除了作为列表的第一个元素的函数之外，通过对列表的其余元素求值来计算函数的参量。
  * 当对一个函数求值时总是返回一个值(除非得到错误信息)。另外，它也可以完成一些被称作附带效果的操作。在许多情况下，一个函数的主要目的是产生一个附带效果。
  
  **最后，希望这篇博客可以记录好第一章所讲。**

## 练习 ##

一个一个来，题目写在博客内吧...

* 通过对一个不在括号内的适当符号求值，产生一个错误信息。

解答:

``` emacs-lisp
一个不存在的变量 ;; => Symbol's value as variable is void: 一个不存在的变量 
```

* 通过对一个在括号内的适当符号求值，产生一个错误信息。

解答:

``` emacs-lisp
(又一个不存在的符号) ;; => Symbol's function definition is void: 又一个不存在的符号
```

* 创建一个每次增加2而不是1的计数器。

解答:

``` emacs-lisp
(setq count 0) ;; 初始器 
(setq count (+ 2 count)) ;; 递增器
count ;;输出
```

* 写一个表达式，当对它求值时，它在回显区输出一条消息。

解答:

``` emacs-lisp
(message "这段消息是要输出至%s%s的" '回显 "区")
```

# 第二章 求值实践 #

这一章主要讲了关于buffer的一些知识，讲了一些关于buffer的函数，并且讲解了一些buffer的注意事项。

## 缓冲区名 ##

讲了两个函数，分别是`(buffer-name)`以及`(buffer-file-name)`。

首先得清楚buffer和文件的概念，buffer的中文翻译叫做缓冲区，它其实是将文件中的内容拷贝到Emacs中，所以在我们修改buffer时，文件并不会改动，只有当我们进行保存修改时才会。而文件是保存在磁盘上的信息，人们常常在修改buffer时说成"我在修改xx文件"，这严格意义上讲是错误的，但人们都知道其实我只是在修改buffer，而不是那个文件，只不过说成文件罢了，所以各位小伙伴不要误解。

计算机没有人类那么聪明，所以大家在写代码时要分清楚这两个的不同。

``` emacs-lisp (buffer-name) ;; => "《GNU-Emacs-Lisp编程入门》读书笔记.md"
(buffer-file-name) ;; =>"/home/evanmeek/Documents/Blog/source/_posts/《GNU-Emacs-Lisp编程入门》读书笔记.md"
```
**表达式`(buffer-name)`用于获取当前buffer的名称而`(buffer-file-name)`用于获取当前buffer所对应文件的完整路径**，还要说明一点，并不是所有的buffer都有所对应的文件，例如`\*scratch\*`buffer就没有所对应的文件。

## 获得缓冲区 ##

如果想获得缓冲区本身，那么可以使用`current-buffer`。

``` emacs-lisp
(buffer-name) ;; => "《GNU-Emacs-Lisp编程入门》读书笔记.md"
(current-buffer) ;; => #<buffer 《GNU-Emacs-Lisp编程入门》读书笔记.md>
```
我们发现这两个函数的返回值挺相似的，但实际上他们却完全不同，`buffer-name`获取到的只是一个名称罢了，而`current-buffer`函数获取到的是一个名称所指向的对象或实体。举个生活上的例子:你对小明说:"小明，帮我拿个苹果"，然后小明就拿给了你"苹"和"果"字，显然这不是你真正想要的，你想要的是叫苹果的那个实体，可以吃的，有维生素的水果。经过这个例子，希望大家都能理解。 

## 切换缓冲区 ##

先介绍一个函数————`other-buffer`，这个函数用于发挥最近常打开过的buffer对象。例如最近常在`\*scratch\*`与`test.el`之间切换buffer，那么当前buffer为`\*scratch\*`时调用`(other-buffer)`时将会返回`test.el`的buffer对象。

再介绍一个函数————`switch-to-buffer`，这个函数接收一个`Buffer`对象的参量，可以切换当前buffer为`Buffer`参量。

``` emacs-lisp
(buffer-name) ;; => "《GNU-Emacs-Lisp编程入门》读书笔记.md"
(other-buffer) ;; => #<buffer *Backtrace*>
;; 根据最近最常打开过的buffer对象切换buffer
(switch-to-buffer (other-buffer))
(buffer-name) ;; => "*Backtrace*"
```
如果想要回到上一个buffer可以键入键序列`C-x b RET`，RET是回车。

前面几次提到`调用(call)`这个概念，实际上Lisp解释器对一个列表的首元素为一个函数进行处理时，就是在调用那个函数。

## 缓冲区大小和位点的定位 ##

先为大家介绍下四个函数:
  * `(point)`  
  ;; 获取当前光标在当前buffer的位点。
  * `(buffer-size)`
  ;; 获取当前buffer的字符数(包括空格)
  * `(point-min)`
  ;; 获取当前光标中位点的最小可能值。默认是1,除非设置了变窄,毕竟默认是从第一个字符开始
  * `(point-max)`
  ;; 获取当前光标中位点的最大可能值。默认是最后一个字符的point,除非设置了增宽。
  
``` emacs-lisp
;; 获取当前buffer的字符数(包括空格)
(buffer-size) ;; => 10636
;; 获取当前光标在当前buffer的位点。
(point) ;; => 10525
;; 获取当前光标中位点的最小可能值。默认是1,除非设置了变窄,毕竟默认是从第一个字符开始
(point-min) ;; => 1

;; 获取当前光标中位点的最大可能值。默认是最后一个字符的point,除非设置了增宽。
(point-max) ;; => 10670
```

## 练习 ##

找一个文件，对它进行操作，将光标移动到缓冲区的中间部分。找出它的缓冲区名、文件名、长度、和你在文件中的位置。

* 缓冲区名

``` emacs-lisp
(buffer-name) ;; => "《GNU-Emacs-Lisp编程入门》读书笔记.md"
```

* 文件名

``` emacs-lisp
(buffer-file-name) ;; => "/home/evanmeek/Documents/Blog/source/_posts/《GNU-Emacs-Lisp编程入门》读书笔记.md"
```

* 长度

``` emacs-lisp
(buffer-size) ;; => 11005
```

* 在文件中的位置

``` emacs-lisp
(point) ;; => 11033
```

# 第三章 如何编写函数定义 #

本章内容较多，不止于函数定义，还介绍了一些常用的函数。

## defun 特殊表 ##

`defun`不以通常的方式对它的参量求值，因为它是特殊表。

这节将简单描述函数定义的过程。

一个函数定义在`defun`之后最多可有5个部分:
* 符号名，这个符号指向了这个函数的定义。
* 一个列表，包含了要传给函数的参量。若没有任何参量要传递，那么可以写空列表。
* 这个函数的文档，由双引号括住，此选项为可选。
* 使当前函数成为一个交互式函数的列表，此选项为可选。交互式函数将会在后的小节讲到。
* 函数的主题，也就是一系列的命令。
下面是一个包含了五个部分的函数模板:

``` emacs-lisp
(defun funciton-name (arguments...)
  "optional-documentation"
  (interactive argument-passing-info) ;; optional
  body...)
```

我们通过这个模板写一个简单的函数吧，这个函数的功能呢是让其参量乘以7。

``` emacs-lisp
(defun multiply-by-seven (number)
  "使number(参量)乘以7"
  (* number 7))
```

这个函数的函数名就是`multiply-by-seven`，而函数名后面的列表也就是函数的参量，当我们调用函数时，传递给函数的参量的值就会被绑定到这个`number`上。并且`number`也可以为其他的名称，这取决于写代码的人，你可以改为`multiplicand`，这可能更符合函数定义的意思。并且这里的`number`的范围是仅在函数定义内才有效的，如果我们在函数定义外对`number`求值，可能会返回个错误信息。所以说，参量列表内的参量名可以是任意的，只要不与参量列表内的其他参量相同即可。这就比如：你班上的外号叫李大头，那么在这个班里的李大头代表的人就是你，而如果是在学校中，也有人的名字叫李大头，这时这个李大头就不代表你了。

跟随参量列表后的叫做函数文档，它的作用是当我们或任何人使用`C-h f`并键入函数名时所查看的函数帮助文档中的文本。这里还要注意一点，有些函数例如`apropos`在查看函数文档时会只显示文档的第一行，所以我们要在第一行就尽量写清楚这个函数的作用。通过`C-h f`查看函数文档将会弹出一个`\*Help\*`Buffer。

而这个例子的第三行就是函数的主体(往往比例子里多很多**，它是一个列表，功能是将`number`乘以7。

函数定义好了，但我们不要直接尝试调用，我先告诉你们调用的方式吧，**把函数名作为一个列表的首元素，其余的作为参量**最后eval即可。
``` emacs-lisp
(multiply-by-seven 7)
```
但可千万不要急着求值，因为肯定会报错。这主要是因为你只是写好了函数定义，并没有把函数定义给安装上。


## 安装函数定义 ##

将光标移动到我们写好的函数定义之后，eval一下即可安装好函数。安装完成后的函数就被包含在Emacs之中了，直到退出Emacs之前。如果已经尝试安装函数定义的童鞋应该已经发现了，在我们eval函数定义后，会在回显区显示函数名，这就代表我们成功安装了这个函数。

### 改变函数定义  ###

想要修改已经安装好的函数定义很简单，我们只需要重新安装一遍即可，例如我们想要将`multiply-by-seven`函数改为用`+`来实现，这样做:

``` emacs-lisp
(defun multiply-by-seven (number)
  "使number(参量)加7次"
  (+ number number number number number number number)) ;; => multiply-by-seven

(multiply-by-seven 7) ;; => 49
```
所以编写Emacs Lisp代码时的流程通常是:**写函数，装函数，测函数，改函数，装函数**。

## 使函数成为交互式函数 ##

交互式函数的特点是可以通过`M-x`调用，还可以通过键序列调用，例如常用的移动光标`C-n`就是一个交互式函数，并且交互式函数是不会自动将返回值输出至回显区的，因为让一个函数称为交互式函数通常被认为是想得到函数的附加效果，而不是返回值。

想要使一个函数称为交互式函数，可以在函数定义时，将`defun`特殊表开头的列表的第四个元素写成一个`interactive`特殊表开头的列表。例如:

``` emacs-lisp
(defun multiply-by-seven-interactive (number)
  "打印 number(参量) 乘以 7
这是个交互式函数"
  (interactive "p")
  (message "7 * %d = %d" number (* number 7))) ;; => multiply-by-seven-interactive
```

安装好这个函数后，可以有三种方式调用它:
* 对表达式`(multiply-by-seven-interactive 7**`求值
* 键入`C-u`然后输入一个数字作为函数的参量，键入`M-x`然后键入函数名最后键入`RET`。
* 还有一种暂时没搞成功，等学到16章的第7节就知道了。

**交互式函数不会自动将返回值打印至回显区** 并且当使用第二种调用方式时，没有在`C-u`之后键入数字的话将会以默认值4来替代。

### 交互的multiply-by-seven函数 ###

我们为`multiply-by-seven`函数定义了交互式版本，但没有解释其中的`(interactive "p")`列表是个什么东西，这里就说一下。

首先`(interactive "p")`中的`p`代表将接收一个前缀参量，这个前缀参量也就是我们通过`C-u 数字 M-x 函数名`这种方式调用时的`数字`了，例如这个数字是`5`那么就会把`5`传递给`number`参量，然后在`message`函数中的`(* 7 5)`求值，最终由于函数是一个交互式函数，所以函数不会自动将返回值输出到回显区中，而`message`函数的返回值原本是带双引号的，由于是交互式函数，我们要的只是函数带来的附加效果，而不是返回值。

### interactive函数的不同选项 ###

前面已经解释过`interactive`函数的`p`选项，其实`interactive`特殊表有20多个预定义的选项，我们可以结合多个选项使得将信息正确交互地选送给函数。

下面介绍两个选项，首先是`r`，**它可以让Emacs将位点所在区域的开始值和结束值作为函数的两个参量**:

``` emacs-lisp
(interactive "r") ;; => (13945 13978)
```

再则是`B`选项，**它可告诉Emacs用缓冲区的名字作为函数的参量**，它会让Emacs在小缓冲区提示用户输入缓冲区名字，并将跟在`B`后面的字符串作为提示，而且Emacs还会进行函数名的补全（按TAB）。

``` emacs-lisp
;; 会出来一个交互式的窗口
(interactive "B请输入Buffer名称:") ;; => ("test.el")
```

下面再看一个例子，可以获取任意Buffer所对应的文件路径以及位点的开始及结束点。

``` emacs-lisp
(defun get-buffer_name-point_start-point_end (buffer start end)
  "获取buffer所对应的文件以及位点的开始结束值"
  (interactive "B请输入Buffer名称: \nr")
  (message "Buffer-file:%s\npoint-start:%d\npoint-end:%d"(buffer-file-name (get-buffer buffer)) start end))
```

通过`interactive`的`B`选项获取任意buffer的名称，再通过`r`选项后去位点的开始和结束值。最后在输出时通过`get-buffer`获取Buffer对象，从而达到目的。

**`interactive`是支持控制字符的，例如上个例子中用到的`\n`。并且`interactive`还可以无参量，这样的话跟`mark-whole-buffer`函数差不多。如果`interactive`的选项不能满足你的要求，那么你可以将参量传递给`nteractive`做为一个列表。**

### 永久地安装代码 ###

前面我们写了那么多的函数，在我们没有关闭Emacs之前这些函数都是可以被我们随意求值的，但是当我们关闭Emacs之后再打开就必须重新安装函数才能求值了。所以有几种方式可以永久地安装函数或其他的代码。

* 如果代码作为个人使用，可以把函数定义的代码放到`.emacs`初始化文件中，当启动Emacs时，将会自动对`.emacs`文件中的代码求值。
* 如果代码很多，可以将函数定义存放至多个文件，然后使用`load`函数使得emacs对单独存放函数的文件求值。
* 如果是当前计算机其他用户需要使用的代码，可以将代码放入`site-init.el`文件中，这样使得所有的用户都可以使用你的代码。
* 如果你想让你的作为全世界的人使用，那么你可以将代码放到互联网上，或着给自由软件基金会发送一份拷贝，它有可能被加入下一个发行版本中。

**Emacs在过去的年代里成长的道路————奉献。**


## let函数 ##


`let`函数与`defun`函数一样，都是EmacsLisp中的特殊表。

`let`函数将一个符号附着到或者绑定到一个值上。这些被绑定的值是只能在`let`函数之内使用，就像说`defun`特殊表举的例子，两个同名的事物在不同的场景下代表了不同的意思，例如你的房子和你朋友的房子都是房子，你对你朋友说，你要粉刷房子，在你听来是要粉刷你家的房子，但你朋友有可能会认为你要粉刷他的房子。

而`let`函数就避免了这种问题，在`let`函数中绑定的变量都只能在`let`函数中访问，这就是局部变量的概念。

`let`函数跟`setq`以及`set`函数有个很大的区别就在于:

* `let`函数绑定的变量可有任意个 `setq`和`set`只能有一个
* `let`函数可以执行一个或多个列表。
* `let`函数绑定的变量都是局部的。

### let表达式的各个部分 ###

`let`表达式分为三个部分，第一个就是`let`符号，第二个是变量列表，第三个是主体。

**第二个部分的变量列表是由一个列表组成的，这个列表内可以是任意多个符号或任意多个由两个元素组成且第一个元素必定是符号的列表。***

**第三个部分是`let`表达式主体，由任意多个列表组成。**

`let`表达式的模板看起来像:

``` emacs-lisp
(let varlist body...)
```

其中变量列表的符号是由`let`特殊表赋初始化值的变量.符号本身的初始值是nil.而作为两元素列表的首元素的每一个符号被绑定到对第二个元素求值后的返回值.

所以一个简单的变量列表看起来可能是这样的:`(apple (pear 10))`.在这个例子中,`apple`的值是nil,因为我们没有为其赋予初始值.而`pear`的值为10.

那么当变量是由两个元素的列表组成,就可以是下面这样的模板:

``` emacs-lisp
(let ((variable value) (variable value) variable...)
  (body1)
  (body2)...)
```











### let表达式例子 ###

现在需要创建一些关于水果的栗子,不同的水果有不同的数量.

``` emacs-lisp
(let (apple (pear 10) (banana '4斤) watermelon)
  (message "苹果数量:%S\t梨子数量:%d\t香蕉数量:%s\t西瓜数量:%S" apple pear banana watermelon)) ;; => "苹果数量:nil	梨子数量:10	香蕉数量:4斤	西瓜数量:nil"
```

我们创建了两个初始值为nil的变量`apple`和`watermelon`,以及一个绑定到10的变量pear,还有一个绑定到`4斤`的变量banana.随后在`let`主体中将创建的变量都用`message`函数打印在回显区.

### let语句中的未初始化变量 ###

在`let`表达式的变量列表中,允许不给予变量初始化值,那么Lisp解释器将会为其默认绑定到nil值上.

并且,如果没有给予初始值,那么它可以称作:`作为独立的原子出现`.




## if特殊表 ##

`if`函数是除了`defun`/`let`特殊表之外的一个特殊表,它用于让计算机做一些判断的工作.

首先来看`if`函数的模板:

``` emacs-lisp
(if if-part
    then)
```
其工作方式是：首先测试`if-part`的返回值是否不为nil，如果不为nil，那么就执行`then`的表达式。

**通常会把then部分放在if-part的下一行，这样更有利于阅读。**

下面做一个简单的栗子:

``` emacs-lisp
(if (> 5 4)
    (message "5 比 4 大!")) ;; => "5 比 4 大!"
```
其中`>`函数测试它的第一个参量和第二个参量进行比较大小，如果第一个参量大于第二个参量则返回“真”，否则返回nil。

可往往在日常编码中，`if-part`的值不能直接确定，它可能是一个表达式，又可能是一个函数调用。

例如测试参量可能被绑定在函数定义的参量上:

``` emacs-lisp
(defun type-of-animal (animal-name)
  "根据animal-name打印信息到回显区
如果animal-name是符号'fierce则返回'tiger"
  (if (equal animal-name 'fierce)
      (message "It's a tiger")))
(type-of-animal 'fierce) ;; => "It’s a tiger"
```

**type-of-animal函数详解**

首先`type-of-animal`是包含了两个特殊表模板，分别是`defun`和`if`。`type-of-animal`是函数名，紧跟着函数名的是函数参量列表，然后跟着的是函数的文档。最后函数的主体内是一个if函数，if函数的的一个参量是一个列表，这个列表的首元素的符号是一个函数`equal`，在Lisp中，`equal`函数用于比较参量一和参量二是否相等，如果相等则输出`if`函数的第二个参量，也是一个列表，这个列表的首元素是符号且是函数`message`，将`It's a tiger`打印至回显区。

## if-then-else表达式 ##


其实`if-then-else`表达式就是在`if`特殊表之上加了一个参量，其他没什么不同，新增的参量是当参量一的值为nil时，对参量三求值。

它的函数模板可以写成这样:

``` emacs-lisp
(if true-or-false-test
    action-to-carry-out-if-the-test-returns-true
  action-to-carry-out-if-the-test-returns-false)
```

例如:

``` emacs-lisp
(if (> 4 5)
  (message "5 大于 4!")
(message "4 小于 5")) ;; => "4 小于 5"
```

通过这个例子，我们发现当`if`函数的第一参量值为nil时就会对第三参量求值。并且第三参量的缩进也要少于第二参量。

那我们现在将`type-of-animal`函数改造成:

```emacs-lisp
(defun type-of-animal (animal-name) ;second version
  "根据animal-name打印信息到回显区
如果animal-name是符号'fierce则输出'It's tiger!否则输出Tt not fierce"
  (if (equal animal-name 'fierce)
      (message "It's tiger")
    (message "It not fierce")))
(type-of-animal 'fierce) ;; =>"It’s tiger"
(type-of-animal 'notfierce)  ;; => "It not fierce"
```

## Lisp中的真与假 ##




Lisp中所有除了nil的都是真，nil也就是我们常说的假，nil有多种意思，一种就是nil代表假，另一种则是代表空列表，但往往都把空列表写成`()`，而当Lisp解释器对表达式求值时，只要值不是nil或空列表那么都是真，不管得到的值为一个数字或字符串或列表，它都代表真。

``` emacs-lisp
(if nil
    'true
  'false) ;; => false
(if t
    'true
  'false) ;; => true
```

真也有另外一种表示方式，在表达式求值后没什么可返回时就会返回`t`，例如:

``` emacs-lisp
(> 5 4) ;; => t
```

## save-excursion函数 ##

各位还记得什么是位点(point)，什么是标记(mark)吗?

Emacs是一个文本编辑器，主要还是与文本打交道，那么`save-excursion函数`就是与文本打交道的一个经典函数。

先让我们来回顾一下位点与标记:

* 位点(point)：及当前buffer中光标所在字符位置，例如当光标置于buffer的开头，那么point应该是1，若置于buffer的末尾，那么point就是当前buffer的字符数了。

* 标记(mark)：标记是buffer的另外一个位置，其中一个就是位点。在buffer中可以自定义很多标记，这样可以方便我们跳转至某个位点。设置标记的函数是`(set-mark-command)`，它绑定了一个键序列`C-SPC`，如果此时想要快速跳转至某个标记点，就可以使用命令`(exehange-point-and-mark`快速回到标记处，它绑定了一个键序列`C-x C-x`，并且还会将当初的位点设置一个标记，方便来回跳转。

**位点与标记之间的缓冲区叫做现域(region)**，有很多条命令是专用于操作现域的，例如:`center-region|count-lines-region|kill-region|print-region`

前面将了很多关于位点与标记的知识，下面正式介绍`save-excursion`函数，这个函数的作用主要是将位点和标记的当前位置保存，然后当其他会影响位点或标记的函数执行完后，再将标记的位点复原。 

`save-excursion`函数模板:

``` emacs-lisp
(save-excursion
  body...)
```
**注意，`save-excursion`函数的函数体允许有多条表达式，但是只返回最后一条表达式的值。**





## 回顾 ##

这一章学的东西还是挺多的，下面我就把书中的所有文字一字不差的抄下来。

先说几个提到但是没有过多解释的函数:

* eval-last-sexp
对光标所处的位点前的最后一个符号表达式求值。如果这个函数激活时没有参量，那么将返回值输出在回显区，否则将打印在当前缓冲区中。

* defun
定义函数。这个特殊表最多可有五个部分：函数名、传送给函数的参量的模板、文档、一个可选的交互函数声明以及函数体。

* interactiv
向解释器声明这个函数可以被交互的使用，并且这个特殊表还可以用一个字符串，分成单个或多个部分，依次传送信息至这个函数的参量。 

* let
声明在`let`表达式主体中使用的变量列表并且给它们赋初始值，初始值要么是nil，要么是一个指定的值，然后对`let`表达式主体的其他表达式求值并返回最后一个表达式的值。

* save-excursion
对这个函数主体求值前，记录位点和标记的值以及当前缓冲区。求值后恢复位点和标记。

* if
对函数的第一个参量求值，如果值为真，则对第二个参量求值，否则对第三个参量求值。

* equal、eq
测试两个对象的结构或内容是否相等用equal，测试两个对象是否完全相当用eq

* < > <= >=
用于判断第一个参量的值是否大于/小于/大于或等于/小于或等于第二个参量的值，如果是则返回真，否则返回nil

* message
用于往回显区内打印消息

* setq set
setq 用于将第一个参量的值绑定到第二个参量的值，而第一个参量的值由`setq`自动加上引用。
set 用于将第一个参量的值绑定到第二个参量的值，但是不会自动为第一个参量加上引用。

* buffer-name
这个函数用于获取一个缓冲区的名字

* buffer-file-name
这个函数用于获取缓冲区所对饮的名字

* current-buffer
这个函数用于获取当前缓冲区的buffer对象

* other-buffer
返回最近选择过的缓冲区

* switch-to-buffer
选择一个缓冲区

* set-buffer
设置当前缓冲区为某一个缓冲区

* buffer-size
返回当前缓冲区的字符数

* point
返回当前光标所对应缓冲区的位置

* point-min
返回当前缓冲区最小的字符数

* point-max
返回当前缓冲区最大的字符数





## 练习 ##

* 编写一个非交互的函数，这个函数将其第一个参量(是一个数)的值翻倍。然后使这个函数成为一个交互函数

非交互:

``` emacs-lisp
(defun double(number)
  "使number翻倍"
  (setq number (* number 2)))

(double 10) ;; => 20
```

交互式:

``` emacs-lisp
(defun double(number)
  "使number翻倍"
  (interactive "n请输入要翻倍的数字: ")
  (setq number (* number 2))
  (message "翻倍后:%d" number))
```

* 编写一个函数，测试`fill-column`的当前值是否大于传送给函数参量的值，如果是则打印适当的信息

``` emacs-lisp
(defun is-bigger-to-fill-column (number)
  "判断number是否比fill-column大"
  (if (> number fill-column)
      (message "%d比fill-column要大" number)
    (message "%d比fill-column要小" number)))

(is-bigger-to-fill-column 79) ;; => "79比fill-column要小"
(is-bigger-to-fill-column 81) ;; => "81比fill-column要大"
```


# 第四章 与缓冲区有关的函数 #

本章将会介绍大量的函数定义。

## 查找更多的信息 ##

可以使用`C-h f`查看一个函数所对应的文档，使用`C-h v`查看一个变量所对应的文档，如果要在源代码文件中查看函数定义，可以使用函数`find-tags`，跳到相应的位置。

Lisp代码可以分为多个模块或包，如果想要查看某个模块的帮助，可以键入`C-h p`。

## 简化的beginning-of-buffer函数定义 ##

对于`beginning-of-buffer`函数你们可能已经使用过了，其绑定的键序列是`M-<`。其作用是将当前光标移动至buffer的起始处。

下面我们将自己实现一个简单的`beginning-of-buffer`函数。

让我们来看看我们需要做什么事:

1. 首先这个函数得是个交互式函数，以便我们能通过键序列调用或用`M-x`调用。
2. 其次我们需要记录个位点为标记
3. 最后我们再跳转到buffer起始处

相比与真正的`beginning-of-buffer`函数定义，没有考虑一些复杂的选项，但是我们先完成这个简化版本吧!

``` emacs-lisp
(defun simple-beginning-of-buffer ()
  "移动光标至buffer开始处"
  (interactive)
  (push-mark)
  (goto-char (point-min)))
```

这个`defun`函数包含了5个部分:

1. 首先是这个函数的函数名————`simple-beginning-of-buffer`
2. 再就是函数的文档
3. 随后是交互式表达式
4. 然后记录位点为标记
5. 最后跳转至buffer的起始处 

由于这个函数是无参量的，所以交互式表达式内也不用写任何字符串，而`push-mark`函数默认将`point`加入到标记中，最后通过`goto-char`跳转至`point-min`的位置。如果想要回到原来的位置可以使用`C-x C-x`。

既然已经写了一个`simple-beginning-of-buffer`那我们也可以写一个`simple-end-of-buffer`吧!

``` emacs-lisp
(defun simple-end-of-buffer()
  "移动光标至buffer结束处"
  (interactive)
  (push-mark)
  (goto-char (point-max)))
```

最后则是，如果遇到不了解的函数，可以将光标放置函数之上，键入键序列`C-h f RET`即可。 

## mark-whole-buffer函数定义 ##

`mark-whole-buffer` 不比`simple-end-of-buffer`复杂多少。

这次我们来看一个函数的完整定义

这是书中的定义:

``` emacs-lisp
(defun mark-whole-buffer ()
  "Put point at beginning and mark at end of buffer."
  (interactive)
  (push-mark (point))
  (push-mark (point-max))
  (goto-char (point-min)))
```

书中讲不知道为啥函数体内的第一条表达式`push-mark`内还需要写`(point)`，但我现在再去看，这个函数已经改变了，并且也改掉了这个冗余的代码。

``` emacs-lisp
(defun mark-whole-buffer ()
  "Put point at beginning and mark at end of buffer.
If narrowing is in effect, only uses the accessible part of the buffer.
You probably should not use this function in Lisp programs;
it is usually a mistake for a Lisp function to use any subroutine
that uses or sets the mark."
  (declare (interactive-only t))
  (interactive)
  (push-mark)
  (push-mark (point-max) nil t)
  ;; This is really `point-min' in most cases, but if we're in the
  ;; minibuffer, this is at the end of the prompt.
  (goto-char (minibuffer-prompt-end)))
```

并且还改了一些代码，先不看`declare`，我们发现变化的有`(push-mark (point-max))`，最新的`mark-whole-buffer`函数中函数体第二个表达式多了两个参量，第二个参量代表如果值不为nil则显示`Mark set`。第三个参量代表如果在瞬时标记模式下，值不为nil则激活。

并且最后一条表达式也修改过了，原本是`point-min`但改为`minibuffer-prompt-end`，其区别在于:

`minibuffer-prompt-end会在返回buffer位置时输出信息至minibuffer`

在是如果当前buffer不是minibuffer那么就返回`point-min`




## append-to-buffer函数定义 ##

由于我看的这本书年代久远(2001)，现在是2019年，整整过去18年，Emacs也已经发生了巨大的变化。

所以我将先试着记录书中所讲的`append-to-buffer`函数再对Emacs 26.3版本的`append-to-buffer`函数进行讲解，希望对看到这篇博客的同仁们提供一些微薄的帮助。

> 这个计划已经鸽了，我发现用我现在所学还是很难解释清楚26.3版本的append-to-buffer函数的工作方式。所以后面的26.版 append-to-buffer会在以后完成，十分抱歉。

首先`append-to-buffer`函数的作用是将指定buffer区域(region)中的文本追加到当前Buffer的point前。

### 旧版append-to-buffer ###

先让我们看看书中的`append-to-buffer`函数定义:

``` emacs-lisp
(defun append-to-buffer (buffer start end)
  "Append to specified buffer the text of the region.
It is inserted into that buffer before its point.
When alling from a program, give three arguments:
a buffer or the name of one, and two character numbers
specifying the portion of the current buffer to be copied."
  (interactive "BAppend to buffer: \nr")
  (let ((oldbuf (current-buffer)))
    (save-excursion
      (set-buffer (get-buffer-create buffer))
      (insert-buffer-substring oldbuf start end))))
```

通过阅读这个函数的文档就能很清晰的了解这个函数的工作方式。

略过函数名和文档，我们直接来看`interactive`。`interative`中的`B`代表让用户选择一个Buffer(可能不存在)并将buffer名称传给函数参量一，其次是一些友好的文本`Append to buffer: `，紧跟其后的`\n`用于控制换行，最后的`r`获取当前区域(point和mark)，并将其传给函数的参量二和参量三。 

随后是一个`let`特殊表，在`let`的变量列表中，定义了一个`oldbuf`，其绑定的值是`(current-buffer)`的返回值，也就是当前Buffer对象。在`let`的表达式体中有一个`save-excursion`函数。

`save-excursion`函数体中有两条表达式，第一条表达式`(set-buffer)`用于将当前缓冲区变换到另外一个缓冲区，而其参量又是一个函数`get-buffer-create`，这个函数的作用是获取指定BUFFER对象或名(称为BUFFER-OR-NAME)，如果这个BUFFER-OR-NAME不存在，将会自动创建。

`save-excursion`函数体的第二条表达式是一个`(insert-buffer-substring)`函数这个函数将参量一从参量二到参量三的区域的字符串插入到当前Buffer的point之前。




### 26.3版append-to-buffer ###

由于本人水平有限，如有错误，欢迎提出issue.

先让我们看函数定义原型:

``` emacs-lisp
(defun append-to-buffer (buffer start end)
  "Append to specified BUFFER the text of the region.
The text is inserted into that buffer before its point.
BUFFER can be a buffer or the name of a buffer; this
function will create BUFFER if it doesn't already exist.

When calling from a program, give three arguments:
BUFFER (or buffer name), START and END.
START and END specify the portion of the current buffer to be copied."
  (interactive
   (list (read-buffer "Append to buffer: " (other-buffer (current-buffer) t))
	 (region-beginning) (region-end)))
  (let* ((oldbuf (current-buffer))
         (append-to (get-buffer-create buffer))
         (windows (get-buffer-window-list append-to t t))
         point)
    (save-excursion
      (with-current-buffer append-to
        (setq point (point))
        (barf-if-buffer-read-only)
        (insert-buffer-substring oldbuf start end)
        (dolist (window windows)
          (when (= (window-point window) point)
            (set-window-point window (point))))))))
```

我们发现函数参量没有变化，并且注释也没有大的变化，只是函数体内发生了较大的变化。

首先是`interactive`函数参量发生了变化，变成了一个`list`函数，回想一下，`list`函数是用于构造一个列表的函数，这个`list`函数的第一个参量是`(read-buffer)`函数。

`read-buffer`函数可以通过buffer名称读取buffer中的字符串并返回。其第一个参量是用于提示用户的友好信息，并且特意指出这个提示信息必须是由冒号和空格结尾且被双引号包围的字符串。第二个参量用于也就是返回值，它的默认值为列表




## 回顾 ##

惯例抄书

* describe-function\describe-variable
打印一个函数或一个变量的文档。通常将其绑定到`C-h f`和`C-h v`

* find-tag
找到存放某个函数或变量的源代码的文件，并切换到这个缓冲区，将位点(光标)置于相应函数或这变量的开始处。习惯上将其绑定到`M--`。

* save-excursion
保存位点和标记的位置，并在对`save-excursion`参量求值之后恢复这些值。它也保存当前缓冲区并返回到该缓冲区。

* push-mark
在指定位置设置一个标记，并在标记环中记录原来标记的值。标记是缓冲区中的一个位置，即使由一些文本被从缓冲区删除或者增加到缓冲区，标记仍将保持它的相对位置。

* goto-char
将位点设置为由参量指定的位置。参量值可以是一个数，也可以是一个标记，甚至可以是一个返回一个位置数字的表达式(point-min)

* insert-buffer-substring
将来自一个缓冲区（这是被作为一个参量而传递给函数的）的文本域拷贝到当前缓冲区

* mark-whole-buffer
将整个缓冲区标记为一个域。一般将这个函数绑定到`C-x h`。

* set-buffer
将Emacs的注意力转移到另一个缓冲区，但是不该便显示的窗口。 

* get-buffer-create\get-buffer
寻找一个已指定名字的缓冲区，或当指定名字的缓冲区不存在时就创建它。如果指定名称的缓冲区不存在，get-buffer函数就返回nil。

## 练习  ##

* 编写自己的`simplified-end-of-buffer`函数定义，然后测试它是否能工作。

``` emacs-lisp
(defun simple-end-of-buffer()
  "移动光标至buffer结束处"
  (interactive)
  (push-mark)
  (goto-char (point-max)))
```

* 用if和get-buffer编写一个函数，这个函数要打印一个说明某个缓冲区是否存在的消息 

``` emacs-lisp
(defun is-exist-buffer (buffer-or-name)
  "判断buffer-or-name是否为一个已存在的buffer"
  (if (bufferp (get-buffer buffer-or-name))
      (message "%s存在!" buffer-or-name)
    (message "此缓冲区不存在!")))
    
(is-exist-buffer "test.el") ;; => "test.el存在!"
```

* 用find-tag找到copy-to-buffer函数的源代码

不会...

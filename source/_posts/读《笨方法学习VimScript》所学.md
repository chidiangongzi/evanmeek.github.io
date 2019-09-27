---
title: 读《笨方法学习VimScript》所学
copyright: true
date: 2019-09-27 18:26:16
categories: 学习记录
tags:

  - Vim
---

身为一名每天使用Vim超过5小时的人来说，十分有必要学习一下VimScript，正好看到这本书作为入门很合适。这篇文章则是记录我读完此册子所学。

<!--more-->

# 为什么选择这本书?

&emsp;首先，我是一个重度Vim用户，目前记笔记，写代码等操作都是在Vim中实现的，为了让这个强大的古老神器能在我手上发挥巨大威力，所以我决定看书学习Vim。而这本书的前言说的就很好，第一句则是`程序猿们很喜欢实现自己的idea`，虽然我现在只是一名学生，但在我日常生活中经常想把自己使用Vim时的好点子加入我的`vimrc` 中。再就是这本书的`每章都只讲述一个主题，虽然内容简短但是信息丰富`，这样我很喜欢，没有过多啰嗦的地方，有些地方这本书更推荐看Vim自带的文档，这样也让读者有一个自我理解与学习的过程，就像书中所说`现实世界中事情的进展并不是遇到问题后可以很快速轻松的解决`。

# 前言

所提到的都是这本书是面向谁的，以及读完这本书能获得些什么，并且给了一些学习时的忠告，最后提醒了要多利用`:help`命令.

# 预备知识

这本书主要讲VimScript所以，在学习VimScript之前，得了解Vim的基本使用，例如`buffer,window,normal mode,insert mode,text mode`。

最好是具有编程经验。

本书基于Vim-7.3版本撰写的，所以读者需要确保系统安装了>=7.3版本的Vim。

## 创建Vimrc文件

这一节没有提到`Vimrc` 是什么，我这里提一下，是`Vimrc`一个文件，文件内的可以写vim的命令，而写在`Vimrc` 中的命令都被称为Ex命令，Ex命令不是这一小节的讨论范围。

主要说到在Linux或Mac OS X中，这个文件位于`home`目录下，并且是以`.vimrc`命名的，而在Windows下则是位于`home`文件夹下，并以`_vimrc`命名。

以上三个系统，都可以在Vim中通过执行`:echo $MYVIMRC`得知此文件的位置等信息。

**注意:若你没有找到此文件，请自行创建** 

# 打印信息

主要提到Vim中打印命令和注释的使用与作用。

Vim中的打印命令有:`echo` 和`echom` ，其区别在于:

- echo 仅仅输出回显表达式结果。

  > 回显表达式

  `echo {expr1}` 其中{expr1}就是回显表达式
- echom 输出回显表达式结果，并且将其存储在`message-history` 内

  > message-history

  `message-history` 是消息历史，可以通过命令查看`:messages` 

## 注释

VimScript可以通过`"` 字符添加注释，就像这样:

```
" 将<space>映射为za
nnoremap <space> za
```

# 设置选项

Vim中有两种选型: 布尔选项(`on` 或`off`)以及键值选项。

## 布尔选项

类似于开关，例如想让Vim中显示行号，可以执行:`:set number`，这就代表开启，如果想要关闭，则可以使用:`:set nonumber` 代表关闭状态，如果不想纠结当前状态，只想切换可以执行:`set number!`，如果想知道当前状态的值，可以执行:`set number?`，这样可以看到选项的值。

## 键值选项

有些选项，比不是像布尔选项只有两种状态，它们可能会有一个不固定的值，例如改变行号宽度的选项`numberwidth` ，如果我们想查看`numberwidth` 的值，可以执行`set numberwidth?`。

## 一次性设置多个选项

前面我们一直在使用`:set`命令设置单个选项的值，不过`:set`命令还允许一次设置多个选项的值。

```
:set numberwidth=2
:set nonumber
```

可以写成:`set numberwidth=2 nonumber` 

## 练习

**'number'的帮助文档:** 在每行前显示行号。

**relativenumber的帮助文档:** 在每行前显示相对于光标所在行的行号。布尔型选项

> 建议开启这个选项，它可以让你在上下移动光标时不需要动脑子去算。

**numberwidth的帮助文档:** 键值选项，该选项可以设置行号的列数，Vim中默认为4，也就是说当行号超过9999则会自动扩容。

**wrap的帮助文档:** 布尔选项，该选项的作用是自动换行，默认打开。

**shiftround的帮助文档:** 布尔选项，表示没看太懂，文档内是说将缩进取整为`shiftwidth` 的倍数。这个是命令是应用于`> 和 <` 命令的

**matchtime的帮助文档:** 键值型选项，默认值为5，作用是设置配对括号的时间。

# 基本映射

从这一章节开始，逐渐变得有趣起来。

映射是数学中一个有趣的概念，而在VimScript中，键盘的映射也是非常重要且能让Vim随你心意的一个重要概念，因为你可以通过键盘映射告诉Vim: `当我按下某组键位时，则执行某些命令`。

最简单的键盘映射是`map`命令，`map`命令还可以使用特殊字符，**`map`命令不可以映射注释** 

## 练习

映射按键`_`，让当前行上移一行。

`:map _ ddkp` 

# 模式映射

我们知道Vim中有很多种模式，常见的有:`normal,visual,insert` 而上一章节所学的`map` 命令只能应用在`normal` 模式下。

不过不用担心，VimScript提供了应用在不同模式下的映射，它们是:`nmap,vmap,imap` 分别对应了三种常见的模式。

**注意:在插入模式映射下，Vim只会按你所想去做，所以如果要执行normal模式下的命令，别忘了使用`<Esc>` 退出插入模式再使用.** 

## 练习

在insert模式下，可通过按`<C-u>` 将当前光标所在的单词转换成大写格式。

```
:imap <C-u> <esc>vgU
```

在normal模式下，按`C-u`将当前光标的单词转换成大写格式。

```
:nmap <C-u> vwgU
```

# 精确映射

书上说本章内容会比较难理解，其实很简单..

前面我们学了`map`以及三种模式对应的映射命令，但他们有一个问题，就是如果当前映射的键再次被映射了，那么当我们使用其快捷键时，就会执行原先映射的键，这就是递归。

想要避免递归映射，我们可以使用另一组映射命令，可以使得映射的键不会进行递归。

例如`nmap` 的非递归映射命令是:`nnoremap` 其中的`nore` 应该就是`not recursion`的意思，其他两种模式映射命令也是如此。

**注意:我们应当在任何时候都使用非递归映射，以免递归映射带来的不必要麻烦** 

## 练习

**unmap的帮助文档:** unmap是一个系列命令，其作用是在映射命令作用的模式中删除映射，同系列的其他命令还有`nunmap vunmap xunmap sunmap ounmap iunmap lunmap cunmap` 等。

# Leaders

Leaders是Vim中让用户自定义的特殊键位，其作用主要是作为映射键位的前缀键，这样可防止在映射过多快捷键后覆盖的问题。

想要设置leader键，执行命令:`:let mapleader = "选择你想要的"`，默认的Leader键为`\`

## Local Leader

前面所提到的Leader更偏向于全局键位映射，如果我们需要对不同文件类型设置不同的快捷键，则可以使用`Local Leader` 。

想要设置`Local Leader` 的键位，可以执行:`:let maplocalleader = "<space>"` 你可以把<space>替换成你想要的。

**本章本小节只是粗略的提了下LocalLeader的作用，后面的章节将会更加详细的介绍。**

## 练习

**mapleader的帮助文档:** 其实也没什么好说的，上面都写完了，这里说一点:`mapleader` 的值仅在定义映射时被使用，就算后面改变'mapleader'也不会影响已经定义过的映射。

**maplocalleader的帮助文档:** 主要就说一两句忠告:在全局插件里应该使用`<Leader>` 而在一个根据文件类型有不同操作的插件里应该使用`<LocalLeader>` ，还有就是`mapleader` 和`maplocalleader` 的值是可以相同的。

# 编辑你的Vimrc文件

这一章算一个小技巧，书中是这么说的：当你在`疯狂编码时` 突然想加点什么到Vimrc中，但是你又必须立刻编辑vimrc以防忘记，并且又不想退出当前文件，以防打断思路，那么本小节将会实现这个小技巧。

## 编辑映射

我们可以在新建一个分屏，然后那个分屏中编辑`vimrc`，通过几个简单的键位，即可实现。

`:nnoremap <Leader>er :vsplit $MYVIMRC<cr>` 

这个命令使用快捷键`Leader+e+r` 实现新建一个`纵向分屏` 并且在纵向分屏中打开`$MYVIM` ，注意最后的`<cr>` 代表回车，你们可以试下去掉会`<cr>`发生什么。

## 重读映射配置

当我们添加完即刻所想的idea后，我们还需要重载配置文件，但还是需要再次拼写那长长的命令，所以我们直接通过精确键盘映射完成重读映射，在多次使用后，重读一次配置文件的时间不超过`0.2秒` 

`:nnoremap <Leader>sr :source $MYVIMRC<CR>` 

## 练习

说让我添加一些没意义的映射...那好吧，我想要快速执行外部命令，并将外部命令的输出插入到当前文本中。

我要执行的外部程序是:`figlet` ，这是一个可以将字符转化为字符画的一个小程序，那么我可以这样映射。

`:nnoremap <Leader>fl :r !figlet ` 

这样当我按下`<Leader>+f+l` 这个键盘映射后将会自动帮我输入我映射的值，然后等到我输入一些内容，按下回车后就会将figlet的执行结果插入到当前文本中。

**myvimrc的帮助文档:** 文档中说，`$MYVIMRC` 是一个环境变量，这个环境变量指向的是`vimrc` 文件，这个文件用于VIM启动时的初始化。并且这个环境变量如果没有被设置或使用VIMINIT则会从5个地方开始查找，分别是`1. 环境变量$VIMINIT 2.用户vimrc文件 3.环境变量$EXINIT 4.用户exrc文件 5. 默认的vimrc文件(位于$VIMRUNTIME/defaults.vim)` 

# Abbreviations

`Abbreviations`是Vim中一个灵活且强大的特性，其主要用于`insert replace command` 模式

书里说了，只讲`insert` 模式下的`abbreviations`，简单的说`abbreviations` 就是一个缩写替换，可以自定义一些缩写，当你在`insert` 模式下键入这些缩写就会被替换成事先定义好的值。

`insert` 模式的`abbreviations` 命令是:`iabbrev` 例如:`:ibbrev name8 EvanMeek` ，执行这条命令当我们在插入模式下键入`name8` 并按下空格，Vim的`abbreviations` 特性就会将其替换为我们定义好的`EvanMeek` 。

## Keyword Characters

`Keyword Characters`是`abbreviations` 的一个概念，Vim中有一个`keyword范围列表` 想要查看这个返回列表可以执行命令:`:set iskeyword?` ，你将会看类似`iskeyword=@,48-57,_,192-255` 的结果，这里简单介绍一下，这是一个格式，这个格式包含了如下几种:

- 48-57 其实是ASCII值在48-57之间的字符，也就是数字(0-9)

- 192-255 是ASCII值，代表了一些特殊的ASCII字符

- @ 代表除了小写字母ASCII字母以外的字母

- `_` 以及下划线

为什么说`Keyword Characters`是`Abbreviations` 的概念，因为: 当在插入模式下键入缩写后的后一个字符不包含在`iskeyword` 列表中则会将定义好的全拼替换掉缩写，例如我们敲<space>就不在`iskeyword` 列表中，所以可以替换。

下面举个`abbreviations` 特性的常用例子吧:

```
:iabbrev em7 email:the_lty_mail@foxmail.com
```

重载配置文件后，当我们在插入模式下键入em7然后再键入一个非`iskeyword` 列表中的字符，将会替换为`email:the_lty_mail@foxmail.com`。

## 为什么不用Mappings?

其实书上的例子已经很好的解释这个问题了。

首先用mappings做一个替换:`:inoremap lol ILoveLOL`，然后你进入`insert` 模式，键入`你玩不玩lol?` ，此时`lol` 将会被替换为`ILoveLOL` ，让我们用`abbreviations` 特性再做相同的操作。

执行命令:

```
:iunmap lol
:iabbrev lol ILoveLOL
```

现在再试试，你就懂了。

## 练习

为我常用的字符串添加`abbreviations` 特性与配置中。

```
:iabbrev info email:the_lty_mail@foxmail.com    name:EvanMeek    WebSize:https://evanmeek.github.io
```



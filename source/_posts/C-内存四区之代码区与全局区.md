---
title: C++内存四区之代码区与全局区
copyright: true
date: 2019-05-11 20:52:44
categories: 学习笔记
tags:
  - C++核心编程
---

其实这一篇应该是作为"C++内存四区"的第一篇的。

<!--more-->

# 0x00 内存分区模型

C++程序在执行时，内存大方向的可划分为 *****************四个区域**

   - 代码区: 存放代码的二进制代码，由操作系统进行管理。

   - 全局区: 存放全局变量和静态变量以及常量。

   - 栈区: 由编译器自动分配释放，存放函数的参数值，局部变量等。

   - 堆区: 由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收。

## 内存四区的意义:

不同区域存放的数据，代表着不同的生命周期，不同的生命周期使我们可以更灵活的编程。

# 0x01 程序运行前

在程序编译后，生成的可执行程序，当我们未执行此程序前，分为两个区域

代码区:

   存放CPU执行的机器指令。
   
   共享的，共享的目的是对于频繁被执行的程序，只需要在内存中有一份代码即可。

   只读的，为了防止程序意外修改代码的指令，所以有了只读。

![代码区示意图](C-内存四区之代码区与全局区/代码区示意图.png)

如上图所示，代码区主要分为两个部分，共享区是存放常备执行的代码，例如程序员所指定的内联函数，或编译器所生成的代码，这些数据在程序跑起来会一直保存在内存中,

而只读部分是为了防止外部对程序内部的数据进行非法访问，举个栗子，你的程序设定买一个苹果需要1金币，但是某开发人员，通过某手段将此内存中的数据修改为-99999金币，那么就会造成数据非法修改。

全局区:

   存储静态或全局变量。

   公共的，就如其名一样，存储在全局区的数据，基本可以被同一个程序任意使用。

   全局对象为类以及函数通信提供了一种简单直接的方式。(但过多的使用全局对象会影响程序的健壮性，稳定性，可维护性，以及可复用性)。

   静态局部变量可以代替站对象保持递归函数被屡次调用时的中间态，减少函数是调用开销以及各层能共享访问。

请看下面的代码:

~~~C++
#include <iostream>

using namespace std;
int g_a=10;
int g_b=20;
const int cg_a(10),cg_b(20);
int main(){

  //global varibale
  cout<<"global varibale g_a memory address :"<<&g_a<<endl; 
  cout<<"global varibale g_b memory address :"<<&g_b<<endl<<endl;
  
  static double s_a=10;
  static double s_b=20;
  //static varibale
  cout<<"static varibale s_a memory address :"<<&s_a<<endl;
  cout<<"static varibale s_b memory address :"<<&s_b<<endl<<endl;

  
  //string const varibale
  cout<<"string const variba sc_a memory address :"<<&"hello"<<endl<<endl;
   
  //const global varibale
  cout<<"const global varibale cg_a memory address :"<<&cg_a<<endl;
  cout<<"const global varibale cg_b memory address :"<<&cg_b<<endl<<endl;

  int l_a = 10;
  int l_b = 20;

  //local varibale 
  cout<<"local varibale a memory address :"<<(int*)&l_a<<endl;
  cout<<"local varibale b memory address :"<<(int*)&l_b<<endl<<endl;

  const int cl_a(10),cl_b(20);
  //const local varibale
  cout<<"const local varibale cl_a memory address :"<<&cl_a<<endl;
  cout<<"const local varibale cl_b memory address :"<<&cl_b<<endl<<endl;

  return 0;
}
~~~

输出结果为:

~~~
global varibale g_a memory address :0x5617e3016058
global varibale g_b memory address :0x5617e301605c

static varibale s_a memory address :0x5617e3016060
static varibale s_b memory address :0x5617e3016068

string const variba sc_a memory address :0x5617e30140e2

const global varibale cg_a memory address :0x5617e301400c
const global varibale cg_b memory address :0x5617e3014010

local varibale a memory address :0x7fff499d89d8
local varibale b memory address :0x7fff499d89dc

const local varibale cl_a memory address :0x7fff499d89e0
const local varibale cl_b memory address :0x7fff499d89e4
~~~

上述代码，输出了全局变量，静态变量，字符串常量，全局常量，局部变量，局部常量的地址，我们可以由内存的地址发现，全局变量，静态变量，字符串常量，全局变量的内存地址似乎都是在同一个内存区块内的，他们的内存地址是连续的。

**全局区则是用于存储，全局变量，静态变量,字符串常量的内存空间**

---


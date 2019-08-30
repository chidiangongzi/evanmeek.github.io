---
title: C++的命名空间与作用域
copyright: true
date: 2019-05-30 15:42:43
categories: 学习笔记
tags:
  - C++
---

本篇文章将会详细的讲解在使用C++时一些关于作用域的易错点，以及在各模块之间有同名冲突问题要如何利用命名空间解决．

<!--more-->

# **命名空间**

> 也称为名字空间，可以解决多模块同名冲突的问题

## **命名空间的作用**

在日后的开发工作中，总是团队开发，那么可能会因为个人习惯问题，造成对左值命名相同．那么在使用两个不同的库时，可能会有两个相同的对象，那么就会出现命名冲突．

解决这种冲突的方法就是在定义时加上前缀，在使用时指定命名空间的作用域即可，这就是命名空间．

## **定义命名空间**

定义命名空间很简单只需要使用`namespace`关键字即可

我们可以定义一个命名空间将自己的类，函数或对象包括起来:

~~~C++
namespace myspace{
    class Test{
    public:
      int a;
      Test(int a):this->a(a){}
    };
    Test t(10);
}

int main(){
  using namespace myspace;

  Test t(20);
  cout<<t.a<<endl;
}
~~~

与类的成员类似，这些对象，函数，类，被称为名字空间的成员．

## **using声明**

> using namespace `命名空间名`;

在前面的内容中，已经不知不觉地使用上了名字空间，例如:

~~~C++
using namespace std;
cout<<"hello"<<endl;
~~~

using声明语句告诉编译器可以尝试者从std命名空间内查找cout和endl.

## **using指令**

倘若我们只需要使用`std`命名空间中的`cout`和`endl`成员，那么可以通过using指令指定待使用的命名空间的成员.

~~~C++
using std::cout;
using std::endl;
cout<<"hello"<<endl;
~~~

using指明会明确的告诉编译器，将使用到std命名空间中cout和endl，这样就不需要编译器依次查找了，效率会提高一点.

## **命名空间的别名**

如果命名空间都有相同的名称了，我们还可以对它设置一个别名，用于区分.

~~~C++
namespace myStd = std;

myStd::cout<<"hello"<<myStd::endl;
~~~

其中`myStd`作为`std`命名空间的别名．

# **作用域**

> 可以简称为`域`,是指对象的可见性问题

C++目前支持3种作用域:
  
  - 局部作用域(local scope);
  
  - 名字作用域(namespace scope);

  - 类域(calss scope);

## **局部作用域**

在每段语句块都包含一个局部的作用域，在这个语句块中声明的对象仅在当前语句块内部起作用．

例如，函数体，循环体都是局部作用域:

~~~C++
void foo(){
  int a(10);
}
//error a超过了作用域，访问不到foo()函数内部的a变量
cout<<a<<endl;
~~~

~~~C++
for(int i=0;i<100;i++){
  cout<<i<<endl;
}
//error i超过了for的作用域，i是for的局部变量
cout<<i<<endl;
~~~

**提示:在Visual C++6.0中上述代码将i输出不会报错，因为它没有遵循该项C++标准，但在VC2003和Dev-C++中都会报错.**

下面再看一个case语句块的作用域

~~~C++
int choose(-1);
cin>>choose;
switch(choose){
  case 0:
    string str;
    break;
  case 1:
    //error:重定义了str
    string str;
    break;
}
~~~

若不用`{}`将代码括起来，那么就会出现重定义的错误，因为在同一个作用域下定义了两个string str变量，正确的代码如下:

~~~C++
int choose(-1);
cin>>choose;
switch(choose){
  case 0:
  {
    string str;
    break;
  }
  case 1:
  {
    //error:重定义了str
    string str;
    break;
  }
}
~~~

我们通过加上`{}`使得给每个case块加上了不同的作用域，也就解决了重定义的问题．

## **函数的作用域**

函数体和上面提到的作用域一样，在函数体内声明的变量，只能在函数体内访问．

函数体内部包括花括号内的代码以及函数的形参列表，它们都受函数的作用域限制．

~~~C++
void foo(int i){
  //正常访问i变量
  cout<<i<<endl;
}
//error 未声明i变量
cout<<i<<endl;
~~~

当函数之间互相调用也是有单独的作用域的，例如递归代码，注意观察i的值，每次调用自身时i的值都是不同的

~~~C++
void foo(int i){
  cout<<i<<endl;
  if(i>0){
    foo(i/2);
  }
}
~~~


# **局部变量的存储类型**

你可能听说过:自动存储类型，静态存储类型，但是你听过`寄存器存储类型`么?

不同的存储类型，决定了C++编译器存储这些属性的空间和方式.

## **自动存储类型**

在默认情况下，我们定义的变量就属于自动存储类型

~~~C++
void foo(){
  int a(10);
  cout<<a<<endl;
}
~~~

在foo()函数体执行完毕后`a`变量将会自动释放，我们也可以换种写法:

~~~C++
void foo(){
  auto int a(10);
  cout<<a<<endl;
}
~~~
这样做只不过为了显式的说明这个是个自动存储类型的变量

我们还可以使用类函数观测自动存储类型的销毁时间:

~~~C++
#include <iostream>

using namespace std;

class Test {
public:
    int a;

    Test(int a);

    ~Test();
};

Test::Test(int a) : a(a) {
    cout << "创建[" << this << "]" << endl;
}

Test::~Test() {
    cout << "销毁[" << this << "]" << endl;
}

int main() {
    Test t(10);
    Test t1(20);
    return 0;
}
~~~

输出结果

~~~
创建[0x7fff82f501c0]
创建[0x7fff82f501c4]
销毁[0x7fff82f501c4]
销毁[0x7fff82f501c0]

Process finished with exit code 0
~~~

以上代码就可观测到自动存储类型变量的自动销毁过程．

**注意，由于自动存储类型变量会自动销毁，所以我们不要保存自动存储类型变量的地址，因为在对象销毁后，它不再具有我们程序赋予它的意义．**

~~~C++
void *foo(){
  auto Test t(10);
  return &t;
}
~~~

## **寄存器存储类型**

寄存器存储类型继承于C语言，我们在对这种类型的变量进行存储数据时程序将会从寄存器中获取，而非内存，这样可以提高效率，这常常用于被频繁使用的变量．

~~~C++
void foo(){
    for (register int i = 0; i < 10000; ++i) {
        cout<<i<<endl;
    }
}
~~~

虽说C++继承了C语言的寄存器存储类型这一特性，但我们对一个变量加上`register`仅仅只能说是一种期望，因为有些编译器可能不会理会我们，编译器可能更清楚，如何处理这个变量更加高效．

## **静态存储类型**

静态存储变量特殊在于:它超出局部作用域的时候，却依然不会被销毁．

请看下面的代码:

~~~C++
#include <iostream>

using namespace std;

class Test {
    int _a;
public:
    Test(int a) : _a(a) {
        cout << "创建[" << this << "]" << endl;
    }

    ~Test() {
        cout << "销毁[" << this << "]" << endl;
    }
};

void foo() {
    //静态变量
    static Test t(10);
    cout << "t对象已销毁" << endl;
}

int main() {
    //调用第一次
    foo();
    //调用第二次
    foo();
    return 0;
}
~~~

输出结果:

~~~
创建[0x5645e7afa19c]
t对象已销毁
t对象已销毁
销毁[0x5645e7afa19c]
~~~

可以看到，我们调用了两次foo()函数，也就是创建了两次Test对象，但是最终输出的结果却只是创建了一次和销毁了一次，也就说的那个程序执行完第一次foo()函数后，静态变量`t`依然存在!

**常见用法**

程序员们偶尔会利用static的特性，让静态变量存储一些历史数据，不需要每次都销毁的数据.

~~~C++
#include <iostream>

using namespace std;

void foo() {
    static int i(0);
    i++;
    cout << "第" << i << "次调用foo()" << endl;
}

int main() {
    for (int i = 0; i < 3; ++i) {
        foo();
    }
    return 0;
}
~~~

输出结果

~~~
第1次调用foo()
第2次调用foo()
第3次调用foo()

Process finished with exit code 0
~~~

今天就先写到这里，继续学习了.

# **命名空间域**

## **全局域**

~~~C++
//全局作用域下的varA
int varA=100;
void foo1(){
    varA++;
}
void foo2(){
    int varA=200;
    ::varA++;
    //输出内部作用域的varA
    cout<<varA<<endl;
    //输出全局作用域的varA
    cout<<::varA<<endl;
}
int main() {
    foo1();
    foo2();
    return 0;
}
~~~

输出结果

~~~
200
102

Process finished with exit code 0
~~~

最外层的varA为全局作用域的变量，当内部作用域出现相同的变量名时，那么外层的变量将会被隐藏。

我们使用域操作符"::"来显式的指定作用域。




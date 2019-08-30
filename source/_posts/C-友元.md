---
title: C++友元
copyright: true
date: 2019-05-17 17:07:28
categories: 学习笔记
tags:
  - C++
---

相比Java的继承，C++的友元在某些场景下更加方便，再加上我是没用过友元的，所以就深入研究了下友元，所以有了这篇文章。

<!--more-->

# 什么是友元？

友元可以访问类中私有的成员。

它的使用场景又如下几种:

- 全局函数作友元

- 类作友元

- 成员函数做友元

# 实例

下面将通过几个案例，分别演示不同场景下，友元的使用方式。

---

## 全局函数作友元

本小节通过使用一个全局函数访问类的私有成员，分别有两种情况，一种为无友元，另一种则使用了友元。

~~~C++
#include <iostream>
using namespace std;

//先声明Person类，防止下面报错
class Person;
//声明showPrivateVar函数，防止报错.
void showPrivateVar();

//定义Person类
class Person{
private:
    //私有属性，money,showPrivateVar函数访问的就是这个
    double money;
public:
    //声明构造函数
    Person();
};

//类外定义构造函数
Person::Person(){
    this->money = 10;
}
/**
 * 访问私有成员
 */
void showPrivateVar(){
    //实例化Person类对象
    Person p;
    //访问Person对象的私有成员
    cout<<"尝试访问Person类的私有属性:"<<p.money<<endl;
}

int main(){
    //调用访问私有成员函数
    showPrivateVar();
    return 0;
}
~~~

显然，这个程序是跑不起来的，因为全局函数showPrivateVar访问了类Person的私有成员，这是没有使用友元的情况下，但是如果我们把友元加上，那么再跑一遍试试。

~~~C++
class Person{
    //使showPrivateVar函数作为Person类的友元
    friend void showPrivateVar();
private:
    //私有属性，money,showPrivateVar函数访问的就是这个
    double money;
public:
    //声明构造函数
    Person();
};
~~~

运行结果:

~~~shell
尝试访问Person类的私有属性:10

Process finished with exit code 0
~~~

我们只是在定义类时加了一行代码，使得showPrivateVar函数作为类的友元，我们就可以在使用showPrivateVar函数时访问Person类的私有成员.

**那么，得出结论：将全局函数作为某类的友元，那么其则可访问类的私有成员。**

---

## 类作类的友元

这个例子，我们将演示，一个类作作为另一个类的友元，并且访问类中私有的成员.

~~~C++
#include <iostream>
using namespace std;

//声明类，防止报错
class Build;
/**
 * Build类的好朋友类，可以访问它的私有属性
 */
class FriendForBuild{
    Build * b;
public:
    //声明构造函数
    FriendForBuild();
    //声明visit函数
    void visit();
};

//定义Build类
class Build{
    friend FriendForBuild;
private:
    //私有房间
    string privateRoom;
public:
    //公共房间
    string publicRoom;
    /**
     * 构造函数
     */
    Build(){
       this->privateRoom = "私人卧室";
       this->publicRoom = "公共客厅";
    }
};

FriendForBuild::FriendForBuild() {
    b = new Build();
}
/**
 * 访问Build类对象的所有成员，包括私有成员
 */
void FriendForBuild::visit(){
    cout<<"我正在访问Build类对象的publicRoom成员:"<<b->publicRoom<<endl;
    cout<<"我正在访问Build类对象的privateRoom成员:"<<b->privateRoom<<endl;
}

int main(){
    FriendForBuild friendForBuild;
    friendForBuild.visit();
    return 0;
}
~~~

输出结果:

~~~shell
我正在访问Build类对象的publicRoom成员:公共客厅
我正在访问Build类对象的privateRoom成员:私人卧室

Process finished with exit code 0
~~~

**可以看到，我们若需要在类中访问另外一个类的私有成员，只需要把当前类作为其他类的友元，这样就可以使得当前类不受私有访问权限的限制。**

---

## 成员函数做友元

上面我们引入了类作类的友元，但他有个缺陷：我们可以通过友元类的所有成员访问类的私有成员了，这样就没一一个太大的限制，那么我们下面只需要将成员函数作为友元就可以避免这种问题。

~~~C++
#include <iostream>
using namespace std;

//声明类，防止报错
class Build;
/**
 * Build类的好朋友类，可以访问它的私有属性
 */
class FriendForBuild{
    Build * b;
public:
    //声明构造函数
    FriendForBuild();
    //声明visit函数
    void visit();
};

//定义Build类
class Build{
    friend void FriendForBuild::visit();
private:
    //私有房间
    string privateRoom;
public:
    //公共房间
    string publicRoom;
    /**
     * 构造函数
     */
    Build(){
       this->privateRoom = "私人卧室";
       this->publicRoom = "公共客厅";
    }
};

FriendForBuild::FriendForBuild() {
    b = new Build();
}
/**
 * 访问Build类对象的所有成员，包括私有成员
 */
void FriendForBuild::visit(){
    cout<<"我正在访问Build类对象的publicRoom成员:"<<b->publicRoom<<endl;
    cout<<"我正在访问Build类对象的privateRoom成员:"<<b->privateRoom<<endl;
}


int main(){
    FriendForBuild friendForBuild;
    friendForBuild.visit();
    return 0;
}
~~~

---

# 总结

友元可以说成时一个类的朋友，这个朋友可以访问类的所有属性，不管是私有的还是公有的，不同的场景下可以使用不同的方法使用友元。

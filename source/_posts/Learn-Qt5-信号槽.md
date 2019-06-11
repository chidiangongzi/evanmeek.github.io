---
title: Learn-Qt5-信号槽
copyright: true
date: 2019-06-10 08:49:35
categories: 学习笔记
tags:
  - C++
  - Qt5
---

信号槽是Qt的一个很重要的特性，掌握信号槽是学好Qt的必要条件之一.


<!--more-->


信号槽，我们可以理解为监听模式或者是观察者模式，当Qt的某个事件发生后，那么它就会发出一个信号，例如一个按钮(button)被点击(clicked)，那么它会发出一个信号.

但是这种信号是毫无目的的，但是如果我们使用连接(connect)函数，那么就可以使用由我们定义的函数(槽slot)来处理这个信号．

简而言之则是，当某个信号发出，被连接的槽函数则会被回调，这就是观察者模式；当这个信号有来连接的槽函数，那么某个操作则会被触发．


下面看代码:

~~~C++

#include <QApplication>
#include <QDebug>
#include <QPushButton>

int main(int argc, char *argv[]) {
  QApplication a(argc, argv);
  QPushButton button("Quit");
  QObject::connect(&button, &QPushButton::clicked, &QApplication::quit);
  button.show();
  return a.exec();
}

~~~

编译运行后，我们将会看到一个显示文本为Quit的Button，当我们点击它则会退出这个应用程序．

下面我们分析一下QObject::connect这个函数.

首先它拥有以下几种重载

~~~C++

QMetaObject::Connection connect(const QObject *, const char *,
                                const QObject *, const char *,
                                Qt::ConnectionType);

QMetaObject::Connection connect(const QObject *, const QMetaMethod &,
                                const QObject *, const QMetaMethod &,
                                Qt::ConnectionType);

QMetaObject::Connection connect(const QObject *, const char *,
                                const char *,
                                Qt::ConnectionType) const;

QMetaObject::Connection connect(const QObject *, PointerToMemberFunction,
                                const QObject *, PointerToMemberFunction,
                                Qt::ConnectionType)

QMetaObject::Connection connect(const QObject *, PointerToMemberFunction,Functor);

~~~

每种重载的返回值都是QMetaObject::Connection，这里暂时不讨论，先让我们看看connect函数最常用的用法:

~~~C++
connect(sender,signal,receiver,slot);
~~~

connect一般会接受前四个参数，第一个sender是发出信号的对象，第二个signal是sender发出的信号,第三个是接收信号的对象，第四个是receiver接收信号之后需要调用的参数．

简而言之，当sender对象发出signal信号由receiver对象接受再调用slot函数．

根据这个常用的形式，我们可以依次分析connect的重载．

- 第一种

  > sender类型为常量QObject指针，signal为常量字符指针，receiver为常量Object指针，slot为常量字符指针，signal和slot都被作为字符串进行处理．

- 第二种

  > sender和receiver仍为常量Object指针，然而signal和slot则为QMetathod引用，由此我们可以对signal和slot进行比较

- 第三种

  > sender仍为const Object*，而signal和slot则是const char*，这里的reveiver被省略了，它由this指针代替.

- 第四种

  > sender和receiver仍为const Object *，而signal和slot则为PointerToMemberFunction，看其名知其意，PointerToMemberFunction则是一个指向成员函数的指针．

- 第五种

  > 注意最后的Functor参数，它可以接收，static函数，全局函数以及Lambda表达式.

经过我们的分析，可以看出，connect()函数的参数里，sender和receiver没有什么区别，都是QObject指针，主要只有signal和slot的形式区别．

信号槽要求信号和槽的参数一致.一致也就是说，参数类型一致．如果不一致，只有槽函数的参数比信号的少的情况才允许，即使是这样，槽函数的参数列表的顺序也必须和信号参数一致．这是因为，你可以使槽函数忽略信号传的参数，但是不能说信号没有这个数据．
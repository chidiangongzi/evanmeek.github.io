---
title: Learn-Qt5-自定义信号槽
copyright: true
date: 2019-06-11 11:26:58
categories: 学习笔记
tags:
  - Qt5
  - C++
---

上一篇信号槽的学习，我们分析了QObject::connect()函数，使用connect()可以让我们连接Qt提供的信号，但Qt的信号槽机制还允许我们自定义的信号和槽，使得我们的程序更加的健壮，具有解耦性．

我们通过一个新闻和订阅者的例子讲解典型的观察者模式．

有一个报纸类`Newspaper`，有一个订阅者类`Subscriber`，`Subscriber`可订阅`Newspaper`，订阅后若`Newspaper`有了新内容，那么`Subscriber`则会立即得到通知．

上面这个案例的观察者是`Subscriber`，被观察者则是`Newspaper`．在实现代码时，观察者会将自身注册自被观察者的一个容器中．被观察者发生了任何变化时，便会通知这个容器的所有观察者．

下面，我们将用Qt的信号槽实现上面的的案例．

~~~C++

//newspaper.h
#include <QObject>

class NewsPaper : public QObject {
  Q_OBJECT
public:
  NewsPaper(const QString &name) : m_name(name) {}
  void send() { emit newPaper(m_name); }
signals:
  void newPaper(const QString &name);

private:
  QString m_name;
};

//reader.h
#include <QObject>
class Reader : public QObject {
    Q_OBJECT
public:
    void receiverNewsPaper(const QString &name){
        qDebug()<<"Newpaper:"<<name;
    }
};

//main.cpp
#include <QCoreApplication>
#include <newspaper.h>
#include <reader.h>

int main(int argc, char *argv[]) {
  QCoreApplication a(argc, argv);
  NewsPaper paper("xx与xxx结婚了!");
  Reader reader;

  QObject::connect(&paper, &NewsPaper::newPaper, &reader,
                   &Reader::receiverNewsPaper);

  paper.send();

  return a.exec();
}

~~~

运行结果:

~~~
Newpaper:xx与xxx结婚了!
~~~

我们看到`Reader`类和`Newspaper`类都继承了`QObject` 类，在Qt中，只有继承了`QObject`类的类才具有信号槽的能力．凡是`Object`类还是它的派生类或者是间接派生类，都应该在类体的第一行代码写上`Q_OBJECT`．这是一个宏，它为我们的类提供了信号槽额机制，国际化机制，以及Qt提供的反射能力（非C++ RTTI)．你可能会认为假如你的类不需要使用信号槽则不添加这个宏，那是错误的，因为它不仅仅提供了信号槽的能力，还有很多操作都依赖于这个宏．目前，只需要知道我们要将这个宏加在头文件内．

再看`Newspaper`类，它的代码很简单，只不过是加了一个signals关键字，signals所列出的块就是该类的信号．信号就是一个个的函数名，返回值为void，参数是该类需要让外界知道的数据.

`Newspaper`类的`send()`函数比较简单，只有一条语句`emit newPaper(m_name);`. emit是Qt对C++的一个扩展关键字，但实际上也是一个宏．emit的翻译是发出，也就是发出`newPaper()`信号．如果有接受者关注这个信号，　那么还需要知道是哪条新闻发出的信号，所以我们将实际的新闻名字`m_name`以参数传递的方式给这个信号，当接收者收到这个信号时，就可通过槽函数获得实际的值，这样也就完成了数据从发出者到接受者的一个转移．

`Reader`类是接受信号的，所以我们也需要继承`QObject`，并且添加`Q_OBJECT`宏．其他的代码则是默认构造函数和一个普通的成员函数．在Qt5中，任何成员函数,static函数,全局函数和Lamabda表达式都可以作为槽函数．槽函数其实也就是普通的成员函数，因此作为成员函数，也会收到public,private等访问控制符的影响．信号也会收到影响，因为如果信号是private的，那么这个信号就不能在类的外面使用，也就没有了意义．

main函数中，我们首先创建了`Newspaper`和`Reader`两个独享，然后使用`QObject::connect()`函数．这个然后我们调用`Newspaper`的`send()`函数．这个函数只有一个语句：发出信号．由于我们将`Newspaper`的信号和`Reader`的槽函数进行了连接，当这个信号发出时，那么将会自动调用`Reader`的槽函数．

总结自定义信号槽需要注意的事项:

- 发送者和接收者都需要的是`QObject`的子类，若草函数是全局函数，Lambda表达式等其他无需接受者则除外．
- 使用signals标记信号函数，信号是一个函数声明，返回void，不需要实现函数代码；
- 使用emit发送信号
- 使用QObject::connect()函数连接信号和槽.
---
title: C++读写文件
copyright: true
date: 2019-05-22 11:20:45
categories: 学习笔记
tags:
 - C++
---

一些简单的读写文件的操作。

<!--more-->

**本篇文章使用C++```fstream```头文件提供的库函数进行读写操作**


> 请引入#include \<fstream\>进行下面的操作。

# **写入**

写入文件步骤如下:

1. 实例化ofstream对象，或者fstream对象.

    > ofstream ofs;
2. 打开文件流
    
    > ofs.open(const std::string &__s,ios_base::open__mode=ios_base::out);

3. 写入文件

    > ofs<<;

4. 关闭文件流

    > ofs.close();

**注意打开文件流函数的参数分别为`路径`和`打开方式`.**

常用的打开方式如下:

|模式标识|适用对象|描述|
|:-:|:-----:|:-:|
|ios::int|ifstream,fstream|打开输入,默认用于`ifstream`和`fstream`|
|ios::out|ofstream,fstream|打开输出，默认用于`ofstream`和`fstream`|
|ios::trunc|ofstream|打开输入，默认用户`ofstream`|
|ios::ate|ifstream|打开并且在打开后将文件指针指向文件末尾，若文件不存在，则出错|
|ios::app|ostream,fstream|打开输出，并且将数据输出至文件末尾，相当与追加|
|iso::binary|ifstream,ofstream,fstream|以二进制的方式打开文件，进行输入或输出|

以上所有的打开方式可以通过或`|`运算符进行联合使用，例如:

~~~C++
//以二进制的方式打开输出
ofstream ofs(path,ios::out|ios::binary);
~~~

**不管是读取操作还是写入操作，只要涉及打开文件函数的调用，我们都需要在使用完之后对文件进行一个关闭的操作**

好的，下面可以看例子了，我们将写入一些数据到一个文件内。

## **以文本写入**

> 下面将读取两种不同类型的文件以作为案例进行讲解。

~~~C++
/**
 * 写入文件
 * @param path 文件路径
 * @param context 内容
 */
void writeFile(string path,string context){
    //实例化写入对象
    ofstream ofs;
    //打开输出
    ofs.open(path,ios::out);
    //向文件写入数据
    ofs<<context<<endl;
    //关闭输出
    ofs.close();
}

int main(){
    //调用
    writeFile("./test.txt","测试");
}
~~~

这样我们就将`测试`这个段文本信息，写入到当前目录下`test.txt`文件内了.

## **以二进制文件写入**


以二进制文件方式写入，C++提供了`write()`库函数,它的函数原型是:

> `write(const _CharT* __s, streamsize __n);`

其要求地一个参数为字符型指针，第二个参数为最大写入字符数大小。

~~~C++
class Student {
private:
    char name[64];
    int age;
public:
    Student(char name[64], int age) {
        for (int i = 0; i < sizeof(name); ++i)
            this->name[i] = name[i];
        this->age = age;
    }
};`
/**
 * 写入二进制文件
 * @param path 
 */
void writeFileByBinary(string path) {
    //创建输出流对象，并且指定路径和文件打开方式
    ofstream ofs(path, ios::out | ios::binary);
    Student *student = new Student("张三", 18);

    //写入文件
    ofs.write((const char *) student, sizeof(Student));

    ofs.close();

    delete (student);
}
int main(){
    writeFileByBinary("student.bin");
}
~~~

这里我们将类成员属性的值以二进制的方式写入进一个文件内。

最终文件内的内容人类是看不大懂的。

![二进制写](C-读写文件/二进制文件.png)

**注意:以二进制方式写入文件,那么需要以二进制的方式读取文件，不然读出的数据将是乱码.**

# **读取**

> 下面将读取两种不同类型的文件以作为案例进行讲解。

## **以文本文件读取**

读取有很多种方式，下面将会演示三种，分别是:

- 逐行读取

- 逐词读取

- 逐字符读取

---

### **逐字符读取(不推荐)**

**逐字符读取：通过输入流读取单个字符，再将读取到的字符存入容器中。因为是单个字符读取，所以效率较低。**

~~~C++
/**
 * 逐字符读取
 * @param path 路径
 */
void readFile04(string path) {
    //实例化读取操作对象
    ifstream ifs;
    //打开文件
    ifs.open(path, ios::in);
    //数据存储变量
    char cbuffer;
    //逐字符读取，并且将读取的内容复制给c,不再进行读的条件是当读取的字符为EOF，代表文件的结尾.
    while ((cbuffer = ifs.get()) != EOF) {
        cout << cbuffer << endl;
    }
    //关闭文件
    ifs.close();
}
~~~

```EOF```代表文件的末尾，它是一个宏，逐字符读取的条件为，若遇到文件末尾，也就代表读取完成。

### **逐行读取(有两种方式，但都是逐行读取)**

第一种：

~~~C++
/**
 * 逐行读取
 * @param path 路径
 */
void readFile02(string path) {
    //实例化
    fstream fs;
    //打开文件
    fs.open(path, ios::in);
    //用字符数组进行缓存
    char buffer[1024] = {0};
    //逐行进行读取，getline(存储读取到的字符的字符数组,最大读取字符数)
    while (fs.getline(buffer, sizeof(buffer))) {
        cout << buffer << endl;
    }
    //关闭文件
    fs.close();
}
~~~

使用`字符数组`作为数据存储容器，用`fstream`对象的`getline()`函数调用，第一个参数为:存储读取到的数据的容器，第二个参数为最大读取数量，这里使用`sizeof()`是为了不出现数据过大，从而使得字符数组不够大，引发数组越界。

第二种:

~~~C++
/**
 * 逐行读取
 * @param path 路径
 */
void readFile03(string path) {
    //实例化读取操作对象
    ifstream ifs;
    //打开文件
    ifs.open(path, ios::in);
    //数据存储容器
    string buffer;
    //使用全局函数getline(输入流，可存储的容器)进行逐行读取
    while (getline(ifs, buffer)) {
        cout << buffer << endl;
    }
    //关闭文件
    ifs.close();
}
~~~

与第一种方法相似，只不过是将数据存储容器更换为了string类型，但是使用的是全局函数`getline(输入对象,数据存储容器)`,它的第一个参数为：输入对象，也就是我们的读取对象，getline会把数据读入至制定的输入流内，再通过输入流存储至容器。

### **逐词读取(以空格区分)**

逐词读取，将会已空格进行区分每个词汇，再读取。

~~~C++
/**
 * 逐词读取文件
 * @param path 文件路径
 */
void readFile01(string path) {
    //实例化读取文件对象
    ifstream ifs;
    //打开文件
    ifs.open(path, ios::in);
    //判断文件是否能打开
    if (!ifs.is_open()) {
        cout << "文件打开失败!" << endl;
        return;
    }
    //字符数组缓存
    char buffer[1024] = {0};
    //将读取的数据放入缓存区
    while (ifs >> buffer)
        cout << buffer << endl;
    //关闭文件
    ifs.close();
}
~~~

这里多了一个判断文件是否能打开的操作，这样可以防止，路径出错使得程序出错。

这种逐词读取的方式是`读取对象`通过`右移运算符`把读取的数据存入容器之中，但是是以空格区分每个词汇。

## **以二进制的方式读取**

前面我们使用了二进制的方式写入文件，那么被写入的文件就会变成二进制文件，这种文件需要使用二进制读取才能将内容正确的读取，下面看一个简单的例子。


~~~C++
/**
 * 以二进制的方式读取文件
 * @param path 路径
 */
void readFileByBinary(string path) {
    //创建输入流对象，并且指定路径和文件打开方式
    ifstream ifs(path, ios::in | ios::binary);
    char * c = new char[64];
    ifs.read(c, sizeof(c));
    cout<<c<<endl;
}
int main(){
    readFileByBinary("Student.smi");
}
~~~

输出结果:

~~~
张三

Process finished with exit code 0
~~~

这里我们将`Student.smi`这个文件用二进制的方式读取，那么就能正确的将文件内容获取，但如果我们以二进制的方式读取一个文本文件，将会出现一些我们不想要的结果。

# **总结**

读取文件创建`ifstream`对象,写入文件创建`ofstream`对象，`fstream`对象既可以读又可以写。

操作文件得先`打开文件`

操作文件完毕得`关闭文件`

二进制文件读取需要读取二进制格式的文件

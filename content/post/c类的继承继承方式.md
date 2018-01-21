+++
title= "c++类的继承,继承方式"
categories= ["code"]
tags= ["继承方式","继承"]
date= "2016-03-27 22:00:00"
+++

来自[慕课网](http://www.imooc.com/learn/426)

实例化子类的时候会实例化父类
<!--more-->
```````
#include <iostream>

using namespace std;
class Person{
public:
    Person();
    ~Person();
    void eat();
    string m_strName;
    int m_iAge;
};
Person::Person(){
    cout <<  "Person()"<< endl;
}
Person::~Person(){
    cout<<  "~Person()"<< endl;
}
void Person::eat(){
    cout << "eat()" << endl;
}

class Worker:public Person{
public:
    Worker();
    ~Worker();
    void work();
    int m_iSalary;
};
Worker::Worker(){
    cout<< "Worker()"<< endl;
}
Worker::~Worker(){
    cout << "~Worker()"<< ;endl;
}
void Worker::work(){
    cout << "work()"<< endl;
}
int main()
{
    Worker worker;
    worker.m_strName = "jim";
    worker.m_iAge = 10;
    worker.eat();
    worker.work();
    worker.m_iSalary =1000;
    return 0;
}
```
输出为
```
Person()
Worker()
eat()
work()
~Worker()
~Person()
```
###父类的不同访问限制的成员，通过不同的继承方式，在子类中的访问限制###
不管以何种继承方式，基类的private属性成员在派生类中都是不可访问的，这也体现了类的封装性。
以public继承方式时，基类中的public属 性成员在派生类中的也是public，protect属性成员在派生类中也是protect。
以private继承方式时，基类的public和 protect在派生类中都是继承到private属性下。
![](http://img.mukewang.com/56e7fb130001204812800720.jpg)
![](http://img.mukewang.com/56e8592b00017f1012800720.jpg)
![](http://img.mukewang.com/56ea67fa0001ccf012800720.jpg)


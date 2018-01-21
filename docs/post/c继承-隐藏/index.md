即使子类的函数有参数而父类的同名函数没有参数，这两个函数也是存在隐藏关系的，子类对象仍然只能调用子类这个成员函数，而不能调用父类继承来的那个同名 函数，若要调用，仍然要采用 子类对象.父类类名::同名函数 的方式调用父类继承来的那个掩藏函数。也就是说，隐藏函数之间无法形成重载，只能隐藏。
<!--more-->
```
#include <iostream>;

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
    cout << "Person()"<< endl;
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
    void eat(int x);
    string m_strName;
};
Worker::Worker(){
    cout << "Worker()"<< endl;
}
Worker::~Worker(){
    cout << "~Worker()"<< endl;
}
void Worker::eat(int x ){
    cout << "worker eat(int x)"<< endl;
}
void Worker::work(){
    Person::m_strName = "person";
    m_strName = "worker";
    cout<< Person::m_strName << endl;
    cout<< m_strName<< endl;
    cout << "work()"<< endl;
}
int main()
{
    Worker worker;
    worker.m_strName = "jim";
    worker.work();
    worker.eat(1);
    worker.Person::eat();
}

```
输出为
```
Person()
Worker()
person
worker
work()
worker eat(int x)
eat()
~Worker()
~Person()

```

+++
title= "c++对象this指针"
categories= ["code"]
tags= ["this","对象"]
date= "2016-03-16 15:24:54"
+++

来自<a href="http://www.runoob.com/cplusplus/cpp-this-pointer.html">http://www.runoob.com/cplusplus/cpp-this-pointer.html</a>和<a href="http://www.imooc.com/learn/405">http://www.imooc.com/learn/405</a>

在 C++ 中，每一个对象都能通过 <strong>this</strong> 指针来访问自己的地址。<strong>this</strong> 指针是所有成员函数的隐含参数。因此，在成员函数内部，它可以用来指向调用对象。
<pre class="brush:cpp;toolbar:false">#include &lt;iostream&gt;
using namespace std;
class Array{
public:
    Array(int len){
        this-&gt;len = len;
    }
    Array&amp; setLen(int len){
        this-&gt;len = len;
        return *this; //返回对这个对象的引用
    };
    Array&amp; printInfo(){
        cout&lt;&lt;"len = "&lt;&lt;this-&gt;len&lt;&lt;endl;
        return *this;  //返回对这个对象的引用
    }
private:
    int len;
};
int main()
{
    Array a(10);
    a.printInfo().setLen(5).printInfo(); //执行完函数后返回这个对象的引用，然后继续调用这个对象的函数
    return 0;
}</pre>
输出为
<pre class="brush:cpp;toolbar:false">len = 10
len = 5</pre>
如果改成返回指针
<pre class="brush:cpp;toolbar:false">#include &lt;iostream&gt;
using namespace std;
class Array{
public:
    Array(int len){
        this-&gt;len = len;
    }
    Array* setLen(int len){
        this-&gt;len = len;
        return this; //返回对这个对象的指针
    };
    Array* printInfo(){
        cout&lt;&lt;"len = "&lt;&lt;this-&gt;len&lt;&lt;endl;
        return this;  //返回对这个对象的指针
    }
private:
    int len;
};
int main()
{
    Array a(10);
    a.printInfo()-&gt;setLen(5)-&gt;printInfo(); //就可以这样子调用了
    return 0;
}</pre>
<pre class="brush:cpp;toolbar:false">len = 10
len = 5</pre>
​

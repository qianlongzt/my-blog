+++
title= "c++常成员函数，常对象"
categories= ["code"]
tags= ["常成员函数","常对象"]
date= "2016-03-16 16:11:46"
+++

c++中可以将对象，成员函数用const修饰为常对象，常成员函数

常对象就是它的值初始化后不能改变值，常成员函数就是这个函数只能读取对象的值，不能修改对象的值。

如果普通成员函数和常成员函数同名，那么这个常用函数只能在常对象中被调用，如果没有同名可以直接调用常成员函数
<pre class="brush:cpp">#include &lt;iostream&gt;

using namespace std;
class Coordinate{
public:
    Coordinate(int x,int y){
        this-&gt;m_iX = x;
        this-&gt;m_iY = y;
    }
public:
    int m_iX;
    int m_iY;
};
class Line{
public:
    Line(int x1,int y1,int x2,int y2):m_coorA(x1,y1),m_coorB(x2,y2){};
    void printInfo(){  //普通成员函数  与下面函数重载
        cout&lt;&lt;printInfo()&lt;&lt;endl;
        cout &lt;&lt; m_coorA.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout &lt;&lt; m_coorB.m_iX &lt;&lt; &quot;,&quot;&lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    } 
    void printInfo() const{ //常成员函数 与上面的函数重载
        cout&lt;&lt;&quot;printInfo() const&quot;&lt;&lt;endl;
        cout&lt;&lt; m_coorA.m_iX &lt;&lt;&quot;,&quot;&lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout&lt;&lt;m_coorB.m_iX&lt;&lt;&quot;,&quot;&lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    }
    void printI() const{ //常成员函数  
        cout&lt;&lt;&quot;printI() const&quot;&lt;&lt;endl;
        cout &lt;&lt;m_coorA.m_iX &lt;&lt;&quot;,&quot;&lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout&lt;&lt;m_coorB.m_iX &lt;&lt;&quot;,&quot;&lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    }
private:
    const Coordinate m_coorA;
    const Coordinate m_coorB;
};
int main()
{
    Line line(1,2,3,4);
    line.printInfo();//调用普通成员函数
    line.printI();//调用常成员函数

    const Line line1(1,2,3,4);
    line1.printInfo();//调用常成员函数
    line1.printI();//调用常采用函数
    return 0;
}</pre><p>&nbsp;</p>
输出为
<pre class="brush:other">printInfo()
1,2
3,4
printI() const
1,2
3,4
printInfo() const
1,2
3,4
printI() const
1,2
3,4</pre><p>&nbsp;</p>
​
<ol>
	<li>常对象只能调用常成员函数，不能调用普通成员函数</li>
	<li>普通对象能够调用常成员函数，也能够调用普通成员函数</li>
	<li>常指针和常引用都只能调用对象的常成员函数。</li>
	<li>对象引用和对象常引用都是对象的别名，一个对象可以有多个对象常引用</li>
</ol>
<pre class="brush:cpp">#include &amp;amp;lt;iostream&amp;amp;gt;
using namespace std;
class Coordinate{
public:
    Coordinate(int x,int y){
        this-&gt;m_iX = x;
        this-&gt;m_iY = y;
    }
public:
    int m_iX;
    int m_iY;
};
class Line{
public:
    Line(int x1,int y1,int x2,int y2):m_coorA(x1,y1),m_coorB(x2,y2){};
    void printInfo(){
        cout&lt;&lt;&quot;printInfo()&quot;&lt;&lt;endl;
        cout &lt;&lt; m_coorA.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout &lt;&lt; m_coorB.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    }
      void printInfo() const{
        cout&lt;&lt;&quot;printInfo() const&quot;&lt;&lt;endl;
        cout &lt;&lt; m_coorA.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout &lt;&lt; m_coorB.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    }
    void printI(){
        cout &lt;&lt;&quot;printI()&quot; &lt;&lt;endl;
        cout &lt;&lt; m_coorA.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorA.m_iY&lt;&lt;endl;
        cout &lt;&lt; m_coorB.m_iX &lt;&lt; &quot;,&quot; &lt;&lt;m_coorB.m_iY&lt;&lt;endl;
    }
private:
    const Coordinate m_coorA;
    const Coordinate m_coorB;
};
int main()
{
    Line line(1,2,3,4);
    const Line&amp; line1 = line;
    const Line* line2 = &amp;line;
    line1.printInfo();
    line1.printI(); // 错误 不能调用普通成员函数

    line2-&gt;printInfo();
    line2-&gt;printI();// 错误 不能调用普通成员函数
    return 0;
}</pre><p>&nbsp;</p>

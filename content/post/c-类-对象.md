+++
title= "C++ 类 &amp; 对象"
categories= ["code"]
tags= ["类"]
date= "2016-03-12 23:32:55"
+++

<div class="title clearfix"><span class="text">来源<a href="http://www.runoob.com/cplusplus/cpp-classes-objects.html">http://www.runoob.com/cplusplus/cpp-classes-objects.html</a>
</span></div>
<div id="content" class="content">

类用于指定对象的形式，它包含了数据表示法和用于处理数据的方法。类中的数据和方法称为类的成员。函数在一个类被称为类的成员。
<h2 class="tutheader">C++ 类定义</h2>
定义一个类，本质上是定义一个数据类型的蓝图。这实际上并没有定义任何数据，但它定义了类的名称意味着什么，也就是说，它定义了类的对象包括了什么，以及可以在这个对象上执行哪些操作。

类定义是以关键字 <strong>class</strong> 开头，后跟类的名称。类的主体是包含在一对花括号中。类定义后必须跟着一个分号或一个声明列表。数据隐藏是面向对象编程的一个重要特点，它防止函数直接访问类类型的内部成员。类成员的访问限制是通过在类主体内部对各个区域标记 。<b>public、private、protected</b> 来指定的。关键字 public、private、protected 称为访问说明符。一个类可以有多个 public、protected 或 private 标记区域。每个标记区域在下一个标记区域开始之前或者在遇到类主体结束右括号之前都是有效的。成员和类的默认访问修饰符是 private。
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Base</span> <span class="pun">{</span>
 
   <span class="kwd">public</span><span class="pun">:</span>
 
  <span class="com">// public members go here</span>
 
   <span class="kwd">protected</span><span class="pun">:</span>
 
  <span class="com">// protected members go here</span>
 
   <span class="kwd">private</span><span class="pun">:</span>
 
  <span class="com">// private members go here</span>
 
<span class="pun">};</span></pre>
<h2 class="tutheader">定义 C++ 对象</h2>
声明类的对象，就像声明基本类型的变量一样。下面的语句声明了类 Box 的两个对象：
<pre class="prettyprint prettyprinted">Box Box1;          // 声明 Box1，类型为 Box
Box Box2();          // 错误声明，编译器会认为是声明一个返回Box类不带参数的Box2函数;
Box *obj = new Box(); //在堆上声明一个Box类对象
Box *obj2 = new Box; // 在堆上声明一个Box类对象</pre>
对象 Box1 和 Box2 都有它们各自的数据成员。
<h2 class="tutheader">访问数据成员</h2>
类的对象的公共数据成员可以使用直接成员访问运算符 (.) 来访问。

需要注意的是，私有的成员和受保护的成员不能使用直接成员访问运算符 (.) 来直接访问。

类的成员函数是指那些把定义和原型写在类定义内部的函数，就像类定义中的其他变量一样。类成员函数是类的一个成员，它可以操作类的任意对象，可以访问对象中的所有成员。
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Box</span>
<span class="pun">{</span>
   <span class="kwd">public</span><span class="pun">:</span>
      <span class="kwd">double</span><span class="pln"> length</span><span class="pun">;</span>         <span class="com">// 长度</span>
      <span class="kwd">double</span><span class="pln"> breadth</span><span class="pun">;</span>        <span class="com">// 宽度</span>
      <span class="kwd">double</span><span class="pln"> height</span><span class="pun">;</span>         <span class="com">// 高度</span>
      <span class="kwd">double</span><span class="pln"> getVolume</span><span class="pun">(</span><span class="kwd">void</span><span class="pun">);</span><span class="com">// 返回体积</span>
<span class="pun">};</span></pre>
成员函数可以定义在类定义内部，或者单独使用<b>范围解析运算符 ::</b> 来定义。在类定义中定义的成员函数把函数声明为<b>内联</b>的，即便没有使用 inline 标识符。所以您可以按照如下方式定义 <b>Volume()</b> 函数：
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Box</span>
<span class="pun">{</span>
   <span class="kwd">public</span><span class="pun">:</span>
      <span class="kwd">double</span><span class="pln"> length</span><span class="pun">;</span>      <span class="com">// 长度</span>
      <span class="kwd">double</span><span class="pln"> breadth</span><span class="pun">;</span>     <span class="com">// 宽度</span>
      <span class="kwd">double</span><span class="pln"> height</span><span class="pun">;</span>      <span class="com">// 高度</span>
   
      <span class="kwd">double</span><span class="pln"> getVolume</span><span class="pun">(</span><span class="kwd">void</span><span class="pun">)</span>
      <span class="pun">{</span>
         <span class="kwd">return</span><span class="pln"> length </span><span class="pun">*</span><span class="pln"> breadth </span><span class="pun">*</span><span class="pln"> height</span><span class="pun">;</span>
      <span class="pun">}</span>
<span class="pun">};</span></pre>
您也可以在类的外部使用<b>范围解析运算符 ::</b> 定义该函数，如下所示：
<pre class="prettyprint prettyprinted"><span class="kwd">double</span> <span class="typ">Box</span><span class="pun">::</span><span class="pln">getVolume</span><span class="pun">(</span><span class="kwd">void</span><span class="pun">)</span>
<span class="pun">{</span>
    <span class="kwd">return</span><span class="pln"> length </span><span class="pun">*</span><span class="pln"> breadth </span><span class="pun">*</span><span class="pln"> height</span><span class="pun">;</span>
<span class="pun">}</span></pre>
在这里，需要强调一点，在 :: 运算符之前必须使用类名。调用成员函数是在对象上使用点运算符（<b>.</b>），这样它就能操作与该对象相关的数据，如下所示：
<pre class="prettyprint prettyprinted"><span class="typ">Box</span><span class="pln"> myBox</span><span class="pun">;</span>          <span class="com">// 创建一个对象</span><span class="pln">

myBox</span><span class="pun">.</span><span class="pln">getVolume</span><span class="pun">();</span>  <span class="com">// 调用该对象的成员函数</span></pre>
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Base</span> <span class="pun">{</span> 
    <span class="kwd">public</span><span class="pun">:</span> <span class="com">// public members go here</span> 
<span class="kwd">    protected</span><span class="pun">:</span> <span class="com">// protected members go here</span> 
<span class="kwd">    private</span><span class="pun">:</span> <span class="com">// private members go here</span> 
<span class="pun">};</span></pre>
<h2>公有（public）成员</h2>
<b>公有</b>成员在程序中类的外部是可访问的。您可以不使用任何成员函数来设置和获取公有变量的值。
<h2>私有（private）成员</h2>
<b>私有</b>成员变量或函数在类的外部是不可访问的，甚至是不可查看的。只有类和友元函数可以访问私有成员。默认情况下，类的所有成员都是私有的。如果您没有使用任何访问修饰符，类的成员将被假定为私有成员。实际操作中，我们一般会在私有区域定义数据，在公有区域定义相关的函数，以便在类的外部也可以调用这些函数。
<h2>保护（protected）成员</h2>
<b>保护</b>成员变量或函数与私有成员十分相似，但有一点不同，保护成员在派生类（即子类）中是可访问的。
<h1>类的<b>构造函数</b></h1>
类的<b>构造函数</b>是类的一种特殊的成员函数，它会在每次创建类的新对象时执行。构造函数的名称与类的名称是完全相同的，并且不会返回任何类型，也不会返回 void。构造函数可用于为某些成员变量设置初始值。
<h2>带参数的构造函数</h2>
默认的构造函数没有任何参数，但如果需要，构造函数也可以带有参数。这样在创建对象时就会给对象赋初始值，如下面的例子所示：
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Line</span>
<span class="pun">{</span>
   <span class="kwd">public</span><span class="pun">:</span>
      <span class="kwd">void</span><span class="pln"> setLength</span><span class="pun">(</span> <span class="kwd">double</span><span class="pln"> len </span><span class="pun">);</span>
      <span class="kwd">double</span><span class="pln"> getLength</span><span class="pun">(</span> <span class="kwd">void</span> <span class="pun">);</span>
      <span class="typ">Line</span><span class="pun">(</span><span class="kwd">double</span><span class="pln"> len</span><span class="pun">);</span>  <span class="com">// 这是构造函数</span>
 
   <span class="kwd">private</span><span class="pun">:</span>
      <span class="kwd">double</span><span class="pln"> length</span><span class="pun">;</span>
<span class="pun">};</span>
 
<span class="com">// 成员函数定义，包括构造函数</span>
<span class="typ">Line</span><span class="pun">::</span><span class="typ">Line</span><span class="pun">(</span> <span class="kwd">double</span><span class="pln"> len</span><span class="pun">)</span>
<span class="pun">{</span><span class="pln">
    cout </span><span class="pun">&lt;&lt;</span> <span class="str">"Object is being created, length = "</span> <span class="pun">&lt;&lt;</span><span class="pln"> len </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
    length </span><span class="pun">=</span><span class="pln"> len</span><span class="pun">;</span>
<span class="pun">}</span>
 
<span class="kwd">double</span> <span class="typ">Line</span><span class="pun">::</span><span class="pln">getLength</span><span class="pun">(</span> <span class="kwd">void</span> <span class="pun">)</span>
<span class="pun">{</span>
    <span class="kwd">return</span><span class="pln"> length</span><span class="pun">;</span>
<span class="pun">}</span>
<span class="com">// 程序的主函数</span>
<span class="kwd">int</span><span class="pln"> main</span><span class="pun">(</span> <span class="pun">)</span>
<span class="pun">{</span>
   <span class="typ">Line</span><span class="pln"> line</span><span class="pun">(</span><span class="lit">10.0</span><span class="pun">);</span>
   <span class="com">// 获取默认设置的长度</span><span class="pln">
   cout </span><span class="pun">&lt;&lt;</span> <span class="str">"Length of line : "</span> <span class="pun">&lt;&lt;</span><span class="pln"> line</span><span class="pun">.</span><span class="pln">getLength</span><span class="pun">()</span> <span class="pun">&lt;&lt;</span><span class="pln">endl</span><span class="pun">;</span>
   <span class="kwd">return</span> <span class="lit">0</span><span class="pun">;</span>
<span class="pun">}</span></pre>
当上面的代码被编译和执行时，它会产生下列结果：
<pre class="prettyprint prettyprinted"><span class="typ">Object</span> <span class="kwd">is</span><span class="pln"> being created</span><span class="pun">,</span><span class="pln"> length </span><span class="pun">=</span> <span class="lit">10</span>
<span class="typ">Length</span><span class="pln"> of line </span><span class="pun">:</span> <span class="lit">10</span></pre>
<h2>使用初始化列表来初始化字段</h2>
使用初始化列表来初始化字段：
<pre class="prettyprint prettyprinted"><span class="pln">C</span><span class="pun">::</span><span class="pln">C</span><span class="pun">(</span> <span class="kwd">double</span><span class="pln"> a</span><span class="pun">,</span> <span class="kwd">double</span><span class="pln"> b</span><span class="pun">,</span> <span class="kwd">double</span><span class="pln"> c</span><span class="pun">):</span><span class="pln"> X</span><span class="pun">(</span><span class="pln">a</span><span class="pun">),</span><span class="pln"> Y</span><span class="pun">(</span><span class="pln">b</span><span class="pun">),</span><span class="pln"> Z</span><span class="pun">(</span><span class="pln">c</span><span class="pun">)</span>
<span class="pun">{</span>
  <span class="pun">....</span>
<span class="pun">}</span></pre>
当类中有常量时，就必须用 初始化列表来初始化
<h2>类的析构函数</h2>
类的<b>析构函数</b>是类的一种特殊的成员函数，它会在每次删除所创建的对象时执行。

析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。
<pre class="prettyprint prettyprinted"><span class="kwd">class</span> <span class="typ">Line</span>
<span class="pun">{</span>
   <span class="kwd">public</span><span class="pun">:</span>
      <span class="kwd">void</span><span class="pln"> setLength</span><span class="pun">(</span> <span class="kwd">double</span><span class="pln"> len </span><span class="pun">);</span>
      <span class="kwd">double</span><span class="pln"> getLength</span><span class="pun">(</span> <span class="kwd">void</span> <span class="pun">);</span>
      <span class="typ">Line</span><span class="pun">();</span>   <span class="com">// 这是构造函数声明</span>
      <span class="pun">~</span><span class="typ">Line</span><span class="pun">();</span>  <span class="com">// 这是析构函数声明</span>
 
   <span class="kwd">private</span><span class="pun">:</span>
      <span class="kwd">double</span><span class="pln"> length</span><span class="pun">;</span>
<span class="pun">};</span>
<span class="com">// 成员函数定义，包括构造函数</span>
<span class="typ">Line</span><span class="pun">::</span><span class="typ">Line</span><span class="pun">(</span><span class="kwd">void</span><span class="pun">)</span>
<span class="pun">{</span><span class="pln">
    cout </span><span class="pun">&lt;&lt;</span> <span class="str">"Object is being created"</span> <span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span>
<span class="pun">}</span>
<span class="typ">Line</span><span class="pun">::~</span><span class="typ">Line</span><span class="pun">(</span><span class="kwd">void</span><span class="pun">)</span>
<span class="pun">{</span><span class="pln">
    cout </span><span class="pun">&lt;&lt;</span> <span class="str">"Object is being deleted"</span> <span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span>
<span class="pun">}</span>
<span class="kwd">double</span> <span class="typ">Line</span><span class="pun">::</span><span class="pln">getLength</span><span class="pun">(</span> <span class="kwd">void</span> <span class="pun">)</span>
<span class="pun">{</span>
    <span class="kwd">return</span><span class="pln"> length</span><span class="pun">;</span>
<span class="pun">}</span>
<span class="com">// 程序的主函数</span>
<span class="kwd">int</span><span class="pln"> main</span><span class="pun">(</span> <span class="pun">)</span>
<span class="pun">{</span>
   <span class="typ">Line</span><span class="pln"> line</span><span class="pun">;</span>
   <span class="com">// 设置长度</span><span class="pln">
   line</span><span class="pun">.</span><span class="pln">setLength</span><span class="pun">(</span><span class="lit">6.0</span><span class="pun">);</span><span class="pln"> 
   cout </span><span class="pun">&lt;&lt;</span> <span class="str">"Length of line : "</span> <span class="pun">&lt;&lt;</span><span class="pln"> line</span><span class="pun">.</span><span class="pln">getLength</span><span class="pun">()</span> <span class="pun">&lt;&lt;</span><span class="pln">endl</span><span class="pun">;</span>
   <span class="kwd">return</span> <span class="lit">0</span><span class="pun">;</span>
<span class="pun">}</span></pre>
当上面的代码被编译和执行时，它会产生下列结果：
<pre class="prettyprint prettyprinted"><span class="typ">Object</span> <span class="kwd">is</span><span class="pln"> being created
</span><span class="typ">Length</span><span class="pln"> of line </span><span class="pun">:</span> <span class="lit">6</span>
<span class="typ">Object</span> <span class="kwd">is</span><span class="pln"> being deleted</span></pre>
<div class="pic-viewer-wrap">
<h2 class="pic-viewer-inner J-viewer-inner">对象的声明历程</h2>
<div class="pic-viewer-inner J-viewer-inner"><img src="http://img.mukewang.com/56e2614b00013aa412800720.jpg" alt="" /></div>
</div>
<h2 class="pic-viewer-inner J-viewer-inner">一个类a作为另一个类b的成员时，先实例化a，在实例化b，析构时先析构b，在析构a；</h2>
<pre class="pic-viewer-inner J-viewer-inner">#include &lt;iostream&gt;
using namespace std;
class Coordinate{
private:
    int m_iX;
    int m_iY;
public:
    int getX(){
        return this-&gt;m_iX;
    }
    int getY(void){
        return this -&gt; m_iY;
    }
    Coordinate(int x,int y){
        this-&gt;m_iX = x;
        this-&gt;m_iY = y;
        cout &lt;&lt; "Coordinate"&lt;&lt;this-&gt;m_iX&lt;&lt;","&lt;&lt;this-&gt;m_iY &lt;&lt;endl;
    }
    ~Coordinate(){
        cout &lt;&lt; "~Coordinate"&lt;&lt;this-&gt;m_iX&lt;&lt;","&lt;&lt;this-&gt;m_iY &lt;&lt;endl;
        cout &lt;&lt; "~Coordinate()" &lt;&lt;endl;
    }
};
class Line{
public:
    Line(int x1,int y1, int x2, int y2):m_coorA(x1,y1),m_coorB(x2,y2){
        cout &lt;&lt;"line()"&lt;&lt;endl;
    }
    ~Line(){
        cout &lt;&lt;"~line()"&lt;&lt;endl;
    }
    void printfInfo(){
        cout &lt;&lt; "("&lt;&lt;this-&gt;m_coorA.getX()&lt;&lt;","&lt;&lt;this-&gt;m_coorA.getY()&lt;&lt;")"&lt;&lt;endl;
        cout &lt;&lt; "("&lt;&lt;this-&gt;m_coorB.getX()&lt;&lt;","&lt;&lt;this-&gt;m_coorB.getY()&lt;&lt;")"&lt;&lt;endl;
    }
private:
    Coordinate m_coorA;
    Coordinate m_coorB;
};
int main()
{
    Line *p = new Line(1,2,3,4);
    p-&gt;printfInfo();
    delete p;
    return 0;
}</pre>
<pre>Coordinate1,2
Coordinate3,4
line()
(1,2)
(3,4)
~line()
~Coordinate3,4
~Coordinate()
~Coordinate1,2
~Coordinate()</pre>
<h2>浅拷贝</h2>
<pre>#include &lt;iostream&gt;
using namespace std;
class Array{
public:
    Array(){
        cout &lt;&lt; "Array"&lt;&lt;endl;
    }
    Array(const Array &amp;arr){
        this-&gt;m_iCount = arr.m_iCount - 1;
        cout &lt;&lt;"Array &amp;"&lt;&lt;endl;
    }
    ~Array(){
        cout &lt;&lt; "~array"&lt;&lt;endl;
    }
    void setCount(int count){
        this-&gt;m_iCount = count;
    }
    int getCount(){
        return this-&gt;m_iCount;
    }
private:
    int m_iCount;
};
int main()
{
    Array arr1;
    arr1.setCount(5);
    Array arr2 = arr1;
    cout &lt;&lt; "arr1 "&lt;&lt;arr1.getCount()&lt;&lt;endl;
    cout &lt;&lt; "arr2 "&lt;&lt;arr2.getCount()&lt;&lt;endl;
    return 0;
}</pre>
<pre>Array
Array &amp;
arr1 5
arr2 4
~array
~array</pre>
<h2>深拷贝</h2>
<pre>#include &lt;iostream&gt;

using namespace std;
class Array{
public:
    Array(int count){
        m_iCount = count;
        m_pArr = new int[m_iCount];
        for(int i=0;i&lt;m_iCount;i++){
            m_pArr[i] = i;
        }
    }
    Array(const Array &amp;arr){
        this-&gt;m_iCount = arr.m_iCount;
        this-&gt;m_pArr = new int[m_iCount];
        for(int i=0;i&lt;m_iCount;i++){
            m_pArr[i] = arr.m_pArr[i];
        }
        cout &lt;&lt;"Array &amp;"&lt;&lt;endl;
    }
    ~Array(){
        delete []m_pArr;
        m_pArr = NULL;
        cout &lt;&lt; "~array"&lt;&lt;endl;
    }
    void printAddr(){
        cout &lt;&lt; "m_pArr  "&lt;&lt;m_pArr&lt;&lt;endl;
    }
    void printArr(){
        for(int i=0;i&lt;m_iCount;i++){
            cout&lt;&lt;m_pArr[i]&lt;&lt;endl;
        }
    }
private:
    int m_iCount;
    int *m_pArr;
};
int main()
{
    Array arr1(5);
    Array arr2 = arr1;
    arr1.printAddr();
    arr1.printArr();
    arr2.printAddr();
    arr2.printArr();
    return 0;
}</pre>
<pre>Array &amp;
m_pArr  0x770e08
0
1
2
3
4
m_pArr  0x770e28
0
1
2
3
4
~array
~array</pre>
</div>

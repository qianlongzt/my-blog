+++
title= "c语言指向函数的指针,返回指针的函数"
categories= ["code"]
tags= ["c","指针","函数"]
date= "2016-03-06 16:41:03"
+++

<div class="entry-content">

<strong>函数指针一般定义：<code> </code></strong>
<pre><strong><code>类型标识符 （*变量名）（形参类型列表）</code></strong></pre>
<code> </code><code></code>如
<code> </code>

<code>char (*f1) (float); int （*f2）（int,float); </code>
<pre><code>double(*f)(double)；
double(*q)(double,dobule);
f=sqrt;//f(5)调用sqrt(5);
q=pow;//q(5,3)调用pow(5,3);
</code></pre>
<code> </code><code></code>
<strong>返回指针的函数一般定义为：
<code> </code></strong>
<pre><strong><code>类型标识符  *函数名（类型标识符 形参，类型标识符 形参）
{
  函数体
}
</code></strong></pre>
</div>

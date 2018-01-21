+++
title= "c语言计算结构体大小"
categories= ["code"]
tags= ["c","结构体大小"]
date= "2016-03-06 16:51:12"
+++

<div class="entry-content">
<div>

来源于知乎：https://www.zhihu.com/question/28958350 和 百度 http://zhidao.baidu.com/link?url=9C9BY8tjt11WX5M3nqcSg1Yxt2ljxRlUqAFVS-DnuXoJwmWjpPHt9WEe9a8eueN2uMoz4RSElZn5kj_1oG-NMq

在缺省对齐下我先给你说下三条准则吧，
【1】结构体变量的大小能够被其最宽基本类型成员的大小所整除
【2】结构体每个成员相对于结构体首地址的偏移量是成员大小的整数倍
【3】结构体的总大小为结构体最宽基本类型成员大小的整数倍
以上都是结构体中只有基本类型时的缺省对齐方式，当有嵌套复合成员时，
【2】改为：复合成员相对于结构体首地址偏移量是复合成员最宽基本类型大小的整数倍
typedef struct node
{
int a[100];
char b;
}kkk;
先是第一成员400个字节，然后还有个char一个字节，为了满足第第三条准则，即总大小401为最宽基本类型的整数背，明显401不是最宽基本类型int（4）的整数背，所以总大小为404
<h2 class="zm-item-title zm-editable-content">如何计算结构体大小？</h2>
<div id="zh-question-detail" class="zm-item-rich-text zm-editable-status-normal">
<div class="zm-editable-content">

我先定义了一个结构体
<div class="highlight">
<pre><code class="language-c"><span class="k">struct</span> <span class="n">X</span>
<span class="p">{</span>
	<span class="kt">char</span> <span class="n">a</span><span class="p">;</span>
	<span class="kt">float</span> <span class="n">b</span><span class="p">;</span>
	<span class="kt">int</span> <span class="n">c</span><span class="p">;</span>
	<span class="kt">double</span> <span class="n">d</span><span class="p">;</span>
	<span class="kt">unsigned</span> <span class="n">e</span><span class="p">;</span>
<span class="p">};</span>
</code></pre>
</div>
由于存储变量时地址对齐的要求，所以这个结构体大小应该是32。

如果我多定义一个任意型的指针
<div class="highlight">
<pre><code class="language-text">struct X
{
	char a;
	float b;
	int c;
	double d;
	unsigned e;
        int *f;
};
</code></pre>
</div>
按照地址对齐的要求，这样结构体大小应该是40，但它仍然是32。

我再加一个任意型的指针
<div class="highlight">
<pre><code class="language-text">struct X
{
	char a;
	float b;
	int c;
	double d;
	unsigned e;
        int *f;
        double *g;
};
</code></pre>
</div>
结果这样结构体大小就直接变成40了。如果指针大小是地址总线大小的话，2个指针就是8字节，加上原来的32字节也刚好等于40字节，并且也满足存储变量时地址对齐的要求。但是为什么刚才加一个指针不变，两个就变了。
所以请问一下各位结构体大小应该如何计算。<a class="zu-edit-button" name="edit"></a>

</div>
</div>
作者：匿名用户
链接：https://www.zhihu.com/question/28958350/answer/42691611
来源：知乎

</div>
<div></div>
<div>一开始的时候是这样的struct X {
char a;   // 1 bytes
char padding1[3]; // 3 bytes
float b;  // 4 bytes
int c;   // 4 bytes
char padding2[4]; // 4 bytes
double d;  // 8 bytes
unsigned e;  // 4 bytes
char padding3[4]; // 4 bytes
};
加了一个指针以后是这样的struct X {
char a;   // 1 bytes
char padding1[3]; // 3 bytes
float b;  // 4 bytes
int c;   // 4 bytes
char padding2[4]; // 4 bytes
double d;  // 8 bytes
unsigned e;  // 4 bytes
int *f;   // 4 bytes
};
再加一个指针以后是这样的struct X {
char a;   // 1 bytes
char padding1[3]; // 3 bytes
float b;  // 4 bytes
int c;   // 4 bytes
char padding2[4]; // 4 bytes
double d;  // 8 bytes
unsigned e;  // 4 bytes
int *f;   // 4 bytes
double *g;  // 4 bytes
char padding3[4]; // 4 bytes
};
这样就好懂多了吧？</div>
</div>

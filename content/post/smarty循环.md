+++
title= "smarty循环"
categories= ["code"]
tags= []
date= "2016-03-10 23:29:46"
+++

<pre>&lt;section name=[循环变量] loop=[遍历的变量]&gt;
     {$[遍历的变量][循环变量].title}
     {$[遍历的变量][循环变量].author}
     {$[遍历的变量][循环变量].content}
&lt;/section&gt;</pre>
sectSmarty的循环 section
<ol>
	<li>section、sectionelse功能多，参数多。或许不是太实用。是smarty用来做循环操作的函数之一。</li>
	<li>了解基本属性name和loopion其他的属性：</li>
	<li>start 循环执行的初始位置（第一个是0）。如果该值为负数，开始位置从数组的尾部算起。例如：
如果数组中有7个元素，指定start为-2，那么指向当前数组的索引为5.非法值（超过了循环数组的下限）将被自动调整为最接近的合法值。</li>
	<li>step 该值决定循环的步长。例如指定step=2将只遍历下标为0、2、4等的元素。如果step为负值，那么遍历数组的时候从后向前遍历。</li>
	<li>设定循环最大执行次数。</li>
	<li>show 决定是否显示该循环。</li>
</ol>
<pre>{foreach item=[循环变量] from=[遍历的变量]}
      
{foreachelse}
     [没有数据遍历时候处理的程序]
{/foreach}</pre>
<pre>{foreach $artlist as $art}
     {$art.title}
     {$art.author}
     {$art.content}
{foreachelse}
     [没有数据遍历时候处理的程序]
{/foreach}</pre>

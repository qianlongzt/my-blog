+++
title= "PHP中的赋值运算符"
categories= ["code"]
tags= ["php","赋值","引用赋值"]
date= "2016-03-06 17:00:37"
+++

<div class="entry-content">
<p align="left">PHP的赋值运算符有两种，分别是：</p>
<p align="left">(1)“=”：把右边表达式的值赋给左边的运算数。它将右边表达式值复制一份，交给左边的运算数。换而言之，首先给左边的运算数申请了一块内存，然后把复制的值放到这个内存中。</p>
<p align="left">(2)“&amp;”：引用赋值，意味着两个变量都指向同一个数据。它将使两个变量共享一块内存，如果这个内存存储的数据变了，那么两个变量的值都会发生变化。</p>

<pre>&lt;?php 
    $a = "我在慕课网学习PHP！";
 $b=&amp;$a;
    $c=&amp;$a;
 $a = "我天天在慕课网学习PHP！";
 
 echo $b."&lt;br /&gt;";
 echo $c."&lt;br /&gt;";
?&gt;</pre>
</div>

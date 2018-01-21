+++
title= "smarty条件判断"
categories= ["code"]
tags= []
date= "2016-03-10 23:13:52"
+++

基本句式
<pre>{if $name eq "Fred"}
    Fred
{elseif $name eq "Wilama"}
     Wilama
{else}
    else
{/if}</pre>
条件修饰符有很多，请记得简单的几个eq ( == ) neq ( !eq ) gt ( &gt; ) lt (&lt; )

修饰符必须和变量或常量用空格分开

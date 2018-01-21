+++
title= "smarty 使用函数"
categories= ["code"]
tags= ["函数","php"]
date= "2016-03-11 16:30:52"
+++

使用php函数
{函数的第一个参数| php内置函数名[:第n个参数]|}  这样子使用函数，函数必须要有一个参数
<ul>
	<li>date函数
<ul>
	<li>{'Y-m-d'| date: $time}</li>
</ul>
</li>
	<li>str_replace函数
<ul>
	<li>{'d'|str_replace:'h':$str}</li>
</ul>
</li>
</ul>
smarty 自定义函数
先在php代码中写好一个函数
<pre>function test($params) {
   $p1 = $params['p1'];
   $p2 = $params['p2'];
   return '传入的参数1值为'.$p1.', 传入的参数2值为'.$p2;
}</pre>
然后在smarty中注册这个函数 registerPlugin 第一个参数可选值 funtion，modifier，block等
<pre>$smarty -&gt; registerPlugin('function','f_test','test');</pre>
然后再模板中使用这个函数  {函数名 [参数=参数值]... }
<pre>{f_test p1='123' p2='234'}</pre>
然后函数的参数就会以关联数组的形式给test函数

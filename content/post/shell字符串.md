+++
title= "Shell字符串"
categories= ["code"]
tags= ["字符串"]
date= "2016-03-08 00:35:38"
+++

<div id="content" class="content">

来自<a href="http://www.imooc.com/wiki/detail/id/786">http://www.imooc.com/wiki/detail/id/786</a>

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。单双引号的区别跟PHP类似。
<h2>单引号</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">str='this is a string'</pre>
单引号字符串的限制：
<ul class=" list-paddingleft-2">
	<li>单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；</li>
	<li>单引号字串中不能出现单引号（对单引号使用转义符后也不行）。</li>
</ul>
<h2>双引号</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">your_name='qinjx'
str="Hello, I know your are \"$your_name\"! \n"</pre>
双引号的优点：
<ul class=" list-paddingleft-2">
	<li>双引号里可以有变量</li>
	<li>双引号里可以出现转义字符</li>
</ul>
<div class="anchor-list"></div>
<h2>拼接字符串</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">your_name="qinjx"
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting $greeting_1  #输出hello, qinjx ! hello, qinjx</pre>
<h2>获取字符串长度</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">string="abcd"echo ${#string} #输出 4</pre>
<h2>提取子字符串</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">string="alibaba is a great company"
echo ${string:1:4} #输出liba</pre>
<div class="anchor-list"></div>
<h2>查找子字符串</h2>
<pre class="shell sh_sh snippet-formatted sh_sourceCode">string="alibaba is a great company"
echo `expr index "$string" is`  #输出3</pre>
</div>
<div class="refer">
<ul class="clearfix">
	<li>贡献者：</li>
	<li>穿山Jack</li>
</ul>
</div>

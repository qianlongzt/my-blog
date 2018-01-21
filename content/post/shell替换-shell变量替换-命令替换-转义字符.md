+++
title= "Shell变量替换，命令替换，转义字符"
categories= ["电脑","code"]
tags= ["变量替换","命令替换转义字符"]
date= "2016-03-07 23:49:07"
+++

来源<a href="http://www.imooc.com/wiki/detail/id/777">http://www.imooc.com/wiki/detail/id/777</a>和<a href="http://www.jb51.net/article/49018.htm">http://www.jb51.net/article/49018.htm</a>
如果表达式中包含特殊字符，Shell 将会进行替换。例如，在双引号中使用变量就是一种替换，转义字符也是一种替换。

举个例子：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash&gt;a=10
echo -e "Value of a is $a \n"
</pre>
运行结果：
<pre class="info-box">Value of a is 10
</pre>
这里 -e 表示对转义字符进行替换。如果不使用 -e 选项，将会原样输出：
<pre class="info-box">Value of a is 10\n
</pre>
下面的转义字符都可以用在 echo 中：
<ul>
	<li>\\ 反斜杠</li>
	<li>\a警报，响铃</li>
	<li>\b退格（删除键）</li>
	<li>\f换页(FF)，将当前位置移到下页开头</li>
	<li>\n换行</li>
	<li>\r回车</li>
	<li>\t水平制表符（tab键）</li>
	<li>\v垂直制表符</li>
</ul>
可以使用 echo 命令的 -E 选项禁止转义，默认也是不转义的；使用 -n 选项可以禁止插入换行符。
<h2>命令替换</h2>
命令替换是指Shell可以先执行命令，将输出结果暂时保存，在适当的地方输出。命令替换(command substitution)是指 Shell 执行命令并将命令替换部分替换为执行该命令后的结果
命令替换的语法：（内嵌的 backtick 符号和双引号都需要进行转义）
<pre class="shell sh_sh snippet-formatted sh_sourceCode">`command`
</pre>
注意是反引号，不是单引号，这个键位于 Esc 键下方。
下面的例子中，将命令执行结果保存在变量中：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
DATE=`date`
echo "Date is $DATE"
USERS=`who | wc -l`
echo "Logged in user are $USERS"
UP=`date ; uptime`
echo "Uptime is $UP"
</pre>
运行结果：
<pre class="info-box">Date is Thu Jul  2 03:59:57 MST 2009
Logged in user are 1
Uptime is Thu Jul  2 03:59:57 MST 2009
03:59:57 up 20 days, 14:03,  1 user,  load avg: 0.13, 0.07, 0.15
</pre>
2. 使用 $(…) 的方式。内嵌的括号则无需转义
<pre>for i in $(cd /old/code/dir ; echo *.c)
 do
 diff -c /old/code/dir/$i $i
 done | more</pre>
<h2>变量替换</h2>
变量替换可以根据变量的状态（是否为空、是否定义等）来改变它的值
可以使用的变量替换形式：
<table style="height: 169px" width="922">
<tbody>
<tr class="firstRow">
<th>形式</th>
<th>说明</th>
</tr>
<tr>
<td>${var}</td>
<td>变量本来的值</td>
</tr>
<tr>
<td>${var:-word}</td>
<td>如果变量 var 为空或已被删除(unset)，那么返回 word，但不改变 var 的值。</td>
</tr>
<tr>
<td>${var:=word}</td>
<td>如果变量 var 为空或已被删除(unset)，那么返回 word，并将 var 的值设置为 word。</td>
</tr>
<tr>
<td>${var:?message}</td>
<td>如果变量 var 为空或已被删除(unset)，那么将消息 message 送到标准错误输出，可以用来检测变量 var 是否可以被正常赋值。
若此替换出现在Shell脚本中，那么脚本将停止运行。</td>
</tr>
<tr>
<td>${var:+word}</td>
<td>如果变量 var 被定义，那么返回 word，但不改变 var 的值。</td>
</tr>
</tbody>
</table>
请看下面的例子：
<pre class="info-box">#!/bin/bash
echo ${var:-"Variable is not set"}
echo "1 - Value of var is ${var}"

echo ${var:="Variable is not set"}
echo "2 - Value of var is ${var}"

unset var
echo ${var:+"This is default value"}
echo "3 - Value of var is $var"

var="Prefix"
echo ${var:+"This is default value"}
echo "4 - Value of var is $var"

echo ${var:?"Print this message"}
echo "5 - Value of var is ${var}"
</pre>
运行结果：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">Variable is not set
1 - Value of var is 
Variable is not set
2 - Value of var is Variable is not set

3 - Value of var is 
This is default value
4 - Value of var is Prefix
Prefix
5 - Value of var is Prefix</pre>
<div class="pic-viewer-wrap">
<div class="pic-viewer-inner J-viewer-inner"><img src="http://img.mukewang.com/56cc603e0001eab112800720.jpg" alt="" /></div>
</div>

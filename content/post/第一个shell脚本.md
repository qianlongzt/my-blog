+++
title= "第一个Shell脚本"
categories= ["电脑","code"]
tags= []
date= "2016-03-07 20:59:14"
+++

<div class="title clearfix"><a href="http://www.imooc.com/wiki/detail/id/768">来源http://www.imooc.com/wiki/detail/id/768</a></div>
<div class="title clearfix"><span class="text"> </span></div>
<div id="content" class="content">

打开文本编辑器，新建一个文件，扩展名为sh（sh代表shell），扩展名并不影响脚本执行，见名知意就好，如果你用php写shell 脚本，扩展名就用php好了。

输入一些代码：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bashecho "Hello World !"</pre>
“#!” 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种Shell。echo命令用于向窗口输出文本。

运行Shell脚本有两种方法。
<h2>作为可执行程序</h2>
将上面的代码保存为test.sh，并 cd 到相应目录：
<pre class="info-box">chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本</pre>
注意，一定要写成./test.sh，而不是test.sh。运 行其它二进制的程序也一样，直接写test.sh，linux系统会去PATH里寻找有没有叫test.sh的，而只有/bin, /sbin, /usr/bin，/usr/sbin等在PATH里，你的当前目录通常不在PATH里，所以写成test.sh是会找不到命令的，要用. /test.sh告诉系统说，就在当前目录找。

通过这种方式运行bash脚本，第一行一定要写对，好让系统查找到正确的解释器。

这里的"系统"，其实就是shell这个应用程序（想象一下Windows Explorer），但我故意写成系统，是方便理解，既然这个系统就是指shell，那么一个使用/bin/sh作为解释器的脚本是不是可以省去第一行呢？是的。
<h2>作为解释器参数</h2>
这种运行方式是，直接运行解释器，其参数就是shell脚本的文件名，如：
<pre class="info-box">/bin/sh test.sh
/bin/php test.php</pre>
这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。

再看一个例子。下面的脚本使用 <strong>read</strong> 命令从 stdin 获取输入并赋值给 PERSON 变量，最后在 stdout 上输出：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
# Author : mozhiyan
# Copyright (c) http://see.xidian.edu.cn/cpp/linux
# Script follows here:
echo "What is your name?"
read PERSON
echo "Hello, $PERSON"
</pre>
运行脚本：
<pre class="info-box">chmod +x ./test.sh
$ ./test.sh
What is your name?
mozhiyan
Hello, mozhiyan
$</pre>
</div>
<div class="refer">
<ul class="clearfix">
	<li>贡献者：</li>
	<li>穿山Jack</li>
</ul>
</div>

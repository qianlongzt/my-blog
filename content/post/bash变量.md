+++
title= "bash变量"
categories= ["电脑","code"]
tags= ["变量"]
date= "2016-03-07 23:17:17"
+++

来源<a href="http://www.imooc.com/video/6511">http://www.imooc.com/video/6511</a>和<a href="http://blog.sina.com.cn/s/blog_6268defa0100wijx.html">http://blog.sina.com.cn/s/blog_6268defa0100wijx.html</a>

变量的分类：
<ol>
	<li>用户自定义变量：变量名和值都是用户自定义的</li>
	<li>环境变量：可以用户自定义，但是对系统生效的环境变量名和变量作用是固定的</li>
	<li>预定义变量：变量名和作用都是固定的，是系统确定的，用户不能定义只能改值</li>
	<li>位置参数变量：这种变量主要是用来向脚本当中传递参数或数据的，变量名不能自定义，变量作用是固定的；（一种预定义变量）</li>
</ol>
变量命名规则：以字母或下划线打头，名字中间可以由字母，下划线，数字组成。
在任何系统中，目录名、文件名、变量名都要有含义
在一个程序里，变量名必须唯一
在Bash中，变量的默认类型都是字符串型。

用户自定义变量：
<ul>
	<li>变量定义
<ul>
	<li>变量名=变量值</li>
	<li>x=5      (等号两边不能加空格)</li>
</ul>
</li>
	<li>变量调用
<ul>
	<li>echo $x   // 输出  5 （字符串5）</li>
</ul>
</li>
	<li>变量叠加
<ul>
	<li>
<pre>x=123
echo "$x"456 //输出1234556
echo ${x}789 //输出123789</pre>
</li>
</ul>
</li>
	<li>变量查看
<ul>
	<li>set
<ul>
	<li>-u 如果设定这个选项，调用未声明变量是会报错（默认无任何提示）</li>
</ul>
</li>
</ul>
</li>
	<li>删除变量
<ul>
	<li>unset 变量名</li>
</ul>
</li>
</ul>
环境变量
<ul>
	<li>与用户自定义变量的区别（pstree（查看进程树））
用户自定义变量只在当前shell中生效
环境变量在当前shell和这个shell的所有子shell中生效</li>
	<li>设置环境变量
<ul>
	<li>export 变量名=变量值</li>
</ul>
</li>
	<li>查看环境变量
<ul>
	<li>set 查看所有变量</li>
	<li>env 查看环境变量</li>
</ul>
</li>
	<li>常用环境变量
<ul>
	<li>HOSTNAME 当前主机名</li>
	<li>SHELL 当前shell</li>
	<li>TERM终端环境</li>
	<li>HISTSIZE 历史命令条数</li>
	<li>SSH_CLIENT 当前操作环境是用ssh链接的，指令记录客户端ip</li>
	<li>SSH_TTY  ssh连接的终端时pts/1</li>
	<li>USER 当前登录的用户</li>
	<li>PATH 系统搜索命令的路径
<ul>
	<li>echo $PATH  // 查看当前搜索路径</li>
	<li>PATH="$PATH":/root/sh     //PATH 加入 /root/sh</li>
</ul>
</li>
	<li>PS1 命令提示符
<ul>
	<li>\d 显示日期，格式为 “星期 月 日”</li>
	<li>\H 显示完整的主机名。如默认主机名 “localhost.localdomain”</li>
	<li>\h 显示短主机名。如默认短主机名“localhost”</li>
	<li>\t 显示24小时制时间，格式为“HH:MM:SS”</li>
	<li>\T 显示12小时制时间，格式 为“HH:MM:SS”</li>
	<li>\A 显示24小时制时间，格式为“HH:MM”</li>
	<li>\u 显示当前用户名</li>
	<li>\w 显示当前所在目录的完整名称。家目录会以 ~代替</li>
	<li>\W 显示所在目录的最后一个目录</li>
	<li>\$ 提示符。如果是root用户会显示提示符 为 “#” ，如果是普通用户会显示提示符为“$”</li>
	<li>\v ：BASH的版本信息</li>
	<li>
<div>\# ：下达的第几个命令</div>
<div></div></li>
</ul>
</li>
	<li>PS2：第一行没输完，等待第二行输入的提示符。</li>
</ul>
</li>
	<li>语系变量
<ul>
	<li>查看 locale
<ul>
	<li>LANG  : 定义系统主语系变量</li>
	<li>LC_ALL:  定义整体语系的变量</li>
	<li>locale -a 查看所有支持的语系</li>
</ul>
</li>
	<li>如果 有图形界面 支持中文
第三方 设置正确支持中文
纯字符界面 不支持中文，可以用第三方插件支持（zhcon等）</li>
</ul>
</li>
</ul>
位置参数变量
<ul>
	<li>$* 返回所有的参数值，把所有的参数值看成一个整体</li>
	<li>$@ 返回所有的参数值，把参数值区分对待</li>
	<li>$# 返回参数值的个数。</li>
	<li>$n n为数字，$0 表示命令本身 $0-$9代表第一个到地九个参数，十个以上的参数需要用大括号包含，如${10},如果没有就是变成$1的值连接上0</li>
</ul>
预定义变量（要在双引号中用，或者不要引号）
<ul>
	<li>$? 最后一次执行命令的返回i状态。如果这个变量的值是0，证明上一个命令正确执行；如果这个值非0（具体是哪个数，由命令自己来决定），证明上一个命令执行不正确</li>
	<li>$$ 当前进程的进程号</li>
	<li>$!后台运行的最后一个进程的进程号</li>
</ul>
read [选项] [变量名]
<ul>
	<li>-p 提示语句</li>
	<li>-t 时间限制，单位为秒</li>
	<li>-s 输入内容时，会隐藏，不会显示出来； echo是输出值</li>
	<li>-n 后面跟数字。比如 -n 2 则输入内容时，只要输入了2个字符，它就自动输出，不会再读后面的了~~只读两个</li>
	<li>echo -e "\n" 要执行转定义符，必须前面加 -e，可以使用 echo 命令的 -E 选项禁止转义，默认也是不转义的；使用 -n 选项可以禁止插入换行符
<ul>
	<li>\\ 反斜杠</li>
	<li>\a警报，响铃</li>
	<li>\b退格（删除键）</li>
	<li>\f换页(FF)，将当前位置移到下页开头</li>
	<li>\n换行</li>
	<li>\r&gt;回车</li>
	<li>\t水平制表符（tab键）</li>
	<li>\v垂直制表符</li>
</ul>
</li>
</ul>

<div id="content" class="content">

Bash 支持很多运算符 :
<ul>
	<li>算数运算符</li>
	<li>关系运算符</li>
	<li>布尔运算符</li>
	<li>字符串运算符</li>
	<li>文件测试运算符</li>
</ul>
原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。
expr 是一款表达式计算工具，使用它能完成表达式的求值操作。
例如，两个数相加：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
val=`expr 2 + 2` 
#val=$(expr 2 + 2)
#declare -i val=2+2
#val=$((2 + 2))可以没有空格
#val=$[ 2 + 2 ] //可以没有空格
echo "Total value : $val"</pre>
运行脚本输出：
<pre class="info-box">Total value : 4</pre>
两点注意：
<ul class=" list-paddingleft-2">
	<li>表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。</li>
	<li>完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。</li>
</ul>
<h2>算术运算符</h2>
先来看一个使用算术运算符的例子：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
a=10
b=20
val=`expr $a + $b`
echo "a + b : $val"
val=`expr $a - $b`
echo "a - b : $val"
val=`expr $a \* $b`
echo "a * b : $val"
val=`expr $b / $a`
echo "b / a : $val"
val=`expr $b % $a`
echo "b % a : $val"
if [ $a == $b ];then
    echo "a is equal to b"
fi
if [ $a != $b ];then
    echo "a is not equal to b"
fi</pre>
运行结果：
<pre class="info-box">a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a is not equal to b</pre>
注意：
<ul class=" list-paddingleft-2">
	<li>乘号(*)前边必须加反斜杠(\)才能实现乘法运算；</li>
</ul>
<table><caption>算术运算符列表</caption>
<tbody>
<tr class="firstRow">
<th>运算符</th>
<th>说明</th>
<th>举例</th>
</tr>
<tr>
<td>+</td>
<td>加法</td>
<td>`expr $a + $b` 结果为 30。</td>
</tr>
<tr>
<td>-</td>
<td>减法</td>
<td>`expr $a - $b` 结果为 10。</td>
</tr>
<tr>
<td>*</td>
<td>乘法</td>
<td>`expr $a \* $b` 结果为  200。</td>
</tr>
<tr>
<td>/</td>
<td>除法</td>
<td>`expr $b / $a` 结果为 2。</td>
</tr>
<tr>
<td>%</td>
<td>取余</td>
<td>`expr $b % $a` 结果为 0。</td>
</tr>
<tr>
<td>=</td>
<td>赋值</td>
<td>a=$b 将把变量 b 的值赋给 a。</td>
</tr>
<tr>
<td>==</td>
<td>相等。用于比较两个数字，相同则返回 true。</td>
<td>[ $a == $b ] 返回 false。</td>
</tr>
<tr>
<td>!=</td>
<td>不相等。用于比较两个数字，不相同则返回 true。</td>
<td>[ $a != $b ] 返回 true。</td>
</tr>
</tbody>
</table>
<div class="pic-viewer-inner J-viewer-inner">

[caption id="" align="aligncenter" width="720"]<img src="http://img.mukewang.com/56dcdea400011ada07200406.jpg" alt="运算符优先级" width="720" height="406" /> 运算符优先级[/caption]

</div>
注意：条件表达式

要放在方括号之间，并且要有空格，例如 [$a==$b] 是错误的，必须写成 [ $a == $b ]。
<h2>关系运算符</h2>
关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

先来看一个关系运算符的例子：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
a=10
b=20
if [ $a -eq $b ];then
    echo "$a -eq $b : a is equal to b"
else
    echo "$a -eq $b: a is not equal to b"
fi
if [ $a -ne $b ];then
    echo "$a -ne $b: a is not equal to b"
else
    echo "$a -ne $b : a is equal to b"
fi
if [ $a -gt $b ];then
    echo "$a -gt $b: a is greater than b"
else
    echo "$a -gt $b: a is not greater than b"
fi
if [ $a -lt $b ];then
    echo "$a -lt $b: a is less than b"
else
    echo "$a -lt $b: a is not less than b"
fi
if [ $a -ge $b ];then
    echo "$a -ge $b: a is greater or  equal to b"
else
    echo "$a -ge $b: a is not greater or equal to b"
fi
if [ $a -le $b ];then
    echo "$a -le $b: a is less or  equal to b"
else
    echo "$a -le $b: a is not less or equal to b"
fi</pre>
运行结果：
<pre class="info-box">10 -eq 20: a is not equal to b
10 -ne 20: a is not equal to b
10 -gt 20: a is not greater than b
10 -lt 20: a is less than b
10 -ge 20: a is not greater or equal to b
10 -le 20: a is less or  equal to b</pre>
<table><caption>关系运算符列表</caption>
<tbody>
<tr class="firstRow">
<th>运算符</th>
<th>说明</th>
<th>举例</th>
</tr>
<tr>
<td>-eq</td>
<td>检测两个数是否相等，相等返回 true。</td>
<td>[ $a -eq $b ] 返回 true。</td>
</tr>
<tr>
<td>-ne</td>
<td>检测两个数是否相等，不相等返回 true。</td>
<td>[ $a -ne $b ] 返回 true。</td>
</tr>
<tr>
<td>-gt</td>
<td>检测左边的数是否大于右边的，如果是，则返回 true。</td>
<td>[ $a -gt $b ] 返回 false。</td>
</tr>
<tr>
<td>-lt</td>
<td>检测左边的数是否小于右边的，如果是，则返回 true。</td>
<td>[ $a -lt $b ] 返回 true。</td>
</tr>
<tr>
<td>-ge</td>
<td>检测左边的数是否大等于右边的，如果是，则返回 true。</td>
<td>[ $a -ge $b ] 返回 false。</td>
</tr>
<tr>
<td>-le</td>
<td>检测左边的数是否小于等于右边的，如果是，则返回 true。</td>
<td>[ $a -le $b ] 返回 true。</td>
</tr>
</tbody>
</table>
<div class="anchor-list"></div>
<h2>布尔运算符</h2>
先来看一个布尔运算符的例子：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
a=10
b=20
if [ $a != $b ];then
    echo "$a != $b : a is not equal to b"
else
    echo "$a != $b: a is equal to b"
fi
if [ $a -lt 100 -a $b -gt 15 ];then
    echo "$a -lt 100 -a $b -gt 15 : returns true"
else
    echo "$a -lt 100 -a $b -gt 15 : returns false"
fi
if [ $a -lt 100 -o $b -gt 100 ];then
    echo "$a -lt 100 -o $b -gt 100 : returns true"
else
    echo "$a -lt 100 -o $b -gt 100 : returns false"
fi
if [ $a -lt 5 -o $b -gt 100 ];then
    echo "$a -lt 100 -o $b -gt 100 : returns true"
else
    echo "$a -lt 100 -o $b -gt 100 : returns false"
fi</pre>
运行结果：
<pre class="info-box">10 != 20 : a is not equal to b
10 -lt 100 -a 20 -gt 15 : returns true
10 -lt 100 -o 20 -gt 100 : returns true
10 -lt 5 -o 20 -gt 100 : returns false</pre>
<table><caption>布尔运算符列表</caption>
<tbody>
<tr class="firstRow">
<th>运算符</th>
<th>说明</th>
<th>举例</th>
</tr>
<tr>
<td>!</td>
<td>非运算，表达式为 true 则返回 false，否则返回 true。</td>
<td>[ ! false ] 返回 true。</td>
</tr>
<tr>
<td>-o</td>
<td>或运算，有一个表达式为 true 则返回 true。</td>
<td>[ $a -lt 20 -o $b -gt 100 ] 返回 true。</td>
</tr>
<tr>
<td>-a</td>
<td>与运算，两个表达式都为 true 才返回 true。</td>
<td>[ $a -lt 20 -a $b -gt 100 ] 返回 false。</td>
</tr>
</tbody>
</table>
<h2 class="anchor-list">字符串运算符</h2>
先来看一个例子：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
a="abc"
b="efg"
if [ $a = $b ];then
    echo "$a = $b : a is equal to b"
else
    echo "$a = $b: a is not equal to b"
fi
if [ $a != $b ];then
    echo "$a != $b : a is not equal to b"
else
    echo "$a != $b: a is equal to b"
fi
if [ -z $a ];then
    echo "-z $a : string length is zero"
else
    echo "-z $a : string length is not zero"
fi
if [ -n $a ];then
    echo "-n $a : string length is not zero"
else
    echo "-n $a : string length is zero"
fi
if [ $a ];then
    echo "$a : string is not empty"
else
    echo "$a : string is empty"
fi</pre>
运行结果：
<pre class="info-box">abc = efg: a is not equal to b
abc != efg : a is not equal to b
-z abc : string length is not zero
-n abc : string length is not zero
abc : string is not empty</pre>
<table><caption>字符串运算符列表</caption>
<tbody>
<tr class="firstRow">
<th>运算符</th>
<th>说明</th>
<th>举例</th>
</tr>
<tr>
<td>=</td>
<td>检测两个字符串是否相等，相等返回 true。</td>
<td>[ $a = $b ] 返回 false。</td>
</tr>
<tr>
<td>!=</td>
<td>检测两个字符串是否相等，不相等返回 true。</td>
<td>[ $a != $b ] 返回 true。</td>
</tr>
<tr>
<td>-z</td>
<td>检测字符串长度是否为0，为0返回 true。</td>
<td>[ -z $a ] 返回 false。</td>
</tr>
<tr>
<td>-n</td>
<td>检测字符串长度是否为0，不为0返回 true。</td>
<td>[ -z $a ] 返回 true。</td>
</tr>
<tr>
<td>str</td>
<td>检测字符串是否为空，不为空返回 true。</td>
<td>[ $a ] 返回 true。</td>
</tr>
</tbody>
</table>
<div class="anchor-list"></div>
<h2>文件测试运算符</h2>
文件测试运算符用于检测 Unix 文件的各种属性。

例如，变量 file 表示文件“/var/www/tutorialspoint/unix/test.sh”，它的大小为100字节，具有 rwx 权限。下面的代码，将检测该文件的各种属性：
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#!/bin/bash
file="/var/www/tutorialspoint/unix/test.sh"
if [ -r $file ];then
    echo "File has read access"
else
    echo "File does not have read access"
fi
if [ -w $file ];then
    echo "File has write permission"
else
    echo "File does not have write permission"
fi
if [ -x $file ];then
    echo "File has execute permission"
else
    echo "File does not have execute permission"
fi
if [ -f $file ];then
    echo "File is an ordinary file"
else
    echo "This is sepcial file"
fi
if [ -d $file ];then
    echo "File is a directory"
else
    echo "This is not a directory"
fi
if [ -s $file ];then
    echo "File size is zero"
else
    echo "File size is not zero"
fi
if [ -e $file ];then
    echo "File exists"
else
    echo "File does not exist"
fi</pre>
运行结果：
<pre class="info-box">File has read access
File has write permission
File has execute permission
File is an ordinary file
This is not a directory
File size is zero
File exists</pre>
<table><caption>文件测试运算符列表</caption>
<tbody>
<tr class="firstRow">
<th>操作符</th>
<th>说明</th>
<th>举例</th>
</tr>
<tr>
<td>-b file</td>
<td>检测文件是否是块设备文件，如果是，则返回 true。</td>
<td>[ -b $file ] 返回 false。</td>
</tr>
<tr>
<td>-c file</td>
<td>检测文件是否是字符设备文件，如果是，则返回 true。</td>
<td>[ -b $file ] 返回 false。</td>
</tr>
<tr>
<td>-d file</td>
<td>检测文件是否是目录，如果是，则返回 true。</td>
<td>[ -d $file ] 返回 false。</td>
</tr>
<tr>
<td>-f file</td>
<td>检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。</td>
<td>[ -f $file ] 返回 true。</td>
</tr>
<tr>
<td>-g file</td>
<td>检测文件是否设置了 SGID 位，如果是，则返回 true。</td>
<td>[ -g $file ] 返回 false。</td>
</tr>
<tr>
<td>-k file</td>
<td>检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。</td>
<td>[ -k $file ] 返回 false。</td>
</tr>
<tr>
<td>-p file</td>
<td>检测文件是否是具名管道，如果是，则返回 true。</td>
<td>[ -p $file ] 返回 false。</td>
</tr>
<tr>
<td>-u file</td>
<td>检测文件是否设置了 SUID 位，如果是，则返回 true。</td>
<td>[ -u $file ] 返回 false。</td>
</tr>
<tr>
<td>-r file</td>
<td>检测文件是否可读，如果是，则返回 true。</td>
<td>[ -r $file ] 返回 true。</td>
</tr>
<tr>
<td>-w file</td>
<td>检测文件是否可写，如果是，则返回 true。</td>
<td>[ -w $file ] 返回 true。</td>
</tr>
<tr>
<td>-x file</td>
<td>检测文件是否可执行，如果是，则返回 true。</td>
<td>[ -x $file ] 返回 true。</td>
</tr>
<tr>
<td>-s file</td>
<td>检测文件是否为空（文件大小是否大于0），不为空返回 true。</td>
<td>[ -s $file ] 返回 true。</td>
</tr>
<tr>
<td>-e file</td>
<td>检测文件（包括目录）是否存在，如果是，则返回 true。</td>
<td>[ -e $file ] 返回 true。</td>
</tr>
</tbody>
</table>
</div>
<div class="refer">
<ul class="clearfix">
	<li>贡献者：</li>
	<li>穿山Jack</li>
</ul>
</div>

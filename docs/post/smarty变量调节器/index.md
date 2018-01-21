<ol>
	<li>首字母大写captitalie
{$articleTitle|captitalize}</li>
	<li>字符串连接 cat
{$articleTitle|cat: " yesterday."}</li>
	<li>日期格式化 date_format
{$date|date_format} //月，日，年
{$date | date_format : " %A, %B %e, %Y %H:%M:%S"}</li>
	<li>为未赋值或为空的变量指定默认值default
{$articleTitle|default:"no title"}</li>
	<li>转码 escape
用于html专门，url转码，在没有转码的变量上转换单引号，十六进制转码，十六进制美化，或者javascript转码。默认是html转码
{$url|escape :"url"}</li>
	<li>小写lower 大写upper
将变量字符串小（大） 写
{$articleTitle|lower} {$articleTitle|upper}</li>
	<li>所有的换行符将被替换为&lt;br /&gt;     nl2br 功能同PHP中的nl2br()函数一样
{$blog|nl2br}</li>
	<li>其他的函数
可以参见手册，原则上应该通过php直接处理完再赋值到smarty变量里，少用smarty函数
类如 wordwrap 行宽 -&gt;  使用css样式来解决 truncate
截取 -&gt; 使用php来截取 或使用css样式来解决</li>
</ol>

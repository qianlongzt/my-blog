+++
title= "php用constant常量的不同输出"
categories= ["code"]
tags= ["php","constant"]
date= "2016-03-06 17:02:17"
+++

<div class="entry-content">
<p align="left">第二种是使用constant()函数。它和直接使用常量名输出的效果是一样的，但函数可以动态的输出不同的常量，在使用上要灵活、方便，其语法格式如下：</p>

<pre class="code">mixed constant(string constant_name)</pre>
<p align="left">第一个参数constant_name为要获取常量的名称，也可为存储常量名的变量。如果成功则返回常量的值，失败则提示错误信息常量没有被定义。（注：mixed表示函数返回值类型为多种不同的类型，string表示参数类型为字符串类型）</p>

<pre>&lt;?php 
$p="";
//定义圆周率的两种取值
define("PI1",3.14);
define("PI2",3.142);
//定义值的精度
$height = "中";
//根据精度返回常量名，将常量变成了一个可变的常量
if($height == "中"){
    $p = "PI1";
}else if($height == "低"){
 $p = "PI2";
}
$r=1;
$area=constant($p)*$r*$r;
echo $area;
?&gt;</pre>
</div>

+++
title= "Smarty类和对象赋值与使用"
categories= ["code"]
tags= ["类传递"]
date= "2016-03-11 13:08:48"
+++

smarty可以将对象传递到模板，然后在模板像php那样使用

class my_object{
function meth1($param){
return $param[0].'已经'.$param[1];
}
}
$myobj=new my_object();
$smarty-&gt;assign('myobj',$myobj);
$smarty-&gt;display("test.html");

//********test.html*******************
&lt;!doctype html&gt;
&lt;html&gt;
&lt;meta charset="utf-8"&gt;
&lt;head&gt;&lt;/head&gt;
&lt;body&gt;
&lt;!--以数组形式--&gt;
{$myobj-&gt;meth1(array('苹果','熟了'))}
&lt;/body&gt;
&lt;/html&gt;

+++
title= "smarty插件"
categories= ["code"]
tags= []
date= "2016-03-11 21:31:31"
+++

smarty插件本质上是function 函数

Smarty 插件常用类型
<ul>
	<li>functions 函数插件</li>
	<li>modifiers 修饰插件</li>
	<li>block functions 区块函数插件</li>
</ul>
制作，使用插件
<ul>
	<li>使用registerPlugin 方法注册写好的自定义函数</li>
	<li>将写好的插件放入smarty解压目录中的libs/plugins/中</li>
	<li>php的内置函数，可以自动以修饰插件（变量调节器插件）的形式在模板中使用</li>
</ul>
创建Smarty function插件：在插件目录里新建文件 function.插件名.php文件（如 function.插件名.php），然后插件方法名字书写规范：
smarty_modifier_插件名([...]){}  如
<pre>function smarty_function_test($params){
   $width = $params['width'];
   $height = $params['height'];
   $area = $width * $height;
   return $area;
}</pre>
调用就是 {函数名 [参数=参数值]..... }
<pre>{test width=151 height=200}</pre>
创建Smarty modifier插件：在插件目录里新建文件 modifier.插件名.php文件（如 modifier.插件名.php），然后插件方法名字书写规范：
smarty_modifier_插件名($param1 [, $param2].....  ){}  如
<pre>    function smarty_modifier_test($utime, $format){
        return date($format,$utime);
    }</pre>
调用就是 {函数名 [参数=参数值]..... }
<pre>{$time|test:'Y-m-d H:i:s'</pre>
创建Smarty block插件：在插件目录里新建文件block.插件名.php文件（如 block.插件名.php），然后插件方法名字书写规范：
smarty_block_插件名( $params,$content ){}  如
<pre>    function smarty_block_test2($params, $content) {
        $replace = $params['replace'];
        $maxnum = $params['maxnum'];
        if($replace == 'true') {
            $content = str_replace("，", ",", $content);
            $content = str_replace('。', ".", $content);
        }
        $content = substr($content, 0, $maxnum);
        return $content;
    }</pre>
调用就是 {函数名 参数=参数值} {传给函数的变量}{/函数名}
<pre>{test2 replace='true' maxnum=100}
    {$str}
{/test2}</pre>

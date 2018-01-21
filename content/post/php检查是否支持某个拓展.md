+++
title= "php检查是否支持某个拓展"
categories= ["code"]
tags= ["php","拓展"]
date= "2016-03-06 16:54:10"
+++

<pre id="J_CodeLang" class="code-head">&lt;?php
if(function_exists('mysql_connect')){
    echo "MySQL扩展已经安装";
}</pre>

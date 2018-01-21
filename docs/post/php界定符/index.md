<div class="entry-content">

我们可以使用Heredoc结构形式的方法来解决该问题，首先使用定界符表示字符串（&lt;&lt;&lt;），接着在“&lt;&lt;&lt;“之后提供一个标识符GOD，然后是字符串，最后以提供的这个标识符结束字符串
<div>&lt;?php
$string1= &lt;&lt;&lt;GOD
我有一只小毛驴，我从来也不骑。
有一天我心血来潮，骑着去赶集。
我手里拿着小皮鞭，我心里正得意。
不知怎么哗啦啦啦啦，我摔了一身泥.
GOD;</div>
<div></div>
<div>echo $string1;
?&gt;</div>
</div>

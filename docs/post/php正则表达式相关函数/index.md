<ol>
	<li>preg_match($pattern, $subject,[array&amp; $match])
用$pattern去匹配$subject 如果有一个匹配就返回并停止匹配，并将匹配到的值写入$match 中 并返回匹配到的个数</li>
	<li>preg_match_all($pattern, $subject, $matches)
用$pattern去匹配$subject 找到所有匹配，并将匹配到的值写入$matches 中 并返回匹配到的个数</li>
</ol>
<pre>$pattern = '/[0-9]/';
$subject = 'helsda1324iuhihf13333';
echo preg_match($pattern,$subject,$match)."\n";
echo preg_match_all($pattern, $subject, $matches)."\n";
var_dump($match);
var_dump($matches);</pre>
<pre>1
9
array(1) {
  [0]=&gt;
  string(1) "1" 
} 
array(1) {
  [0]=&gt;
  array(9) {
    [0]=&gt;
    string(1) "1" 
    [1]=&gt;
    string(1) "3"
    [2]=&gt;
    string(1) "2"
    [3]=&gt;
    string(1) "4"
    [4]=&gt;
    string(1) "1" 
    [5]=&gt;
    string(1) "3" 
    [6]=&gt;
    string(1) "3"
    [7]=&gt;
    string(1) "3" 
    [8]=&gt;
    string(1) "3" 
  } 
}</pre>
<h2>正则替换函数</h2>
<pre>mixed preg_replace(mixed $pattern,mixed $replacement, mixed $subject) 和
mixed preg_filter(mixed $pattern,mixed $replacement,mixed $subject)</pre>
<ol>
	<li>$pattern 是字符串，$replacement必须是字符串</li>
	<li>$pattern 是数组, $replacement 可以是数组，也可以是字符串
<ol>
	<li>数组：一一对应，如果不对应
<ol>
	<li>$pattern 数目大于 $replacement ,则对应的置换为空</li>
	<li>$pattern数目小于 $replacement ，则$replacement中多余的不会使用</li>
</ol>
</li>
	<li>字符串，每一个匹配到的都替换成字符串</li>
</ol>
</li>
	<li>$subject 可以是数组，也可以是字符串
<ol>
	<li>数组
对每一个数组数据进行匹配</li>
	<li>字符串
对字符串进行匹配</li>
</ol>
</li>
</ol>
preg_replace在返回匹配中会输出未发生匹配的字段
preg_filter 在返回匹配中不会输出未发生匹配的字段

preg_grep 函数
<pre>preg_grep($pattern, $subject);</pre>
preg_grep 只输出匹配的值，如果在数组中会保留索引
<pre>$pattern = '/[0-9]/';
$subject = array('hels','da13','24iuh','ihf13333');
var_dump(preg_grep($pattern, $subject));</pre>
<pre>array(3) {
  [1]=&gt;
  string(4) "da13"
  [2]=&gt;
  string(5) "24iuh"
  [3]=&gt;
  string(8) "ihf13333" 
}</pre>
<h2>preg_split函数</h2>
preg_split($pattern, $subject)以$pattern 作为分割模式，将$pattern进行分割
explode()函数是一个非正则表达式版本
<pre>$pattern = '/[0-9]/';
$subject = 'helsda1324iuhihf13333';
var_dump(preg_split($pattern, $subject)</pre>
<pre>array(10) {
  [0]=&gt;
  string(6) "helsda"
  [1]=&gt;
  string(0) ""
  [2]=&gt;
  string(0) ""
  [3]=&gt;
  string(0) ""
  [4]=&gt;
  string(6) "iuhihf"
  [5]=&gt;
  string(0) ""
  [6]=&gt;
  string(0) ""
  [7]=&gt;
  string(0) ""
  [8]=&gt;
  string(0) ""
  [9]=&gt;
  string(0) ""
}</pre>
<h2>preg_quote正则转义函数</h2>
preg_quote($str) 将字符串中的 正则符号进行转义

正则运算符
<pre>.\+*?[^](){}=!&lt;&gt;|:-$</pre>
<pre>$str= '~`!@#$%^&amp;*()_-+={}[]\|:;"\'/?.&gt;,&lt;';
echo $str."&lt;br/&gt;";
$str = preg_quote($str);
echo $str;</pre>
<pre>~`!@#$%^&amp;*()_-+={}[]\|:;"'/?.&gt;,&lt;
~`\!@#\$%\^&amp;\*\(\)_\-\+\=\{\}\[\]\\\|\:;"'/\?\.\&gt;,\&lt;</pre>

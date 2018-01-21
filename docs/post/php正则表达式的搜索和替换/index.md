<header class="entry-header">
<div class="entry-content">

1、str_replace(‘js’,’php’,$str) 替换字符串
2、$result = sprintf(‘%01.2f’,$str) 格式化
3、addslashes($str) 字符串的转义
<div id="studyMain">
<div class="wrap">
<div id="js-code-container" class="cmain-container">
<div id="js-aticle-container" class="cwrap-autoheight aticle-container">
<div id="J_PanelCode" class="code-panel">
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

正则表达式的搜索与替换在某些方面具有重要用途，比如调整目标字符串的格式，改变目标字符串中匹配字符串的顺序等。

例如我们可以简单的调整字符串的日期格式：
<pre class="code">$string = 'April 15, 2014';
$pattern = '/(\w+) (\d+), (\d+)/i';
$replacement = '$3, ${1} $2';
echo preg_replace($pattern, $replacement, $string); //结果为：2014, April 15</pre>
其中${1}与$1的写法是等效的，表示第一个匹配的字串，$2代表第二个匹配的。

通过复杂的模式，我们可以更加精确的替换目标字符串的内容。
<pre class="code">$patterns = array ('/(19|20)(\d{2})-(\d{1,2})-(\d{1,2})/',
                   '/^\s*{(\w+)}\s*=/');
$replace = array ('\3/\4/\1\2', '$\1 =');//\3等效于$3,\4等效于$4，依次类推
echo preg_replace($patterns, $replace, '{startDate} = 1999-5-27'); //结果为：$startDate = 5/27/1999
//详细解释下结果：(19|20)表示取19或者20中任意一个数字，(\d{2})表示两个数字，(\d{1,2})表示1个或2个数字，(\d{1,2})表示1个或2个数字。^\s*{(\w+)\s*=}表示以任意空格开头的，并且包含在{}中的字符，并且以任意空格结尾的，最后有个=号的。</pre>
用正则替换来去掉多余的空格与字符：
<pre class="code">$str = 'one     two';
$str = preg_replace('/\s+/', ' ', $str);
echo $str; // 结果改变为'one two'</pre>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</header>

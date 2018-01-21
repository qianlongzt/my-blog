<div class="entry-content">

php中有非常多的字符串处理函数，其中就有字符串截取函数。

1、英文字符串的截取函数substr()

函数说明：substr(字符串变量,开始截取的位置，截取个数）

例如：
<pre class="code">$str='i love you';
//截取love这几个字母
echo substr($str, 2, 4);//为什么开始位置是2呢，因为substr函数计算字符串位置是从0开始的，也就是0的位置是i,1的位置是空格，l的位置是2。从位置2开始取4个字符，就是love。</pre>
2、中文字符串的截取函数mb_substr()

函数说明：mb_substr(字符串变量,开始截取的位置，截取个数, 网页编码）

例如：
<pre class="code">$str='我爱你，中国';

//截取中国两个字

echo mb_substr($str, 4, 2, 'utf8');//为什么开始位置是4呢，和上一个例子一样，因为mb_substr函数计算汉字位置是从0开始的，也就是0的位置是我,1的位置是爱，4的位置是中。从位置4开始取2个汉字，就是中国。中文编码一般是utf8格式</pre>
php中有一个神奇的函数，可以直接获取字符串的长度，这个函数就是strlen()。
<pre class="code">$str = 'hello';
$len = strlen($str);
echo $len;//输出结果是5</pre>
strlen函数对于计算<u><strong>英文</strong></u>字符是非常的擅长，但是如果有<u><strong>中文汉字</strong></u>，可以使用<code class="marker">mb_strlen()</code>函数获取字符串中中文长度。

例子如下：
<pre class="code">$str = "我爱你";
echo mb_strlen($str,"UTF8");//结果：3，此处的UTF8表示中文编码是UTF8格式，中文一般采用UTF8编码</pre>
</div>

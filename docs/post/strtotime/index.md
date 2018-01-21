将格式化的日期字符串转换为Unix时间戳，格式化格林威治（GMT）标准时间
<div class="entry-content">

strtotime函数预期接受一个包含美国英语日期格式的字符串并尝试将其解析为 Unix 时间戳。

函数说明：strtotime(要解析的时间字符串, 计算返回值的时间戳【默认是当前的时间，可选】)
返回值：成功则返回时间戳，否则返回 FALSE

比如
<pre class="code">echo strtotime("now");//相当于将英文单词now直接等于现在的日期和时间，并把这个日期时间转化为unix时间戳。这个效果跟echo time();一样。
echo strtotime("+1 seconds");//相当于将现在的日期和时间加上了1秒，并把这个日期时间转化为unix时间戳。这个效果跟echo time()+1;一样。
echo strtotime("+1 day");//相当于将现在的日期和时间加上了1天。
echo strtotime("+1 week");//相当于将现在的日期和时间加上了1周。
echo strtotime("+1 week 3 days 7 hours 5 seconds");//相当于将现在的日期和时间加上了1周3天7小时5秒。
</pre>
gmdate 函数能格式化一个GMT的日期和时间，返回的是格林威治标准时（GMT）。
举个例子，我们现在所在的中国时区是东八区，领先格林威治时间8个小时，有时候也叫GMT+8，那么服务器运行以下脚本返回的时间应该是这样的：
当前时间假定是2014-05-01 15:15:22
<pre> echo date('Y-m-d H:i:s', time()); //输出为：2014-05-01 15:15:22
 echo gmdate('Y-m-d H:i:s', time()); //输出为：2014-05-01 07:15:22</pre>
因为格林威治时间是现在中国时区的时间减去8个小时，所以相对于现在时间要少8个小时

</div>

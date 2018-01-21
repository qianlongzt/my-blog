require_once('smarty/Smarty.class.php'); //引入smarty类
$smarty = new Smarty();//实例化 smarty类
$smarty -&gt; left_delimiter = "{"; //定义左定界符
$smarty -&gt; right_delimiter = "}";//定义右定界符
$smarty -&gt; template_dir = "tpl";//定义模板 目录
$smarty -&gt; compile_dir = "template_c";//定义编译完成的目录
$smarty -&gt; cache_dir = "cache";//定义缓存目录

$smarty -&gt; caching = true;//开启模板缓存，默认不缓存
$smarty -&gt; cache_lifetime = 120;//定义缓存时间

$smarty -&gt; assign($key,$value);// 在smarty变量池中加入变量名为key 值为value的变量
$smarty -&gt; display('test.html');//生成模板

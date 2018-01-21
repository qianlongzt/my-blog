+++
title= "json"
categories= ["code"]
tags= ["json"]
date= "2016-03-06 16:51:00"
+++

<div class="entry-content">

分清字符集与字符编码的区别 ，json是只能用于unicode字符编码，而不是字符集

$jsonStr={“key”:”value”,”key1″:”value1″};
默认json_decode返回为对象
$obj=json_decode($jsonStr);//返回为对象
$arr=json_decode($jsonStr,true);//返回为数组

JSON的值可以是下面这些类型：
<ul>
	<li>数字（整数或浮点数），比如123，12.3</li>
	<li>字符串（在双引号中）</li>
	<li>逻辑值（true 或 false）</li>
	<li>数组（在方括号中）</li>
	<li>对象（在花括号中）</li>
	<li>null</li>
</ul>
json在javascript中可以用eval和JSON.parse()进行解析 后者更安全只认识json，前者可以执行javascript脚本

JSON
<ol>
	<li>并列的数据之间用逗号;</li>
	<li>影射用冒号（": "）表示;</li>
	<li>并列数据的集合（数组）用方括号：</li>
	<li>影射的集合用大括号.</li>
</ol>
JSON的缺点
<ol>
	<li>要求字符集，必须是Unicode，受约束性强</li>
	<li>语法过于严谨，必须遵循JSON语法四个原则</li>
	<li>映射的集合（对象）用大括号（"{}"）表示</li>
</ol>
JSON的优点：
<ol>
	<li>数据格式比较简单，易于读写，格式多是压缩的，占用带宽小&lt;br&gt;</li>
	<li style="text-align: left;">支持多种语言，包括ActionScript，C，C#,ColdFusion,Java,JavaScript,Perl,PHP,Python,Ruby等服务器端语言，便于服务器端的解析</li>
</ol>
XML + JSON + Serialize + Array()
<ol>
	<li>XML 非常适合Web传输，提供统一的方法来描述和交换独立于应用程序或供应商的结构化数据。</li>
	<li>JSON</li>
	<li>Serialize是一种类似于JSON的数据格式，但是PHP的serialize是将变量序列化，返回一个具有变量类型和结构的字符串表达式。</li>
	<li>Array()基本数据类型，不能用于数据的传输和交替</li>
</ol>
<h2>json与serialize对比</h2>
<pre>$arr = array("username","age");
var_dump($arr);
var_dump(serialize($arr));</pre>
<pre id="line1">array(2) {
<span id="line2"></span>  [0]=&gt;
<span id="line3"></span>  string(8) "username"
<span id="line4"></span>  [1]=&gt;
<span id="line5"></span>  string(3) "age"
<span id="line6"></span>}
<span id="line7"></span>string(39) "a:2:{i:0;s:8:"username";i:1;s:3:"age";}"
<span id="line8"></span>string(18) "["username","age"]"</pre>
<pre>$arr = array("username"=&gt;"hello","age"=&gt;10);
var_dump($arr);
var_dump(serialize($arr));
var_dump(json_encode($arr));</pre>
<pre><span id="line9"></span>array(2) {
<span id="line10"></span>  ["username"]=&gt;
<span id="line11"></span>  string(5) "hello"
<span id="line12"></span>  ["age"]=&gt;
<span id="line13"></span>  int(10)
<span id="line14"></span>}
<span id="line15"></span>string(48) "a:2:{s:8:"username";s:5:"hello";s:3:"age";i:10;}"<span id="line16">
</span>string(29) "{"username":hello","age":10}"</pre>
<h2>对象json和serialize化</h2>
<pre>class muke{
    protected $name= "dsfs";
    public $bbb = "doisjf";
    private $aaa = "dsiafh";
    public function a(){

    }
}
$arr = new muke();
var_dump($arr);
var_dump(serialize($arr));
var_dump(json_encode($arr));</pre>
<pre id="line1">object(muke)#1 (3) {
<span id="line2"></span>  ["name":protected]=&gt;
<span id="line3"></span>  string(4) "dsfs"
<span id="line4"></span>  ["bbb"]=&gt;
<span id="line5"></span>  string(6) "doisjf"
<span id="line6"></span>  ["aaa":"muke":private]=&gt;
<span id="line7"></span>  string(6) "dsiafh"
<span id="line8"></span>}
<span id="line9"></span>string(92) "O:4:"muke":3:{s:7:"*name";s:4:"dsfs";s:3:"bbb";s:6:"doisjf";s:9:"mukeaaa";s:6:"dsiafh";}"
string(16) "{"bbb":"doisjf"}"</pre>
<h2>json字符串转回到数组或对象</h2>
<pre>$str = '{"bbb":"doisjf"}';
var_dump(json_decode($str,true));
var_dump(json_decode($str,false));

</pre>
<pre id="line1">array(1) {
<span id="line2"></span>  ["bbb"]=&gt;
<span id="line3"></span>  string(6) "doisjf"
<span id="line4"></span>}
<span id="line5"></span>object(stdClass)#1 (1) {
<span id="line6"></span>  ["bbb"]=&gt;
<span id="line7"></span>  string(6) "doisjf"
<span id="line8"></span>}
<span id="line9"></span></pre>
</div>

+++
title= "php爬46级成绩"
categories= ["code"]
tags= ["curl","cet"]
date= "2016-03-18 19:51:00"
+++

```php
<?php
$data = "id=33037015210xxxx&name="
.urlencode(mb_convert_encoding("xx","GBK","UTF-8"));

$curl = curl_init("http://cet.99sushe.com/getscore");
curl_setopt($curl,CURLOPT_RETURNTRANSFER,1);
curl_setopt($curl,CURLOPT_POST,1);
curl_setopt($curl,CURLOPT_POSTFIELDS, $data);
curl_setopt($curl,CURLOPT_HTTPHEADER,array(
        "Content-Type:application/x-www-form-urlencoded;charset=utf-8",
        "Content-Length:".strlen($data),
        "Host: cet.99sushe.com",
        "Referer: http://cet.99sushe.com",
        "Connection: keep-alive"
));
$output = curl_exec($curl);
$result =  mb_convert_encoding($output, "UTF-8", "GBK");
$arr = explode(",",$result) ;
if((int)$arr[0] == 6){
    echo "英语四级";
} else if((int)$arr[0] == 6) {
    echo "英语六级";
}
echo "<br />";
echo "总分：".$arr[4]."<br />";
echo "听力：".$arr[1]."<br />";
echo "阅读：".$arr[2]."<br />";
echo "写作和翻译：".$arr[3]."<br />";
echo "学校：".$arr[5]."<br />";
echo "姓名：".$arr[6]."<br />";
```
```
英语四级
总分：xxx
听力：xxx
阅读：xxx
写作和翻译：xxx
学校：xxx
姓名：xx
```

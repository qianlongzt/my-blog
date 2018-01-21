+++
title= "php文件上传"
categories= ["code"]
tags= ["文件上传"]
date= "2016-03-24 12:05:00"
+++

来源[慕课网](http://www.imooc.com/learn/219)

文件上传原理
-----

将客户端的文件上传到服务器端，在将服务器端的临时文件移动到指定目录即可
<!--more-->

###php 配置###

1. file_uploads = On 支持HTTP上传
2. upload_tmp_dir = 临时文件保存的目录
3. upload_max_filesize = 2M 允许上传文件的最大值
4. max_file_uploads = 20 允许一次上传的最大文件数
5. post_max_size = 8M POST方式发送数据的最大值
6. max_execution_time = 1 设置了脚本被解析器终止之前允许的最大执行时间，单位为秒，防止程序写的不好而占尽服务器资源
7. max_input_time = 60 脚本解析输入数据允许的最大时间，单位为秒
8. max_input_nesting_level = 64 设置输入变量的嵌套深度
9. max_input_vars = 1000 接受多少输入的变量
10. memory_limit = 128M 最大单线程的独立内存使用量

文件要用post方式提交和 `enctype="multipart/form-data"`

```
class="brush:other">enctype="multipart/form-data"
```

$_FILES 根据前段的写法有不同的表示

```html
<input type="file" name="myFile[]" />
<input type="file" name="myFile[]" />
<input type="file" name="myFile[]" />
<input type="file" name="myFile[]" />
```
和
```html
input type="file" name="myFile[]" multiple="multiple" /&gt;&lt;br /&gt;
```
在后端中$_FILES是一样的,通过print_r($_FILES)
```other
Array
(
    [myFile] => Array
        (
            [name] => Array
                (
                    [0] => 1.pdf
                    [1] => 2.pdf
                    [2] => 3.pdf
                    [3] => 4.pdf
                )

            [type] => Array
                (
                    [0] => application/pdf
                    [1] => application/pdf
                    [2] => application/pdf
                    [3] => application/pdf
                )

            [tmp_name] => Array
                (
                    [0] => Z:\TEMP\phpF519.tmp
                    [1] => Z:\TEMP\phpF529.tmp
                    [2] => Z:\TEMP\phpF53A.tmp
                    [3] => Z:\TEMP\phpF55A.tmp
                )

            [error] => Array
                (
                    [0] => 0
                    [1] => 0
                    [2] => 0
                    [3] => 0
                )

            [size] => Array
                (
                    [0] => 2297318
                    [1] => 2365302
                    [2] => 6194922
                    [3] => 10342758
                )

        )

)
````
如果是在html中加了multiple属性但是没有对名字写[] ,如
```html
<input type="file" name="myFile1" multiple="multiple" />
```
输出的是最后一个文件
```other
Array
(
    [myFile1] => Array
        (
            [name] =>4.pdf
            [type] => application/pdf
            [tmp_name] => Z:\TEMP\phpA778.tmp
            [error]=> 0
            [size] => 10342758
        )

)
```
$_FILES变量中包含客户端文件的名字name，文件类型type（mime），服务器上这个文件的临时名字tmp_name（全路径），错误代码error，文件大小size(单位字节)

对于用数组上传的文件，结构是
```other
[input中的name，不含"[]"] => Array
        (
            [name] => Array
                (
                    [0] => name1 //第一个文件名
                    [1] => name2 //第二个文件名
                    [N] => nameN  //第N个文件名
                )

            [type] => Array
                (
                    [0] => type1//第一个文件类型
                    [1] => type2 //第二个文件类型
                    [N] => typeN  //第N个文件类型
                )

            [tmp_name] => Array
                (
                    [0] =>; tmp_name1 //第一个文件在服务器的缓存文件名
                    [1] => tmp_name2 //第二个文件在服务器的缓存文件名
                    [N] => tmp_nameN  //第N个文件在服务器的缓存文件名
                )

            [error] => Array
                (
                    [0] => error1 //第一个文件上传过程的错误码
                    [1] => error2 //第二个文件上传过程的错误码
                    [N] => errorN  //第N个文件上传过程的错误码
                )

            [size] => Array
                (
                    [0] => size1 //第一个文件大小
                    [1] => size2 //第二个文件大小
                    [2] => size3 //第三个文件大小
                    [N] => sizeN  //第N个文件大小
                )

        )
```
对于单个文件上传
````other
[myFile1] => Array
        (
            [name] => 文件名
            [type] =>  文件类型
            [tmp_name] => 文件的临时存放位置
            [error] => 文件的错误码
            [size] => 文件的大小
        )
```
###将数组上传的文件和普通上传的文件转成数组###
```php
private function sortFile()
    {
        foreach ($_FILES as $file) {
            $i = 0;
            if (is_array($file['name'])) {
                foreach ($file['name'] as $key => $value) {
                    $this -> files[$i]['name'] = $file['name'][$i];
                    $this -> files[$i]['tmp_name'] = $file['tmp_name'][$i];
                    $this -> files[$i]['size'] = $file['size'][$i];
                    $this -> files[$i]['type'] = $file['type'][$i];
                    $this -> files[$i]['error'] = $file['error'][$i];
                    $i++;
                }
            } elseif (is_string($file['name'])) {
                $this -> files[$i]['name'] = $file['name'];
                $this -> files[$i]['tmp_name'] = $file['tmp_name'];
                $this -> files[$i]['size'] = $file['size'];
                $this -> files[$i]['type'] = $file['type'];
                $this -> files[$i]['error'] = $file['error'];
            }
            $i++;
        }
    }
```

###文件的错误码###
1. UPLOAD_ERR_OK
其值为 0，没有错误发生，文件上传成功。
2. UPLOAD_ERR_INI_SIZE
其值为 1，上传的文件超过了 php.ini 中 upload_max_filesize 选项限制的值。
3. UPLOAD_ERR_FORM_SIZE
其值为 2，上传文件的大小超过了 HTML 表单中 MAX_FILE_SIZE 选项指定的值。
4. UPLOAD_ERR_PARTIAL
其值为 3，文件只有部分被上传。
5. UPLOAD_ERR_NO_FILE
其值为 4，没有文件被上传。
6. UPLOAD_ERR_NO_TMP_DIR
其值为 6，找不到临时文件夹。PHP 4.3.10 和 PHP 5.0.3 引进。
7. UPLOAD_ERR_CANT_WRITE
其值为 7，文件写入失败。PHP 5.1.0 引进。
8. UPLOAD_ERR_EXTENSION
其值为8，上传的文件被PHP扩展程序中断

然后通过move_uploaded_file() 或者copy 来进行复制
```php
move_uploaded_file($tmp_name,"uploads/".$filename);
//移动成功返回true，失败返回false ，会判断文件是不是上传到服务器的
copy($tmp_name,"uploads/".$filename);
//移动成功返回true，失败返回false ，不会判断文件是不是上传服务器的，有风险
```
###可以在客户端进行一些限制，不过对懂程序的等于没有限制###
```html
<input  type="file" name="file" accpet="image/jpeg,image/gif,image/png" ><!--限制文件类型-->
<input type="hidden" name="MAX_FILE_SIZE" value="字节数" /> <!----限制文件大小-->
```
###通过浏览器下载文件###
```php
<?php
$filename = "upload/".$_GET['filename'];
header("content-disposition:attachment;filename=".basename($filename));
header("content-length:",filesize($filename));
readfile($filename);
```

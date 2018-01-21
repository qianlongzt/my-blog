+++
title= "php，数据库的操作"
categories= ["code"]
tags= ["php","数据库"]
date= "2016-03-06 16:53:36"
+++

<div class="entry-content">

PHP中一个数据库可能有一个或者多个扩展，其中既有官方的，也有第三方提供的。像Mysql常用的扩展有原生的mysql库，也可以使用增强版的mysqli扩展，还可以使用PDO进行连接与操作。

不同的扩展提供基本相近的操作方法，不同的是可能具备一些新特性，以及操作性能可能会有所不同。

mysql扩展进行数据库连接的方法：
<pre class="code">$link = mysql_connect('mysql_host', 'mysql_user', 'mysql_password');</pre>
mysqli扩展：
<pre class="code">$link = mysqli_connect('mysql_host', 'mysql_user', 'mysql_password');</pre>
PDO扩展
<pre class="code">$dsn = 'mysql:dbname=testdb;host=127.0.0.1';
$user = 'dbuser';
$password = 'dbpass';
$dbh = new PDO($dsn, $user, $password);</pre>
</div>
<footer class="entry-footer"><span class="posted-on"><span class="screen-reader-text">发布于 </span></span></footer>

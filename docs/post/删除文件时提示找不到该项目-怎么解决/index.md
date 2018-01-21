来自[百度经验](http://jingyan.baidu.com/article/e4d08ffdf5ab470fd2f60df4.html) 和[百度知道](http://zhidao.baidu.com/link?url=ha5Y3ol5QJjW0pDaLhQAkz6B8-CT51dpPSeSi5tcPpQYkQ9ZYS6wW7vldj75AjJ2FOdSLgEUWYcadnml483T-K)和[百度文库](http://wenku.baidu.com/link?url=Mm0cdarzTXUqEvA62zEw4b2eTkvfdd-BbqO9Geb3I9Ukp7W7_AH0WcWl7t6H9EW4n8xwdWqgprbcRGIes9cojpfAdedrWr4zFykn05BjbAe)

**故障现象**在使用Windows系统删除文件或者文件夹的时候，有时会出现“找不到该项目”的错误提示，可能再次“重试”也无济于事。

故障原因
------

磁盘文件索引出现问题，造成已删除的文件夹还存在，但再次删除却出现该问题。

1. 使用下载工具创建的文件夹，在未下载完成前自行删除了该文件。
2. 存在守护进程所致。
3. 系统中木马，或者被恶意隐藏。
4. 文件或文件夹名称不符合Windows命名规范，含有特殊字符等。比如，防删除的Ghost文件夹，添加了特殊的字符。
<!--more-->

![](http://c.hiphotos.baidu.com/exp/w=500/sign=d4bc32603d6d55fbc5c676265d234f40/d439b6003af33a871b7b5ea4c65c10385343b57e.jpg "删除文件时提示“找不到该项目”")

##步骤/方法##

1.  针对原因1的解决方法：进行磁盘碎片整理以修复分区。
2. 针对原因2的解决方法：待下载完成之后重试，或者退出下载软件之后重试。
3. 针对原因3的解决方法：尝试使用专业文件解锁软件，进行解锁后再进行尝试删除。
4. 针对原因4的解决方法：安装并更新杀毒软件进行全面扫描，如果无法查杀，可重装系统。
5. 针对原因5的解决方法：可以采用批量处理文件的方法进行删除操作。

##批量处理文件的方法：

把以下代码复制粘贴到一新建的txt记事本文档中，并另存为del.bat文件（或者你喜欢的名字），注意扩展名为批处理文件bat；
```
DEL /F /A /Q \\?\%1
RD /S /Q \\?\%1
```

del 删除命令。
/F 强制删除只读文件。
/S 从所有子目录删除指定文件。
/Q 安静模式。删除全局通配符时，不要求确认。
%systemdrive% 系统文件夹，如C:\windows，有的朋友将系统装在D中，则表示D:\WINDOWS
*.tmp 指临时文件的通配符

全句意思是：强制删除系统文件夹下所有的格式为tmp的文件(哪怕文件是只读的)，并且在删除时不用向用户询问是否继续或终止!

```
RD [/S] [/Q] [驱动器:]路径
```
/S 除目录本身外，还将删除指定目录下的所有子目录和
文件。用于删除目录树。

/Q 安静模式，加 /S 时，删除目录树结构不再要求确认

把你想要删除的文件或者文件夹拖到该批处理文件图标上，即可批量删除文件。

![](http://d.hiphotos.baidu.com/exp/w=500/sign=8e2d2aba970a304e5222a0fae1c9a7c3/b7fd5266d0160924d82afca5d40735fae6cd3404.jpg "删除文件时提示“找不到该项目”，怎么解决?") />

最后。。。恩，做个WARNING或者CAUTION吧，呵呵。。。 就是。。谨慎使用
（这里要感谢purplelichen和版主HAT @ www.cn-dos.net forum 提供的例子）
在文件名包含某些特殊字符时有误删除的潜在危险！ 设h:是一个u盘，下面有一个fdel.bat:
```
DEL /F /A /Q \\?\%1
RD /S /Q \\?\%1
```
同时h:下还有一个名为 &amp;1.txt  的文本文件，此时 你想用 fdel.bat 删除 &1.txt，当你把 &1.txt 拖到
fdel.bat 上后，h:下的所有的文件和文件夹将全部不复存在。。。
这正是特殊字符"&"(另："^&"也有类似效果)的作用了（执行的时候变成了`rd /s /q \\?\"h:\&1.txt"`，&的前后会并列，于是`h:\` 被清空，然后才是定位`1.txt`以便删除。。。
于是综上：该bat很强大很简洁，但是一定不要用于删除文件名中（尤其是文件名首字符为&或^&）的文件或文件夹，否则可能造成误删除。

附：
相对安全的代码，具体就不详解了，主要是加入了文件名的判定：（ZJHJ @ www.cn-dos.net forum 提供，有修改，感谢\~\~）
以下没有验证过，使用也请谨慎。。。。
```
@echo off
if not "%~n1"=="" if not exist "%~f1" goto CHK
if not "%~n1"=="" if exist "%~f1" goto CHK
color 7c
cls
@echo
@echo 顽固文件垃圾桶
@echo
@echo 可删除任意顽固文件或目录，将目标文件或目录拖放到本bat图标上即可.
@echo
@echo 为了用户文件安全，已对带有"&"、"^&"组合字符文件名的危险删除进行阻止
@echo
@echo 原作者QQ: 251485609
@pause >nul 2>nul
echo on
goto eof

:CHK
set rt="%~n1"
if "%rt:~1,1%"=="&" goto FINE
if "%rt:~1,2%"=="^&" goto FINE
del /f /a /q \\?\%1 >nul 2>nul
rd /s /q \\?\%1 >nul 2>nul
echo on
goto eof

:FINE
@echo
@echo 为了安全，不支持此类危险删除！
echo on
pause >nul 2>nul
```

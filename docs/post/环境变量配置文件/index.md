source 配置文件 重新加载这个配置文件
. 这个点是source的缩写 source 配置文件 = . 配置文件
<ul>
	<li>放在/etc下的配置文件是对所有用户生效的，放环境变量文件：</li>
	<li>修改配置文件后，必须注销重新登陆才会生效</li>
	<li>使用source 配置文件</li>
	<li>或者 . 配置文件</li>
	<li>.和source等效</li>
</ul>
环境变量配置文件中主要是定义对系统操作环境生效的系统默认环境变量，如PATH等。
/etc/profile
/etc/profile.d/*.sh
~/.bash_profile
~/.bashrc
/etc/bashrc
<ul>
	<li>在用户家目录的是只对该用/户生效</li>
	<li>etc下的文件对所有用户生效：</li>
</ul>
正常登录
<div class="pic-viewer-wrap">
<div class="pic-viewer-inner J-viewer-inner"></div>
<div class="pic-viewer-inner J-viewer-inner">
<div class="pic-viewer-wrap">
<div class="pic-viewer-inner J-viewer-inner"><img src="http://img.mukewang.com/5695fd760001caef12800720.jpg" alt="" /></div>
<div class="pic-viewer-inner J-viewer-inner"></div>
非正常登录（su）
<div class="pic-viewer-inner J-viewer-inner">
<div class="pic-viewer-wrap">
<div class="pic-viewer-inner J-viewer-inner"><img src="http://img.mukewang.com/5695fd5d0001f48112800720.jpg" alt="" /></div>
</div>
注销时 生效的环境变量配置文件
<ul>
	<li class="pic-viewer-inner J-viewer-inner">~/.bash_logout</li>
</ul>
&nbsp;

bash的命令历史

</div>
<div class="pic-viewer-inner J-viewer-inner">
<ul>
	<li>~/.bash_history</li>
</ul>
<div class="pic-viewer-inner J-viewer-inner">登陆 的显示信息</div>
<ul>
	<li class="pic-viewer-inner J-viewer-inner">/etc/issue</li>
	<li class="pic-viewer-inner J-viewer-inner">\d 显示当前系统日期
\s 显示操作系统名称
\l 显示登陆的终端号，这个比较常用
\m 显示硬件系统结构，如i386，i686等
\n 显示主机名
\o 显示域名
\r 显示内核版本
\t 显示当前系统时间
\u 显示当前登陆用户的序列号</li>
</ul>
远程登陆欢迎信息：
<ul>
	<li>/etc/issue.net （默认是不启用的，不支持转义符）
在/etc/ssh/sshd_config决定，加入"Banner /etc/issue.net"行才能生效</li>
</ul>
登陆之后欢迎信息：/etc/motd
issue是登陆之前生效的，motd是登陆之后生效的，建议写在motd中

</div>
</div>
</div>
</div>

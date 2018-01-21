+++
title= "Linux软件安装管理"
categories= ["电脑"]
tags= ["liunx","yum","rpm"]
date= "2016-03-06 16:25:31"
+++

来源： <em><a href="http://www.imooc.com/note/447?sort=last">Linux软件安装管理_学习笔记_慕课网</a></em>

源码包：
<ul>
	<li>开源，可以修改源代码的。软件是编译安装，所以更加适合自己的系统，更加稳定且效率更高。卸载方便。安装过程步骤较多，编译过程时间较长，因为是编译安装，安装过程中一旦报错新手很难解决。</li>
</ul>
二进制包（RPM包）
<ul>
	<li>安装简单、快捷。但不能看到源码、不灵活、有依赖性</li>
</ul>
脚本安装包：
<ul>
	<li>将安装命令写成脚本，直接执行脚本</li>
</ul>
rpm安装：
<ul>
	<li>rpm包命名规则
<ul>
	<li>软件包名-软件版本-软件发布的次数-适合的Linux平台-适合的硬件平台-包扩展名</li>
</ul>
</li>
	<li>1. rpm安装过程中会出现的三种依赖：
<ol>
	<li>树状依赖：A&gt;B&gt;C ：我们可以先装C到B到A 。</li>
	<li>环状依赖：A&gt;B&gt;C&gt;A ：我们可以一条命令同时装A,B,C，其中的依赖由安装程序内部自己解决。</li>
	<li>模块依赖：指库依赖,就是依赖某个/些函数，此时必须得通过http://www.rpmfind.net/搜索出其他rpm包内部包含了这个/些函 数，然后先装这个rpm包。</li>
</ol>
</li>
	<li>2. 我们知道，rpm安装软件的依赖问题往往需要耗费大量寻找依赖包的时间，如何解决这个问题？这就是yum要做的，通过搭建服务器，把某个rpm软件包所需要的所有依赖的rpm都集中一起，然后合理安装。</li>
	<li>rpm 安装命令 rpm -ivh 包全名
<ul>
	<li>-i(install) 安装</li>
	<li>-v（verbose）显示详细信息</li>
	<li>-h (hash) 显示进度</li>
	<li>--nodeps 不检测依赖性</li>
</ul>
</li>
	<li>rpm 升级命令 rpm -Uvh 包全名
<ul>
	<li>-U(upgrade) 升级</li>
	<li>-v（verbose）显示详细信息</li>
	<li>-h (hash) 显示进度</li>
	<li>--nodeps 不检测依赖性</li>
</ul>
</li>
	<li>rpm 卸载命令 rpm -e 包名
<ul>
	<li>rpm准备了这个卸载命令的原因是，我们安装时根本不知道这个包装了在哪里（要知道linux下的安装的软件的文件散布多个地方的，很难一一找），而rpm知道，所以干脆就为我们准备了这条便利的命令。</li>
</ul>
</li>
	<li>rpm 查询命令
<ul>
	<li>rpm -qi 包名：可以查看已经安装的包的信息</li>
	<li>rpm -qip 包全名：可以查看未安装的包的信息</li>
	<li>rpm -ql 包名 ： 查看已经安装的包中包含的文件(带路径)</li>
	<li>rpm -qlp 包全名 ： 查看未安装的包中包含的文件(带路径)</li>
	<li>当面对一个文件时，我们如果想知道其属于哪个软件的，就可以如下：</li>
	<li>rpm -qf 文件名(路径)</li>
	<li>rpm -qR 可以安装前查看包依赖的信息，不过太过细，所以眼花缭乱，不常用。因此我们还是直接安装包，等报依赖时在细细查找。</li>
</ul>
</li>
	<li>rpm 校验 rpm -V 包名
<ul>
	<li>S 文件大小是否改变</li>
	<li>M 文件的类型或者文件的权限是否被改变</li>
	<li>5 文件MD5校验和是否改变（可以理解成文件内容是否改变）</li>
	<li>D 设备的主从代码是否改变</li>
	<li>L 文件的路径是否改变</li>
	<li>U 文件的所有者是否改变</li>
	<li>G 文件的属组是否改变</li>
	<li>T 文件的修改时间是否改变</li>
	<li>c  配置文件（config file）</li>
	<li>d 普通文档（documentation）</li>
	<li>g “鬼”文件（ghost file），很少见，就是该文件不应该被这个rpm包包含</li>
	<li>L 授权文件（license file）</li>
	<li>r 描述文件（read me）</li>
</ul>
</li>
	<li>rpm2cpio 包全名 | cpio -idv .文件绝对路径
<ul>
	<li>前面的【.】代表当前路径，不能省略。</li>
	<li>【文件绝对路径】和包里文件的绝对路径对应，也就是告诉了cpio要去包里提取哪个文件。
注：cpio只知道提取文件，并不知道要从什么地方提取文件，因此我们通常要使用【|】管道符或【&lt;】输入重定向告诉cpio我们应该从什么设备去取出文件。
使用输入重定向的cpio命令格式：
cpio 选项 &lt; [文件|设备]
选项：
<ul>
	<li>-i：copy-in模式，还原</li>
	<li>-d：还原时自动新建目录</li>
	<li>-v：显示还原过程</li>
</ul>
</li>
	<li>比如  rpm2cpio /mnt/cdrom/Packages/coreutils-8.22-15.el7.x86_64.rpm | cpio -idv ./usr/bin/ls  从安装包中提取ls命令 到 当前目录下的 ./bin/ls 中</li>
</ul>
</li>
</ul>
yum 在线安装
<ul>
	<li>1、yum的优点：将所有软件包放到官方服务器上，当进行yum在线安装时，可以自动解决依赖性问题。（rpm缺点：安装过程中，rpm包依赖性太强）</li>
	<li>2、redhat的yum在线安装需要付费，centOS不需要。</li>
	<li>3、在【/etc/yum.repos.d/】目录中，默认有4个yum源文件，其中【CentOS-Base.repo】是基本yum源文件，如果我们能上网，那它是默认生效的，而其他的都是默认不生效的。</li>
	<li>4、[base]：名字可以随便起。</li>
	<li>5、name：名字也是随便起。</li>
	<li>6、mirrorlist和baseurl一个是主站点，一个是辅助站点，这两个有一个就行。可以找一个163或清华大学的yum源更换。</li>
	<li>7、enabled：默认生效。</li>
	<li>8、gpgcheck：一般都要开启，开启后安装时会验证rpm包是否是官方的，以保证系统安全。</li>
	<li>9、gpgkey：默认系统安装后，在目录【/etc/pki/rpm-gpg】下都会存在数字证书。注：前面的【file://】表示文件协议，后面的【/etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6】是数字证书的位置。</li>
</ul>
光盘yum源
<ul>
	<li>linux中的注释，往往是#，要注意：需要顶格！！！！</li>
	<li>yum程序在读取yum源文件时，是通过后缀名来识别的，因此如果我们不想yum程序读取某一个源文件，可以修改其后缀。</li>
	<li>搭建本地yum源时，要注意的是yum源文件中的url地址应该是iso文件的挂载地址，而不用到Packages目录中，这是约定的，否则一些配置文件yum无法找到。</li>
</ul>
yum 命令
<ul>
	<li>yum list 查看所有可用软件包列表</li>
	<li>yum search 关键字  查看与关键字相关的包</li>
	<li>yum -y install 包名 安装这个包 且 自动回答yes</li>
	<li>yum -y remove 报名 卸载这个包 且 自动回答yes</li>
	<li>yum grouplist 列出所有可用的软件组列表</li>
	<li>yum groupinstall 软件祖名 安装指定软件组，组名可以由grouplist查询出来</li>
	<li>yum groupremove 软件组名 卸载指定组名</li>
</ul>
源码包安装
<ul>
	<li>下面以安装apache2为例，解压缩后的目录为【httpd-2.2.31】
<ul>
	<li>安装时必须进入到解压缩后的目录【httpd-2.2.31】中</li>
	<li>./configure --prefix=/usr/local/apache2 该命令用于软件配置与检查（基本上每个源码包都会有该命令，即使个别的没有该命令，也会提供相关替代命令），它有以下几点功能
<ol>
	<li>定义需要的功能选项；</li>
	<li>检测系统环境是否符合安装要求；</li>
	<li>把a中定义好的功能选项和b中检测系统环境的信息都写入Makefile文件，用于后续的编辑。（后续的【make】和【make install】命令都会依赖该文件）</li>
	<li>执行命令【./configure --prefix=/usr/local/apache2】，该命令用于指定安装位置为：【/usr/local/apache2】（其中的 【apache2】目录不需要提前创建，【make install】命令执行时会自动创建）。</li>
	<li>命令执行后，会在当前目录生成Makefile文件。</li>
	<li>执行【make】命令，编译源码（这一步通常比较耗时）；</li>
	<li>执行【make install】命令，安装程序，此时会创建【/usr/local/apache2】目录
<ol>
	<li>如果命令执行过程中发生终止，并且出现error、warn或no提示，则表明出错，否则，一切正常。</li>
	<li>若执行【./configure】或【make】命令时出现错误，是不需要删除【/usr/local/apache2】目录的，因为程序还没有真正安 装。只需要执行【make clean】命令即可，该命令用于清除缓存、临时文件等，使安装环境恢复到未安装状态。</li>
	<li>若执行【make install】命令时报错，则需要删除【/usr/local/apache2】目录，并且执行【make clean】命令才行。</li>
</ol>
</li>
</ol>
</li>
</ul>
</li>
</ul>
脚本安装包
<ul>
	<li>下载好脚本后直接执行</li>
</ul>

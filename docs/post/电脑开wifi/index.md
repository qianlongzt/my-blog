来自 <a href="http://www.22zy.net/tech/2365.html">http://www.22zy.net/tech/2365.html</a>
<pre class="brush:other">netsh wlan set hostednetwork mode=allow ssid=Edwin key=1234asdf</pre>
ssid为wifi热点名称，key为wifi热点密码（要大于8位） mode表明是否启用虚拟WiFi网卡，allow为启用，disallow为禁用，以后要关掉的话就将命令中的“allow”改为“disallow” 了netsh wlan set hostednetwork mode=disallow），这个要记住了，要不然不知道怎么关闭。
ssid是建立好的无线网的名称，最好用英文，以后手机就连接这个名字的wifi就可以了；
key是无线网的密码，必须要八个以上字符，区分大小写。

然后在
<pre class="brush:other">控制面板\网络和 Internet\网络连接</pre>
<strong>如果看到一个名字为Microsoft Virtual Wifi Miniport Adapter，表示虚拟wifi网卡建立成功，如果没有，可能是你的无线网卡不支持这个功能。</strong>

<img src="http://img.22zy.net/uploads/allimg/c150215/1423bF63c4P-55037.jpg-w600" alt="cmd命令开启电脑WiFi热点的方法_wifi热点,电脑WiFi热点,电脑WiFi" />

<strong>将网络共享到虚拟WiFi</strong>

1）在“网络连接”窗口中，右键点击已连接到Internet的无线网络连接，依次点击“属性”、“共享”，勾选“允许其他网络连接（N）”，并选择你所刚才创建的wifi网络

<img src="http://img.22zy.net/uploads/allimg/c150215/1423bF6433V0-AI7.jpg-w600" alt="cmd命令开启电脑WiFi热点的方法_wifi热点,电脑WiFi热点,电脑WiFi" />

<img src="http://img.22zy.net/uploads/allimg/c150215/1423bF64L040-ON6.jpg-w600" alt="cmd命令开启电脑WiFi热点的方法_wifi热点,电脑WiFi热点,电脑WiFi" />

2）点击确定之后，提供共享的网卡图标旁会出现“共享的”字样表示已共享网络

<strong>6、打开虚拟网络</strong>

1）在命令提示符中继续运行下面的代码：
<pre class="brush:other">netsh wlan start hostednetwork</pre>
打开虚拟wifi网络,如图所示已打开刚才建立的

参数说明：start表示开启，stop表示关闭

<img src="http://img.22zy.net/uploads/allimg/c150215/1423bFA13540-XV3.jpg-w600" alt="cmd命令开启电脑WiFi热点的方法_wifi热点,电脑WiFi热点,电脑WiFi" />

2）为了方便，可以分别把start/stop命令分别写到一个txt文件中，把后缀名txt改成bat,用管理员身份执行就可以方便的开/关wifi网络

start.bat:
<pre class="brush:other">netsh wlan start hostednetwork</pre>
stop.bat:
<pre class="brush:other">netsh wlan stop hostednetwork</pre>
<strong>7、成功开启电脑WiFi热点，手机可以通过搜索该热点连接WiFi上网了。</strong>

如果不能连接，查看是不是开启了dhcp服务，没有开启就要在手机上手动输入ip

<img src="http://img.22zy.net/uploads/allimg/c150215/1423bFA51040-a405.jpg-w600" alt="cmd命令开启电脑WiFi热点的方法_wifi热点,电脑WiFi热点,电脑WiFi" />

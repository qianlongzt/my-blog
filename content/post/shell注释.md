+++
title= "Shell注释"
categories= ["电脑","code"]
tags= ["注释"]
date= "2016-03-08 00:24:39"
+++

来自<a href="http://www.imooc.com/wiki/detail/id/783">http://www.imooc.com/wiki/detail/id/783</a>

以“#”开头的行就是注释，会被解释器忽略。

sh里没有多行注释，只能每一行加一个#号。只能像这样：

shell第一行写明用什么解释器
<pre class="shell sh_sh snippet-formatted sh_sourceCode">#--------------------------------------------
# 这是一个自动打ipa的脚本，基于webfrogs的ipa-build书写：
# https://github.com/webfrogs/xcode_shell/blob/master/ipa-build
# 功能：自动为etao ios app打包，产出物为14个渠道的ipa包
# 特色：全自动打包，不需要输入任何参数
#--------------------------------------------####
# 用户配置区 开始 #######
# 项目根目录，推荐将此脚本放在项目的根目录，这里就不用改了
# 应用名，确保和Xcode里Product下的target_name.app名字一致#####
# 用户配置区 结束  #####</pre>
如果在开发过程中，遇到大段的代码需要临时注释起来，过一会儿又取消注释，怎么办呢？每一行加个#符号太费力了，可以把这一段要注释的代码用一对花括号括起来，定义成一个函数，没有地方调用这个函数，这块代码就不会执行，达到了和注释一样的效果。
<div class="refer">
<ul class="clearfix">
	<li>贡献者：</li>
	<li>穿山Jack</li>
</ul>
</div>

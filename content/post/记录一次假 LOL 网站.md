+++
title= "记录一次假 LOL 网站"
categories= ["电脑","code"]
tags= ["qq","qq内置浏览器"]
date= "2017-05-26 21:26:00"
+++

我首先看到，英雄联盟每日签到！免费皮肤等你来拿！http://url.cn/49c78Ep?kdegnqrtZJ&_xc=1

然后这个链接会经过 12次 302 跳转到 http://www.zx1718.com.cn/

然后这个网站会判断 UA，如果是手机QQ内置浏览器，会显示假网站，否则会跳转到真网站（http://lol.qq.com）

进去会显示抽奖，第三次会中。然后跳转到 http://www.zx1718.com.cn/Logo.pdf 要求登录QQ。

这个代码经过rc4加密，然后base64编码。解码后是这样子（http://paste.ubuntu.com/24666416/）

登录的时候会判断qq号长度等。具体判断没有仔细看。

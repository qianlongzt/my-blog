+++
title= "[转]多个 SSH KEY 的管理"
categories= ["电脑"]
tags= ["git"]
date= "2017-02-01 01:59:00"
+++

前言：多ssh-key模式 是开发时可能遇到的问题，新手在使用多 ssh key 模式时很容易不知所措。

>情景：工作室有一台公用电脑，使用它的开发人员混杂，使用时如何做到不同用户互不影响？如何实现多个ssh-key？如何实现多个ssh-key的配置？如何保证使用正确的私钥验证提交？

github提交验证机制

我们在个人的电脑上使用如下命令可生成ssh key

`$ ssh-keygen -t rsa -C "youremail@email.com"`
这时会在用户根目录下生成一个.ssh文件夹，一个私钥：id_rsa，一个公钥：id_rsa_pub，该公钥和私钥包含了你邮箱的信息，具有随机不可复现性！

ssh公钥私钥同时生成且唯一配对。公钥用于远程主机，私钥存储在本地工作机，私钥用于在push（即write操作）时验证身份。因为公钥与私钥的唯一对应性，只有能和公钥配对的私钥才能对远程主机进行写操作！

我们在使用github时会发现有两个地方牵涉到公钥添加，一个是账号设置下的ssh setting，另一个是单个仓库设置的Deploy key。添加至前者则代表 私钥主机可对当前远程主机的所有仓库进行写操作，添加至后者则代表 私钥主机只能对当前仓库进行写操作。

每次连接时SSH客户端发送本地私钥（默认~/.ssh/id_rsa）到远程主机进行公私钥配对验证！

同一工作主机，多个ssh key


对于公共电脑，多人使用，解决方案需要做到以下几点：

多个用户ssh key共存，不覆盖
互不影响
push时智能地对应的私钥

解决方案：

`ssh-keygen -t rsa -C "youremail@email.com" -f ~/.ssh/second `
生成新的ssh key并命名为second

或者`ssh-keygen -t rsa -C "youremail@email.com"`
在询问时定义名称

此时ls出.ssh目录，会发现多了second公钥和私钥
```
id_rsa 
id_rsa.pub 
known_hosts 
list.txt 
second 
second.pub 
```
远程主机添加公钥

在~/.ssh/目录下新建config文件，用于配置各个公私钥对应的主机
```
# Default github user(first@mail.com)  默认配置，一般可以省略
Host github.com
Hostname github.com
User git
Identityfile ~/.ssh/github
# second user(second@mail.com)  给一个新的Host称呼
Host second.github.com  // 主机名字，不能重名
HostName github.com   // 主机所在域名或IP
User git  // 用户名称
IdentityFile C:/Users/username/.ssh/id_rsa_second  // 私钥路径
```
注意：

每个邮箱能配置一个公私钥，邮箱是一个重要的身份识别标志
几个主机的命名不能相同；
私钥路径也可以写为 ~/.ssh/...；
如有需要还可以添加Port:xxxx端口配置。 

测试连接情况 
`$ ssh -T git@second.github.com`

现在开始使用新的公私钥进行工作吧

情景1：使用新的公私钥进行克隆操作

`git clone git@second.github.com:username/repo.git`
注意此时要把原来的github.com配置成你定义的second.github.com
情景2：已经克隆，之后才添加新的公私钥，我要为仓库设置使用新的公私钥进行push操作

修改仓库的配置文件：.git/config 为
```
[remote "origin"]
    url = git@second.github.com:itmyline/blog.git
```
即可

之后就照平常一样工作就行啦！


原文https://www.zybuluo.com/yangfch3/note/172120

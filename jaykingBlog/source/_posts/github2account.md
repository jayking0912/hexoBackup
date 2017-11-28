---
title: 多个账号github SSH key切换
date: 2017-03-07 20:15:32
tags: github
---

如果是单账户，很方便，默认拿id_rsa与你的 github服务器的公钥对比；

如果是多用户如user1,user2,那么就不能用在user2的身上了，怎么办呢？

下面我将使用图文形式详细想大家介绍下多github用户配置ssh key；

## **新建user1、user2的SSH Key**

\#新建user1 SSH key：

$ cd ~/.ssh     

\# 切换到C:\Users\Administrator\.ssh

\#ssh-keygen -t rsa -C "user1@email.com" 

一路回车即可；

 # 新建user2的SSH key

\#ssh-keygen -t rsa -C "user2@email.com"

\# 设置名称为id_rsa_user2

(/c/Users/Administrator/.ssh/id_rsa):** /c/Users/Administrator/.ssh/id_rsa_user2**



## **密钥添加到SSH agent中**

因为默认只读取id_rsa，为了让SSH识别新的私钥，需将其添加到SSH agent中：

ssh-add ~/.ssh/id_rsa_user2

如果出现Could not open a connection to your authentication agent的错误，就试着用以下命令：

ssh-agent bash 

ssh-add ~/.ssh/id_rsa_user2

## **修改config文件**

 在~/.ssh目录下找到config文件，如果没有就创建：

touch config     

然后修改我的config配置如下：

如果存在的话，其实就是往这个config中添加一个Host：

\#建一个github别名，新建的帐号使用这个别名做克隆和更新

其规则就是：从上至下读取config的内容，在每个Host下寻找对应的私钥。这里将GitHub SSH仓库地址中的git@github.com替换成新建的Host别名如：github2，那么原地址 是：git@github.com:test/Mywork.git，替换后应该是：git@github2:test/Mywork.git

打开新生成的~/.ssh/id_rsa_user2.pub文件，将里面的内容添加到GitHub后台。

第一个github帐号下的SSH Key中也要记得添加。



## **测试**

$ ssh -T git@github.com

Hi chenlianjiang! You've successfully authenticated, but GitHub does not provide shell access.

 $ ssh -T git@github2 

Hi 1047353200! You've successfully authenticated, but GitHub does not provide shell access.



## **应用**

测试成功，尝试克隆1047353200账号下的远程仓库。如下：

$ git clone git@github2:1047353200/git-demo.git
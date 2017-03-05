---
title: Hexo 建立自己的博客
date: 2017-03-04 21:30:29
tags:
---
通过各种比对，我最终选择了用hexo建立自己的博客，现在记录下建博客的过程和遇到的问题

## 建立仓库
仓库名必须为【your_user_name.github.io】（必须与你github名字对应！）
然后添加秘钥，有的忽略

## 安装node.js和git
略

## 安装 hexo
定位博客本地放置的路径

### 下载安装hexo
``` bash
$ npm install -g hexo-cli
```
### 安装好hexo以后，在终端输入：
$ hexo

### 初始化博客
``` bash
// 建立一个博客文件夹，并初始化博客，<folder>为文件夹的名称，可以随便起名字
$ hexo init <folder>
// 进入博客文件夹，<folder>为文件夹的名称
$ cd <folder>
// node.js的命令，根据博客既定的dependencies配置安装所有的依赖包
$ npm install
```
### 配置博客
基于上一步，我们对博客修改相应的配置，我们用到_config.yml文件

### 修改网站相关信息
``` bash
title: inerdstack
subtitle: the stack of it nerds
description: start from zero
author: inerdstack
language: zh-CN
timezone: Asia/Shanghai
```
language和timezone都是有输入规范的，详细可参考语言规范和时区规范。

注意：每一项的填写，其:后面都要保留一个空格，下同。

### 配置统一资源定位符（个人域名）
``` bash
url: http://inerdstack.com
```
对于root（根目录）、permalink（永久链接）、permalink_defaults（默认永久链接）等其他信息保持默认。

### 配置部署
``` bash
deploy:
  type: git
  repo: https://github.com/iNerdStack/inerdstack.github.io.git
  branch: master
```
其中repo项是之前Github上创建好的仓库的地址

*需要进github 的 setting 里将github page 选择为master,否则无法使用

然后执行命令：
``` bash
npm install hexo-deployer-git --save
```
3.0后全部改成我上面这种格式了

### 发表一篇文章

在终端输入：
``` bash
// 新建一篇文章
hexo new "文章标题"
```
我们可以在本地博客文件夹source->_post文件夹下看到我们新建的markdown文件。

保存后，我们进行本地发布：
``` bash
$ hexo server
```
打开浏览器，输入：
http://localhost:4000/
我们可以在浏览器端看到我们搭建好的博客和发布的文章
我们也可以手动添加Markdown文件在source->_deploy文件夹下

发布
``` bash
 hexo clean  # 清空
 hexo generate 或 hexo g    # 生成
 hexo deploy 或 hexo d      # 发布
    或
 hexo clean  # 清空
 hexo d -g  # 生成、发布
```
## 绑定个人域名
在自己的域名解析输入如下
记录类型 主机记录 解析线路 记录值
 A        @       默认   192.30.252.153
 CNAME    WWW     谷歌   jayking0912.github.io
 A        @       谷歌   192.30.252.154
 CNAME  cphp709dbj默认   zz.baidu.com

 如果网站要百度收录请参考 http://www.pmdog.me/2015/12/07/hexo%E8%A2%AB%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95%E6%96%B9%E6%B3%95/
 未测试

此时输入个人域名
会看到 github 404报错，这说明我们的域名已经成功映射到了Github网站，但是它找不到我们的博客的位置，所以我们需要实现个人博客向个人域名的映射，进入Github博客的仓库
点击上图上方偏右的Create new file按钮，创建一个文件
文件名为CNAME(注意：没有扩展名)，文件内容为个人域名(注意：没有http://，没有www)，然后选择下方的Commit new file按钮。然后在浏览器端重新输入我们的域名，我们可以看到域名绑定成功
当我们在本地使用hexo deploy命令再一次部署博客时，会发现博客网页的css样式丢失或是404错误，这是因为本地的博客工程里面还没有CNAME，当我们重新部署后，远程的博客工程会和本地保持同步，将CNAME文件删除，所以我们要在本地添加CNAME文件：
这里我们需要注意的是：CNAME文件添加的目录是在根目录下的source文件夹，而不是.deploy_git文件夹，完成添加后重新部署，博客网站又会恢复正常。



 ## 参考：
 http://blog.csdn.net/u010828718/article/details/55506957
 http://blog.csdn.net/gdutxiaoxu/article/details/53576018
 http://www.jianshu.com/p/5e0ca2b14815
 http://www.jianshu.com/p/e99ed60390a8
 http://www.jianshu.com/p/465830080ea9
 http://www.pmdog.me/2015/12/07/hexo%E8%A2%AB%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95%E6%96%B9%E6%B3%95/
 http://www.jianshu.com/p/cea41e5c9b2a?open_source=weibo_search


---
title: 群晖git创建项目
date: 2017-12-01 20:48:51
tags: nas
---

群晖创建git 项目需要 ssh登陆 root 账号，命令行输入指令

//git根目录
cd /volume2/git/

//创建目录
mkdir xxx.git

//cd 
cd xxx.git

//初始化
git init --bare

//返回
cd ../

//设为 git用户
chown git:users xxx.git/

//访问权限
chmod -R 777 xxx.git/
---
title: sourcetree 密码更换
date: 2017-11-28 20:48:51
tags: vs
---

因为考虑到公司 nas的安全性，将git 账号密码更改后发现 sourcetree 一直提示 权限不通过，找了半天也找不到改密码的地方
最后 mac 直接卸了重装就好了 ，但是win卸了死活跳不出输密码的界面
最后无意中发现  ：
在 本地用户 user/appdata/local/Atlassian/sourcetree 目录下面有个 password 的文件，删除就可以了
同时在 mac 下可以到 keychain 下找到对应的账户 删除
---
title: Mac 10.12安装 mysql
date: 2017-03-12 20:48:51
Tags:mysql Mac
---

**安装步骤：**

一、官方下载dmg安装包进行安装

1、登陆官网下载

[https://downloads.mysql.com/archives/community/](https://downloads.mysql.com/archives/community/)

2、解压出pkg文件

3、安装

4、测试

▲验证是否安装成功，进入/usr/local/mysql/bin/，用ls命令查看是否有mysql

每次都要进入到mysql的目录上进行启动，那么有两种方式alias和ln进行设置，ln其实不推荐，路径时很大的问题。推荐使用alias。

```
alias mysql=/usr/local/mysql/bin/mysql
```

▲启动mysql的服务，输入以下命令：

```
sudo /usr/local/mysql/support-files/mysql.server start 
```

注意，start为启动，那么stop就是停止，全命令如下：

```
sudo /usr/local/mysql/support-files/mysql.server stop
```

或者

![image](http://upload-images.jianshu.io/upload_images/712523-8cd12cc1d29ea995.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

▲修改mysql初始化密码

避免服务已经启动，所以第一步先关闭mysql的服务

```
sudo /usr/local/mysql/support-files/mysql.server stop
```

开启安全模式启动mysql，这种方式可以不用输入默认密码

```
sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
```

此时，关闭这个终端窗口，再重新启动一个

进入/usr/local/mysql/bin/，以root身份启动mysql

```
./mysql -u root
```

输入以下命令修改密码，其中PASSWORD里面就是要设置的密码

```
UPDATE mysql.user SET authentication_string=PASSWORD(‘root‘) WHERE User=‘root‘;
FLUSH PRIVILEGES;
```

退出mysql，输入

```
quit;
```

停止mysql服务

```
sudo /usr/local/mysql/support-files/mysql.server stop
```

再启动mysql服务

```
sudo /usr/local/mysql/support-files/mysql.server start
```

使用以下命令进入mysql

```
./mysql -u root -p
```

 此时，要求输入密码，就是前面设置的root密码

再测试是否正常

```
show databases; 
```

此时，如果出现：ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.的错误提示时，需要再设置一次密码

```
SET PASSWORD = PASSWORD(‘root‘);
```
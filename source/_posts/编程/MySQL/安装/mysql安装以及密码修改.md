---
title: mysql安装以及密码修改
categories: 
  - 编程
  - MySQL
  - 安装
date: 2018-12-14 01:58:11
updated: 2021-03-20 10:21:09
abbrlink: e124ac2c
---
<div id='my_toc'><a href="/blog/e124ac2c/#安装" class="header_1">安装</a>&nbsp;<br><a href="/blog/e124ac2c/#安装mysql服务" class="header_1">安装mysql服务</a>&nbsp;<br><a href="/blog/e124ac2c/#启动mysql服务" class="header_1">启动mysql服务</a>&nbsp;<br><a href="/blog/e124ac2c/#使用mysql" class="header_1">使用mysql</a>&nbsp;<br><a href="/blog/e124ac2c/#验证" class="header_2">验证</a>&nbsp;<br><a href="/blog/e124ac2c/#mysql用户登录" class="header_1">mysql用户登录</a>&nbsp;<br><a href="/blog/e124ac2c/#修改root用户密码" class="header_1">修改root用户密码</a>&nbsp;<br><a href="/blog/e124ac2c/#情况1-记得原来root用户的密码" class="header_2">情况1 记得原来root用户的密码</a>&nbsp;<br><a href="/blog/e124ac2c/#登录root用户" class="header_3">登录root用户</a>&nbsp;<br><a href="/blog/e124ac2c/#修改密码" class="header_3">修改密码</a>&nbsp;<br><a href="/blog/e124ac2c/#重启服务使新密码生效" class="header_3">重启服务使新密码生效</a>&nbsp;<br><a href="/blog/e124ac2c/#情况2-记不得root用户密码" class="header_2">情况2 记不得root用户密码</a>&nbsp;<br><a href="/blog/e124ac2c/#修改my-in登录时跳过密码检查" class="header_3">修改my.in登录时跳过密码检查</a>&nbsp;<br><a href="/blog/e124ac2c/#重启mysql服务" class="header_3">重启mysql服务</a>&nbsp;<br><a href="/blog/e124ac2c/#直接登录mysql修改密码" class="header_3">直接登录mysql修改密码</a>&nbsp;<br><a href="/blog/e124ac2c/#其他知识" class="header_1">其他知识</a>&nbsp;<br><a href="/blog/e124ac2c/#关闭mysql服务" class="header_2">关闭mysql服务</a>&nbsp;<br><a href="/blog/e124ac2c/#debug" class="header_1">debug</a>&nbsp;<br><a href="/blog/e124ac2c/#The-service-already-exists" class="header_2">The service already exists</a>&nbsp;<br><a href="/blog/e124ac2c/#解决方案-###​" class="header_2">解决方案 ###​</a>&nbsp;<br><a href="/blog/e124ac2c/#参考链接" class="header_1">参考链接</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 安装
解压安装包即可安装
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/install.png)
# 安装mysql服务
以管理员身份打开cmd，cd到mysql安装目录下的bin目录：
```
cd C:\Users\lan\Desktop\mysql\数据库\mysql5.5.8\bin
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/binMulu.png)
然后输入命令:
```
mysqld -install
```
安装mysql服务,安装成功命令输出如下:
```
C:\Users\lan\Desktop\mysql\数据库\mysql5.5.8\bin>mysqld -install
Service successfully installed.
C:\Users\lan\Desktop\mysql\数据库\mysql5.5.8\bin>
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/anzhuangfuwu.png)
# 启动mysql服务
服务安装后，就可启动mysql了,输入下面的命令启动服务：
```
net start mysql
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/start.png)
# 使用mysql
直接输入命令:
```
mysql
```
即可进入mysql
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/into.png)
## 验证
输入`show databases;`查看当前有多少个数据库,看到如下界面表示mysql安装成功了:
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/showDatabases.png)
# mysql用户登录
如使用密码登录root用户：`mysql -u root -p`,-u 后面表示用户，-p表示让用户输入密码
# 修改root用户密码
## 情况1 记得原来root用户的密码
### 登录root用户
默认的root用户没有密码，现在来设置root用户的密码。
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/rootnopassword.png)
### 修改密码
```
use mysql;
update user set password=password('新密码') WHERE User='root';
flush privileges;
```
如,想把root用户的密码设置为root，则写为:`update user set password=password('root') WHERE User='root';`
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/updatePassBypassword.png)
### 重启服务使新密码生效
```
exit
net stop mysql
net start mysql
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/restart.png)
这样就不能只用空密码登录了，只能使用新密码进行登录。
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/restart_login.png)

## 情况2 记不得root用户密码
这种情况，需要修改配置文件，让mysql跳过密码检查。可以直接登录，登录后的密码修改操作还是一样的。
### 修改my.in登录时跳过密码检查
先退出myql,然后，打卡mysql安装目录下面的my.in文件，这个是mysql的配置文件
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/install/my_in.png)
在my.ini的`[mysqld]`字段加入：`skip-grant-tables`，然后保存。
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/add_in_my_in.png)
### 重启mysql服务
修改配置文件后，管理员下cmd，输入下面两条指令重启mysql服务:
```
net stop mysql
net start mysql
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/restart.png)
### 直接登录mysql修改密码
现在直接输入mysql就可以登录了，修改密码操作与情况1一样。
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/changpassword/nopasswordIn.png)
# 其他知识
## 关闭mysql服务
先关闭服务，然后再删除服务。
```
net stop mysql
mysqld -remove
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/mysql/remove/remove.png)
# debug
## The service already exists
`mysqld -install` 报错：
```
​The service already exists
```
原因是之前安装了以后卸载了，服务没删掉。
## 解决方案 ###​
`sc query mysql`，查看一下名为mysql的服务，如果有，则删除mysql服务。
```
sc delete mysql
```
然后再安装`mysqld -install`就能成功了。
# 参考链接
[mysql以zip安装，解决the service already exists](https://www.cnblogs.com/dichters/p/5929209.html)

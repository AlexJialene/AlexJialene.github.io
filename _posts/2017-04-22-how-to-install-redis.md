---
layout: post
title: 虚拟机安装redis学习
tags: ['redis']
---

# redis的安装配置/ubuntu

* 我的虚拟机用的oracle vm virtualbox 
* 参考[http://redis.io/documentation​ ](http://redis.io/documentation)redis官方api
* 由于服务器上安装redis的网上教程比较多，所以就不写这个了，这里针对一些像作者这样的穷比只能用虚拟机来进行学习开发的人群用

## 下载redis
	$ sudo apt-get update
	$ sudo apt-get install redis-server
## 启动
	$ redis-server
查看redis是否启动

	$ redis-cli

若成功我们将启动成为如下终端 ： [本地ip ]:[端口号]

	redis 127.0.0.1:6379>

然后我们继续输入如下命令

	redis 127.0.0.1:6379> ping
	PONG

出现pong 则代表 redis 安装成功。

**注意：** 127.0.0.1为本地ip，我们从mac（或window）中访问时候应该设置成虚拟机桥段ip（主从）

首先我们找到已经安装好的目录；一般都是 etc/redis ,找到redis.conf ， 然后用管理员权限打开

	vi redis.conf

然后用vi 搜索 ：/bind ,找到bind，把本地的127.0.0.1 ，改成桥段ip ，保存退出

接下来修改映射 ( 也是桥段ip )（保证mac/window 能够连接得到你的redis 服务）
redis-cli -h [IP地址] -p [端口号]
如：

	redis-cli -h 10.37.129.3 -p 6379

## 重启redis 服务

	redis-cli shutdown

	redis-server redis.conf

到这里我们回到 Mac/window 连接一下redis服务

	telnet 10.37.129.3 6379
	...
	ping

	+PONG

如上输出 +pong 即代表成功了

注释：本文中出现 ... 为略过意思。
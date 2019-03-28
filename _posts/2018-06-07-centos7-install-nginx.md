---
layout: post
title: centos 7 安装 nginx
tags: ['nginx']
---

### 安装 gcc gcc-c++ （已经安装请忽略）

```
$ yum install -y gcc gcc-c++
```

### 安装ssl库
```
$ cd /usr/
$ wget http://http://www.openssl.org/source/openssl-1.0.1j.tar.gz
$ tar -zxvf openssl-1.0.1j.tar.gz
$ cd openssl-1.0.1j
$ ./config
$ make && make install
```
### 安装PCRE库

```
$ cd /usr/
$ wget http://downloads.sourceforge.net/project/pcre/pcre/8.33/pcre-8.33.tar.gz
$ tar -zxvf pcre-8.33.tar.gz
$ cd pcre-8.33
$ ./configure
$ make && make install
```
### 安装zlib库
```
$ cd /usr/
$ wget http://zlib.net/zlib-1.2.11.tar.gz
$ tar -zxvf zlib-1.2.11.tar.gz
$ cd zlib-1.2.11
$ ./configure
$ make && make install
```

### 正式安装nginx

#### 下载
```
$ cd /usr/
$ wget http://nginx.org/download/nginx-1.8.0.tar.gz
$ tar -zxvf nginx-1.8.0.tar.gz
$ cd nginx-1.8.0  
```
#### 配置
```
./configure --with-http_stub_status_module --with-http_gzip_static_module --with-http_realip_module --with-http_sub_module --with-http_ssl_module --with-pcre=/usr/nginxEnv/pcre-8.33 --with-zlib=/usr/nginxEnv/zlib-1.2.11 --with-openssl=/usr/nginxEnv/openssl-1.0.1j
```
注意：
* --with-http_ssl_module 是支持ssl的模块（https）
* --with-pcre 是指向上面编译安装好的pcre库的源码
* --with-zlib 是指向上面编译安装好的zlib库的源码
* --with-openssl 是指向上面编译安装好的openssl库的源码

#### 编译安装
```
$ make
$ make install
```
* 默认安装在/usr/local/nginx/ 文件夹里面

### 查看是否安装成功

```
$ cd /usr/local/nginx/sbin/
$ ./nginx -t
```
输出如下即成功了

```
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

```

> 附上ssl证书[nginx.conf](http://blog.keizyi.me/file/nginx.conf){:target="_blank"}配置文件
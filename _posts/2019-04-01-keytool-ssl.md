---
layout: post
title: 根据ip自签ssl证书以及springboot设置
tags: ['https', 'ssl']
---

由于工作中某些原因在Android中需要用到自签证书，服务器端为springboot。

## 命令

```
keytool -genkey -alias server -keyalg RSA -storetype PKCS12 -keysize 2048 -keystore /Users/lamkeizyi/Downloads/server.p12 -dname "CN=Alex Dennis,OU=huashitu,O=huashitu,L=Guangzhou,ST=Guangdong,c=cn" -validity 3650 -storepass 123456 -keypass 123456 -ext SAN=IP:xxx.xxx.x.xxx

```

注意：-ext SAN=IP:xxx.xxx.x.xxx 可指定自签IP。

* -genkey：生成key
* -alias：别名，独一无二，通常不区分大小写
* -keyalg： 指定密钥的算法（如 RSA,  DSA（如果不指定默认采用DSA））
* -storetype：指定密钥仓库类型，无指定默认为JKS，但oracle建议使用PKCS12
* -keysize ：指定证书大小
* -keystore：指定密钥库的名称，可指定路径，例如：E:/ssl/ 需要注意的是运行该命令之前需要先创建好该目录。
* -validity：证书的有效期，单位：天。


## 导出cer证书

```
keytool -export -alias server -file /Users/lamkeizyi/Downloads/server.cer -keystore /Users/lamkeizyi/Downloads/server.p12 -storepass 123456

```

## springboot 配置

```
server:
  port: 8080
  ssl:
    key-alias: server
    key-store: server.p12
    enabled: true
    key-store-password: 123456
    key-store-type: PKCS12
    ciphers: TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,
			 TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,
			 TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,
			 TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,
			 TLS_ECDHE_RSA_WITH_RC4_128_SHA,
			 TLS_RSA_WITH_AES_128_CBC_SHA256,
			 TLS_RSA_WITH_AES_128_CBC_SHA,
			 TLS_RSA_WITH_AES_256_CBC_SHA256,
			 TLS_RSA_WITH_AES_256_CBC_SHA,
			 SSL_RSA_WITH_RC4_128_SHA

```

上面配置是springboot application.yml配置。注意`server.ssl.ciphers` 参数，配置允许加密套件。

参考链接: [https://www.jianshu.com/p/2b91ca9e9564](https://www.jianshu.com/p/2b91ca9e9564)

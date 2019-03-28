---
layout: post
title: 搭建个人GitHub的maven仓库并发布jar包
tags: ['maven']
---


因为个人觉得自己写的jar包要提交到maven中央仓库很麻烦，所以就用github托管并搭建个人maven仓库来发布jar包 <br>
这里采用的不是项目直接deploy到GitHub，而是先deploy到本地，然后再提交GitHub

### `deploy local`
idea pom.xml 配置形式指定deploy路径
```
<distributionManagement>
        <repository>
            <id>lamkeizyi-repo</id>
            <url>file:/Users/lamkeizyi/Documents/maven/maven-repo/repository/</url>
        </repository>
</distributionManagement>
```
运行找到maven选项运行deploy即可 <br>

或者命令输入
```
mvn deploy -DaltDeploymentRepository=lamkeizyi-repo::default::file:/Users/lamkeizyi/Documents/maven/maven-repo/repository/
```

### `commit push GitHub`
```
cd /Users/lamkeizyi/Documents/maven/maven-repo/
git init
git add repository/*
git commit -m ''deploy my repo''
git remote add origin your GitHub''s url
git push origin master
```
----
现在我们就可以在项目中引入我们maven仓库以及jar包了
> [参考我自己的仓库](https://github.com/AlexJialene/maven-repo)

github使用了raw.githubusercontent.com这个域名用于raw文件下载 . 所以在项目中引入maven包分为2步 <br>

1.先引入maven仓库
```
<repositories>
    <repository>
        <id>lamkeizyi-repo</id>
        <url>https://raw.githubusercontent.com/AlexJialene/maven-repo/master/repository</url>
    </repository>
</repositories>
```
2.导入想要的jar包
```
<dependency>
    <groupId>syuio</groupId>
    <artifactId>syuio</artifactId>
    <version>1.0-beta-1</version>
</dependency>
```
然后就开始在你的项目中使用吧
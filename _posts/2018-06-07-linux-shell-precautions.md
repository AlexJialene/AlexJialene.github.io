---
layout: post
title: linux shell一些注意事项
tags: ['shell', 'Linux']
---

项目中需要用到流媒体（rtmp）录制成flv文件存在数据库，然后用ffmpeg转成mp4，然后通知后台转换成功，flv-MP4转换时候的时间比较长，所以就写了个shell脚本去监控酱紫。也会踩点坑，因为和普通的程序还是有点出入的。好了接下来进入正题

# 正文
	#!/bin/bash
这个就不用太多解释了，声明这是一个shell脚本文件

## 变量

```
name_name="this''s name"
echo $name_name
name_name="set name"
```

* 变量名和等号之间不能有空格
* 首个字符必须为字母（a-z，A-Z）
* 中间不能有空格，可以使用下划线（_）
* 不能使用标点符号
* 不能使用bash里的关键字
* 使用变量时候应该加美元符：$name_name
* 二次赋值不需要加上美元符：name_name="set name"

## 参数传递

```
lsFile(){
    echo "the file -f $1"
}
lsFile "value1" "value2"

```	

* 参数传递为 方法名 arg1 arg2（空格隔开，注意这里方法名不需要加括号）
* 方法中获取参数为 $1  同理获取第二个参数为$2
* 另一种执行写法为 ./test.sh 1 2 3 同理

## test和算术运算符与方法return

```
a=10
b=10
c=`expr $a + $b`
echo $c
demo(){
	if [ $a -eq $b ] then
		echo "a equal b"
	fi
	#return "value" no
	return 0 #return "0" yes
}
```

* -eq 等判断只是数字
* 加减乘除等需要 `` 符号里运行 
* 方法return 只支持数字，不支持字符串
* 注意 if [ ] 中括号与参数的空格 ，不可忽略
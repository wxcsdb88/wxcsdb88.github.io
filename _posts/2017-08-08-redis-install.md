---
layout: post
title:  "linux系统安装redis"
date:   2017-08-08 00:00:00
categories: NoSQL
description: linux系统安装redis
keywords: db,NoSQL,redis
author: wxcsdb88
---

ubuntu 14.04 安装 redis 并设置开机启动

## Install
```
sudo mkdir /usr/local/redis
cd  /usr/local/redis
wget http://download.redis.io/releases/redis-4.0.1.tar.gz
sudo tar xzf redis-4.0.1.tar.gz
#建立链接
ln -s redis-2.6.14 redis
cd redis
#安装到指定目录中
sudo make PREFIX=/usr/local/redis install
```

## Service
复制脚本到/etc/rc.d/init.d目录
```
sudo cp /usr/local/src/redis/utils/redis_init_script /etc/init.d/redis  
sudo cp  /usr/local/src/redis/redis.conf  /usr/local/redis/6379.conf
vim /etc/rc.d/init.d/redis  

#/usr/local/redis/
$EXEC $CONF &，后边的 &，表示将服务转到后台运行；
EXEC、CLIEXEC、CONF 等三处路径都要改
```

## Env
```
vi /etc/profile
export REDIS=/usr/local/redis/bin
export PATH=$REDIS:$PATH
source /etc/profile
```

## onboot startup
```
sudo update-rc.d redis defaults
```

## remove onboot
```
sudo update-rc.d -f redis remove
```
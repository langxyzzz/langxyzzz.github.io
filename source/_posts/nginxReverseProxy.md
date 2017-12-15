---
title: Nginx反向代理
date: 2017-12-15 16:23:53
categories: Linux
tags:
 - Linux
 - Nginx
---
Nginx是一个高性能的HTTP和反向代理服务器，Nginx是一款轻量级的Web服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，下面来说一下Nginx如何配置反向代理。
# 下载安装Nginx
我们可以到[Nginx官网](http://nginx.org/en/download.html)去下载
直接下载linux稳定版的就可以了
{% asset_img nginx.png %}
以此1.12.2稳定版本为例
右键复制链接地址
在安装nginx之前需要先安装一些nginx的依赖,然后开始安装nginx,到服务器里面执行:
``` bash
$ yum install gcc zlib zlib-devel pcre-devel openssl openssl-devel
$ wget http://nginx.org/download/nginx-1.12.2.tar.gz
$ tar -zxvf nginx-1.12.2.tar.gz
$ cd nginx-1.12.2
$ ./configure
$ make
$ make install
```
# 配置反向代理（以默认安装路径为例）
## 配置/usr/local/nginx/conf/nginx.conf
``` bash
$ vim /usr/local/nginx/conf/nginx.conf
```
插入“<font color=#FF0000>include vhost/*.conf</font>”
保存退出
配置nginx的主要目的是把nginx所有的配置文件都放在vhost文件夹里面，便于维护和修改
## 创建vhost文件
``` bash
$ mkdir /usr/local/nginx/conf/vhost
$ cd /usr/local/nginx/conf/vhost
$ vim text.conf
```
{% asset_img nginx2.png %}
保存退出
listen:是配置nginx的端口
server_name:是你的域名
proxy_pass:是你的服务器公网地址
## 重启nginx
``` bash
$ /usr/local/nginx/sbin/nginx -s reload
```
# END
下面是我个人的服务器和域名配置的反向代理
{% asset_img nginx3.png %}

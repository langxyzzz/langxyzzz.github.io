---
title: Git实现ssh登录
date: 2018-12-5 16:21:09
categories: git
tags: 
 - 教程 
 - git
---
git实现ssh登录，就实现了免密登录
## 安装Git
Git[下载地址](https://www.git-scm.com/download/)

## 生成密钥
### 生成密钥
安装好git后，打开"Git Base Here"输入
``` base
$ ssh-keygen -t rsa -C "lang_xy@163.com"
```
{% asset_img github1.png %}
此时 C:\Users\用户名\.ssh 下会多出两个文件 id_rsa 和 id_rsa.pub，记得把"lang_xy@163.com"换成你自己的账号
### 查看密钥
接着输入下面内容，查看密钥
``` base
$ cat ~/.ssh/id_rsa.pub
```
{% asset_img github2.png %}
## 登录github配置密钥
登录[github](https://github.com/)点击自己github头像，选择Settings
{% asset_img github3.png %}
接着点击SSH and GpG keys，接着创建一个SHH keys
{% asset_img github4.png %}
最后title随便输入，然后把刚刚输入的密钥填进key
{% asset_img github5.png %}
然后点击Add SSH key就好了
## 验证密钥是否生效
回到"Git Base Here"，输入
``` base
$ ssh -T git@github.com
```
{% asset_img github6.png %}
返回上面信息就是成功了，就可以不需要每次使用都需要登陆了。
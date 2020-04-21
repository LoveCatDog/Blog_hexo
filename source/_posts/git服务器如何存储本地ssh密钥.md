---
title: git服务器如何存储本地ssh密钥
date: 2020-04-21 11:59:13
tags: git
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'git服务器如何存储本地ssh密钥'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e9e786ac2a9a83be545c86d.jpg'  #缩略图
---

### 背景环境
> Git（读音为/gɪt/）是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。

当安装git之后，将github上项目clone到本地后，再次push项目到github上会出现以下错误

![](https://pic.downk.cc/item/5e9e730ac2a9a83be541efe0.png)

### 解决步骤
1. 在下载好的Git中的bin目录下（一般是 C:\Program Files\Git\bin）打开bash.exe输入命令ssh-keygen -t rsa -C "username" (注：username为你git上的用户名)，如果执行成功。返回：
```javaScript
 Generating public/private rsa key pair.
 Enter file in which to save the key (/Users/username/.ssh/id_rsa): //这里的username是电脑上的用户名，
```

这个地址也是文件的存储地址，然后按回车，

如果以前有存储地址会返回/Users/your username/.ssh/id_rsa already exists.Overwrite (y/n)?直接输入y回车。

如果以前没有储存地址就会出现Enter passphrase(empty for no passphrase);也直接回车，

两种情况回车后都会出现 Enter same passphrase again 然后接着回车会显示
```javaScript
The key's randomart image is:
+---[RSA 3072]----+
|+o*.+*=*=o+      |
| **+*.o+.=       |
|++o/.o  o .      |
|.+X.*.E  .       |
|.. o.+  S        |
|.. .  .          |
|. .              |
|                 |
|                 |
+----[SHA256]-----+
```

这说明SSH key就已经生成了。文件目录就是：username/.ssh/id_rsa.pub.

2. 然后找到系统自动在.ssh文件夹下生成两个文件，id_rsa和id_rsa.pub，用记事本打开id_rsa.pub将全部的内容复制。
![](https://pic.downk.cc/item/5e9e76f0c2a9a83be5449c24.png)

3. 打开https://github.com，登陆账户，进入设置（Settings）找到 SSH and GPG keys  再带点击 Add SSH Key 将复制的内容粘贴到key中
![](https://pic.downk.cc/item/5e9e772dc2a9a83be544c1e6.png)
4. 仍然在bash.exe中输入ssh -T git@github.com然后会跳出一堆内容你只需输入yes回车就完事了，然后它会提示你成功了。
![](https://pic.downk.cc/item/5e9e7768c2a9a83be544e6f6.png)

大功告成，再次输入之前的指令就成功了

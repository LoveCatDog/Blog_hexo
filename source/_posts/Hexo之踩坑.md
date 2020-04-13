---
title: Hexo之踩坑
date: 2020-04-13 16:57:16
tags: 
 - Hexo
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Hexo之踩坑'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1586778521085&di=b93c6de6a01580d43962ef6ceb0a9786&imgtype=0&src=http%3A%2F%2Fpic2.zhimg.com%2Fv2-a11d47bc3401edaf671f202cd6365a07_1200x500.jpg'  #缩略图
---


背景环境：本着在家有时间将github上由hexo创建的blog克隆到本地，但由于本机首次配置，一路踩了不少坑~
### 问题一

```JavaScript
 bash: hexo: command not found
```
本着能解决问题就不重装的原则，首先检查 nodejs 和 npm 是否正常，依次输入命令 node -v 和 npm -v 看看是否有相关版本信息

![](https://pic.downk.cc/item/5e942360c2a9a83be5d8fb00.png)

出现了版本信息就证明 nodejs 和 npm 是没有问题的，那么就应该是环境变量的配置问题了，在【此电脑】右键【属性】，依次选择【高级系统设置】-【环境变量】，选择系统变量 Path，将 node_modules 下的 .bin 文件路径添加到 Path 里面

> 我本地blog的项目下的系统变量为：D:\workspace\hexo_blog\Blog_hexo\node_modules\.bin

![](https://pic.downk.cc/item/5e942482c2a9a83be5d9c4e8.png)


环境变量添加好了之后重新打开 git 即可运行 hexo 命令，如果此时仍然无法执行 hexo 命令，那就只能拿出终极绝招了，运行命令 npm install hexo-cli -g 重新安装 hexo 即可！
>hexo -version  //查看hexo安装版本
之后本项目的配置ok，大兄弟们可以继续在该项目开发了...
![](https://pic.downk.cc/item/5e942574c2a9a83be5da5d1a.png)

###  问题二

> Hexo初始化的时候，提示如下错误？

```JavaScript
 $ hexo init
FATAL D:\workspace\hexo_blog\Blog_hexo\ not empty, please run `hexo init` on an empty folder and then copy your files into it
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
Error: target not empty
    at Hexo.initConsole (D:\workspace\hexo_blog\Blog_hexo\node_modules\hexo\node_modules\hexo-cli\lib\console\init.js:23:27)
    at Hexo.tryCatcher (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\util.js:16:23)
    at Hexo.<anonymous> (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\method.js:15:34)
    at D:\workspace\hexo_blog\Blog_hexo\node_modules\hexo\lib\hexo\index.js:248:17
    at Promise._execute (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\debuggability.js:384:9)
    at Promise._resolveFromExecutor (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:518:18)
    at new Promise (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:103:10)
    at Hexo.call (D:\workspace\hexo_blog\Blog_hexo\node_modules\hexo\lib\hexo\index.js:244:12)
    at D:\workspace\hexo_blog\Blog_hexo\node_modules\hexo\node_modules\hexo-cli\lib\hexo.js:67:17
    at tryCatcher (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\util.js:16:23)
    at Promise._settlePromiseFromHandler (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:547:31)
    at Promise._settlePromise (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:604:18)
    at Promise._settlePromise0 (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:649:10)
    at Promise._settlePromises (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\promise.js:729:18)
    at _drainQueueStep (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\async.js:93:12)
    at _drainQueue (D:\workspace\hexo_blog\Blog_hexo\node_modules\bluebird\js\release\async.js:86:9)

```

**解决方案**：Hexo 初始化只能找一个空目录初始化

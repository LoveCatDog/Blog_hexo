---
layout: _post
title: window下node.js和npm的安装和配置
date: 2020-02-05 12:10:44
tags: 
 - npm
 - node.js
 - 环境配置
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Windows下Node.js与npm的安装与配置'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e3a24672fb38b8c3cbb99c3.png'  #缩略图
---

### Windows下Node.js与npm的安装与配置

1. 先下载[Node.js](https://nodejs.org/en/ "node.js官网")，左侧为稳定版，右侧为最新版，推荐稳定版

![node.js官网]( https://pic.downk.cc/item/5e3a24672fb38b8c3cbb99c3.png "node.js官网展示")

2. Node.js安装，运行下载后的.msi文件，一路按下一步就可以了，也可以根据需求选择相关配置等选项。我选择的安装路径为 D:\program\nodejs ,安装之后按快捷键“ Window + R ”输入cmd，再运行cmd,执行node -v 和 npm -v命令 查看版本，若可查询到版本，
若执行结果为下图所示出现版本号，那恭喜您已成功安装。

![ww]( https://pic.downk.cc/item/5e3a23da2fb38b8c3cbb8a81.png '查询 node.js && npm 版本')

3. 配置npm的全局模块的存放路径以及cache的路径，我选择的路径使Node.js的安装路径，在此路径下建两个文件夹node_global 和 node_cache，现在的文件目录如下

![](https://pic.downk.cc/item/5e3a2eb42fb38b8c3cbca263.png '配置npm的全局模块的存放路径以及cache的路径')

4. 执行以下命令，再使用命令npm config get prefix,查看设置

![](https://pic.downk.cc/item/5e3a2ff02fb38b8c3cbcc8e3.png '查看设置')

5. 配置环境变量:在控制面板里面，按照如下图的流程进行环境配置。

![](https://pic.downk.cc/item/5e3a3e7d2fb38b8c3cbe60c6.png '查看设置')

然后重启cmd,网上大多数教程到此位置，再执行bower -v时，若可查到版本那就成功了

### 恭喜您配置成功，开启学习之旅吧！




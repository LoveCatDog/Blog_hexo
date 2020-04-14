---
title: Webpack之踩坑
date: 2020-04-14 16:13:00
tags:
 - Webpack
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Webpack之踩坑'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1550924156,4168612678&fm=15&gp=0.jpg'  #缩略图
---
### 使用clean-webpack-plugin小插件报错CleanWebpackPlugin is not a constructor

> clean-webpack-plugin是webpack的一个小插件：
由于每次打包的时候有可能文件名称不一样，打包后的文件就叠加到dist目录下了。

所以cleanWebPackPlugin作用就是在每次打包之前，先把dist目录删掉，创建最新的目录，避免一些不必要的文件还留在dist目录下

```javaScript
安装：npm install clean-webpack-plugin -D
```

正确的使用方法如下：

```javaScript
//引入clean-webpack-plugin的包
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

//在plugins中配置
plugins: [new CleanWebpackPlugin()]
```

我在使用过程中碰到错误：TypeError: cleanWebpackPlugin is not a constructor  主要有以下三种情况会报错：

+ 引入时与之前版本不同，如果还像以前那样用 

```javaScript
const CleanWebpackPlugin = require('clean-webpack-plugin'); 
```
+ 这个问题很奇怪，由于是我个人习惯原因，我在引入的时候第一个字母会小写，如

```javaScript
const { cleanWebpackPlugin } = require('clean-webpack-plugin');
```

+  配置时不能传参数，在最新版的webpack中 new CleanWebpackPlugin()；中不需要写里面的目标路径，会自动清除生成的文件夹，比如是dist文件夹，如果加上了目标路径（如：new CleanWebpackPlugin('./dist')）则会报错。



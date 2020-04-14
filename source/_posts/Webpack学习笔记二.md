---
title: Webpack学习笔记二
date: 2020-04-14 18:18:06
tags:
 - Webpack
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Webpack学习笔记二'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2617879016,3871876383&fm=15&gp=0.jpg'  #缩略图
---

### sourceMap
> 源代码与打包后的代码的映射关系。例如，在某个源文件中test.js里面有个错误，如果开启状态，那么打包后运行的报错信息就会说明是错误的具体位置，如果是关闭状态，报错后，提示的报错位置，会是打包的出口文件。

在开发模式中，默认开启，关闭的话，可以在配置文件里添加：


```javaScript
  devtool: 'source-map', //在开发模式中，默认开启，关闭的话，可以在配置文件里添加
```
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928171509219-2071822995.png)

** devtool的常见配置：**

+ eval：速度最快，使用eval包裹模块代码
+ source-map：产生.map文件
+ cheap：较快，不用管列的信息，也不包含loader的sourcemap
+ Module：第三方模块，包含loader的sourcemap
+ inline：将.map作为DataURI嵌入，不单独生成.map文件
推荐配置：
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928170754998-705067429.png)

### webpackDevServer
> webpackDevServer是一个提升开发效率的利器。之前每次改完代码后，都需要重新打包一次，刷新一次，安装使用了webpackDevServer以后，就可以改善这一块的操作和体验了。

首先需要进行安装：
```javaScript
npm install webpack-dev-server -D
```

然后修改package.json

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928171305020-399219513.png)

并且在配置文件webpack.config.js中进行相关配置：

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928171725428-732430282.png)

然后执行命令npm run server进行打包。

### 解决跨域

> webpackDevServer的另一重要功能就是解决跨域：

当我们在某一个页面中使用下面这种方式进行请求时，就会报跨域错误：

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928172513847-1574180694.png)

此时，就可以通过配置webpackDevServer来解决跨域了：

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928172753239-672594260.png)
 然后修改上面的请求就可以了：
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928172845561-1250307681.png)

### Hot Module Replacement(HMR：热模块替换)

HMR是webpack自带的一个功能，使用过程中，首先需要引入：
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190928174039867-342564790.png)


#### 处理js模块HRM

上面的处理，对样式的更新十分有效，但是如果要处理js的话，则还需要在此基础上添加module.hot.accept来观察模块更新。


### babel处理ES6

babel-loader是webpack与babel的通信桥梁，@babel/preset-env里包含了ES6转ES5的转换规则。

使用前首先需要安装：
```javaScript
npm i babel-loader @babel/core @babel/preset-env -D
```

然后在配置文件webpack.config.js中进行配置

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929092646875-1533326868.png)

#### @babel/polyfill

此时，只是将一些简单的ES6进行了转换了，如果要想完全能正常使用，还需要借助@babel/polyfill，把es6的新特性都装进来，弥补低版本浏览器中性能的缺失。

首先进行安装：npm install @babel/polyfill -D

然后在使用到promise等ES6语法的文件顶部进行引入：

index.js

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929093433463-1736760340.png)
在配置文件webpack.config.js中进行按需加载的配置。（polyfill默认会把所有特性都注入进来，如果不添加下面的配置，则会让打包体积变的非常大）
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929094019872-857595124.png

然后进行打包就可以了。

还有另外一种做法，在项目根目录下新建.babelrc的文件，然后将上面配置里面的options部分移入到这个文件中，再进行打包，也是可行的。)

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929101039216-90765873.png)

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929101051719-536225977.png)

**webpack.config.js**

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929101122334-674418316.png)


### @babel/plugin-transform-runtime

当我们开发的是组件库、工具库的时候，polyfill就不合适了，因为polyfill是注入到全局变量window下的，会污染全局环境。这种情况下，用@babel/plugin-transform-runtime更合适。

首先进行安装：

npm install --save-dev @babel/plugin-transform-runtime

npm install --save @babel/runtime

 然后使用前，还需要注释掉前面index.js里面polyfill的引入

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929093433463-1736760340.png)

再到.babelrc里面添加配置

![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190929101655008-633598107.png)

配置完成以后，就可以打包使用了。
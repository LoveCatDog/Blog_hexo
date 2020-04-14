---
title: Webpack学习笔记一
date: 2020-04-14 13:31:58
tags:
 - Webpack
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Webpack学习笔记一'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2617879016,3871876383&fm=15&gp=0.jpg'  #缩略图
---


### 什么是webpack

![](https://pic.downk.cc/item/5e9549f9c2a9a83be592fe95.png)

本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。详细使用可参考[webpack官网](https://www.webpackjs.com/) 
### 安装
#### 本地安装
1. 要安装最新版本或特定版本，请运行以下命令之一：
```javaScript
npm install --save-dev webpack
npm install --save-dev webpack@<version>
```

2. 如果你使用 webpack 4+ 版本，你还需要安装 CLI。

```javaScript
npm install --save-dev webpack-cli
```

> 对于大多数项目，我们建议本地安装。这可以使我们在引入破坏式变更(breaking change)的依赖时，更容易分别升级项目。通常，webpack 通过运行一个或多个 npm scripts，会在本地 node_modules 目录中查找安装的 webpack：

```javaScript
"scripts": {
    "start": "webpack --config webpack.config.js"
}
```

注意：当你在本地安装 webpack 后，你能够从 node_modules/.bin/webpack 访问它的 bin 版本。

#### 全局安装

1. 以下的 NPM 安装方式，将使 webpack 在全局环境下可用：
```javaScript
npm install --global webpack
```

> 不推荐全局安装 webpack。这会将你项目中的 webpack 锁定到指定版本，并且在使用不同的 webpack 版本的项目中，可能会导致构建失败。


#### 本地安装示范

1. 项目初始化以后执行安装命令
```javaScript
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install --save-dev webpack webpack-cli
```

![](https://pic.downk.cc/item/5e954fe8c2a9a83be596bf66.png)
2. 安装以后，查看安装版本
```javaScript
 npx webpack -v
```
![](https://pic.downk.cc/item/5e955024c2a9a83be596e683.png)
3. 此时会发现，直接执行webpack -v会报错，因为只是针对全局的命令，项目里面的话，需要借助npx，包括后面的其他webpack相关命令也是这样的。
安装完成以后，在项目根目录新建文件夹src，然后在src下新建index.js文件。

![](https://pic.downk.cc/item/5e955161c2a9a83be597b75a.png)

4. 做了最简单的操作以后，就可以进行打包了：


```javaScript
npx webpack
```
![](https://pic.downk.cc/item/5e9551afc2a9a83be597f96c.png)

> 这里使用命令npx webpack进行打包，没有指定入口文件，代表采用默认路径下（根目录-->src-->index.js）的文件作为入口文件，如果要采用其他文件作为入口文件，则需要在打包是进行指定：

![](https://pic.downk.cc/item/5e955296c2a9a83be59893bb.png)

> 上面这个就是指定根目录下的test.js作为入口文件。
打包完成以后，就会在根目录下生成一个dist文件夹。

![](https://pic.downk.cc/item/5e9552fcc2a9a83be598d971.png)

#### webpack配置文件
+  默认配置文件

> 在上面的简单操作中，我们没有对项目进行任何配置，这种零配置的项目是很弱的，在正常项目中，总会根据特定的需求进行相应的配置。

刚刚执行命令npx webpack test.js时，表示使用根目录下的test.js为入口文件进行打包处理，默认打包后的模块名称为main.js，放在根目录下的dist文件夹下。零配置的话，全部都是默认的，要想进行自定义，就需要使用到webpack的配置文件进行自己想要的配置。

```javaScript
npx webpack
npx webpack test.js

```
webpack有默认的配置文件webpack.config.js，刚刚上面的两个打包命令：
 都没有指定配置文件，则代表使用默认的配置文件webpack.config.js进行打包（上面项目中不存在webpack.config.js这个文件，则表示零配置。如果项目中存在这个配置文件，并且打包的时候，没有指定配置文件，那么就会默认选中webpack.config.js）。

+ 自定义配置文件

> 除了上面的默认配置文件以外，我们也可以自定义一个配置文件，然后在打包的时候进行指定就可以了：

```javaScript
 touch webpack.config.js
 npx webpack --config webpack.config.js

```
![](https://pic.downk.cc/item/5e9554f4c2a9a83be59a178d.png)

这个就表示指定使用webpack.config.js文件作为配置文件进行打包。

*webpack.config.js*
```javaScript
const path = require("path");
module.exports={
    mode:'development',  //模式：none  development  production
    // entry:"./src/index.js",   //入口文件，不指定打包后的名称，则默认为main.js
    entry:{
        main:"./src/index.js"   //指定打包后的文件名称为main.js
    },
    output:{
        path:path.resolve(__dirname,'dist'),  //打包后的文件存放的位置，必须是绝对路径
        filename:"[name].js"    //打包后的文件的名称，[]表示占位符，表示此处使用前面指定的名称，如果这里进行指定，则会覆盖前面的指定
    }
}
```

+  在目录下输入 npm init，执行以下操作即可创建package.json文件

> 我们还需要调整 package.json 文件，以便确保我们安装包是私有的(private)，并且移除 main 入口。这可以防止意外发布你的代码。

**package.json**

![](https://pic.downk.cc/item/5e955794c2a9a83be59bd123.png)

```javaScript
{
  "name": "demo",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "dependencies": {
    "webpack": "^4.42.1",
    "webpack-cli": "^3.3.11"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "LoveCatDog",
  "license": "ISC"
}
```

+ 除了上面这些简单配置外，还可以修改打包命令，只需要修改package.json里的scripts就可以了。
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190926224534828-1730262881.png)

 修改为：
![](https://img2018.cnblogs.com/blog/1304208/201909/1304208-20190926224621400-1699261067.png)

+  此时，我们就可以执行命令npm run bundle进行打包了。（因为npm run执行的命令，会优先使用项目工程里的包，效果和npx类似，所以这里不需要使用添加npx）

 ![](https://pic.downk.cc/item/5e955998c2a9a83be59d206e.png)

#### loader和module

1. loader是模块转换器，用于把模块原内容按照需求转换成新内容。
2. webpack是模块打包工具，而模块不仅仅是js，还可以使css、图片或者其他格式，但是webpack默认只知道如何处理js模块，那么其他格式的模块处理，就需要借助于loader了（loader里的配置，单个是对象，多个用数组，遵循自右向左，从下到上的顺序）。
3. module是模块，在webpack里一切皆模块，一个模块对应着一个文件。webpack会从配置的Entry开始递归找出所有依赖的模块。

> 当webpack处理到不认识的模块时，需要在webpack中的module处进行配置，当检测到时什么格式的模块，就使用什么loader来处理。

![](https://pic.downk.cc/item/5e955c59c2a9a83be59f13d8.png)

![](https://pic.downk.cc/item/5e955c0bc2a9a83be59ed7f3.png)

 上面，在入口文件中引入了一个图片模块以后，在进行打包，就直接报错了，这个时候，我们就需要使用到一个file-loader了。

 ##### file-loader

> 处理静态资源模块，就是当我们需要模块（txt、svg、csv、excel、图片等）仅仅是从源代码移动到打包目录的时候，就可以使用file-loader来处理了。其作用原理就是把打包入口中识别出的资源模块，移动到输出目录，并且返回一个地址名称。

要使用file-loader，首先需要进行安装：npm install file-loader -D

然后在配置文件*webpack.config.js*中配置使用：
![](https://pic.downk.cc/item/5e955d90c2a9a83be59fdefc.png)

再执行上面的打包操作：

![](https://pic.downk.cc/item/5e955f62c2a9a83be5a0fbf9.png)

最后的打包文件中，除了默认的出口文件外，还多了一个图片资源，就是上面引入的那个图片。但是此时有个问题，这个图片的名称改变了，因此，我们还需要进行相关的配置options。
```javaScript

 module: {
        rules: [{
            test: /\.(png|jpe?g|gif)$/, //jpe?g 同时匹配jpeg 和 jpg
            use: {
                loader: 'file-loader',
                options: {
                    //name:"[name].[ext]",//名称和后缀的占位符（使用资源的默认名称和后缀）
                    name: '[name]_[hash].[ext]',
                    outputPath: 'images/' //资源打包存放的位置
                }
            }
        }]
    }
```

![](https://pic.downk.cc/item/5e9561aac2a9a83be5a2c49d.png)

**补充：**
![](https://pic.downk.cc/item/5e956111c2a9a83be5a25cda.png)

##### url-loader
> 可以处理file-loader所有的事情，但是遇到jpg格式的模块，会把该图片转换成base64格式字符串，并打包到引入的js里。对小体积的图片比较合适，大图片就不合适了。

```javaScript
 npm install url-loader -D //安装url-loader 依赖
```
![](https://pic.downk.cc/item/5e956435c2a9a83be5a47ffb.png)

##### css-loader、style-loader和sass-
+ css-loader用于分析css模块之间的关系，并合并成一个css
+ style-loader会把css-loader生成的内容，以style挂载到页面的head部分
+ sass-loader用于把sass语法转换成css，依赖node-sass模块

```javaScript
 npm install style-loader css-loader sass-loader -D

```
![](https://pic.downk.cc/item/5e956445c2a9a83be5a48d19.png)

*更多loader配置，可以参看[官网loader](https://www.webpackjs.com/loaders/)介绍列表。*

##### Plugins

> plugin可以在webpack运行到某个阶段的时候，帮你做一些事情，类似于生命周期的概念。

+ html-webpack-plugin

html-webpack-plugin会在打包结束后，自动生成一个html文件，并把打包生成的js模块引入到该html中。
首先安装进行安装：
```javaScript
npm install --save-dev html-webpack-plugin
```
并在项目根目录下新建一index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="root"></div>

</body>

</html>
```

然后在配置文件中进行相关配置：
![](https://pic.downk.cc/item/5e9566a6c2a9a83be5a66812.png)

最后进行打包
![](https://pic.downk.cc/item/5e95676ec2a9a83be5a6dd88.png)

+ 多入口配置
> 在上面配置的基础上，我们在src下新建两个js，然后在入口处进行配置：

 ```javaScript
  entry: {
        // main: "./src/index.js" //指定打包后的文件名称为main.js
        index: "./src/index.js",
        list: "./src/list.js",
        detail: "./src/detail.js"
    },
 ```

然后打包，此时在dist文件下对应生成了3个出口文件，但是，在app.html文件中，却只引入了一个

 ![](https://pic.downk.cc/item/5e956857c2a9a83be5a7817d.png)

 + 多出口配置
 ```javaScript
  plugins: [
        new htmlWebpackPlugin({
            title: '首页', //用于生成页面的title元素
            filename: 'index.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'head', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['index']
        }),
        new htmlWebpackPlugin({
            title: '列表', //用于生成页面的title元素
            filename: 'list.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'body', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['list']
        }),
        new htmlWebpackPlugin({
            title: '首页', //用于生成页面的title元素
            filename: 'detail.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'body', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['detail']
        }),
    ]
 ```
![](https://pic.downk.cc/item/5e956a31c2a9a83be5a8f9cc.png)

 > 这样生成的每个html文件里，相应引入配置的js文件了。

 + clean-webpack-plugin
 > 目前，我们每次进行打包的时候，都需要先删除dist文件夹，然后再打包，否则之前同名的文件被覆盖了，但是不同名的文件会被保留。现在clean-webpack-plugin就可以替我们完成打包前的清除工作。

首先进行安装：

```javaScript
npm install --save-dev clean-webpack-plugin
```

然后使用就可以了

![](https://pic.downk.cc/item/5e956b13c2a9a83be5a9841b.png)

+ mini-css-extract-plugin
> 前面style-loader会把css-loader生成的内容，以style挂载到页面的head部分。这里mini-css-extract-plugin这是将css形成一个单独的文档。

首先进行安装：
```javaScript
npm install --save-dev mini-css-extract-plugin
```

然后引入并使用：
![](https://pic.downk.cc/item/5e956c1cc2a9a83be5aa339f.png)

### 完整的webpack.config.js
```javaScript
const path = require("path");
const htmlWebpackPlugin = require('html-webpack-plugin'); //打包结束后，自动生成一个html文件，并把打包生成的js模块引入到该html中
// const {
//     cleanWebpackPlugin
// } = require('clean-webpack-plugin'); //完成打包前的清除工作
//引入clean-webpack-plugin的包
const {
    CleanWebpackPlugin
} = require('clean-webpack-plugin');
const miniCssExtractPlugin = require('mini-css-extract-plugin'); //将css形成一个单独的文档

module.exports = {
    mode: 'development', //模式：none  development  production
    // entry:"./src/index.js",   //入口文件，不指定打包后的名称，则默认为main.js
    entry: {
        // main: "./src/index.js" //指定打包后的文件名称为main.js
        index: "./src/index.js",
        list: "./src/list.js",
        detail: "./src/detail.js"
    },
    output: {
        path: path.resolve(__dirname, 'dist'), //打包后的文件存放的位置，必须是绝对路径
        filename: "[name].js" //打包后的文件的名称，[]表示占位符，表示此处使用前面指定的名称，如果这里进行指定，则会覆盖前面的指定
    },
    module: {
        rules: [{
                test: /\.(png|jpe?g|gif)$/, //jpe?g 同时匹配jpeg 和 jpg
                use: {
                    loader: 'file-loader',
                    options: {
                        //name:"[name].[ext]",//名称和后缀的占位符（使用资源的默认名称和后缀）
                        name: '[name]_[hash].[ext]',
                        outputPath: 'images/' //资源打包存放的位置
                    }
                }
            },
            {
                test: /\.(png|jpe?g|gif)$/, //jpe?g 同时匹配jpeg 和 jpg
                use: {
                    loader: 'url-loader',
                    options: {
                        //name:"[name].[ext]",//名称和后缀的占位符（使用资源的默认名称和后缀）
                        name: '[name]_[hash].[ext]',
                        outputPath: 'images/', //资源打包存放的位置
                        limit: 2048, //小于2048，才转化为base64
                    }
                }
            },
            {
                test: /\.css$/,
                use: [miniCssExtractPlugin.loader, 'css-loader']
            },
            {
                test: /\.scss$/,
                use: ["style-loader", 'css-loader', 'sass-loader']
            },
        ]
    },
    plugins: [
        // new cleanWebpackPlugin(),
        new CleanWebpackPlugin(),
        new miniCssExtractPlugin({
            filename: '[name].css' //打包后的名称
        }),
        new htmlWebpackPlugin({
            title: '首页', //用于生成页面的title元素
            filename: 'index.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'head', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['index']
        }),
        new htmlWebpackPlugin({
            title: '列表', //用于生成页面的title元素
            filename: 'list.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'body', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['list']
        }),
        new htmlWebpackPlugin({
            title: '首页', //用于生成页面的title元素
            filename: 'detail.html', //输出的HTML文件名，默认是index.html
            template: './index.html', //模板文件路径，支持加载器，比如html!./index.html
            inject: 'body', //true | 'head' | 'body' | false 注入所有的资源到特定的template或者templateContent中
            //true 或者body ,表示所有的js资源被放置到body元素的底部，head则表示放到head元素中。
            chunks: ['detail']
        }),
    ]
}
```
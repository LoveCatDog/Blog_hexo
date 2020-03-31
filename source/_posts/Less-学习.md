---
title: Less 学习
date: 2020-03-11 14:21:35
tags: 
 - css
 - Less
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'Less 学习'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e688c3d98271cb2b81aa481.png'  #缩略图
---


### 一、 css预编译
常见的css预编译器有三种：less 、 sass 、 stylus。
Bootstrop使用的是less。
[在线编译](http://tools.jb51.net/code/less2css "在线编译")：http://tools.jb51.net/code/less2css

![less代码示例](https://pic.downk.cc/item/5e68842098271cb2b81756bf.png)


### 二、 Less
Less是一门css预处理语言，他扩展了css语言，增加了变量、Mixin、函数等特性，使css更容易维护和扩展。他不是一个直接使用的语言，而是一个生成css的语言。Less可以运行在Node或浏览器端。

Css计算：cacl（）

### 三、 使用方法
1. Node环境的使用方法
```javascript
//方法一:
npm install -g less
//方法二: 在vscode的应用商城中寻找：Easy LESS

```

2. 浏览器环境
* 1) 引入less文件，类似于css文件，单类型不一样。
```html
<Link rel=”stylesheet/less”  type=”text/css”  href=”style.less”/>
```
* 2) 引入解析less的less.js
```html
<script src=”less.js” type =”text/javascript”></script>
<script src="cdnjs.cloudflare.com/ajax/libs/less.js/3.8.1/less.min.js" ></script>  
```
> 下载地址：https://raw.github.com/less/less.js/v2.5.3/dist/less.min.js


### 四、 快速起步

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet/less" href="styles.less">
    <!-- <script src="less.js"></script> -->
    <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.8.1/less.min.js"></script>
</head>
<body>
    
</body>
</html>
```
### 五、 less 语法
####  1、变量
 * 1)普通变量，不能重复定义
    ```html
    @themeColor: green;
    ```

* 2)选择器变量
    ```html
    @mySelector: .bottom;
    ```

* 3)属性变量
    ```html
    @positionStyle: position;
    @absolute: absolute;
    ```

* 4) Url变量
    ```html
    @images: "../assets"; //需要添加引号
    ```

* 5) 声明变量
    ```html
    @Rules: {
    width: 1000px;
    border: 1px solid #f5f5f5;
    };
    ```

* 6) 变量运算

    ```html
    @width: 15px;
    @color: #111;
    ```

* 7) 变量的作用域
> 就近原则，不是指代码位置，而是值代码的层级结构

* 8)  用变量的定义变量
> 解析的顺序是从后向前逐层解析

    ```html
    @LoveCat: "I am loveCat";
    @var: "LoveCat";
    ```

####  2、嵌套
* 1) &符号，表示的是上一级选择器的名字

* 2) 嵌套覆盖原有样式
    ```html
    .value {
    color: red; //被覆盖，因为外层比嵌套的层级低
    }
    ```

#### 3、 媒体查询
    ```html
    body {
    @media screen {
        @media (max-width: 1200px) {
        width: 100px;
        }
    }
    }
    //生成的css
    // @media screen and (max-width: 1200px) {
    //   body {
    //     width: 100px;
    //   }
    // }
    ```

#### 4、混合方法

* 1)无参数方法，方法如声明的集合，使用值直接键入名称即可
    ```html
    .card() {
    //TODO:do something
    }
    ```

* 2) 具体参数方法
    ```html
    .setSize(@width_size,@height_size) {
    width: @width_size;
    height: @height_size;
    }
    ```

* 3) 默认参数方法
    ```html
    .border(@a:10px,@b:50px,@c:30px,@color:red) {
    border: solid 1px @color;
    box-shadow: @arguments; //指代的是 全部参数
    }
    ```

* 4) 不传参
    ```html
    .boxShadow(...) {
    box-shadow: @arguments;
    }
    ```
* 5) 方法的匹配模式

* 6) 方法的命名空间
    ```html
    #card() {
    background: #723232;
    .d(@w:300px) {
        width: @w;
        #a(@h:300px) {
        height: @h; //可以使用上一层传进来的方法
        width: @w;
        }
    }
    }
    ```

* 7) 条件语句：Less没有if / else 但是less具有一个when，and，not与“，”语法。
    ```html
    #card {
    // and 运算符 ，相当于 与运算 &&，必须条件全部符合才会执行
    .border(@width,@color,@style) when (@width>100px) and(@color=#999) {
        border: @style @color @width;
    }
    // not 运算符，相当于 非运算 !，条件为 不符合才会执行
    .background(@color) when not (@color>=#222) {
        background: @color;
    }
    // , 逗号分隔符：相当于 或运算 ||，只要有一个符合条件就会执行
    .font(@size:20px) when (@size>50px) , (@size<100px) {
        font-size: @size;
    }
    }
    ```

* 8)条件运算符
    ```html
        > >= = =< <
    ```

* 9) 循环语法：less没提供一个for等循环的方法，但是可以使用递归的方法实现
    ```html
    .generate-columns(4);
    .generate-columns(@n,@i:1) when (@i =< @n) {
    .columns-@{i} {
        width: (@i * 100% / @n);
    }
    .generate-columns(@n, (@i + 1)); //@i ++
    }

    /* 生成后的 CSS */
    .column-1 {
    width: 25%;
    }
    .column-2 {
    width: 50%;
    }
    .column-3 {
    width: 75%;
    }
    .column-4 {
    width: 100%;
    }
    
    ```

* 10) 方法中的important ：相当于每个属性都设置一个important 不循序覆盖
    ```html
    .pad_margin {
    padding: 15px 0px;
    margin: 0 15px 0 0;
    }
    ```

* 11) 多种颜色需要遍历
    ```html
    //定义一个背景颜色的集合
    @backgroundColor: rgb(109, 179, 226), rgb(250, 125, 119), rgb(72, 197, 174),
    rgb(250, 192, 84);

    //获取背景颜色的长度
    @backgroundLen: length(@backgroundColor);
    .loop(@index) when (@index < = @backgroundLen) {
    .backgroundcard(@index, extract(@backgroundColor, @index));
    .loop (@index+1);
    }
    .loop(1);

    .backgroundcard(@className,@colorValue) {
    //less：A
    .bottom_@{className} {
        background: @colorValue;
        transition: all 0.3s;
    }
    //less：B
    .order_box_item:hover .bottom_@{className} {
        height: 100%;
        z-index: -1;
    }
    }
    ```
#### 5、less注释：语法类似于js
> // : 单行注释 || /**/ : 多行注释

#### 6、属性的拼接语法
> +：代表逗号，+_代表的是空格

* 1) 空格
    ```html
    .Animation() {
    transform+_: scale(2);
    }
    .main {
    .Animation();
    transform+_: rotate(15deg);
    }

    /* //生成的 CSS 
        .main {
            transform: scale(2) rotate(15deg);
        }
    */
    ```

* 2) 逗号
    ```html
    .boxShadow() {
    box-shadow+: inset 0 0 10px #555;
    }
    .main {
    .boxShadow();
    box-shadow+: 0 0 20px black;
    }
    /* //生成后的 CSS 
    .main {
        box-shadow: inset 0 0 10px #555, 0 0 20px black;
    }*/
    ```

#### 7、继承（扩展） extend 是less的一个伪类，它可以继承所匹配声明中的全部样式
    ```html
    .animation {
    transition: all 0.3s ease-out;
    .hide {
        transform: scale(0);
    }
    }
    #main {
    // 继承animation
    &:extend(.animation);
    }
    #con {
    //继承 .animation .hide
    &:extend(.animation .hide);
    }
    ```

* 1)  all 全局搜索替换:匹配所有的声明
    ```html
    #main {
    width: 200px;
    &:after {
        content: "Less is good!";
    }
    }

    #wrap:extend(#main all) {
    // 继承#main的全部属性
    }
    ```

* 2) 扩展的注意事项
// 选择器和扩展之间 是允许有空格的：pre:hover :extend(div pre).
// 可以有多个扩展: pre:hover:extend(div pre):extend(.bucket tr) - 注意这 与 pre:hover:extend(div pre, .bucket tr)一样。
// 扩展必须在最后 : pre:hover:extend(div pre).nth-child(odd)。 如果一个规则集包含多个选择器，所有选择器都可以使用extend关键字。

#### 8、导入：less文件中可以引入其他的less文件 可使用关键字import

* 1) 导入less文件，可以省略后缀
    ```html
    import "index.less"; 
    // 或许 import "index";
    ```

* 2) @import 可以放在任何地方

* 3) reference:引入一个less 文件 但不会编译它
    ```html
    @import (reference) "bootstrap.less";
    #wrap: extend(.navbar all) {
    }
    // @import (reference)使用导入外部文件，只能在less中使用，主要是为了继承和方法，最终编译的时候里面的内容不会产生css。
    ```
* 4)  once:@import语句的默认行为。表明相同的文件只会被导入一次，随后的导入文件的重复代码都不会解析。
    ```html
    @import (once) "foo.less";
    @import (once) "foo.less"; //重复导入的代码不会被解析
    ```

* 5) multiple :使用@import (multiple)允许导入多个同名文件。
    ```html
    @import (multiple) "foo.less";
    @import (multiple) "foo.less";
    ```

#### 9、避免编译：???
    ```html
    #main {
    width: ~"calc(300px - 30px)";
    }
    ```

#### 10、less中可使用js
    ```html
    @content: ` "aaa" .toUpperCase() `;
    #randomColor {
    @randomColor: ~"rgb(`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`,`Math.round(Math.random() * 256)`)";
    }
    #wrap {
    width: ~"`Math.round(Math.random() * 100)`px"; //随机值（0~100）px
    &:after {
        content: @content; // AAA
    }
    height: ~"`window.innerHeight`px"; //由电脑而异
    //   alert: ~"`alert(1)`";
    #randomColor();
    background-color: @randomColor; //随机颜色
    }
    ```

### 六、less的函数
>  参考手册：
 http://lesscss.cn/functions/
 https://www.w3cschool.cn/less/namespaces_accessors.htm

+ 1) 判断类型：
    * Isnumber():判断是否为数字
    * Iscolor():判断是否是颜色
    * Isurl():判断是否是路径

+ 2) 颜色
    * saturate:增加一定数值的颜色饱和度
    * lighten:增加一定数值的颜色亮度
    * darken:降低一定数值的颜色亮度
    * fade:给颜色设置一定数值的透明度
    * mix:根据比例混合两种颜色

+ 3) 数学函数
    * ceil
    * floor
    * round
    * sqrt
    * abs
    * pow

### 七、代码实例（需与以上结合）
    ```html
    .order_box {
    .card();
    .boxShadow(1px, 4px, 30px, red);
    @Rules();
    background: url("@{images}/images/logo.png"); //变量使用大括号包裹

    &:after {
        content: @@var; //将@vart替换为@LoveCat
    }

    &_item {
        //&_item 理解为order_box_item
        width: calc((100% - @width * 4) / 4);

        display: inline-block;
        text-align: center;
        // padding: 15px 0px;
        // margin: 0 15px 0 0;
        .pad_margin() !important;
        cursor: pointer;
        background: #f5f5f5;
        position: relative;
        .title {
        color: #666;
        }
        .value {
        color: @color * 3; //#333
        font-weight: 500;
        font-size: 20px;
        }
        @{mySelector} {
        //   position: absolute;
        @{positionStyle}: @absolute; //变量名 必须使用大括号包裹
        //   width: 100%;
        //   height: 10px;
        .setSize(100%, 10px);
        background: @themeColor;
        bottom: 0;
        }
    }
    }
    ```
### 补充

【转载来自简书】：https://www.jianshu.com/p/868d1bcbe12a

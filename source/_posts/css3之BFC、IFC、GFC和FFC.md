---
title: css3之BFC、IFC、GFC和FFC
date: 2020-04-13 15:50:50
tags:
 - css
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'css3之BFC、IFC、GFC和FFC'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e94196cc2a9a83be5d27ec9.png'  #缩略图
---


### css3之BFC、IFC、GFC和FFC

![](https://pic.downk.cc/item/5e94196cc2a9a83be5d27ec9.png)
### BFC 

> 块级格式化上下文：Block Formatting Contexts
页面上的一个隔离的渲染区域，容器里面的子元素不会再布局上影响到外面的元素。
那BFC一般有什么用呢？比如常见的多栏布局，结合块级别元素浮动，里面的元素则是在一个相对隔离的环境里运行。

常见的会生成BFC的元素：
根元素
float不为none
position为absolute或fixed
display为inline-block, table-cell, table-caption, flex,inline-flex 
overflow不为visible 

#### 自适应两栏布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>自适应两栏布局</title>
</head>
<style>
    body {
        width: 300px;
        position: relative;
    }

    .aside {
        width: 100px;
        height: 150px;
        float: left;
        background: #f66;
    }

    .main {
        height: 200px;
        background: #ccd1ff;
    }
</style>

<body>
    <div class="aside"></div>
    <div class="main"></div>
</body>

</html>
```
> 每个元素的margin box的左边， 与包含块border box的左边相接触：因aside 存在float ，所以导致main左边对齐。

![](https://pic.downk.cc/item/5e9412cfc2a9a83be5cec891.png)

> 由于BFC的区域不会与float box重叠。此时，如果想要两个元素不再重叠，只需要让第二个元素形成BFC就可以了：

```html
.main {
        height: 200px;
        background: #fcc;
        overflow: hidden;
    }
```

![](https://pic.downk.cc/item/5e9412e1c2a9a83be5ced1a0.png)

#### 清除内部浮动
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>清除浮动</title>
</head>
<style>
    .par {
        border: 5px solid #fcc;
        width: 300px;
    }

    .child {
        border: 5px solid #f66;
        width: 100px;
        height: 100px;
        float: left;
    }
</style>

<body>
    <div class="par">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</body>

</html>
```
> 由于内部元素产生了浮动，所以父级元素会高度丢失，产生下面的效果：

![](https://pic.downk.cc/item/5e9413c8c2a9a83be5cf4eab.png)

> 由于计算BFC的高度时，浮动元素也参与计算，为达到清除内部浮动，我们可以触发par生成BFC，那么par在计算高度时，par内部的浮动元素child也会参与计算。

![](https://pic.downk.cc/item/5e941428c2a9a83be5cf79f4.png)
#### 防止垂直 margin 重叠
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>防止垂直 margin 重叠</title>
</head>
<style>
    p {
        color: #f55;
        background: #ccd1ff;
        width: 200px;
        line-height: 100px;
        text-align: center;
        margin: 100px;
    }
</style>

<body>
    <p>Haha</p>
    <p>Hehe</p>
</body>

</html>
```
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>防止垂直 margin 重叠</title>
</head>
<style>
    p {
        color: #f55;
        background: #ccd1ff;
        width: 200px;
        line-height: 100px;
        text-align: center;
        margin: 100px;
    }
</style>

<body>
    <p>Haha</p>
    <p>Hehe</p>
</body>

</html>
```
> Box垂直方向的距离由margin决定。由于属于同一个BFC的两个相邻Box的margin会发生重叠，因此，上面的两个p元素就会产生margin重叠。

![](https://pic.downk.cc/item/5e941670c2a9a83be5d0a3b2.png)
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>防止垂直 margin 重叠</title>
</head>
<style>
    p {
        color: #f55;
        background: #ccd1ff;
        width: 200px;
        line-height: 100px;
        text-align: center;
        margin: 100px;
    }

    .wrap {
        overflow: hidden;
    }
</style>

<body>

    <div class="wrap">
        <p>Haha</p>

    </div>
    <p>Hehe</p>
</body>

</html>
```
> 为了避免这种margin重叠，我们可以在p外面包裹一层容器，并触发该容器生成一个BFC。那么两个P便不属于同一个BFC，就不会发生margin重叠了。

![](https://pic.downk.cc/item/5e941685c2a9a83be5d0b4b9.png)

### IFC
IFC(Inline Formatting Contexts)直译为"内联格式化上下文"，IFC的linebox（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响) 

### FFC
FFC(Flex Formatting Contexts)直译为"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container）。
### GFC
GFC(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。 



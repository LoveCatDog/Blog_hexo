---
title: vue中props传值失败
date: 2020-01-06 16:55:59
tags: vue
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'vue中props传值失败,输出undefined'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://th.wallhaven.cc/small/nk/nko8m7.jpg'  #缩略图
---
## vue props传值失败 输出undefined

**背景：父组件传值给子组件，子组件通过props接收父组件的值，但是在vue中 子组件通过props获取到的值为undefined？**


![加油！](https://th.wallhaven.cc/small/4x/4xrzxv.jpg "会吃鱼的猫")


因为vue语法中规定HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。
这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名：
>   

 ### 例子一：
 
```HTML
<Children :data = "goodId" />
//因为html不区分大小写，所有值都会转化为小写，所以会获取不到值。
<Children :data = "good-id" />
 ```
 ### 例子二:
【 请注意】以下代码中data值不能使用驼峰命名，否则会导致传值失败

 > 父组件

 ```HTML
//html结构中
<GoodRecommend :recommendid="data" />
```
``` javaScript
//vue实例中

data() {
    return {
    data：'1'
    }
}，
```


 > 子组件
```javaScript
props: {
    recommendid: {
        type: Number,
        default: 1
    }
},
mounted() {
    this.getFeath();
},
methods: {
    getFeath() {
        let categoryId = this.recommendid; //获取商品id
        console.log("categoryId", categoryId);//获取父组件传来的值（recommendid：1）
    } 
}

```

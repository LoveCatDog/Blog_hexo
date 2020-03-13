---
title: css3动画之悬浮
date: 2020-03-12 19:24:29
tags:
 - css
 - Less
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'css3动画之悬浮'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e6af3dae83c3a1e3a616f45.png'  #缩略图
---

![示例](https://pic.downk.cc/item/5e6af342e83c3a1e3a611cbe.png)

### 语法
 + 列表函数
     - 获取列表的长度  length(@backgroundColor)  //4
     - 获取列表元素  extract(@backgroundColor, 3)  //rgb(72, 197, 174)
 + 循环函数
     - loop定义循环次数，when条件判断，符合进入函数，不符合不进入函数。之后次数+1，形成循环。
     - loop函数调用，直接传值1。

### 题目
1. 鼠标悬浮之后，底部颜色条动画过渡到高度100%;
2. 使用less语法，遍历颜色。

```html
<template>
  <div style="padding: 20px;">
    <h4 style="padding: 10px 0;">动画css</h4>
    <ul class="order_box">
      <li v-for=" orderItem of orderList" :key="orderItem.id" class="order_box_item">
        <p class="title">{{orderItem.title}}</p>
        <p class="value">{{orderItem.value}}</p>
        <div :class="'bottom  bottom_'+orderItem.id "></div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      count: 0, //计数
      firstName: "Foo",
      lastName: "Bar",
      orderList: [
        { id: 1, value: 1, title: "待支付", color: "rgb(109, 179, 226)" },
        { id: 2, value: 4, title: "待发货", color: "rgb(250, 125, 119)" },
        { id: 3, value: 30, title: "待收货", color: "rgb(72, 197, 174)" },
        { id: 4, value: 1, title: "待评价", color: "rgb(250, 192, 84)" }
      ]
    };
  },
  methods: {
    increment() {
      this.count++;
    }
  }
};
</script>
<style lang="less" scoped>
//1)普通变量，不能重复定义
@themeColor: green;

//2)选择器变量
@mySelector: .bottom;

// 3)属性变量
@positionStyle: position;
@absolute: absolute;

//6) 变量运算

@width: 15px;
@color: #111;
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
//亲，您少些了下面很多重复的代码 css A
// .bottom_1 {
//   background: rgb(109, 179, 226);
//   transition: all 0.3s;
// }
// .bottom_2 {
//   background: rgb(250, 125, 119);
//   transition: all 0.3s;
// }
// .bottom_3 {
//   background: rgb(72, 197, 174);
//   transition: all 0.3s;
// }
// .bottom_4 {
//   background: rgb(250, 192, 84);
//   transition: all 0.3s;
// }

.order_box {
  width: 1000px;
  position: relative;

  &_item {
    //&_item 理解为order_box_item
    width: calc((100% - @width * 4) / 4);
    margin: 0 15px 0 0;

    display: inline-block;
    text-align: center;
    padding: 15px 0px;
    cursor: pointer;
    background: #f6f6f6;
    position: relative;

    &:hover {
      background: transparent;
      .title,
      .value {
        color: #fff;
      }
      // css B
      //   .bottom_1 {
      //     height: 100%;
      //     z-index: -1;
      //   }
      //   .bottom_2 {
      //     height: 100%;
      //     z-index: -1;
      //   }
      //   .bottom_3 {
      //     height: 100%;
      //     z-index: -1;
      //   }
      //   .bottom_4 {
      //     height: 100%;
      //     z-index: -1;
      //   }
    }

    .title {
      color: #666;
      z-index: 10;
      font-size: 12px;
      padding: 10px 0;
    }
    .value {
      color: @color * 3; //#333
      font-weight: 500;
      font-size: 26px;
      z-index: 10;
    }
    @{mySelector} {
      //   position: absolute;
      @{positionStyle}: @absolute; //变量名 必须使用大括号包裹
      width: 100%;
      height: 10px;
      //   background: @themeColor;
      bottom: 0;
    }
  }
}
</style>
```



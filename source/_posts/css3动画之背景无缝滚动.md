---
title: css3动画之背景无缝滚动
date: 2020-03-13 10:48:47
tags:
 - css
 - 动画
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'css3动画之背景无缝滚动'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://pic.downk.cc/item/5e6af516e83c3a1e3a620715.jpg'  #缩略图

---
![示例](https://pic.downk.cc/item/5e6b02dbe83c3a1e3a67bed0.png)

> （1） 背景来自jq22：http://www.jq22.com/demo/html5bg20151116/
（2） 动画来自：https://segmentfault.com/a/1190000003721884

```html
<template>
  <div class="body">
    <div class="page">
      <div class="page_box">
        <ul class="box item1">
          <li></li>
        </ul>
        <ul class="box item2">
          <li></li>
        </ul>
      </div>
      <div class="title">背景无缝左右滚动</div>
    </div>
  </div>
</template>
<style lang="less" scoped>
/*核心css*/
@keyframes moveup {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-100%);
  }
}
/*样式*/
.page {
  margin-top: 200px;
  height: 100vh;
  overflow: hidden;
  position: relative;
  .title {
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    font-size: 48px;
    color: rgba(255, 255, 255, 0.8);
    font-weight: 600;
  }
  .page_box {
    width: 200vw;
    .box {
      animation: moveup 20s linear infinite;
      margin: 0;
      display: inline-block;
      float: left;
      li {
        background: url(https://pic.downk.cc/item/5e6af516e83c3a1e3a620715.jpg)
          no-repeat center center;
        width: 100vw;
        height: 100vh;
        background-size: cover;
        list-style: none;
      }
    }
  }
}
</style>



```

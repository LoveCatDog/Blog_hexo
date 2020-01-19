---
layout: _posts
title: Vuex是什么？
date: 2020-01-19 16:17:18
tags: vue, vuex
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: ' Vuex是什么,让我们慢慢细读...'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://vuex.vuejs.org/flow.png'  #缩略图
---
## What Is Vuex？
 Vuex是一个专为Vue.js应用程序开发的【状态管理模式】。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。是不是还有点迷？我们往下看。

### What Is “状态管理模式”？
让我们从一个简单的Vue的计数demo开始；
```HTML
<template>
  <div class="test">{{count}}</div>
</template>
<script>
export default {
  name: "test",
  data() {
    return {
      count: 0 //计数
    };
  },
  methods: {
    inCrement() {
      this.count++;
    }
  }
};
</script>
<style lang="less" scoped>
.test {
}
</style>
```
> 这个状态自管理应用包含以下几个部分
1. state:驱动应用的数据源;
2. view:以声明方式将state映射到视图；
3. actions：相应在view上的用户输入导致的状态变化。
以下是一个表示“单向数据流”理念的简单示意图：

![单向数据流简单示意图](https://vuex.vuejs.org/flow.png)
但是，当我们的应用遇到【多个组件共享状态】时，单向数据流的简洁性容易被破坏；
1. 多个视图依赖于同一个状态；
2. 来自不同视图的行为需要变更同一个状态。
对于问题一，传参的方法对于多层嵌套的组件将会非常繁琐，并且对于兄弟组件的状态传递无能为力。
对于问题二，我们经常会采用父子组件直接引用或通过事件来变更和同步状态的多份拷贝，以上这些模式非常脆弱，通常会导致无法维护代码。

为此我们将组件的共享状态抽取出来，以一个全局单例模式管理。将组件树构成一个巨大的“视图”，不管在树的哪个位置。任何组件都能获取状态或者触发行为！

通过定义和隔离状态管理中的各种概念并通过强制规则维持视图和状态间的独立性，我们的代码将会变得更结构化且易维护。

这就是 Vuex 背后的基本思想，借鉴了 Flux、Redux 和 The Elm Architecture。与其他模式不同的是，Vuex 是专门为 Vue.js 设计的状态管理库，以利用 Vue.js 的细粒度数据响应机制来进行高效的状态更新。
![状态管理库的示例图](https://vuex.vuejs.org/vuex.png)


### How To Use Vuex

Vuex 可以帮助我们管理共享状态，并附带了更多的概念和框架。这需要对短期和长期效益进行权衡。

如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex。一个简单的 store 模式就足够您所需了。但是，如果您需要构建一个中大型单页应用，您很可能会考虑如何更好地在组件外部管理状态，Vuex 将会成为自然而然的选择。引用 Redux 的作者 Dan Abramov 的话说就是：

> Flux 架构就像眼镜：您自会知道什么时候需要它。

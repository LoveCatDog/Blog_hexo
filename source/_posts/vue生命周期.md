---
layout: posts
title: vue生命周期
date: 2020-01-06 10:38:30
tags: vue
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'vue生命周期分析'
top_img: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=523850375,708362261&fm=26&gp=0.jpg' #设置顶部图
cover: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1485227289,2712798579&fm=11&gp=0.jpg'  #缩略图
---
### 实现vue生命周期

开发人员提供了一个Web开发人员可以在Vue.js应用程序的整个生命周期中使用的各种方法的讨论。

生命周期钩子是在Vue对象生命周期的某个阶段执行的已定义方法。从初始化开始到它被破坏时，对象都会遵循不同的生命阶段。这是一个vue生命周期的导购图，表示挂钩顺序。（这给了用户在不同阶段添加自己代码的机会。）

#### beforeCreate（对象诞生）

> Vue对象新的方法实例化。它创建了了一个Vue类的对象来处理DOM元素。对象这个生命周期阶段可以通过beforeCreated挂钩来访问。我们可以在这个钩子中插入我们的代码，在对象初始化之前执行。

#### created(创建：具有默认特性的对象)

> 在这个生命阶段，对象及其事件完全初始化。 created 是访问这个阶段并编写代码的钩子。

#### beforeMounted（对象在DOM中适合形状）

> 这个钩子被调用 beforeMounted。在这个阶段，它检查是否有任何模板可用于要在DOM中呈现的对象。如果没有找到模板，那么它将所定义元素的外部HTML视为模板。

#### mounted（Dom准备就绪）
> 一旦模板准备就绪。它将数据放入模板并创建可呈现元素。用这个新的数据填充元素替换DOM元素。这一切都发生在mounted钩子上

#### beforeUpdate（更改已完成，但尚未准备好更新DOM）

> 在外部事件/用户输入beforeUpdate发生更改时，此钩子即 在反映原始DOM元素的更改之前被触发。
为了解决这个问题 beforeUpdated，我添加了下面的代码。它通过更新DOM来更改运行时中的hello_message。

#### updated （更新：在DOM中呈现的更改）
> 然后，通过实际更新DOM对象并触发updated，屏幕上的变化得到呈现 。

#### beforeDestroy（对象准备死掉）
> 就在Vue对象被破坏并从内存中释放之前， deforeDestroy 钩子被触发，并允许我们在其中处理我们的自定义代码。
为了激发这个钩子，我添加了下面的代码来销毁Vue对象。

#### beforeDestroy(销毁:对象停止并从内存中删除)

> 该 destroyed 钩子被成功运行销毁对象上调用。

### 概要

> 我们可以使用生命周期钩子在Vue对象生命周期的不同阶段添加我们的自定义代码。它将帮助我们控制在DOM中创建对象时创建的流程，以及更新和删除对象。

### 示意图

![vue生命周期](https://cn.vuejs.org/images/lifecycle.png "vue生命周期导购图")


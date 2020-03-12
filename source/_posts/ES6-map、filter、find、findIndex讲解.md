---
title: ES6-map、filter、find、findIndex讲解
date: 2020-03-12 10:23:15
tags: 
 - ES6
 - javascript
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'ES6-map、filter、find、findIndex讲解'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://w.wallhaven.cc/full/4v/wallhaven-4vr5pp.png'  #缩略图
---

### map （映射）
    ```javascript
    var arrList =[1,2,3,4]; 
    console.log(arrList.map(item => item * item ))
    // [1, 4, 9, 16]
    ```

### filter （过滤筛选）

```javascript
var users = [
  {name: "张含韵", "email": "zhang@email.com"},
  {name: "江一燕",   "email": "jiang@email.com"},
  {name: "李小璐",  "email": "li@email.com"}
];
//获取所有人的email
var emailList=users.map(userItem => userItem.email);
console.log(emailList.join(','))
// zhang@email.com,jiang@email.com,li@email.com

//获取指定人的email(使用正则匹配)
var liEmail=emailList.filter(email=>/^li/g.test(email))
console.log(liEmail.join('')) 
// li@email.com
```

### find
```javascript
[1, 4, -5, 10].find((n) => n < 0)    // -5
//但是如果将n < 0 , 替换成 n < 20,得到的结果是1 ，你得细品，找规律，
```

### findIndex
```javascript
[1, 4, -5, 10].findIndex((value,index,arr) => console.log(value,index,arr));
/**
 * value:值  index：值对应的下标 arr：数组
  1 0  [1, 4, -5, 10]
  4 1  [1, 4, -5, 10]
 -5 2  [1, 4, -5, 10]
 10 3  [1, 4, -5, 10]
 **/
```

### some （至少一个符合）
```javascript
//只要数组值至少一个值符合（三的倍数）则为true
var numbers = [2, 4, 10, 6, 8];
    var a = numbers.some((item,index)=>{
        if(item%3===0){
            return true;
        }else{
            return false;
        }
    });
    console.log(a)
```

### every （任何一个都需要符合）
```javascript
//如果数组中每个值都符合（偶数）则为true
var numbers = [2, 4, 10, 4, 8];
    var a = numbers.every((item,index)=>{
        if(item%2===0){
            return true;
        }else{
            return false;
        }
    });
    console.log(a)
```





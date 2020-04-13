---
title: javascript 中五种实现B继承A的方法
date: 2020-04-10 16:16:16
tags: 
 - javascript
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'javascript 中五种实现B继承A的方法'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1756956988,136600965&fm=26&gp=0.jpg'  #缩略图
---


![会吃鱼的猫](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1756956988,136600965&fm=26&gp=0.jpg "会吃鱼的猫")

### javascript 中五种实现B继承A的方法

#### 1.继承第一种方式：对象冒充
```javascript
   	function Parent(userName) {
            this.userName = userName;
            this.hello = function () {
                alert(this.userName)
            }
        }

        function Child(userName, passWord) {
            this.method = Parent; // Child 中的method作为临时属性，指向Parent对象
            this.method(userName);
            delete this.method; //销毁this.method属性，此时Child 已经拥有Parent的所有属性和方法

            this.passWord = passWord;
            this.world = function () {
                alert(this.passWord);
            }
        }


        var parent = new Parent('wujia');
        var child = new Child('guozheng', '123');
        parent.hello();
        child.hello();
        child.world();
```
#### 2.继承第二种方式：call()方法 
> 第一个参数的值赋值给类中出现的this，第二个参数开始依次赋值给类所接受的参数

```javascript
 		function test(str) {
            alert('1:' + this.name + '  ' + str)
        }
        var object = new Object();
        object.name = 'wujia';
        test.call(object, 'guozheng');

        function Parent1(userName) {
            this.userName = userName;
            this.hello = function () {
                alert('2:' + this.userName)
            }
        }

        function Child1(userName, passWord) {
            Parent1.call(this, userName); //继承了test的方法和属性
            this.passWord = passWord;
            this.world = function () {
                alert('3:' + this.passWord);
            }
        }
        var parent = new Parent1('jia');
        var child = new Child1('zheng', '123');
        parent.hello();
        alert('2')
        child.hello();
        alert('3')
        child.world();
```
#### 3.继承第三种方式：apply()方法 
> 第一个参数为赋值给类中出现的this，第二个参数为数组类型

``` javascript
		function Parent2(userName) {
            this.userName = userName;
            this.hello = function () {
                alert('2:' + this.userName)
            }
        }

        function Child2(userName, passWord) {
            Parent2.apply(this, new Array(userName)); //继承了test的方法和属性
            this.passWord = passWord;
            this.world = function () {
                alert('3:' + this.passWord);
            }
        }
        var parent = new Parent2('jia1');
        var child = new Child2('zheng2', '1233');
        parent.hello();
        child.hello();
        child.world();
```

####  4.继承第四种方式：原型链方式
>  即子类通过prototype 将所有在父类中通过prototype追加的属性和方法都追加到Child4，从而实现继承

```javascript
 		function Person() {
            Person.prototype.hello = "hello";
            Person.prototype.sayHello = function () {
                alert(this.hello);
            }
        }

        function Child4() {}

        Child4.prototype = new Person(); //Child4 继承Person
        Child4.prototype.world = 'world';
        Child4.prototype.sayWorld = function () {
            alert(this.world);

        }
        var city = new Child4;
        city.sayHello();
        city.sayWorld();

```

#### 5.继承第五种方式：混合方法（混合call和原型链方式）

```javascript
		function Parent5(hello) {
            this.hello = hello;
        }

        Parent5.prototype.sayHello = function () {
            alert(this.hello)
        }

        function Child5(hello, world) {
            Parent5.call(this, hello); //将父类的属性继承过来
            this.world = world; //新增属性
        }

        Child5.prototype = new Parent5(); //继承Parent5 继承
        Child5.prototype.sayWorld = function () { //新增方法
            alert(this.world);
        }
        var city = new Child5('wjia', 'zheng');
        city.sayHello();
        city.sayWorld();
```
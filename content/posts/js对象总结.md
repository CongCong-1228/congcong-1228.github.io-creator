---
title: "Js对象总结"
date: 2021-12-13T15:28:51+08:00
draft: false
---

# JS对象总结

在说js对象之前，先回顾一下js的七种数据类型，分别是number,string,boolean,symbol,undefined,null,object。五种falsy值，undefined,null,'',0,NaN。

## 1，声明对象

对象是键值对的集合，其中键名是字符串，就算不加引号，js也会把他转成字符串。键值可以是数值，字符串，数组，函数，对象等。普遍使用以下代码声明一个对象。
```
let obj = {
    name:'jack',
    arr:[],
    func: (){
        console.log('function')
    }
    obj1:{
        a:'hello'
    }
}
```
## 2，增删改查

* (1) 删 
```
delete obj.name        //直接删除一个键值对
obj.name = undefined   //将一个键值改成undefined（属性名依然存在）
name in obj            //判断属性名是否存在

```
* (2) 查
```
Object.keys(obj)       //查看所有属性名
Object.values(obj)     //查看所有属性值
console.dir(obj)       //查看所有属性（包括隐藏属性）
obj.hasOwnProperty('') //检查该属性是否自身所有
obj['key']             //查看属性值

```
* (3) 增
  
```
obj.name = 'jack'                  //直接赋值
obj['name'] = 'jack'               //直接赋值，和上面一样作用
Object.assign(obj,{'name':'jack'}) //批量赋值
```
* (4) 改
改的操作和增的操作基本一致。

## 3，原型链

我们知道每个对象都有隐藏属性__proto__，指向自己的原型，那么如果要自己增加原型该怎么做呢。
首先我们自己创建一个原型对象。
```
let common = {
    country:'china',
    address:'Asia',
    getCountry(){
        console.log(this.country)
    }
}
// 先声明一个对象，他有自己的属性和函数

let obj = Object.create(common)   
//然后使用Object.create()方法,以common对象为原型，创建一个新的对象obj

Object.assign = (obj,{'name':'jack'})
//然后使用Object.assign()批量赋值给Obj对象

obj.getCountry()                  
console.log(obj.address)
//这样我们就可以直接使用原型common的属性。

```

## 4，类

上面我们讲了原型链，类的实现就是根据原型链来的。我们通常在声明一个类的时候，都会首先创建构造函数（创建一个对象的函数），函数有一个属性叫做prototype，要知道在js中函数也是一种对象，因此函数的prototype属性，可以理解为一个普通对象的__proto__属性。就是一个函数的prototype属性是指向他的原型的。
类的话可以理解为一类事物，比如说动物，他们都有共同的属性，都被称为动物，都会吃东西，都会跑。但是种类（名字）不同，他们的这种共有属性，我们可以理解为一类对象的原型。我们可以通过prototype来实现。

```
function Animal(name){
    name = this.name
}
//这就是一个简单的构造函数，他们表示动物都有自己的名字，名字是不同的。

Animal.prototype.run = function(){
    console.log(this.name + 'can run')

}
Animal.prototype.eat = function(){
    console.log(this.name + 'can eat')
}
//上面几行代码，我们声明的是动物这个类，都会跑和吃。可以理解在他们的原型Animal上添加了两个函数，在以后声明对象的时候可以随时调用。

let animal1 = new Animal('Dog')
//通过构造函数，我们声明一个animal1，给他传入的名字是dog。

animal1.eat()
animal1.run()
//我们可以直接调用Animal方法

```
这样我们便通过原型的方法来实现了创建一个类。在ES6，js引入了一种新的语法class，class的用法非常简单，他和原型都是用来给对象分类的，现在我们用class语法来实现创建一个类。

```
class Animal{
    constructor(name){
        this.name = name
    }
    //构造函数
    run(){
        console.log(this.name + 'can run')
    }
    eat(){
        console.log(this.name + 'can eat')
    }
    //类似原型带的函数
}
let animal1 = new Animal('dog')  //使用new创建一个对象

```
 
这里new x()自动做了这些事
* 自动创建了空对象
* 自动为空对象关联原型，原型地址指定为x.prototype
* 自动将空对象作为this关键字运行构造函数
* 自动return this

以上代码讲述了如何用class创建对象，相比之下，class确实写起来更方便，但是如果要理解如何实现的话，我觉得prototype的方法更能让人读懂实现原理，每个人的理解应该不同，我觉得都学会使用就可以的。

公式
**对象.__proto__ = 构造函数.prototype**


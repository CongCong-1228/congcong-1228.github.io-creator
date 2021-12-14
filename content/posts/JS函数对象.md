---
title: "JS函数对象"
date: 2021-12-14T15:20:56+08:00
draft: false
---

# JS函数对象

`在讲函数之前，我们需要先知道函数也是一种对象。`

## 1,定义函数

```javascript
function fn(形参1,形参2){
    语句
    return 返回值
} //具名函数

let a = function(x,y){
} //匿名函数

let f1 = ()=>{}
 //箭头函数

let f2 = new Function('x','y','return x+y')
//使用构造函数，基本没人用，可以让你知道所有函数都是Function构造的，包括Object，Array，Function本身。

fn()
//函数调用

```
## 2，函数要素（每个函数都有）

* 调用时机
函数在调用的时候，才会去使用，并不是声明了直接使用，注意调用时机。

* 作用域
每个函数都会默认创建一个作用域，一般都在{}中，其中在全局作用域声明的变量是全局变量，比如window的属性，其他的变量都是局部变量。作用域遵循`就近原则`。

* 闭包
如果一个函数用到了外部的变量，那么这个函数加这个变量，就叫做闭包。
```javascript
function f1(){
    let a = 2
    function f2(){
        console.log(a)
    }
}
```
上述代码就是一种简单的闭包。

* 形式参数
在创建一个函数时，会给这个函数赋予参数，这些就是形式参数，并不是实际的参数，实际的参数在调用函数时传递，然后赋值给形参。
```javascript
function fn(a,b){
    return a+b
}
fn(1,2)
```
上述代码中的a,b是形式参数。1，2是实际参数，会被赋值给a，b。

* 返回值
每个函数都有返回值，没有写return，默认返回值是undefined。函数执行完了才会返回，只有函数有返回值。
```javascript
function fn(){
    
}
//不指定return 默认返回值为undefined
function f1(a,b){
    return a+b
}
```

* 调用栈
JS引擎在调用一个函数前，会把函数所在的环境push到一个数组里，这个数组叫做调用栈，等函数执行完，就会把环境pop出来，然后返回到之前的环境中，继续执行代码。如果调用栈中压入的帧过多，程序就会崩溃。（爆栈）

* arguments（箭头函数没有）

arguments是包含了函数所有参数的伪数组（伪数组指的是没有pop，push等方法，原型直接指向Object的数组）。
```javascript
function fn(){
    console.log(arguments)
    console.log(...arguments) //...是es6新的语法，因为不确定arguments中有几个，用...来展开这些参数。
}
fn(1,2)
此时fn会打印出arguments
```
也就是说在你传递参数，调用函数之前，浏览器会把你传递的参数放在arguments中，方便你以后用来调用这些参数。

* this（箭头函数没有）
JS在每个函数中都加了this，this的作用是用来帮助函数获取一个未知的对象，就是用来引用未来的对象。我们通常使用call方法来传递this。
```javascript
function fn(){
    console.log(this.name)
}
fn.call({name:'1'})
```
这样就是通过call来为函数传递了一个对象。不过这个一般搭配对象来使用

```javascript
let obj = {
    name:'jack',
    fn(){
        console.log(this.name)
    }
}
obj.fn()  === obj.fn.call(fn) //如果这样调用fn方法，等价于obj.fn.call(fn)，js会默认帮你把fn前面的obj传进去，作为你要传递的对象。
obj.fn.call({name:'Tom'})  //使用call方法调用的话，传进去的对象就是你自己指定的对象，这样更容易理解一些。

```
`需要注意的是，对象中的函数和对象是完全不同的两个东西，他们没有任何联系，不要弄混淆。`

this的存在就是我们想让函数获取对象的引用，但是不想通过变量名实现，JS就通过这个额外的this来实现，类似于python中的self参数。我们可以再通过一个例子来理解一下this，比如下面的代码
```javascript
Array.prototype.forEach2 = function(fn){
    for(let i =0;i<this.length;i++){
        fn(this[i],i)
    }
}
let arr = [1,2,3,4]
arr.forEach2((item)=>console.log(item)) === arr.forEach2.call(arr,(item)=>console.log(item))
//上述两种调用方法是相同的，只是大家都普遍使用第一种调用方法，但第二种方法更能说明this的作用是什么。

```
上述代码就是forEach实现的原理，就是通过this来获取我们的数组，然后来进行使用的。


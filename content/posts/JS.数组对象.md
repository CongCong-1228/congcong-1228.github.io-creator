---
title: "JS.数组对象"
date: 2021-12-13T20:12:37+08:00
draft: false
---

# JS数组对象

## 1，声明数组

```javascript
let arr = [1,2,3]
let arr = new Array(1,2,3)
//直接声明
let arr = '1,2,3'.split(',')
let arr = '123'.split('')
Array.from('123')
//字符串转数组
arr1.concat(arr)  //concat合并两个数组
arr1.slice(1)     //从第一个开始切
arr1.slice(0)     //切全部数组

```

## 2，增删改查

因为数组也是对象，数组的增删改查都可以使用对象的方法来达成，但是不够靠谱，所有我们这里只说数组独有的方法。

* (1) 删
  
```javascript
arr.pop()     //删除数组最后一个元素
arr.shift()   //删除数组第一个元素
arr.splice(start,n,'a','b')  //splice方法接受参数，第一个参数表示从第几个开始删除，第二个参数表示删除几个，第三个参数表示用什么来替换。
```
* (2) 增
```javascript
arr.push('a')    //从尾部增加一个元素
arr.unshift('a') //从头部增加一个元素
```
* (3) 查

```javascript
let arr = [1,2,3]
for(let i = 0; i<arr.length;i++){
    console.log(arr[i])
}
//使用for循环遍历数组，得到数组中每个元素

arr.indexOf(value)    //查找元素下标
arr.find(fn())        //找到符合条件的元素
arr,findIndex(fn())   //找到符合条件的元素下标

```
* (4) 排序
```javascript
arr.sort()   //默认从小到大
arr.sort(function(){
    return 1    //从大到小
    return -1   //从小到大  
    return 0    //相对位置不变
}
arr.sort((a,b)=>a-b)  //从小到大，通常这样写
arr.sort((a,b)=>b-a)

```
* (5) 数组变换

数组变换一般用的就是这三种方法，map，filter，reduce。

```javascript
let arr = [1,2,3,4,5]
let arr1 = arr.map(item=>item*item)

//map函数的方法用于，n--->n的情况，一个数组中元素变换，但是数量不变

let arr2 = ['a','ab','abc','abcd','abcde']
let arr3 = arr2.filter(item => item.length>3)

//filter函数的方法用于，n--->少的情况，一个数组中元素变换，数量减少

let arr4 = [1,2,3,4,5,6,7,8]
let arr5 = arr4.reduce((result, item)=>{
    return result+=item
},0)

// reduce函数的方法用于，n--->1的情况，reduce用于多变一的情况，reduce是个功能很强大的函数，可以实现map和filter的功能。

let arr4 = [1, 2, 3, 4, 5, 6, 7, 8]
let arr5 = arr4.reduce((result, item) => {
    return result += item
}, 0)
console.log(arr5)

//reduce实现map功能

let arr6 = arr2.reduce((result, item) => {
    result = item.length > 3 ? result.concat(item) : result.concat([])
    return result
}, [])
console.log(arr6)

//reduce实现filter功能

```

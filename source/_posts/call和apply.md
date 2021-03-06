---
title: call 和 apply
date: 2017-01-24 18:13:20
tags:
---
call和apply的区别

<!-- more -->

# 调用一个对象的一个方法，以另一个对象替换当前对象

apply(func,数组参数)：

```
function add(a,b){
  return a+b;  
}
function sub(a,b){
  return a-b;  
}
var a1 = add.apply(sub,[4,2]);　　//sub调用add的方法
var a2 = sub.apply(add,[4,2]);
alert(a1);  //6     
alert(a2);  //2
```



## 模拟实现
```
Function.prototype.newCall = function(context) {
  context.fn = this;  // 通过this获取call的函数
  context.fn();
  delete context.fn;
}
let foo = {
  value: 1
}
function bar() {
  console.log(this.value);
}
bar.newCall (foo); // 1
```

>但是如果说有传参数呢？  
所以我们可以进行优化一下，因为传入的参数数量是不确定的，所以我们可以从Arguments对象中去获取，这个比较简单。  
问题是参数是不确定的，我们如何传入到我们要执行的函数中去呢 ？ 这里我们有两种选择：一种是通过eval拼接的方式，另一种就要用到es6了。

```
Function.prototype.newCall = function(context, ...parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }
  let fn = Symbol()
  context[fn] = this
  context[fn](...parameter);
  delete context[fn]
}
let person = {
  name: 'Abiel'
}
function sayHi(age,sex) {
  console.log(this.name, age, sex);
}
sayHi.newCall (person, 25, '男'); // Abiel 25 

```

实现了call之后，apply也是同样的思路。

===========================================

## apply实现：
```
Function.prototype.newApply = function(context, parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }
  let fn = Symbol()
  context[fn] = this
  context[fn](...parameter);
  delete context[fn]
}

```
## bind
初体验：


```
Function.prototype.bind = function (context) {
  var me = this
  return function () { // bind之后得到的函数
    return me.call(context)  // 执行是改变this执行
  }
}


加入参数：

Function.prototype.bind = function (context,...innerArgs) {
  var me = this
  return function (...finnalyArgs) {
    return me.call(context,...innerArgs,...finnalyArgs)
  }
}
let person = {
  name: 'Abiel'
}
function sayHi(age,sex) {
  console.log(this.name, age, sex);
}
let personSayHi = sayHi.bind(person, 25)
personSayHi('男')
```

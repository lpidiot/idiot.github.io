---
title: js-作用域链
comments: true
date: 2018-11-29 20:18:21
urlname: action_scope
tags:
- javascript
- 笔记
- 前端
categories:
- 前端
---

> 作用域链

私有作用域中，在代码执行时遇到一个变量，如果是私有变量，name它与外界无任何关系，如果不是私有变量则会到当前作用域的上级作用域进行查找，没有就继续上级查找，一直找到window为止，这就是作用域链

### 区分全局/私有变量

- 全局作用域下声明的变量(即预解释中)为全局变量(废话)
- 私有作用域下`声明`的变量和`函数的形参`都是私有变量

<br/>

### 函数执行时的一些动作
- 首先形成一个私有作用域，然后按照下面的步骤执行
   1 如果有形参，先给形参赋值
   2 进行私有作用域的预解释
   3 私有作用域中的代码从上到下执行
   
<br/>

### 闭包
函数形成了新的私有作用域保护了里面的私有变量不受外界的干扰，这就是`闭包`

<br/>

### 带不带var的小知识
前面提到，带var的变量会在当前作用域进行预解释自动定义，不带var的则不会
```javascript
        console.log(a);  //undefined
        console.log(b);   //b is not defined
        var a=20;
        b=20;
```
报b没有定义的错误，但是我们换个写法
```javascript
        var a=20;
        b=20;
        console.log(a);  //20
        console.log(b);  //20
```
没错b的值也是20==事实上在这里，` b=20;`相当于给`window`添加了一个属性名为 'b',属性值为 20 的属性
而`var a=20;`给全局作用域增加了一个全局变量 a 但不仅如此，它也给`window`添加了一个属性名为 'a',属性值为 20 的属性
对于b，它不是全局变量，我们得到的值实际上是`window.b`

<br/>

### 小例子
```javascript
 console.log(total);  //undefined
        var total=0;
        function fn(num1,num2) {
            console.log(total);
            total=num1+num2;
            console.log(total);
        }
        fn(100,200);//0   300
        console.log(total);   //300
```


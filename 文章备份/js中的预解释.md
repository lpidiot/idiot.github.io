---
title: js中的预解释
comments: true
date: 2018-11-26 10:44:58
urlname: Pre_interpretation
tags:
- javascript
- 笔记
- 前端
categories:
- 前端
---

> js预解释


写在前面:假期试着学了点js基础知识,现在也差不多忘记了,重新整理下方便以后查阅(别再忘了喂QAQ)

### obj/function类型的数值中的操作
obj类型 单独开辟一块内存空间来储存属性名及属性值
函数类型 单独开辟一块内存空间来储存函数本身(字符串)
```javascript
 function fn(){
            console.log('测试');
        }
        console.log(fn);
        console.log(fn());
```
`console.log(fn)` 打印了字符串'console.log('测试');'
`console.log(fn())` 返回return后面的值 没有则返回undefined,
这里看控制台出现了 '测试' 以及undefined,原因是fn被执行打印了 '测试'

### 预解释(变量提声)
当前作用域中，js代码执行之前，浏览器首先会默认的吧所有带var和function的进行提前的声明(declare)或者定义(defined)
对于 var--->仅声明
对于 function--->声明加定义

例
```javascript
 var a=10;
        var obj={name:'小明',age:'19'}
        function fn(num1,num2){
            var total=num1+num2;
            console.log(total);
        }
```


预解释中的操作:
var a;
var obj;
fn(num1,num2)=xxxfff000;

注:开辟的内存空间xxxfff000,内容为“
var total=num1+num2;
console.log(total);
”

由于预解释的存在的一些有趣的东西
```javascript
 console.log(a);
        fn(100,200);
        var a=13;
        function fn(num1,num2) {
            var total=num1+num2;
            console.log(total);
        }
```
1行中直接打印a，按理应该报错(没声明变量嘛)，但控制台显示undefined，因为预解释已经声明了下面的a，但是没有定义

2行中打印了300，原因同(function在预解释中直接声明+定义了)

注意 预解释仅发生在当前作用域中,且预解释完成后的操作在之后的代码执行时不会重复(效率)

### 无节制的预解释

预解释的时候会忽略条件，比如
```javascript
    if (!('num' in window)) {
        var num = 12;
    }
    console.log(num);	//undefined
```

预解释忽略掉条件直接对`num`进行了声明(当然同时也给window添加了一个叫num的属性)导致接下来if条件不成立
对于函数
```javascript
    fn();

    function fn() {
        console.log('ok');
    }

    fn();
```
由于预解释的提前声明+定义所以在前面也能正常使用，当然也可以用匿名函数函数表达式(把函数定义部分赋值给一个变量/元素的某一事件)来避免这个情况↓
```javascript
    fn();	//undefined
    var fn = function () {
        console.log('ok');
    }
    fn();	//ok
```
这里fn仅会被预解释声明

---
title: js内存优化
comments: true
date: 2018-12-03 11:18:16
urlname: js_RAM
tags:
- javascript
- 笔记
- 前端
categories:
- 前端
---

### 自执行函数
注：这种方式的函数不会进行预解释操作，当代码执行到这个位置时才会定义+执行
`function(num){console.log(num);}(100);`
报错
加上()就好了
`(function(num){console.log(num);}) (100);`

原因未知，除了加括号还能加其他符号来操作
`+function(num){console.log(num);}(100);`
`-function(num){console.log(num);}(100);`
`~function(num){console.log(num);}(100);`
`!function(num){console.log(num);}(100);`
............

### js中的内存
栈内存：提供供js代码执行的环境-->作用域(全局作用域,私有作用域，`只有函数执行时才会产生私有作用域`)
堆内存:用来存储引用数据类型的值-->对象存储是属性名+属性值，函数存储的是`代码字符串`

### 手动释放内存
> 堆内存的释放

对象数据类型或函数数据类型在定义的时候首先会开辟一个堆内存，堆内存有个引用地址，当有变量引用了这个地址，则该内存被占用，不进行销毁。

对于使用过的无用的变量我们可以手动销毁掉优化内存，想要堆内存释放/销毁，只需要把引用它的变量赋值为`null`即可(其实是不指向该堆内存即可)，当堆内存没有没有任何东西占用，浏览器就会在空闲时间将它销毁

> 栈内存的释放

函数执行产生私有作用域(栈内存)，当私有作用域中的代码被执行完成后，当前作用域会被主动进行释放和销毁
但是，当前作用域中部分内存被当前作用域以外其他东西占用时，当前作用域也就不销毁了
```javascript
    function fn() {
        var num = 200;
        return function () {
            console.log(num);
        }
    }

    var a=fn();
```
上面例子中a仅仅做了个引用，但fn()形成的私有作用域也不会被销毁了，改一改↓
```javascript
    function fn() {
        var num = 200;
        return function () {
            console.log(num);
        }
    }
    //fn();	//销毁
	fn()();	//不立即销毁(最后一次调用完成后再销毁)
```


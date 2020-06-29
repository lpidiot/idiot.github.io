---
title: js中查找上级作用域
comments: true
date: 2018-12-03 15:59:35
urlname: findSuper
tags:
- javascript
- 笔记
- 前端
categories:
- 前端
---

### 如何查找上级作用域
当前函数是在哪里定义的，它的上级作用域就是谁，`与函数在哪执行的没有任何关系`↓
```javascript
    var num = 100;

    function fn() {
        var num = 200;
        return function () {
            console.log(num);
        }
    }

    var f = fn();
    f();    //200
    ~function () {
        var num = //300;
        f();    //200
    }();

```
---
title: easyui-messager组件
comments: true
date: 2018-11-23 10:38:11
urlname: easyui_messager
tags:
- easyui
- 笔记
- 前端
categories: 
- 前端
---
> easyui中消息窗口(messager)的使用

### 文件的引入
```
    <link rel="stylesheet" type="text/css" href="myfile/js/easyui/themes/default/easyui.css">
    <link rel="stylesheet" type="text/css" href="myfile/js/easyui/themes/icon.css">
    <script type="text/javascript" src="myfile/js/easyui/jquery.min.js"></script>
    <script type="text/javascript" src="myfile/js/easyui/jquery.easyui.min.js"></script>
    <script type="text/javascript" src="myfile/js/easyui/locale/easyui-lang-zh_CN.js"></script>
```
- 1 主题文件还是有必要引入的,原因是默认样式有点..丑
- 2 icon图标样式,基本必加
- 3 jquery核心 不用说
- 4 easyui全部组件的整合,通常加这个即可,easyui本身不大,没必要单个组件去引用(easyuiloader也不推荐)
- 5 国际化
<br/>

### alert警告窗口

算是可以代替js的默认弹窗了
```javascript
$.messager.alert('小提示','提示信息aaaaa','error',function () {
                alert('关闭了提示框');
            });
```
> 参数: title, msg, icon, fn

- title：在头部面板显示的标题文本。
- msg：显示的消息文本。
- icon：显示的图标图像。可用值有：error,question,info,warning。
- fn: 在窗口关闭的时候触发该回调函数。

### confirm确认框

```javascript
$.messager.confirm('标题','确认？',function (f) {
                if(f){
                    alert('点击了确认');
                }else{
                    alert('点击了取消');
                }
```

> 参数: title, msg, fn

- title：在头部面板显示的标题文本。
- msg：显示的消息文本。
- fn(b): 当用户点击“确定”按钮的时侯将传递一个true值给回调函数，否则传递一个false值。
<br/>

### prompt弹窗输入

```javascript
 $.messager.prompt('请输入', 'aaa', function (val) {
                 alert(val);
             })
```
相当于js的
```javascript
var a = window.prompt('请输入', 'password');
             alert(a);
```

> 参数: title, msg, fn

- title：在头部面板显示的标题文本。
- msg：显示的消息文本。
- fn(val): 在用户输入一个值参数的时候执行的回调函数。
<br/>

### progress进度条

```javascript
var option = {
                 title: '标题',
                 text: '载入中',
                 msg: '内容',
                 interval: '500' //设置时间间隔
             }
             $.messager.progress(option);
```

> option中的属性

- title：在头部面板显示的标题文本。默认：空。
- msg：显示的消息文本。默认：空。
- text：在进度条上显示的文本。默认：undefined。
- interval：每次进度更新的间隔时间。默认：300毫秒

显示进度消息窗口`$.messager.progress();`
关闭进度消息窗口`$.messager.progress('close');`
<br/>

### show消息窗口

```javascript
var option = {
                showType: 'slide', //定义将如何显示该消息。可用值有：null,slide,fade,show。默认：slide。
                showSpeed: 600,       //定义窗口显示的过度时间。默认：600毫秒。
                width: 500,      //定义消息窗口的宽度。默认：250px。
                height: 100,                     //定义消息窗口的高度。默认：100px。
                title: '标题文字',               //在头部面板显示的标题文本。
                msg: '内容啊啊啊啊',            //显示的消息文本。
                // style: '',                  //定义消息窗体的自定义样式。
                timeout: 4    //如果定义为0，消息窗体将不会自动关闭，除非用户关闭他。如果定义成非0的树，消息窗体将在超时后自动关闭。默认：4 秒。
            }
            $.messager.show(option);
```

>option中的属性:

- showType：定义将如何显示该消息。可用值有：null,slide,fade,show。默认：slide。
- showSpeed：定义窗口显示的过度时间。默认：600毫秒。
- width：定义消息窗口的宽度。默认：250px。
- height：定义消息窗口的高度。默认：100px。
- title：在头部面板显示的标题文本。
- msg：显示的消息文本。
- style：定义消息窗体的自定义样式。
- timeout：如果定义为0，消息窗体将不会自动关闭，除非用户关闭他。如果定义成非0的树，消息窗体将在超时后自动关闭。默认：4秒。 

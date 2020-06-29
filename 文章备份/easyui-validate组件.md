---
title: easyui-validate组件
comments: true
date: 2018-11-23 15:09:05
urlname: easyui_validate
tags:
- easyui
- 笔记
- 前端
categories:
- 前端
---

> easyui校验(validate)

官方依旧提供了通过标签以及js创建两种方式,当然你也可以两者结合使用,并不冲突

### 通过标签创建
新建一个表单
给要校验的`<input>`输入框加上类`class="easyui-validatebox"`将他渲染为一个校验框

下面是一个必须输入的框,且需要输入正确的邮箱
```html
<input id="vv" class="easyui-validatebox" data-options="required:true,validType:'email'" />  
````

同上 用js的形式
```javascript
$('#vv').validatebox({
    required: true,
    validType: 'email'
});
```
> option/js中{}内的属性

- required boolean值,是否定义为必填字段
- validType 定义字段验证类型
  - email：匹配E-Mail的正则表达式规则。
  - url：匹配URL的正则表达式规则。
  - length[0,100]：允许在x到x之间个字符。
  - remote['youURL','paramName']：发送ajax请求需要验证的值，当成功时返回true
- missingMessage 当文本框未填写时出现的提示信息(即定义了`required`后校验失败的提示)
- invalidMessage 当文本框的内容被验证为无效时出现的提示。

### 自定义校验规则

先添加js
举例:
```javascript
$.extend($.fn.validatebox.defaults.rules, {
                minmaxLength: {
                    validator: function (value, param) {
                        return value.length >= param[0] && value.length <= param[1];
                    },
                    message: '提示信息'
                }
            });
```
`minmaxLength`就是自己写的规则了，该方法实现了输入值要在[a,b]间才校验通过

`message` 为校验失败时的提示信息

看下例子就秒懂了

```html
<input type="text" name="name" class="easyui-validatebox" 
data-options="required:true,validType:'minmaxLength[2,5]',missingMessage:'姓名必填',invalidMessage:'该字段在2到5个字符'">
```

该字段必须在2到5个字符之间

<br/>

### 表单的提交
普通ajax/submit提交 这里不多说

easyui的提交方式
```javascript
$('#submit').click( function (){
                 $('#myform').form('submit',{
                     url:'save',
                     onSubmit:function () {
                         if(!$('#myform').form('validate')){
                             $.messager.show({
                                 title:'提示',
                                 msg:'校验失败！'
                             });
                             return false;
                         }
                     },
                     success:function (result) {
                         alert('ok');
                     }
                 })
             });
```
`url`提交地址

`$('#myform').form('validate')`是判断校验是否通过,详细查api去=

`onSubmit`定义了表单提交时的操作,这里校验失败时直接`return false;`不提交。(否则什么都不做就通过了提交了呗=)
<br/>
也可以只定义表单的提交动作
```javascript
 $('#myform').form({
                url: 'save',
                onSubmit: function () {
                    if (!$('#myform').form('validate')) {
                        $.messager.show({
                            title: '提示',
                            msg: '校验失败！'
                        });
                        return false;
                    }
                },
                success: function (result) {
                    alert('ok');
                }
            })
```

然后随意用什么提交一下

```javascript
$('#你的提交按钮id').click(function () {
                 $('#你的表单id').submit();
             })
```
完成

<br/>

### 实例-html部分
```html
 <form id="myform">
        <table>
            <tr>
                <td>姓名</td>
                <td><input type="text" name="name" class="easyui-validatebox" required="true"
                           validType="minmaxLength[2,5]"
                           missingMessage="姓名必填"></td>
            </tr>
            <tr>
                <td>年龄</td>
                <td><input type="text" id="age" name="age"></td>
            </tr>

            <tr>
                <td>城市</td>
                <td><input type="text" id="city" name="city" class="easyui-combobox" url="getCity" valueField="id"
                           textField="name">
                </td>
            </tr>
            <tr>
                <td>开始时间</td>
                <td><input type="text" id="starttime" name="starttime"></td>
            </tr>
            <tr>
                <td>结束时间</td>
                <td><input type="text" id="endtime" name="endtime"></td>
            </tr>
            <tr>
                <td>电话</td>
                <td><input type="text" id="calla" name="calla"></td>
            </tr>
            <tr>
                <td>邮箱</td>
                <td><input type="text" id="email" name="email" class="easyui-validatebox" required="true"
                           validType="email"></td>
            </tr>


            <tr>
                <!-- <td><a class="easyui-linkbutton" onclick="save()">提交</a></td>-->
                <td><a id="submit" class="easyui-linkbutton">提交</a></td>
            </tr>

        </table>
    </form>
```

### 实例-jsvascript部分

```javascript
<script type="text/javascript">

        $(function () {
            $.extend($.fn.validatebox.defaults.rules, {
                minmaxLength: {
                    validator: function (value, param) {
                        return value.length >= param[0] && value.length <= param[1];
                    },
                    message: '该字段在2到5个字符'
                }
            });

            /*数据校验*/
            $('#age').numberbox({
                min: 0,
                max: 150,
                required: true,
                precision: 0,
                missingMessage: '年龄在0到150'
            });

            /*日期控件*/
            /* $('#calla').datebox({
                 required: true,
                 editable: false

             });*/

            /*日期时间组件*/
            $('#starttime,#endtime').datetimebox({
                required: true,
                editable: false

            });


            /*easyui form表单提交*/
            /* $('#submit').click( function (){
                 $('#myform').form('submit',{
                     url:'save',
                     onSubmit:function () {
                         if(!$('#myform').form('validate')){
                             $.messager.show({
                                 title:'提示',
                                 msg:'校验失败！'
                             });
                             return false;
                         }
                     },
                     success:function (result) {
                         alert('ok');
                     }
                 })
             });*/


            /*仅定义表单  下边用.submit提交*/
            $('#myform').form({
                url: 'save',
                onSubmit: function () {
                    if (!$('#myform').form('validate')) {
                        $.messager.show({
                            title: '提示',
                            msg: '校验失败！'
                        });
                        return false;
                    }
                },
                success: function (result) {
                    alert('ok');
                }
            })

            /* $('#submit').click(function () {
                 $('#myform').submit();
             })*/

            $('#myform').find('input').on('keyup', function (event) {
                if (event.keyCode == '13') {
                    $('#myform').submit();
                }
            })


        })
 /*普通ajax提交*/
        /* function save() {
             $.ajax({
                 type: 'post',
                 data: $('#myform').serialize(),
                 dataType:'text',
                 cache:false,
                 url:'save',
                 success:function (result) {
                     $.messager.alert('提醒','保存成功','error');
                 },
                 error:function (result) {
                     $.messager.alert('提醒','保存失败','error');
                 }
             })
         }*/


    </script>
```

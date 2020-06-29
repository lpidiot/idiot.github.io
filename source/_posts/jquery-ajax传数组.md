---
title: jquery-ajax传数组
comments: true
date: 2018-11-30 11:19:26
urlname: ajax_deliver
tags:
- jquery
- 笔记
- 前端
categories:
- 前端
---

> jquery-ajax中传数组的问题

无聊写个批量操作的小功能，批量嘛当然得用到数组，我的前台代码：
```javascript
				······
    var select = $('#mytab4').datagrid('getSelections');
    if (select == null) {
        return;
    }
    var list = new Array();
    for (var i in select) {
        list.push(select[i].id);
    }
				······
    $.ajax({
        url: 'book/confirmReturn',
        type: 'post',
        cache: false,
        data: {ids: list},
        success: function (result) {
            if (result.success) {
                $('#mytab5').datagrid('reload');
                $.messager.show({
                    title: '提示',
                    msg: result.msg,
                    iconCls: 'ok'

                });
            } else {
                $.messager.show({
                    title: '提示',
                    msg: result.msg,
                    iconCls: 'error'
                });
            }
        }
    });
```
有些多余，看第19行就行，再看看后台代码(springmvc)
```java
    @RequestMapping(value = "/confirmReturn")
    @ResponseBody
    public Object confirmReturn(Integer[] ids) {
        HashMap<String, Object> map = new HashMap<>();
        try {
            for (Integer id : ids) {
                System.out.println(id);
                /*Borrow borrow = borrowService.findById(id);
                Bookmsg bookmsg = bookmsgService.findById(borrow.getApplybook());
                bookmsg.setNumber(bookmsg.getNumber() + 1);
                bookmsgService.save(bookmsg);
                borrowService.deleteById(id);*/
            }
            map.put("success", true);
            map.put("msg", "操作成功");
        } catch (Exception e) {
            map.put("success", false);
            map.put("msg", "操作失败，请刷新后重试");
        }
        return map;
    }
```
请无视注释的内容= 提交时没报数据转换异常，而try捕获到异常，打印id也没有被执行，问题应该在前台的数据传递上

回头看看浏览器控制台的参数↓
![控制台](http://t1.aixinxi.net/o_1cth8lj3h1n361r31q7s1k0ru0sa.jpg)

ids[]并不是我们希望得到的ids(貌似会自动给数组带上[])

### 解决办法
设置ajax的属性traditional为true阻止深度序列化即可
修改后的前台代码：
```javascript
                            $.ajax({
                                url: 'book/confirmReturn',
                                type: 'post',
                                cache: false,
                                traditional: true,//阻止深度序列化
                                data: {ids: list},
                                success: function (result) {
                                    if (result.success) {
                                        $('#mytab5').datagrid('reload');
                                        $.messager.show({
                                            title: '提示',
                                            msg: result.msg,
                                            iconCls: 'ok'

                                        });
                                    } else {
                                        $.messager.show({
                                            title: '提示',
                                            msg: result.msg,
                                            iconCls: 'error'
                                        });
                                    }
                                }
                            });
```

再看浏览器控制台
![修改后](http://t1.aixinxi.net/o_1cth9sueb1jdi1k28f7fb4m5hba.jpg-w.jpg)

ok，不带[]了，后台控制台也正常打印了过来的值

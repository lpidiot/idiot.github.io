---
title: easyui-layout&tabs组件
comments: true
date: 2018-11-23 15:21:59
urlname: easyui_layout&tabs
tags:
- easyui
- 笔记
- 前端
categories:
- 前端
---

> easy ui-layout&tabs

其实没什么好记的(简单),写个例子以备不时之需

### js部分(动态添加tabs选项卡)
```javascript
<script type="text/javascript">
        $(function () {
            $('a[title]').click(function () {
                var str=$(this).attr('title');
                var title=$(this).html();
                if($('#tt').tabs('exists',title)){ //判断选项卡是否存在
                    $('#tt').tabs('select',title);//选中选项卡
                }else{
                    /*添加选项卡*/
                    $('#tt').tabs('add',{
                        title:title,
                        content:'<iframe frameborder="1"  style="width:100%;height:100%;" src='+str+'></iframe>',
                        closable:true
                    })
                }

            })
        })
    </script>
```

<br/>
### html部分

```html
<div id="cc" class="easyui-layout" fit="true" href="index" style="width: 100%;height: 100%;">
    <div data-options="region:'north',title:'North Title',split:false" style="height:100px;"></div>
    <!--   <div data-options="region:'south',title:'South Title',split:true" style="height:100px;"></div>-->
    <!-- <div data-options="region:'east',iconCls:'icon-reload',title:'East',split:true" collapsed="true" style="width:100px;"></div>-->
    <div data-options="region:'west',title:'菜单',split:false,iconCls:'icon-ok'" collapsed="false" style="width:200px;">

        <div id="aa" class="easyui-accordion" fit="true">
            <div title="Title1" data-options="iconCls:'icon-save',selected:true" style="overflow:auto;padding:10px;">
                <a title="/">用户列表</a><br/>
                <a title="validate">编辑</a>
            </div>
            <div title="Title2" data-options="iconCls:'icon-reload'" style="padding:10px;">
                content2
            </div>
            <div title="Title3">
                content3
            </div>
        </div>
    </div>
    <div data-options="region:'center',title:'center title'" style="padding:5px;background:#eee;">
        <div id="tt" class="easyui-tabs" fit="true">
        </div>
    </div>
</div>
```


---
title: easyui-datagrid组件
comments: true
date: 2018-11-29 19:40:06
urlname: easyui_datagrid
tags:
- easyui
- 笔记
- 前端
categories:
- 前端
---


由于datagrid涉及的配置较多，不推荐不推荐不推荐直接用标签渲染
(写得较乱，自己回过头能看懂就够了=)

html部分一个table即可
```html
<table id="mytab"></table>
```

在写js前注意，配置列的时候会用到`[[]]`如果用的是thymeleaf模板来写需要自己换行处理，个人喜欢直接取消内联
```javascript
<script type="text/javascript" th:inline="none">
...
</script>
```

开始配置:
```javascript
$('#mytab').datagrid(options);
```

### datagrid-options对象常用的配置

| 属性名 | 属性值类型 | 说明 | 默认值 |
| :--- | :----- | :------ | --- |
| idField | string | 指明哪一个字段是标识字段。可以说是必配id了 | null |
| url | string | 一个URL从远程站点请求数据。 | null |
| title | string | 标题文字 | null |
| width | number | 表格的宽度 | null |
| height |  number | 表格的高度 | null |
| fitColumns | boolean |  真正的自动展开/收缩列的大小，以适应网格的宽度，防止水平滚动 | false |
| loadMsg | string | 载入数据时的提示文字 | Processing, please wait … |
| nowrap | boolean | 折行显示(一列内容太多时自动折算成多行显示) | false |
| frozenColumns | array | 同列属性，但是这些列将会被冻结在左侧。(与fitColumns一起使用会冲突看不出效果) | null |
| striped | boolean | 斑马线 | false |
| rownumbers | boolean | 如果为true，则显示一个行号列。 | false |
| singleSelec | boolean | 单行选择(false时可多选) | false |
| remoteSort | boolean | 默认排序(false后才可自己定义初始排序) | true |
| sortName |  | 定义哪些列可以进行排序(应该是设置初始排序字段) | null |
| sortOrder | string | 排序方式，只能为asc/desc，和sortName配合 | asc |
| rowStyler | function | 返回样式如'background:red'。带2个参数的函数：index：该行索引从0开始row：与此相对应的记录行。 |  |
| pagination | boolean | 如果为true，则在DataGrid控件底部显示分页工具栏。 | false |
| pageSize | number | 在设置分页属性的时候初始化页面大小(就是说一页显示多少条记录=) | 10 |
| pageList | array | 创建一个下拉框选择可设置一页多少条记录 | [10,20,30,40,50] |
| toolbar |array,selector  | 顶部的工具栏 | null |
| columns | array | DataGrid列配置对象 | undefined |


### 创建数据表格前台查询传给后台的数据

```java
 private Integer page;//页数
 private Integer rows;//每页记录数
 private String order;//排序方式
 private String sort;//排序字段
```
建这样一个工具类存放比较合适

### 创建数据表格前台需要的数据形式

```
{"total":2,
"rows":[
{"id":1,"bookname":"图书1","number":2,"bookurl":null,"auther":"aaa"},
{"id":2,"bookname":"图书2",number":3,"bookurl":null,"auther":"qqq"}
]
}
```
total是总记录数,rows是具体的数据
由于这种结构，在springmvc环境中我一般都是
```java
HashMap<String, Object> map = new HashMap<>();
        Page<bookMsg> page = bookMsgService.findAll(spec, form.buildpage());
        List<bookMsg> list = page.getContent();
        map.put("total", page.getTotalElements());
        map.put("rows", list);
        return map;
```
`bookMsg`是实体类，`bookMsgService`是对应的服务层，`spec`是条件查询，这里忽视就好，
`form`是上面提到的工具类对象，`.buildpage()`是工具类中根据前台的参数生成对应的分页信息

```
  public Pageable buildpage(){
        page--;
        if(order!=null&&sort!=null){
            Sort by = Sort.by(Sort.Direction.fromString(order), sort);
            return PageRequest.of(page,rows,by);
        }else {
            return PageRequest.of(page,rows);
        }
    }
```
前台page页数从1开始，后台从0故自减



### rowStyler例子
(给age=20的列加上蓝色背景色)
```javascript
                rowStyler:function(index,row){
                    if(row.age==20){
                        return"background:blue";
                    }

                },            //给特殊列做特殊处理
```

frozenColumns例子：
```javascript
 frozenColumns: [[
                {field: 'id', title: '编号', width: 80, hidden: true},
                {field: 'empty', width: 50, checkbox: true}      //显示选择框,field值随便填个json数据中没有的即可
            ]]
```

### colmns例子：
```javascript
 columns: [[
                {
                    field: 'bookname',
                    title: '书名',
                    width: 80,
                    align: 'center',
                    sortable: true,
                    formatter: function (value, record, index) {
                        return '<span title=' + value + '>' + value + '</span>';
                    }
                },
				{
                    field: 'remarks',
                    title: '简介',
                    width: 80,
                    align: 'center',
                    sortable: false,
                    formatter: function (value, record, index) {
                        return '<span title=' + value + '>' + value + '</span>';
                    }
				}
]]
```
colmns和frozenColumns都是一个二维数组[[]],其中给对象，每个对象都是一列的属性
- `field: 'bookname'`列字段名称-表示取数据中叫bookname的字段
- `title: '书名'` 列标题文本
- `align` 对齐方式
- `sortable` 是否允许该字段排序，默认false
- `formatter` 单元格formatter(格式化器)函数，带3个参数：
   - value：字段值。
   - row：行记录数据。
   - index: 行索引。 

返回一个string(可用标签),目前也就处理显示的文本用到过=






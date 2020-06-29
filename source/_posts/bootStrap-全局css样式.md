---
title: bootStrap-全局css样式(内容较多)
comments: true
date: 2018-12-10 14:40:52
urlname: bootstrap_css
tags:
- bootStrap
- 前端
- 笔记
categories:
- 前端
---

主要为bootStrap的一些小笔记=其中包括了部分以前没用过的html标签
`<abbr>` 标记一个缩写

`<small>` 标签呈现小号字体效果

### bootStrap中部分文本样式

- `class="text-left"`标签居左

- `class="text-right"` 标签居右

- `class="text-center"` 标签居中

- `class="text-uppercase"` 字母全部大写

- `class="text-lowercase"` 字母全部小写

- `class="text-capitalize"` 首字母大写

- `class="list-unstyled"` 无样式

```html
<div class="container">
    <div>
        <h2>hello world
            <small>副标题</small>
        </h2>
        <p>文本突出
            <mark>我我我</mark>
        </p>
        <p class="text-left">居左</p>
        <p class="text-center">居中</p>
        <p class="text-right">居右</p>
        <p class="text-uppercase">asdsafwfas全部大写</p>
        <p class="text-lowercase">asdASDfasqwADS全部小写</p>
        <p class="text-capitalize">asdad首字母大写</p>
        <p>这里这里这里<abbr title="这里是缩写">这里</abbr></p>
        <ul class="list-unstyled">
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>
</div>
```
对应的效果---（请无视导航栏）
![](http://t1.aixinxi.net/o_1ctuhtiqh86b1pbr16lo17en12eta.png-w.jpg)

### 栅格的偏移

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
    </div>
    <div class="row">
        <div class="col-md-3">col-md-3</div>

    </div>
</div>
```
![](http://t1.aixinxi.net/o_1ctujmk4t9gu1jjg1p0911krvv6a.png-w.jpg)
`col-md-3`这一列默认是左对齐的，添加`offset`样式即可偏移列
```html
<div class="container">
    <div class="row">
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
    </div>
    <div class="row">
        <div class="col-md-3 col-md-offset-2">col-md-3</div>

    </div>
</div>
```
`col-md-offset-2`向右偏移2个md栅格的长度，效果-

![](http://t1.aixinxi.net/o_1ctujsgau17qm1g4a12oman6df6a.png-w.jpg)

### 栅格的简单排序
```html
<div class="container">
    <div class="row">
        <div class="col-md-9">col-md-9</div>
        <div class="col-md-3">col-md-3</div>
    </div>
</div>
```
`col-md-9`肯定在前而`col-md-3`在后，下面交换位置
```html
<div class="container">
    <div class="row">
        <div class="col-md-9 col-md-push-3">col-md-9</div>
        <div class="col-md-3 col-md-pull-9">col-md-3</div>
    </div>
</div>
```

### 代码块的处理
bootStrap提供了几个代码显示的样式

- 行内代码:使用`<code>`标签，例`<code>&ltselect&gt</code>` 显示效果类似这样`<select>`

- 命令:`<kbd>`标签，命令依旧放标签体

- 代码块：`<pre>`

- 输出：`<samp>` 无明显效果==

- 变量：`<var>`


### 表格
- 默认的加class`table`即可
- 斑马线: `table-striped`
- 加边框(默认无边框)：`table-bordered`
- 鼠标悬停显示： `table-hover`
- 紧缩的表格： `table-condensed`

状态类(就是加颜色)-通过这些状态类可以为行或单元格设置颜色。

| Class | 描述 |
| -- | -- |
| .active | 鼠标悬停在行或单元格上时所设置的颜色 |
| .success | 标识成功或积极的动作 |
| .info | 标识普通的提示信息或动作 |
| .warning | 标识警告或需要用户注意 |
| .danger | 标识危险或潜在的带来负面影响的动作 |

### 表单
```html
<div class="container">
    <form>
        <div class="form-group">
            <label>用户名</label>
            <input type="text" class="form-control" placeholder="username">
        </div>
        <div class="form-group">
            <label>密码</label>
            <input type="password" class="form-control">
        </div>
    </form>
</div>
```
其中`<label>`必须添加否则无法解析，有时候不需要这个laber标签可以把它隐藏
给<label>添加class`sr-only`即可

内联表单：给表单添加样式`form-inline`
水平表单： `form-horizontal`

### 表单中的部分标签
单选框
```html
    <form class="form-horizontal">
        <div class="radio">
            <label><input type="radio" name="sex">男</label>
        </div>
        <div class="radio">
            <label><input type="radio" name="sex">女</label>
        </div>
    </form>
```
复选框
```html
    <form class="form-horizontal">
        <div class="checkbox">
            <label>
                <input type="checkbox">选我
            </label>
        </div>
    </form>
```

下拉框
```html
    <form class="form-horizontal">
       <select class="form-control">
           <option>no1</option>
           <option>no2</option>
           <option>no3</option>
       </select>
    </form>
```
让下拉框直接展示:给select标签加上属性`multiple`即可

### form中标签的状态
不可选-加上disabled属性即可
```html
<input type="text" class="form-control" placeholder="hello" disabled>
```
要使form中所有标签不可选可以将form中的标签装到`<fieldset></fieldset>`当中并设置 `<fieldset disabled>`

只读：加上属性`readonly`，注意只读与不可选有显示上的区别
```html
<input type="text" placeholder="hello" class="form-control" readonly>
```
禁用状态：加属性`disabled='disabled'`

激活状态：加类`active`

静态的标签:加class`form-control-static`


### 输入框的状态：给父级添加一个class

- `has-success`:通过(绿色)
- `has-warning`:警告(黄)
- `has-error`: 错误(红)
- `btn-default` 默认

```html
<div class="container">
    <div class="form-group has-success">
        <label>用户</label>
        <input type="text" class="form-control">
    </div>
    <div class="form-group has-warning">
        <label>用户</label>
        <input type="text" class="form-control">
    </div>
    <div class="form-group has-feedback">
        <label>用户</label>
        <input type="text" class="form-control">
    </div>
    <div class="form-group has-error">
        <label>用户</label>
        <input type="text" class="form-control">
    </div>
</div>
```
加上图标显示更好，bootStrap中图标一般用`<span>`来引用，在表单的`<input>`标签中使用图标要给父容器一个`has-feedback`(必须，否则位置会乱)的类,再给`<span>`加上类`form-control-feedback`以及想要的图标样式
```html
<div class="container">
    <div class="form-group has-success has-feedback">
        <label>用户</label>
        <input type="text" class="form-control">
        <span class="glyphicon glyphicon-ok form-control-feedback"></span>
    </div>
</div>
```

![](http://t1.aixinxi.net/o_1cu1jpqtau0g1ef481a77qdt6a.png-w.jpg)

### 按钮
依旧提供了同状态一样的一套，按钮首先加`btn`类
- `btn-default` 默认(白灰)

- `btn-success`:安全(绿色)

- `btn-info`:一般(蓝色)

- `btn-warning`:警告(黄)

- `btn-error`: 危险(红)

```html
    <button type="button" class="btn btn-default">default</button>
    <button type="button" class="btn btn-success">success</button>
    <button type="button" class="btn btn-info">info</button>
    <button type="button" class="btn btn-warning">warning</button>
    <button type="button" class="btn btn-danger">danger</button>
```
![](http://t1.aixinxi.net/o_1cu1jug2c6f51638q6qgg31crja.png-w.jpg)
按钮的大小设置和栅格系统的区分差不多
下面是从小到大的按钮
```
    <button type="button" class="btn btn-info btn-xs">xs</button>
    <button type="button" class="btn btn-info btn-sm">sm</button>
    <button type="button" class="btn btn-info">info</button>
    <button type="button" class="btn btn-info btn-lg">lg</button>
```
设置`btn-block`则按钮会充满父容器

### 下拉菜单
| 类 | 描述 |
| - | - |
| .dropdown | 指定下拉菜单，下拉菜单都包裹在 .dropdown |
| .dropdown-menu | 创建下拉菜单 |
| .dropdown-menu-righ | 下拉菜单右对齐 |
| .dropdown-header | 下拉菜单中添加标题 |
| .dropup | 指定向上弹出的下拉菜单 |
| .disabled | 下拉菜单中的禁用项 |
| .divider | 下拉菜单中的分割线 |

最简单的下拉菜单
```html
<div class="container">
    <div class="dropdown">
        <button id="menu1" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            菜单 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" aria-labelledby="menu1">
            <li><a href="#">aa</a></li>
            <li><a href="#">bb</a></li>
            <li><a href="#">cc</a></li>
        </ul>
    </div>
</div>
```
注意`.dropdown`可以没有
下拉菜单的布局--在菜单主容器中如上面的`.dropdown`中添加类`pull-right`,这样menu1按钮就到屏幕右边去了，内容跟着到右边去：ul中添加类`dropdown-menu-right`  完成
```html
<div class="container">
    <div class="dropdown pull-right">
        <button id="menu1" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            菜单 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu dropdown-menu-right" aria-labelledby="menu1">
            <li class="dropdown-header">标题</li>
            <li><a href="#">aa</a></li>
            <li><a href="#">bb</a></li>
            <li class="divider"></li>
            <li><a href="#">cc</a></li>
        </ul>
    </div>
</div>
```
其中第7行是标题，通过加类`.dropdown-header`实现，第十行是分割线，通过`.divider`完成
![](http://t1.aixinxi.net/o_1cu1k22pbeppnp71f6p16uk1rm5a.png-w.jpg)
不可选择的菜单-加类`disabled`即可，如`<li class="disabled"><a href="#">cc</a></li>`

### 按钮组
将按钮放在`.btn-group`的容器中即可
```html
<div class="container">
    <div class="btn-group">
        <button type="button" class="btn btn-default">Left</button>
        <button type="button" class="btn btn-default">Center</button>
        <button type="button" class="btn btn-default">Right</button>
    </div>
</div>
```
效果
![](http://t1.aixinxi.net/o_1cu1k6v74c1m12ml1lr6csnr21a.png-w.jpg)
多个按钮组(一般作工具类)用`btn-toolbar`
```html
<div class="container">
    <div class="btn-toolbar">
        <div class="btn-group">
            <button type="button" class="btn btn-default">Left</button>
            <button type="button" class="btn btn-default">Center</button>
            <button type="button" class="btn btn-default">Right</button>
        </div>
        <div class="btn-group">
            <button type="button" class="btn btn-default">Left</button>
            <button type="button" class="btn btn-default">Center</button>
            <button type="button" class="btn btn-default">Right</button>
        </div>
    </div>
</div>
```
按钮组的大小依然是以xs,sm,lg来指定，如`<div class="btn-group btn-group-sm">`不多说

按钮组和菜单的嵌套
```html
<div class="container">
    <div class="btn-group">
        <button type="button" class="btn btn-default">Left</button>
        <button type="button" class="btn btn-default">Center</button>
        <button type="button" class="btn btn-default">Right</button>
        <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            菜单 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">aaa</a></li>
            <li><a href="#">bbb</a></li>
        </ul>
    </div>
</div>
```

按钮组默认都是水平排列的，想垂直排列可以在将`btn-group`改为`btn-group-vertical`

让按钮组占满一整行：用`btn-group-justified`包裹按钮组即可
```html
<div class="container">
    <div class="btn-group btn-group-justified">
        <div class="btn-group">
            <button type="button" class="btn btn-default">aaa</button>
        </div>
        <div class="btn-group">
            <button type="button" class="btn btn-default">bbb</button>
        </div>
    </div>
</div>
```
效果
![](http://t1.aixinxi.net/o_1cu1kbb1fhftjl31fbf11e51v6ea.png-w.jpg)

分裂式下拉菜单：用按钮组做出的实用功能,先做个和上面一样的下拉菜单
```html
<div class="container">
    <div class="btn-group">
        <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            下拉菜单 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
            <li><a href="#">4</a></li>
        </ul>
    </div>
</div>
```
先看看未点击时的效果：
![](http://t1.aixinxi.net/o_1cu1lcn1jd751sggptp180c7l4a.png-w.jpg)

这样的按钮是一个整体，假设需要点小箭头才出现菜单的效果就可以用按钮组来实现了(分裂式)
我们用一个按钮组完成一个按钮，其中两个button一个负责显示文本，一个显示箭头以及互动
```html
<div class="container">
    <div class="btn-group">
        <button class="btn btn-default">分裂式下拉菜单</button>
        <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
            <li><a href="#">4</a></li>
        </ul>
    </div>
</div>
```
效果
![](http://t1.aixinxi.net/o_1cu1ln7mi1gl71l5kmiml7j1r2aa.png-w.jpg)

菜单的内容显示位置，默认下拉框是向下的↓
![](http://t1.aixinxi.net/o_1cu1k22pbeppnp71f6p16uk1rm5a.png-w.jpg)

可以在按钮的容器中添加`dropup`类来反向

普通按钮直接改`dropdown`为`dropup`即可
```html
<div class="container">
    <div class="dropup">
        <button id="menu1" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            菜单 <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" aria-labelledby="menu1">
            <li class="dropdown-header">标题</li>
            <li><a href="#">aa</a></li>
            <li><a href="#">bb</a></li>
            <li class="divider"></li>
            <li><a href="#">cc</a></li>
        </ul>
    </div>
</div>
```
效果
![](http://t1.aixinxi.net/o_1cu1mb4od6d0e47102m1fpk1scma.png-w.jpg)
按钮组的话在`btn-group`后添加`dropup`即可
```html
<div class="container">
    <div class="btn-group dropup">
        <button class="btn btn-default">分裂式下拉菜单</button>
        <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
            <li><a href="#">4</a></li>
        </ul>
    </div>
</div>
```

### 输入框组
同按钮组一样，用group来包裹，输入框组的父容器添加类`input-group`即可

```html
<div class="container">
    <div class="input-group">
        <span class="input-group-addon">$</span>
        <input class="form-control" type="text" placeholder="username">
        <span class="input-group-addon">.00</span>
    </div>
</div>
```
第2和第4行中的`<span>`是为输入框添加格外的内容，使用时给`<span>`加上类`input-group-addon`即可，前后都可加也可以单一使用
 效果(请忽视掉username是什么鬼)
 ![](http://t1.aixinxi.net/o_1cu32q6sq2uqdmk1egkm0o81a.png-w.jpg)

`span`中也可以添加单选、复选按钮，直接添加即可
```html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="input-group">
            <span class="input-group-addon">
                <input type="checkbox">
            </span>
                <input class="form-control" type="text">
            </div>
        </div>
    </div>
</div>
```
![](http://t1.aixinxi.net/o_1cu33f5m99ra1ngjmbi1ssv1btna.png-w.jpg)
单选框同，改第6行中type为`ridao`即可

附加按钮：如果用按钮的话`<span>`的类要改为`input-group-btn`(通俗)
下面给个添加菜单的例子就一目了然了
```html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="input-group">
            <span class="input-group-btn">
                <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">菜单 <span
                        class="caret"></span></button>
                <ul class="dropdown-menu">
                    <li><a href="#">a</a></li>
                     <li><a href="#">b</a></li>
                </ul>
            </span>
                <input class="form-control" type="text">
            </div>
        </div>
    </div>
</div>
```
![](http://t1.aixinxi.net/o_1cu33pm74j0d46kq0c1grl248a.png-w.jpg)

### 标签页(tabs)
创建一个ul列表，添加类`nav nav-tabs`,再添加js控制即可
```html
<div class="container">
    <ul class="nav nav-tabs" id="myTab">
        <li class="active"><a href="">A</a></li>
        <li><a href="">B</a></li>
        <li><a href="">C</a></li>
    </ul>
</div>
<script type="text/javascript">
    $(function () {
        $('#myTab a').click(function (e) {
            e.preventDefault();
            $(this).tab('show');
        });
    })
</script>
```
![](http://t1.aixinxi.net/o_1cuarnruj5r9175714lg1qe61k83a.png-w.jpg)

标签页切换时内容的切换：a标签中herf指定要显示的内容id并添加属性`data-toggle="tab`，添加带类`tab-content`的容器并在其中添加带上面herf中id的内容容器,内容容器一般添加类`tab-pane`
```html
<div class="container">
    <ul class="nav nav-tabs" id="myTab">
        <li><a href="#div1" data-toggle="tab">A</a></li>
        <li><a href="#div2" data-toggle="tab">B</a></li>
        <li><a href="#div3" data-toggle="tab">C</a></li>
    </ul>
    <div class="tab-content">
        <div id="div1" class="tab-pane">aaa</div>
        <div id="div2" class="tab-pane">bbb</div>
        <div id="div3" class="tab-pane">ccc</div>
    </div>
</div>
```
![](http://t1.aixinxi.net/o_1cuasiudqk9r1lfk1c201hmr1i8ba.png-w.jpg)


胶囊式标签页：改上面`nav-tabs为`nav-pills` 其他不变
![](http://t1.aixinxi.net/o_1cuaru0o1t9l11601kot1de71ad2a.png-w.jpg)

垂直的标签页：ul中添加类`nav-stacked`

两端对齐的标签页：ul中添加类 `nav-justified`

禁止点击：li中添加类`disabled`

注意，标签页中也是可以使用菜单的

### 导航栏
```html
<nav class="navbar navbar-default">
    <div class="navbar-header"><a class="navbar-brand">Poject Name</a></div>
    <div class="collapse navbar-collapse">
        <a class="navbar-brand">aaa</a>
        <a class="navbar-brand">bbb</a>
    </div>
</nav>
```
`navbar-default`指定样式，这里是默认的

a标签添加`navbar-brand`以适应样式

`navbar-header`指定头，一般用来指定项目名/Logo之类的

`collapse navbar-collapse`就是与头对应的显示导航内容

具体显示看图
![](http://t1.aixinxi.net/o_1cuat71n0v337vn18564n71sk9a.png-w.jpg)

由于导航内容大多是多个，用ul来装更合适(因为还能渲染成tab方便展示)
```html
<nav class="navbar navbar-default">
    <div class="container">
        <div class="navbar-header"><a class="navbar-brand">Poject Name</a></div>
        <div class="collapse navbar-collapse">
            <ul class="nav navbar-nav">
                <li><a href="#">Home</a></li>
                <li class="dropdown"><a href="#" class="dropdown-toggle" data-toggle="dropdown">Tag <span
                        class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">hello1</a></li>
                        <li><a href="#">hello2</a></li>
                        <li><a href="#">hello3</a></li>
                    </ul>
                </li>
                <li><a href="#">About</a></li>
            </ul>
        </div>
    </div>
</nav>
```

![](http://t1.aixinxi.net/o_1cuaticfcdjj1pn31bdn7o1svma.png-w.jpg)

导航栏中的表单：form中添加样式`navbar-form`

导航栏中的按钮：button中添加样式`navbar-btn`

导航栏中的文本：p中添加`navbar-text`

此外，添加`.navbar-left`和`.navbar-right`能让标签居左或居右显示

nav中添加`.navbar-fixed-top`或`.navbar-fixed-bottom`能让导航条固定在顶部或底部

`.navbar-static-top`能让导航条静止在顶部(不会因为下翻而消失)


`.navbar-inverse`使导航条反色，看图(比较完整的导航条，超喜欢这个颜色)
![](http://t1.aixinxi.net/o_1cub00b5aiv52qc1v6ptm81qe1a.png-w.jpg)
代码：
```html
<nav class="navbar navbar-inverse">
    <div class="container">
        <div class="navbar-header"><a class="navbar-brand">Poject Name</a></div>
        <div class="collapse navbar-collapse">
            <ul class="nav navbar-nav">
                <li><a href="#">Home</a></li>
                <li class="dropdown"><a href="#" class="dropdown-toggle" data-toggle="dropdown">Tag <span
                        class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">hello1</a></li>
                        <li><a href="#">hello2</a></li>
                        <li><a href="#">hello3</a></li>
                    </ul>
                </li>
            </ul>
            <p class="navbar-text">this is a test demo</p>
            <div class="navbar-right"><a class="navbar-brand">About</a></div>
            <form class="navbar-form navbar-right">
                <input class="form-control" type="text">
                <button class="btn btn-success">检索</button>
            </form>
        </div><!--collapse/-->
    </div><!--containter-->
</nav>
<div class="container">
    ······
</div>
<nav class="navbar navbar-fixed-bottom">
    <ol class="breadcrumb">
        <li><a href="#">Home</a></li>
        <li><a href="#">Library</a></li>
        <li><a href="#">Data</a></li>
    </ol>
</nav>
```
### 媒体对象
这里的媒体图像指的是图片＋标题＋文字的显示(类似于博客评论或 Twitter 消息等)
```html
<div class="container">
    <div class="media">
        <a href="#" class="media-left"><img src="images/test.jpg"></a>
        <div class="media-body">
            <h2 class="media-heading">标题</h2>
            内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
            内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
            容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
        </div>
    </div>
</div>
```
![](http://t1.aixinxi.net/o_1cub1098s1cvl8454o1o57m9ha.png-w.jpg)

根据类名就很明了，`media`为容器 `media-left`为左侧图像(可right) `media-body`为与图像对应的内容，`media-heading`为标题

这样设置的媒体对象默认是顶部对齐的(内容较多时体现，图像会显示在靠上的位置)

中部对齐：媒体容器中添加`media-middle`

底部对齐：媒体容器中添加`media-bottom`

### 媒体列表
如果这样的内容有很多个，用这种div形式就有些不合适了，这时候可以用到媒体列表
创建ul列表添加`media-list`即可，字标签li的步骤同上面div一样
```html
<div class="container">
    <ul class="media-list">
        <li class="media">
            <a href="#" class="media-left"><img src="images/test.jpg"></a>
            <div class="media-body">
                <h2 class="media-heading">标题</h2>
                内容内容内容内容
            </div>
        </li>
    </ul>
</div>
```

### 面板
```html
<div class="container">
    <div class="panel panel-default">
        <div class="panel-body">
            内容
        </div>
    </div>
    <div class="panel panel-success">
        <div class="panel-heading">
            常规面板
        </div>
        <div class="panel-body">
            Hello
        </div>
        <div class="panel-footer">
            footer
        </div>
    </div><!--defaultPanel-->
    <div class="panel-default">
        <div class="panel-heading">表格面板</div>
        <div class="panel-body">
            <table class="table table-bordered">
                <thead>
                <tr>
                    <th>标题1</th>
                    <th>标题2</th>
                    <th>标题3</th>
                </tr>
                </thead>
                <tbody>
                <tr>
                    <td>内容1</td>
                    <td>内容2</td>
                    <td>内容3</td>
                </tr>
                <tr>
                    <td>内容1</td>
                    <td>内容2</td>
                    <td>内容3</td>
                </tr>
                <tr>
                    <td>内容1</td>
                    <td>内容2</td>
                    <td>内容3</td>
                </tr>
                </tbody>
            </table>
        </div>
    </div><!--tablePanel-->
    <div class="panel panel-info">
        <div class="panel-heading">列表面板</div>
        <ul class="list-group">
            <li class="list-group-item">aaa</li>
            <li class="list-group-item">aaa</li>
            <li class="list-group-item">aaa</li>
        </ul>
    </div><!--ulPanel-->
</div>
```
效果

![](http://t1.aixinxi.net/o_1cub311m018k71mbir0svm6q6ia.png-w.jpg)


### 具有响应式特性的嵌入内容
```html
<div class="container">
    <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" src="http://www.baidu.com"></iframe>
    </div>
</div>
```
![](http://t1.aixinxi.net/o_1cubdc6oum8r1mqp1ag19531ta8a.png-w.jpg)

### Well
div中添加类`well`就能有嵌入（inset）的简单效果。可选的添加`well-lg` `well-sm`来调整大小
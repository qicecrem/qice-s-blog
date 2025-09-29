# BootStrap
 它提供了响应式栅格系统、丰富的预建组件、实用的 CSS 工具类以及可插拔的 JavaScript 插件，帮助开发者快速构建跨设备、跨浏览器的一致化界面。
# 模板
```
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

   <script src="js/jquery-3.7.1.slim.min.js"></script>
    
    <script src="js/bootstrap.min.js"></script>
    <script>
      
    </script>
  </head>
  <body>

    <h1>你好，世界！</h1>

    
    
  </body>
</html>
```
# 响应式布局
## 实现
依赖于栅格系统:将一行平均分成12个格子,可以指定元素占几个格子
## 步骤
1. 定义容器
container :两边留白
container-fluid: 100%宽度
2. 定义行 样式:row
3. 定义元素 指定不同元素在不同设备上所占的格子数目 样式: col-设备代号-格子数目
#### 设备代号:
- xs 超小屏 手机 :col-xs-12
- sm 小屏 平板
- md 中等屏 桌面显示器
- lg  大屏 
** 注意: ** 
一行元素如果超过12,则超出部分自动换行
栅格属性可以向上兼容,栅格类适用于屏幕宽度大于或等于分界点大小的设备
如果正是设备宽度小于设置栅格类属性的设备代码的最小值,会一个元素占满一整行
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-6 col-md-4">内容 A</div>
    <div class="col-xs-12 col-sm-6 col-md-4">内容 B</div>
    <div class="col-xs-12 col-sm-6 col-md-4">内容 C</div>
  </div>
</div>
```
####  `.hidden-xs`, `.hidden-sm`, `.visible-lg-block` 等工具类，可在不同设备下隐藏或显示元素。
#  基础样式（Global CSS）
## 排版（Typography）
### 列表
- .list-unstyled 移除列表默认样式
- .list-inline 水平排列列表项
### 文本辅助
- text-muted 浅灰色次要文本
- .text-primary 主题色强调文本
- .text-right 右对齐文本
- .lead	 加粗加大文本
## 按钮
```html
<button class="btn btn-default">默认</button>
<button class="btn btn-primary">主要</button>
<button class="btn btn-success">成功</button>
<button class="btn btn-danger">危险</button>
```

* 大小：`.btn-lg`, `.btn-sm`, `.btn-xs`
* 块级：`.btn-block`
* 激活状态: `.active`
* 链接: `<a href="#" class="btn btn-primary btn-lg active" role="button">Primary link</a>`
* 禁用:  `<button type="button" class="btn btn-lg btn-primary" disabled="disabled">Primary button</button>`
## 图片
* `.img-responsive`：宽度自适应，保持比例
* 圆形：`.img-circle`
* 缩略图：`.img-thumbnail`
## 表格
```html
<table class="table table-bordered table-hover">
  <thead><tr><th>#</th><th>姓名</th><th>年龄</th></tr></thead>
  <tbody>
    <tr><td>1</td><td>张三</td><td>28</td></tr>
  </tbody>
</table>
```

* 条纹：`.table-striped`
* 悬停效果：`.table-hover`
* 紧凑：`.table-condensed`

## 表单
```html
<form>
  <div class="form-group">
    <label for="email">邮箱</label>
    <input type="email" class="form-control" id="email" placeholder="输入邮箱">
  </div>
  <button type="submit" class="btn btn-primary">提交</button>
</form>
```
* 水平表单：`.form-horizontal` + `.col-*-*`
* 行内表单：`.form-inline`
* 控件大小：`.input-lg`, `.input-sm`
# 组件
## 导航条
```
<nav class="navbar navbar-default">
  <!-- 导航栏容器，使用流体布局占满整个宽度 -->
  <div class="container-fluid">
    <!-- 导航栏头部区域，包含品牌标识和移动端菜单按钮 -->
    <div class="navbar-header">
      <!-- 移动端菜单切换按钮，点击后展开/收起导航菜单 -->
      <button type="button" class="navbar-toggle collapsed" 
              data-toggle="collapse" data-target="#nav-menu">
        <!-- 汉堡菜单图标，由三个横线组成 -->
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <!-- 品牌标识，通常是网站名称或Logo，点击返回首页 -->
      <a class="navbar-brand" href="#">品牌</a>
    </div>

    <!-- 可折叠的导航菜单区域，小屏幕时会隐藏 -->
    <div class="collapse navbar-collapse" id="nav-menu">
      <!-- 主导航链接，水平排列 -->
      <ul class="nav navbar-nav">
        <!-- 当前激活页面（首页），会高亮显示 -->
        <li class="active"><a href="#">首页</a></li>
        <!-- 普通导航链接 -->
        <li><a href="#">链接</a></li>
        
        <!-- 示例：下拉菜单（可展开的子菜单） -->
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown">
            更多 <span class="caret"></span> <!-- 下拉箭头图标 -->
          </a>
          <ul class="dropdown-menu">
            <li><a href="#">子链接1</a></li>
            <li><a href="#">子链接2</a></li>
          </ul>
        </li>
      </ul>

      <!-- 示例：右对齐导航项（如用户菜单、搜索框） -->
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">登录</a></li>
        <li><a href="#">注册</a></li>
      </ul>
    </div>
  </div>
</nav>
```
## 面板
```html
<div class="panel panel-primary">
  <div class="panel-heading">标题</div>
  <div class="panel-body">内容</div>
  <div class="panel-footer">页脚</div>
</div>
```
##  标签页（Tabs）与手风琴（Collapse）
###  标准标签（.nav-tabs）
```
<ul class="nav nav-tabs">
  <li class="active"><a href="#tab1" data-toggle="tab">标签1</a></li>
  <li><a href="#tab2" data-toggle="tab">标签2</a></li>
</ul>

<div class="tab-content">
  <div id="tab1" class="tab-pane fade in active">内容1</div>
  <div id="tab2" class="tab-pane fade">内容2</div>
</div>
```
### 胶囊标签（.nav-pills）
```
<ul class="nav nav-pills">
  <li class="active"><a href="#pill1" data-toggle="pill">标签1</a></li>
  <li><a href="#pill2" data-toggle="pill">标签2</a></li>
</ul>

<div class="tab-content">
  <div id="pill1" class="tab-pane fade in active">内容1</div>
  <div id="pill2" class="tab-pane fade">内容2</div>
</div>
```
### 手风琴（Accordion）
手风琴是一种垂直折叠面板，允许用户展开 / 收起内容，常用于信息分层展示。它基于 Bootstrap 的 Collapse 插件 实现。
```
<div class="panel-group" id="accordion">
  <!-- 面板1 -->
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title">
        <a data-toggle="collapse" data-parent="#accordion" href="#collapse1">
          面板标题1
        </a>
      </h4>
    </div>
    <div id="collapse1" class="panel-collapse collapse in">
      <div class="panel-body">内容1</div>
    </div>
  </div>

  <!-- 面板2 -->
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title">
        <a data-toggle="collapse" data-parent="#accordion" href="#collapse2">
          面板标题2
        </a>
      </h4>
    </div>
    <div id="collapse2" class="panel-collapse collapse">
      <div class="panel-body">内容2</div>
    </div>
  </div>
</div>
```
## 提示（Tooltip）与弹出框（Popover）

```js
$('[data-toggle="tooltip"]').tooltip();
$('[data-toggle="popover"]').popover();
```

* 在触发元素上添加 `data-toggle` 属性
* 可通过 JS 配置位置、触发方式
##  模态框（Modal）

```html
<button data-toggle="modal" data-target="#myModal">打开模态框</button>
<div class="modal fade" id="myModal">
  <div class="modal-dialog">
    <div class="modal-content">
      <!-- .modal-header、.modal-body、.modal-footer -->
    </div>
  </div>
</div>
```
# 插件
所有插件依赖于 jQuery，通过调用方法或在标签上添加 `data-` 属性初始化。

| 插件名称      | 功能描述  |
| --------- | ----- |
| Carousel  | 轮播图   |
| Dropdown  | 下拉菜单  |

`

`
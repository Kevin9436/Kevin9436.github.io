---
layout: post
title: "CSS学习笔记（一)"
author: Kevin9436
date: 2018-06-21 20:10
category: notes
---

之前简单写了个个人主页，用的是别人的模板，基本功能算是都实现了，但是很多地方都还不能让我满意。于是本着生命不止折腾不息的信念开始学习CSS，之后想按照自己想法实现网页的各种样式，在此也顺便记录一下我的学习过程。首先介绍一下我的学习主要资源：[菜鸟联盟](http://www.runoob.com)，上面有很多资源供学习。  
下文中我感觉比较重要的属性就详细的记录了，其余的见网站。  

***

# 1 CSS语法
选择器 {属性:值; 声明;...;声明}  
h1 {color:blue; font-size:19px;}  
注释结构： /\*blabla\*/
# 2 CSS选择器
摘自[Lambert和Elvirangle的笔记](http://www.runoob.com/css/css-id-class.html)
## 2.1 ID选择器
ID选择器（ID selector，IS）：使用 # 标识selector，语法格式：`#S{...}`（S为选择器名）。  
```
<style>
#name{
  color:red;
}
</style>
<!--下面文字是红色的-->
<p id="name">red text</p>
```  
## 2.2 类选择器
类选择器（class selector，CS）：使用 . 标识selector，语法格式：`.S{...}`（S为选择器名）。  
```
<style>
.value{
  text-align:center;
}
</style>
<!--下面的文字是居中对齐的-->
<p class="value">center text</p>
```  
## 2.3 元素选择器
元素选择器（element selector，ES）：又叫标签选择器，使用标签名作为selector名，语法格式：`S{...}`（S为选择器名）。  
```
<style>
p{
  font-style:italic;
}
</style>
<!--下面的文字是斜体的-->
<p style="font-style:italic">italic text</p>
```  
## 2.4 属性选择器
属性选择器（attribute selector，AS）：ES其实是AS的一个特例，在AS基础上还能对selector描述得更具体，语法格式为 `E[attr[~=][|=][^=][$=][*=]VALUE]{...}`，是并没有得到所有浏览器支持的选择器，因此不举例。
## 2.5 包含选择器
包含选择器（package selector，PS）：指定目标选择器必须处在某个选择器对应的元素内部，语法格式：`A B{...}`（A、B为HTML元素/标签，表示对处于A中的B标签有效；A也可为类名，写法为.A）。  
```
<style>
p{
  color:red;
}
div p{
  color:yellow;
}
</style>
<p>red text</p><!--文字是红色的-->
<div>
  <p>yellow text</p><!--文字是黄色的-->
</div>
```  
## 2.6 子选择器
子选择器（sub-selector，SS）：类似于PS，指定目标选择器必须处在某个选择器对应的元素内部，两者区别在于PS允许"子标签"甚至"孙子标签"及嵌套更深的标签匹配相应的样式，而SS只匹配子标签，语法格式：`A>B{...}`（A、B为HTML元素/标签；A也可为类名，写法为.A）。  
```
<style>
div>p{
  color:red;
}
</style>
<div>
  <p>red text</p><!--文字是红色的-->
  <table>
    <tr>
      <td>
        <p>no red text;</p><!--文字是非红色的-->
      </td>
    </tr>
  </table>
</div>
```  
## 2.7 相邻兄弟选择器
相邻兄弟选择器（Adjacent sibling selector）可选择紧接在另一元素后的元素，且二者有相同父元素。语法格式：`A+B{...}`    
```
<style>
div+p
{
  background-color:yellow;
}
</style>
<div><p>白色背景</p></div>
<p>黄色背景</p>
<p>白色背景</p>
```  
## 2.7 后续兄弟选择器
后续兄弟选择器选取所有指定元素之后的相邻兄弟元素，语法格式：`A~B{...}`（A、B为HTML元素/标签；A也可为类名，写法为.A）。  
```
<style>
div~p{
  color:red;
}
</style>
<div><p>no red text</p><div>
<p>red text</p> <!--文字是红色的-->
<p>red text</p> <!--文字还是红的-->
<h1>headline</h1>
<p>red text</p> <!--文字还是红的-->
```  
## 2.8 通用选择器
语法形式为：\*{属性：属性值}。它的作用是匹配 html 中的所有元素标签。  
```
<!--使用html中任意标签元素字体颜色全部设置为红色：-->
<style>
*{color:red;}
</style>
<body>
<h1>标题为红色</h1>
<p>段落也为红色</p>
</body>
```  
## 2.9 分组选择器
样式表中有具有相同样式的元素，可将每个选择器用逗号分开。  
```
h1,h2,p
{
color:green;
}
```  
# 3 样式表
## 3.1 外部样式表
样式应用于多个页面，html文件连接到外部的css文件。每个页面使用 &lt;link&gt; 标签链接到样式表, &lt;link&gt; 标签在（文档的）头部：  
```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```  
## 3.2 内部样式表
在单个html文件中设置样式，可使用 &lt;style&gt; 标签定义格式。
## 3.3 内联样式表
在单个元素上使用样式。例如：  
```
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```  
## 3.4 多重样式优先级
- 内联样式 > ID选择器 > 伪类 > 属性选择器 > 类选择器 > 元素选择器 > 通用选择器  
- !important规则例外：当 !important 规则被应用在一个样式声明中时,该样式声明会覆盖CSS中任何其他的声明, 无论它处在声明列表中的哪里。 (不建议使用)

## 4 背景
- *background-color* 可用16进制、RGB和颜色名称
- *background-image* 默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体
- *background-repeat* 平铺属性：*-x* 水平方向；*-y* 垂直方向
- *background-attackment* 背景图像是否固定或者随着页面的其余部分滚动：scroll 滚动(默认);fixed 固定的;inherit 继承父类
- *background-position* 设置背景图像的起始位置
- *background* 简写，属性顺序如上

## 5 文本
- *color* 可用16进制、RGB和颜色名称
- *text-decoration* 文本修饰：overline、line-through、underline
- *text-indent* 第一行缩进
- *text-align* 文本对齐：center、left、right、justify
- *letter-spacing* 字符间距
- *word-spacing* 字间距

## 6 字体
- *font-family* 字体属性
- *font-size* 字体大小
- *font-style* 字体样式：normal、italic、inherit
- *font-weight* 字体粗细

## 7 链接
- *a:link* 正常，未访问过的链接
- *a:visited* 用户已访问过的链接
- *a:hover* 当用户鼠标放在链接上时
- *a:active* 链接被点击的那一刻  
（设置的顺序不可变换）

## 8 列表
- *list-style-type* 列表项标记的类型
- *list-style-image* 指定图片为列表项标记
- [浏览器兼容性解决方案](http://www.runoob.com/css/css-list.html)

## 9 表格
- *boder* 边框格式
- *width*
- *height*
- *text-align*
- *vertical-align*
- *padding* 表格填充
- *background* 背景
- *color* 表格字体颜色

## 10 盒子模型
![盒子模型图解](http://www.runoob.com/images/box-model.gif)

## 11 边框
- *boder-witdth* 
- *boder-style*
- *boder-color*
- 可分别设置上下左右边框，可简写

## 12 轮廓
轮廓（outline）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

## 13 外边距
margin 清除周围的（外边框）元素区域。margin 没有背景颜色，是完全透明的，可单独改变上下左右的外边距，可简写。
- *auto* 设置浏览器边距，结果依赖于浏览器
- *length*
- *%* 适用百分比定义边距
- margin可为负，重叠

## 14 内边距（填充）
当元素的 padding（填充）内边距被清除时，所释放的区域将会受到元素背景颜色的填充。
- *length*
- *%*

## 15 尺寸
CSS可根据像素值或者百分比来进行元素尺寸设置，个人感觉百分比更好一些，在不同屏幕上也能够更好地适配。此外还可以定义元素的最大最小长宽。

## 16 显示
### 16.1 隐藏
- *visibility:hiden* 不可见但是留位置
- *display:none* 不可见也不留位置

### 16.2 块级元素(block)和内联元素(inline)
块级元素
- 总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示
- 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制
内联元素
- 和相邻的内联元素在同一行
- 宽度(width)、高度(height)、内边距的top/bottom和外边距的top/bottom都不可改变，就是里面文字或图片的大小

## 17 定位
- *position* static;fixed;relative;absolute;sticky
- *overflow* 设置当元素的内容溢出其区域时发生的事情。
- *left*/*right*/*top*/*bottom*
- *z-index* 设置元素的堆叠顺序
- *cursor* 显示光标移动到指定的类型

## 18 浮动
- *float* 一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。浮动元素之后的元素将围绕它。浮动元素之前的元素将不会受到影响。
- *clear* 元素浮动之后，周围的元素会重新排列，为了避免这种情况，使用 clear 属性，clear 属性指定元素两侧不能出现浮动元素。
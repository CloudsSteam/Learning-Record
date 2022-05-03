[toc]
## @路径
at-rule:@规则，@语句，css语句，css指令

1. import
@import "路径"；
导入另外一个css文件


2. charset

@charset"utf-8";
告诉浏览器该css文件，使用的字符编码集是utf-8，必须写到第一行

## web字体和图标

### web字体
用户电脑上没有安装相应字体，强制让用户下载该字体
使用@font-face指令制作一个新字体
```
@font-face{
    font-famly:"good night";
    src:url("./font/晚安体.ttf");
}
p{
    font-family:"good night";
}
```

### 字体图标

iconfont.cn

在线离线代码

## 块级格式化上下文
全称Block Formatting Context 简称BFC
独立的渲染区域，它规定了在该区域中，常规流块盒的布局

- 常规流块盒在水平方向上，必须撑满包含块
- 在包含块的垂直方向上依次摆放
- 常规流块盒若外边距无缝相邻，则进行外边距合并
- 常规流块盒的自动高度和摆放位置，无视浮动元素

浮动元素 定位元素 overflow元素

创建BFC属性元素，自动高度需要计算浮动元素
解决高度坍塌创建BFC属性更改overflow:hidden达到效果
`.clearfix{overflow:hidden;}`

创建BFC元素，边框盒不会与浮动元素重叠
常规流盒会避开浮动元素，不能无视浮动元素了

创建BFC元素，不会和它子元素进行外边距合并
(不同BFC的外边距不能合并渲染互不干扰，同一个BFC才能)


## 布局
### 多栏布局
两栏布局    三栏布局
侧边栏常用
左float:left右overflow:hidden(左定宽右不定宽)

### 等高

1. CSS3的弹性盒
2. JS控制
3. 伪等高

### 元素书写顺序
优先书写浮动元素,因常规流会无视它
若要优先搜索引擎优化书写主要元素则margin:(0.Xpx);

### 后台页面布局

>顶部直接固定定位，下面容器height100%然后设置padding-top和box-sizing，浏览器不管高宽都适应
>再下面分别左右浮动高度相对于父元素直接100%(设置百分比看包含块)，有需求再overflow:auto调出滚动条


## 浮动细节规则

浮动盒子的顶边不得高于上一个盒子的顶边
若剩余空间无法放下浮动的盒子，则该盒子向下移动，直到具备足够的空间能容纳盒子，然后再向左或右移动


## 行高的取值

line-height

- px像素值
- 无单位的数字  /(先继承倍数，再计算子元素)
- em单位    /当前字体大小倍数，(先计算像素值，再继承)
- 百分比

设置line-height像素固定值，子元素字体大小不一致不好控制

## body的背景

背景颜色填充的是边框盒

**画布 canvas**
一块区域
渲染区域

- 最小宽度为视口宽度
- 最小高度为视口高度

**HTML元素背景**
覆盖画布

**body元素背景**
如果HTML元素有背景，body元素正常(背景覆盖边框盒)
如果HTML元素没有背景，body元素的背景覆盖画布


**关于画布景图**
- 背景图的宽度百分比，相对于视口(无关body元素宽度)  /设置body背景颜色没问题
- 背景图的高度百分比，相对于网页高度
- 背景图的横向位置百分比，预设值，相对于视口
- 背景图的纵向位置百分比，预设值，相对于网页高度
>奇奇怪怪的

## 行盒的垂直对齐
### 多个行盒垂直方向上的对齐
给没有对齐元素设置vertical-align

vertical-align:middle;(top,bottom,text-bottom,text-top,super,sub,middle..数值调整)
预设值
数值


### 图片的底部白边

图片的父元素是一个块盒，块盒高度自动，图片底部和父元素底边之间往往会出现空白

解决方法
- 设置父元素的字体大小为0
- 将图片设置为块盒

## 参考线-深入理解字体
font-size,line-height,vertical-align,font-family
### 文字

文字通过一些文字制作软件制作，比如fontforge
制作文字时，会有几根参考线，不同的文字类型，参考线不一样
同一种文字类型参考线一致

文字对齐
top
(line gap)

text top,ascent,顶线
super,上基线
baseline，基线
sub，下基线
text bottom，descent，底线

(line gap)
bottom
(五条线主要起文字对齐作用)

### font-size
字体大小，设置的是文字的相对大小

文字的相对大小，看字体比值*设置的像素

文字顶线到底线的距离，是文字的实际大小(content-area,内容区)

### 行高
顶线向上延申的空间，和底线向下延申的空间，两个空间相等，该空间叫做gap(空隙)

gap默认情况下，是字体设计者决定
top到bottom叫做virtual-area(虚拟区)

行高，就是virtual-area

行高设为实际大小
line-height:normal;

### vertical-align

决定参考线：font-size，font-family，line-height

一个元素如果子元素出现行盒，该元素内部也会产生参考线

- baseline：该元素的基线与父元素的上基线对齐
- super:该元素的基线与父元素的上基线对齐
- sub：该元素的基线与父元素的下基线对齐
- text-top:该元素的virtual-area的顶边，对齐父元素的text-top
- text-bottom:该元素的virtual-area的定边，对齐父元素text-bottom
- top：该元素的virtual-area的定边，对齐父元素的顶边(该行中的最低底边line-box的顶边)
- bottom：该元素的virtual-area底边，对齐父元素的底边(该行汇总的最低底边line-box的底边)

行盒组合起来，可以形成多行，每一行的区域叫做line-box，line-box的顶边是该行内所有行盒最高顶边，底边是该行行盒的最低底边。

实际，一个元素的实际占用高度(高度自动)，高度的计算通过line-box计算

行盒：lnline-box
行框：line-box


## 堆叠上下文

堆叠上下文(stack context),它是一块区域，这块区域有某个元素创建，它规定了该区域中的内容在z轴上排列的先后顺序

### 创建堆叠上下文的元素

- html元素(根元素)
- 设置了z-index(**非auto**)数值的定位元素

有堆叠上下文的排在后面
### 同一个堆叠上下文中元素在z轴上的排列

从后到前的排列顺序：
1. 创建堆叠上下文的元素的背景和边框(创建堆叠上下文，子元素也是堆叠上下文，父元素永远在最后)
2. 堆叠级别(z-index,stack level)为负值的堆叠上下文  /都是负数，值越大越靠前。值相同后面覆盖前面
3. 常规流非定位的块盒   /先刷背景，再刷负数，再常规流块盒
4. 非定位的浮动盒子     /浮动盒子
5. 常规流非定位行盒     /覆盖了背景没有覆盖文字(p元素块盒，生成匿名行盒)，而span是行盒背景都不会覆盖
6. 任何z-index是auto的定位子元素，以及z-index是0的堆叠上下文
7. 堆叠级别为正值的堆叠上下文

每个堆叠上下文，独立于其他堆叠上下文，它们之间不能相互穿插


## svg

svg:scalable vector graphics可缩放的矢量图

1. 该图片使用代码书写而成
2. 缩放不会失真
3. 内容轻量

### 怎么使用
svg可以嵌入浏览器，也可以单独成为一个文件

img`<img src="imgs/weixin.svg" alt="">`  
背景图`backgroud:url("imgs/weixin.svg") no-repeat center/cover`
embed嵌入资源(`<embed src="imgs/weixin.svg" type="image/svg+xml">`)
object`<object data="imgs/weixin.svg" type="image/svg+xml"></object>`
iframe`<iframe src="imgs/weixin.svg"></iframe>`

rect矩形
circle圆形
ellipse椭圆
line线条
polyline折线(fill设置透明或者none，把stroke描边打开)
polygon多边形 
path路径
M = moveto                       (移动光标到/开始于 某个位置)
L = lineto                      （直线）
H = horizontal lineto           （水平线）
V = vertical lineto             （垂直线）
C = curveto                     （三次曲线）
S = smooth curveto              （平滑三次曲线）
Q = quadratic Bézier curve       （二次贝塞尔曲线）
T = smooth quadratic Bézier curveto
A = elliptical Arc               （椭圆弧）
Z = closepath                    （闭合）

A
半径1
半径2
顺时针旋转角度
小弧(0)或大弧(1)
顺时针(1) 逆时针(0)
终点坐标


属性
cx，cy中心点
fill填充颜色
stroke描边颜色以及宽度

## 数据链接

data url

### 书写方式

数据链接：将目标文件的数据直接书写到路径位置

语法：data:MIME,数据

优点：
1. 减少了浏览器中的请求
减少请求中浪费的时间
2. 有利于动态生成数据
缺点：
增加了资源的体积
导致了传输内容增加，从而增加了单个资源的传输时间
不利于浏览器的缓存
浏览器通常会缓存图片文件，css文件，js文件
会增加原资源的体积到原来的4/3

应用场景：
1. 但请求单个图片体积较小，并且该图片因为各种原因，不适合制作雪碧图，可以使用数据链接。
2. 图片由其他代码动态生成，并且图片较小，可以使用数据链接。

### base64
一种编码方式
通常用于将一些二进制数据，用一个可书写的字符串表示。


## 浏览器的兼容性
- 市场竞争
- 标准版本的变化

### 厂商前缀
比如：box-sizing，谷歌旧版本浏览器中使用-webkit-box-sizing:border-box

- 市场竞争，标准没有发布
- 标准仍在讨论中(草案)，浏览器厂商希望先支持

IE: -ms-
Chrome,safari: -webkit-
opera: -o-
firefox: -moz-

浏览器处理样式或元素时，使用如下方式
当遇到无法识别的代码时，直接略过

1. 谷歌浏览器的滚动条样式

div::-webkit-scrollbar{
    滑动栏
}

div::-webkit-scrollbar-track{
    轨道
}

div::-webkit-scrollbar-thumb{
    滑动块
}

div::-webkit-scrollbar-track{
    两端按钮
}

实际上，在开发使用中自定义的滚动条，往往是使用div+css+js实现的

2. 多个背景图中选一个作为背景

根据尺寸和网络条件来自行选择
background-image:-webkit-image-set(url("img/small.jpg")1x,url("img/big.jpg")2x);

### css hack
补丁
根据不同的浏览器(主要针对IE)，设置不同的样式和元素

1. 样式
IE中，css的特殊符号
_属性       兼容IE5，6
*属性       IE5，6，7都能识别
属性值\9    兼容ie5~ie11
属性值\0    兼容ie8~ie11
属性值\9\0  兼容ie9~ie10

```
只能ie浏览器识别
<!--[if IE]〉
<p>
    这是浏览器
</p>|
<![endif]-->
```

```
针对低版本ie浏览器不识别
<!--[if !(IE)]><-->
<p>
    这是非浏览器
</p>
<!--<![endif]-->
```
`<!--[if !(lt IE8)]><--> 小于ie8不识别`
> ie6外边距bug，浮动元素的左外边距翻倍

### 渐近增强 和优雅降级

两种解决兼容性问题的思路，会影响代码的书写风格
- 渐进增强：先适应大部分浏览器，然后针对新版本浏览器加入新的样式
书写代码时，先尽量避免书写有兼容性问题的代码，完成后，再逐步加入新标准中的代码。

- 优雅降级：先制作完整的功能，然后针对低版本浏览器进行特殊处理
书写代码时，先不用特别在意兼容性，完成整个功能后，再针对低版本浏览器处理样式。

### caniuse
查找css兼容性
[caniuse.com](https://caniuse.com/)




## 居中总结

居中：盒再其包含块中居中

### 行盒(行块盒)水平居中
直接设置行盒(行块盒)父元素`text-align:center`子元素行盒也能居中

### 常规流块盒水平居中
定宽，设置左右margin为auto

### 绝对定位元素的水平居中
定宽，设置左右坐标为0(left:0,right:0),将左右margin设置为auto
>实际上，固定定位(fixed)是绝对定位(absolute)的特殊情况

### 单行文本的垂直居中
设置文本所在元素的行高，为整个区域的高度

### 行块盒或块盒内多行文本的垂直居中

没有完美方案
设置盒子上下内边距相同。达到类似效果

### 绝对定位的垂直居中
定高，设置上下坐标为0(top:0,bottom:0),将上下margin设置为auto



## 样式补充

### display:list-item
设置为该属性值的盒子，本质上仍然是一个块盒，但同时该盒子会附带另外一个盒子
(就是li前面的小圆点，为次盒子，后面主区域为主盒)
元素本身生成的盒子叫做主盒子，附带的盒子称为次盒子，次盒子和主盒子水平排列


涉及的css：
1. ```list-style-type```
设置次盒子中内容的类型

2. ```list-style-position```
设置次盒子相对于主盒子的位置

3. 速写属性```list-style```上面两个一起写

4. ```list-style-image```设置图片
**清空次盒子**
list-style:none

### 图片失效时的宽高

如果img元素的图片链接无效，img元素的特性和普通行盒一样，无法设置宽高
则设置为块盒就有效宽高

### 行盒中包含行块盒或可替换元素

行盒的高度与它内部的行块盒或可替换元素的高度无关


### text-align:justify

text-align:start;从起始位置对齐

- left:左对齐
- right:右对齐
- center:居中
- justify:除最后一行外，分散对齐(空白平均分布)

### 制作一个三角形
透明隐藏不需要的

### direction 和writing-mode

开始start->结束end
左left->右end
开始和结束是相对的，不同国家有不同的习惯
左右是绝对的
direction设置的是开始到结束的方向(rtl,ltr)
writing-mode:设置文字书写方向(垂直书写，从右到左2)

### utf-8编码

### 项目开发注意事项
- 重视心态
- 摆正心态
- 独立完成

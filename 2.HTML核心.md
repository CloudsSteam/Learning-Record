

[toc]
## 第一个网页


Emmet插件自动生成

## 注释
注释不参与运行
注释格式书写
```
<!-- 添加注释 -->
```

## 元素
```
<a href="http://www.duyiedu.com" title="黑龙江渡一教育">渡一教育</a>
    <title>Document</title>
```
整体：element 元素

元素=起始标记(begin tag)+结束标记(end tag)+元素内容+元素属性

属性=属性名+属性值

属性的分类
-局部属性：某些元素特有属性
-全局属性：所有元素通用
有些元素没有结束标记，这样的元素叫做**空元素**
两种写法
```
<meta charset="UTF-8">
<meta charset="UTF-8" /> /闭环
```

## 元素的嵌套
元素不能相互嵌套
父元素，子元素，祖先元素，后代元素，兄弟元素

## 标准的文档结构
```
<!DOCTYPE html>     /文档申明，告诉浏览器当前文档使用的标准是HTML5.不写导致浏览器进入怪异渲染模式
<html lang="en">    /html根元素不必需，可隐含。XHTML必需。lang属性：或zh-CN，cmn-hans
<head>              
    <meta charset="UTF-8">  /meta为文档的元数据：附加信息。charset为内容编码
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  /适配手机端
    <meta http-equiv="X-UA-Compatible" content="ie=edge">       /适配ie浏览器
    <title>Document</title>
</head>
<body>
           /文档体，页面上所有要参与显示的元素，都应该放置到文档体中
</body>
</html>
```

## 语义化

1. 每个HTML元素都有具体的含义
a元素：超链接
p元素：段落
h1元素：一级标题
2. 所有元素与展示效果无关
浏览器带有默认的css样式，所有每个元素有一些默认样式
**重要：选择什么元素，取决于内容的含义，而不是显示出的效果**
元素展示到页面中的效果应该由css决定

3. 为什么需要语义化?
为了搜索引擎优化(SEO)
每隔一段时间，搜索引擎会从整个互联网中，抓取页面源代码
为了让浏览器理解网页
阅读模式，语音模式

## 文本元素
**快速生成标签**
`h$*6>{$级标题}          >表子元素，{}表补充文本，$占位符自动补充`
### h
表1级标题~6级标题
### p
段落，paragraphs
> lorem,乱数假文，没有任何实际含义的文字
### span[无语义]
没有语义，仅设置样式
块级元素是独占一行，行级元素不行
>某些元素在显示时会独占一行(块级元素)，而某些元素不会(行级元素)
```
块级转行级display:inline /行级元素没有高度
行级转块级但是又不独占一行（display：inline-block）
行级元素与块级元素的切换可以通过修改display属性实现）
1.display:inline;//将块级元素转化为行级元素，这时块级元素设置的宽高无效
2.display:block;//将行级元素转块级元素，这时原本的行级元素会变成块级元素独占一行，同时可以设置宽高
3.display:inline-block;//将行级元素转块级元素，不会独占一行，可以设置宽高
```
- 行内元素：a img span b strong input select section 
- 块级元素：div p table ul lo li h1-h6 dl dt 
- 空元素：br hr img input link meta 

>现到了HTML5，已经弃用这种说法。元素代表什么含义，与显示无关/来自w3c官方文档

### pre
预格式化文本元素
空白折叠：在源代码中的连续空白字符(空格，换行，制表)，在页面显示时，会被折叠为一个空格
而在pre元素内部出现的内容，会按照源代码格式显示到页面上。/<pre
通常在网页中显示源代码，pre元素功能的本质：它靠一个默认的css属性，style="whithe-space:pre"
若要显示代码时，通常外面套code元素，code表示代码区域

### HTMl实体
实体字符，HTMLEntity
实体字符通常用在页面中显示一些特殊符号
- &单词;
- &#数字;

小于lt，大于gt，空格nbsp，版权符号copy,&符号amp


### a元素

超链接，跳转即超链接
#### href属性
hyper reference:通常表示跳转地址
- 跳转地址
- 跳转某个锚点
- 功能链接      
/点击后触发某个功能例.执行js代码(javascript:).发送邮件(mailto:)拨号(tel:)
```
<a href="www.licensor993.com">
    baidu
</a>
```

**速写标签**
```
a[href="#chapter$"]*6>{章节$}
((h2[id="chapter$"]>{章节$})+p>lorem10)*6
```
#### target属性
新开标签页还是在覆盖源标签页
两种取值
- _self:在当前页面窗口打开，默认
- _blank:在新窗口中打开


## 路径的写法
绝对路径和相对路径
1. 绝对路径格式：
```
协议名://主机名:端口号/路径
协议名:http,https,file
主机名：域名，IP地址
端口号：http对应80，https对应443
```

2. 相对路径格式
以./开头，./表示当前资源所在的目录
../表示返回上一级目录

```
```

## 图片元素
img元素，空元素
src属性:source，图片路径
alt属性:当图片资源失效时，将使用该属性文字替代图片

### 和a元素联用
点击图片跳转链接
```
    <a href="">
        <img src="" alt="">
    </a>
    
```
### map元素
点图片不同位置就跳转相应的网址
map子元素：area
```
    <a href="">
        <img usemap="#solarMap" src="" alt="">
    </a>
    <map name="solarMap">
        <area shape="circle" coords="(x,y,r)" href="" alt="" target="">            /圆形
        <area shape="rect" coords="(左上角xy，右下角xy)" href="" alt="" target="">   /矩形
        <area shape="poly" coords="(四个点的xy)" href="" alt="" target="">          /多边形
    </map>
    /其原点在图片左上角
```
### figure元素
指代，定义，通常用于把图片图片标题描述包裹起来
子元素：figcaption(把标题包起来)

## 多媒体元素
### video视频
```
    <video src=""></video>
```
- controls:控制控件的显示(有些默认是关闭需打开)
`controls="controls"`
某些属性，只有两种状态：1.不写 2.取值为属性名，这种属性叫做**布尔属性**
而布尔属性，在HTML5中，可以不用书写属性值，直接为controls
 
- autoplay:布尔属性，自动播放
- muted:布尔属性，静音播放
- loop:循环播放

### audio音频
和视频布尔属性完全一致
```
    <audio src=""></audio>
```

### 兼容性
1. 旧版本的浏览器不支持这两个元素

2.  不同浏览器支持音视频格式可能不一致
```
<video controls autoplay muted loop style="width:500px;">
    <source src="media/open.mp4">
    <source src="media/open.webm">
</video>
```

## 列表元素
### 有序列表
ol:ordered list
li:list item
```
<ol type=" ">/1,i,a,A(type属性用途除非很重要，不然用css定制前置样式)
    <li>    </li>
    <li>    </li>
    <li>    </li>
    <li>    </li>
    <li>    </li>
    <li>    </li>
</ol>
```
### 无序列表
ul：unordered list
无序列表常用于制作菜单或新闻列表
改属性便可达到有序列表的样式。不要为了样式而选择列表css中(list-style-type: ;)

### 定义列表
通常用于一些术语的定义
dl:definition list
dt:definition title
dd:definition description
```
<dl>
    <dt></dt>
    <dd>
         
    </dd>
</dl>
```

## 容器元素
容器元素：该元素代表一个块区域，内部用于放置其他元素
没划分好容器，直接影响到后续css样式制作

### div元素
没有语义，非常纯净，需要样式css来加
### 语义化容器元素
header:通常用于表示页头，也可以用于表示文章头部
footer：通常用于表示页脚，也可以表示文章尾部
artcle:通常用于表示整篇文章
section:通常用于表示文章的章节
aside:通常表示侧边栏
什么情况都用对应的容器，方便整理查看，样式css都可以做

## 元素包含关系
>以前：块级元素独占一行，行级元素不换行
>块级元素可以包含行级元素，行级元素不可以包含块级元素，a元素除外

> 现：元素的包含关系由元素的内容类别决定。内容类别MDN查看
总结：
1. 容器元素中可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的子元素(ul>li,ol>li,dl>dt+dd)
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素


## 百度新闻练习

**快速生成标签**
`ul*5>(li>h3>a>lorem5)+(li*6>a>lorem5)`

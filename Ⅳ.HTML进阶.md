# HTML进阶
## iframe元素
 
通常用于在网页中嵌入另一个页面
iframe可替换元素

1. 通常行盒
2. 通常显示的内容取决于元素的属性
3. css不能完全控制其中的样式
4. 具有行块盒的特点

target="_blank"点击跳转新页面，(name="myframe",target="myframe")
应用：b站视频搬用套用

## 在页面中引用(flash)
object
embed       /和object一样设置
它们都是可替换元素
MIME多用途互联网邮件类型
比如MIME:image/jpeg
```
<object data="资源地址" type="MIME资源类型">     
    <param name="" value="">    /传参
</object>
```

浏览器兼容性写法

    <object data="" type="">
        <param name="" value="">
        <embed src="" type="">
    </object>


## 表单元素
一系列元素用于收集用户数据

### input元素
-   type属性:输入框类型
    text      普通文本输入框
    password  密码框
    date      日期选择框，兼容性问题
    search    搜索框,兼容性问题
    range     滑块
    color     颜色选择
    number    数字输入框
    checkbox  多选框    /默认选中加checked
    radio     单选框    /加name值划为同一类(name="值")
    image



- value属性：输入框初始显示的值
- placeholder属性：显示提示的文本，点击文本框输入内容文本消失
    (type="password" placeholder="请输入密码")
    
设置::placeholder样式(伪元素)


input元素可以制作按钮

当type值为reset重置，button普通，submit提交时，input表示按钮



### select元素

下拉列表选择框
```
    <select>
        <option >成都</option>
        <option >北京</option>
        <option selected>哈尔滨</option>
    </select>
    
```
通常和option元素配合使用    /selected布尔属性默认选中

`<optgroup> </optgroup>`也可分组再选项，组名不可选m中

若要多选列表则加上`<select multiple>`

### textarea元素
文本域，多行文本框
`<textarea name="" id="" cols="30列" rows="10行"></textarea>`
一般都用css来书写样式

css属性
>resize:none，both两个方向都可以，horizontal水平，vertical垂直可调整


### 按钮元素
button
type属性：reset，submit，button，默认值submit

### 表单状态

readonly属性：布尔属性，是否只读，不会改变表单显示样式

disabled属性：布尔属性，是否禁用，会改变表单显示样式

### 配合表单元素的其它元素

#### label
通常配合单选和多选框使用
标签文本

- 显示关联
可以通过for属性，让label元素关联某一个表单元素，for属性书写表id的值 
id和for关联起来，点label也可选中
```
    <input id="radMale" name="gender" type="radio">
    <label for="radMale">男</label>
```

- 隐式关联
直接把input放label里面(省了for)
label 内联应用应该把for属性去除 
```
    
    <label >
        <input name="gender" type="radio">
    男</label>
```

#### datalist
数据列表
该元素本身不会显示到页面，通常用于和普通文本框配合

通过id关联快速显示预览词条

#### form元素

通常，会将整个表单元素，放置form元素的内部，作用是当提交表单时，会将form元素内部的表单内容以合适的方式提交到服务器。

form元素对开发静态页面没有什么意义


#### fieldsed元素
语义分组

## 美化表单元素

### 新的伪类

1. focus元素聚焦时的样式

tabindex优先聚焦选中
```
tabindex="数字"
```

2. checked

单选或多选框被选中的样式

```
input:checked+label{
    color:red;
}
```
一般用于配置选中兄弟元素样式意想不到

### 常见用法
1. 重置表单元素样式

2. 设置textarea是否允许调整尺寸
resize:none
both两个方向都可以
horizontal水平
vertical垂直可调整

3. 文本框边缘到内容的距离
input{padding:0 10px;}
textarea{text-indent:1em;}

4. 控制单选和多选框

## 表格元素


## 其他元素

1. abbr
缩写词
2. time
提供给浏览器或搜索引擎阅读的时间
3. b(bold)
无语义元素，主要用于加粗字体
4. q
一小段应用文本
5. blockquote
大段引用的文本
6. br 
主要用于再文本中换行
7. hr
主要用于分隔
8. meta
还可以用于搜索引擎优化(SEO)
9. link
链接外部资源(CSS，图标)
rel属性：relation，链接的资源和当前网页的关系
网站图标
`<link rel="shortcut icon" type="image/x-icon" href="favion.ico">`

type属性：链接的资源的MIME类型


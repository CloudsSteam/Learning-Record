## 本地化存储

### cookie
浏览器第一次请求到服务器
服务器响应请求中携带cookie
浏览器第二次请求，携带cookie
>>服务器根据cookie辨别用户，也可以修改cookie内容

1. cookie不可跨域
2. cookie存储在浏览器里面
3. cookie有数量与大小的限制
    1. 数量在50个左右
    2. 大小在4kb左右
4. cookie的存储时间非常灵活
5. cookie不光可以服务器设置，客户端也可以设置
document.cookie
key:value

// document.cookie='name=kaivon';

>cookie的属性
1. name     cookie的名字，唯一性
2. value    cookie的值
3. domain   设置cookie在哪个域下有效
4. path     cookie的路径
5. expires  cookie的过期时间
    GMT
    UTC
6. max-age  cookie的有效期倒计时
7. HttpOnly 有这个标记的cookie，前端无法获取
8. Secure   设置cookie只能通过HTTPS协议传输
9. SameSite 设置cookie在跨域请求的时候不能被发送


document.cookie='color=red; domain=127.0.0.1;path=/docs;    
//规定docs路径下才能看到这cookie

console.log(new Date());

document.cookie='margin=20;expires='+new Date(2108,1,1);


```
var btn=document.querySelector('#btn');
btn.onclick=function(){
    ajax('js/data.json',function(data){
        console.log(data);
    })
}
```

### cookie封装及应用

<script>
var manageCookie={
    //设置cookie
    set:function(name,value,date){
        //expires date:要求用户传入的是一个时间节点(默认传入为天数)
        //var endDate=new Date();   //过期时间点
        //endDate.setDate(endDate.getDate()+data);
        //document.cookie=name+'='+value+';expires='+endDate;
        document.cookie=name+'='+value+';max-age='+date;
    },
    //移除cookie
    remove:function(){
        this.set(name,'',0);    //只需要把时间设置为0就可以了
    },
    //获取cookie
    get:function(){
        //'name=kaivon;padding=30;width=40;'
        var cookies =document.cookie.split(';');
        //==>['name=kaivon','padding=30','width=40']
        for(var i=0;i<cookies.length;i++){
            var item=cookies[i].split('=');
             //==>['name','kaivon'],['padding','30'],['width','40']
            if(item[0]==name){
                return item[1];
            }
        }  
    } 
}
manageCookie.set('left',100,10000);
manageCookie.remove('left');

	//拖拽

    >理解bind函数
	var drag = {
		init: function (dom) {
			this.dom = dom;
			this.bindEvent();
			var l = manageCookie.get('newLeft');
			var t = manageCookie.get('newTop');
			this.dom.style.left = l ? l + 'px' : '100px';
			this.dom.style.top = t ? t + 'px' : '100px';
		},
		bindEvent: function () {
			this.dom.onmousedown = this.mouseDown.bind(this);
		},
		mouseDown: function (e) {
			document.onmousemove = this.mouseMove.bind(this);
			document.onmouseup = this.mouseUp.bind(this);
			this.disX = e.clientX - this.dom.offsetLeft;
			this.disY = e.clientY - this.dom.offsetTop;
		},
		mouseMove: function (e) {
			this.newLeft = e.clientX - this.disX;
			this.newTop = e.clientY - this.disY;
			this.dom.style.left = this.newLeft + 'px';
			this.dom.style.top = this.newTop + 'px';
		},
		mouseUp: function () {
			document.onmousemove = null;
			document.onmouseup = null;
			//鼠标抬起的时候需要存储(cookie)一下此刻盒子的位置信息
			manageCookie.set('newLeft', this.newLeft, 10000);
			manageCookie.set('newTop', this.newTop, 10000);
		}
	}
		drag.init(document.getElementById('box'));
</script>


### webstorage

#### localstorage
两种存储
LocalStorage
seeionStorage

1. length       本地存储数据的数量
2. key()        通过索引找到存储的数据
3. getItem()    通过键名取到本地存储数据
4. setItem()    设置一个本地存储数据
5. removeItem() 删除一个本地存储数据
6. clear()      清空本地存储数据


console.dir(Storage);
console.log(localStorage,sessionStorage);
console.log(localStorage.length);

//创建storage
localStorage.setItem('name','kaivon');
localStorage.setItem('age','18');
localStorage.setItem('sex','male');
localStorage.setItem('insterest','drink');
存储时以开头字母顺序存储


var color = ["red","green"];    //"red","green"
var color ={c1:'red',c2:'green'}    //[Object Object]
localStorage.setItem('color',color);

存对象
var color ={"c1":"red","c2":"green"}    //[Object Object]
localStorage.setItem('color',JSON.stringify(color));    //转成json字符串
console.log(JSON.parse(localStorage.getItem('color'))); //要用再转成json对象
 

localStorage.removeItem('color');   //清除单个对象
LocaLStorage.clear();               //清除所有对象

localstorage发生变化能监听到事件，不同页面切换


#### localstorage 应用-01

//请求数据
ajax('js/shoppingData.json',function(data){
	console.log(data);
}); 


//添加商品操作事件

function addEvent(){
	var trs=document.querySelectorAll('.product tr');
	for (var i=0;i<trs.length;i++){
		action(trs[i],i);
	}

	function action(tr,n){
		var tds=tr.children,
			img=tds[0].children[0],
			imgSrc=img.getAttribute('src'),
			name=tds[1].children[0].innerHTML,
			colors=tds[1].children[1].children,
			price=pareseFloat(tds[2].innerHTML),
			spans=tds[3].querySelectorAll('span'),
			strong=tds[3].queryselector('strong'),
			joinBtn=tds[4].children[0],
			selectNum=0;
	}
}


//颜色按钮点击事件
var last=null,		//上一次选中的按钮
	colorValue='',	//选中的颜色
	colorId='';		//选中商品对应的id
for(var i=0;i< colors.length;i++){
	color[i].onclick=function(){
		last&&last!=this&&(last.className='');		//当点击上一个和当前不同时才清除last.className

		this.className=this.clssName? '':'active';
		colorValue=this.className?this.innerHTML : '';
		colorId=this.className ?this.dataset.id : '';
		imgSrc=this.className? 'images/img_0' +(n+1)+ '-'+(this.index+1)+'.png':'images/img_0'+(n+1)+'-1.png';

		img.src=imgSrc;
		last=this;		
		//把当前点击的游戏对象赋值给last，当前点击的对象相对于下次要点击的时候是它一个对象(last)
	}
}
	

//加入购物车功能

joinBtn.onclick=function(){
	if(!colorValue){
		alert('请选择颜色')；
		return;
	}
	if(!selectNum){
		alert('请添加购买数量')；
		return;
	}

	//给selectData对象赋值
	selectData[colorId]={
		"id":colorId,
		"name":name,
		"color":colorValue,
		"price":price,
		"num":selectNum,
		"img":imgSrc,
		"time":new Date().getTime(),
	};

	localStorage.setItem('shoppingCart',JSON.stringify(selectData));		//json将对象转化为字符串
										// JSON.parse对立面

	img.src='images/img_0'+(n+1)+'-1.png';
	last.className='';
	strong.innerHTML=selectNum=0;

	createSelectDom();
}										

//开头
var selectData={};	//用来存储所有的商品信息，以及所有的商品
function init(){
	selectData=JSON.parse(localStorage.getItem('shoppingCart'))||{};	
	//第一次收到为空但JSON.parse返回为null
	createSelectDom();
}
init();



//删除功能

function del(){
	var btns=document.querySelectorAll('.selected tbody button');
	var tbody=document.querySelector('.selected tbody');

	for(var i=0; i<btns.length;i++){
		btns[i].onclick=function(){
			//删除对象里的数据
			delete selectData[this.dataset.id];
			localStorage.setItem('shoppingCart',JSON.stringify(selectData));
			//删除DOM结构
			tbody.removeChild(this.parentNode.parentNode);
			
			//更新总价格
			var totalPrice=document.querySelector('.selected th strong');
			totalPrice.innerHTML=parseFloat(totalPrice.innerHTML)-parseFloat(this.parentNode.parentNode.children[3].innerHTML)+'.00元'；
		}；
	}
}


#### Restful API

Restful API 是一种互联网软件架构的设计规范，设计指南，设计风格，设计原则

1. API接口 Application Programming Interface
前后端分离的产物
2. Rest		Resource Representational State Transfer	
资源在网络中以某种表现形式进行状态转移
软件和网络的交叉点

* Resource
资源
URI：统以资源标识符，是一个字符串。用来标识互联网资源的名称
URL：统一资源定位符。它是一种具体的URI

* Representational
表现层
文本	text\html\xml\json\二进制

* State Transfer
状态转化

网络上都是资源有自己特定的URI有具体的表现形式，通过前后端数据API交互操作
通过http中的请求方式getpost，符合则称为Restful架构


Restful API具体设计规范
1. 协议
	HTTPS
2. https://www.kaivon.com/api/

3. 版本
https://api.kaivon.com/v1

4. 路径
https://api.kaivon.com/v1/blogs

5. 方法
	1. GET 获取资源
	 	GET https://api.kaivon.com/v1/blogs			获取所有的文章
	 	GET https://api.kaivon.com/v1/blogs/id		获取某一篇文章
	2. POST 添加资源
		POST https://api.kaivon.com/v1/blogs	 	添加一篇文章

	3. PUT 修改资源(客户端需要提供改变后的完整资源)
		POST https://api.kaivon.com/v1/blogs/id	  	修改某一篇文章
	4. PATCH	更新资源(客户端需要提供改变的属性)
		PATCH https://api.kaivon.com/v1/blogs/id		更新某一篇文章
	5. DELETE	删除资源
		DELETE https://api.kaivon.com/v1/blogs/id		删除某一篇文章

6. 数据过滤
	1. ?limit=10	指定返回数据的数量
		GET https://api.kaivon.com/v1/blogs?limit=10
	2. ?offset=10	指定一个偏移量
		GET https://api.kaivon.com/v1/blogs?offset=10
	3. ?page=2&per_page=10	指定第几页，以及每页的数量
		GET https://api.kaivon.com/v1/blogs?page=2&per_page=10
	4. ?sortby=time&order=arc	指定返回结果按照哪个属性排序，以及排序的方式
		GET https://api.kaivon.com/v1/blogs?sortby=time&order=arc

7. 状态码
8. 返回结果
	1. GET		资源对象列表(数组),如果取的是一条数据，那返回一个对象
	2. POST		返回添加后的资源对象，以及有可能会加上是否成功
	3. PUT		返回修改后的资源对象，以及有可能会加上是否成功
	4. PATCH	返回更新后的资源对象，以及有可能会加上是否成功
	5. DELETE	返回空，以及有可能会加上是否成功
9. 返回的数据格式
	尽量使用JSON，避免使用XML

##### 总结
1. 看URL就知道要什么
2. 看HTTP method就知道干什么
3. 看HTTP stuts code就知道结果如何

## jQuery

#### jQuery简介

jQuery是一个快速小型且功能丰富的JavaScript库，
借助易于使用的API使HTML文档的遍历和操作，事件处理，动画和Ajax等事情
变得更加简单，兼具多功能性和可扩展性

```三个显示一样
<script>
$(document).ready(function(){
	var box=document.getElementById('box');
	console.log(box);
});

$().ready(function(){
	var box=document.getElementById('box');
	console.log(box);
});

$(function(){
	var box=document.getElementById('box');
	console.log(box);
})

</script>

```
document.addEventListener('DOMContentLoaded',function(){
	console.log('dom内容加载完毕')；
})；	//和ready一致，不过是原生js

$(document).ready(function(){
	console.log('ready完成了');
});
window.onload=function(){
	console.log('load完成了')
};
ready当我们页面中dom元素加载完就会触发
onload当页面整个下载完成加载完成才触发

>原生js和jQuery对比(离大谱)

* 原生js写法

var btn =document.getElementById('btn');
btn.onclick=function(){
	var div=document.createElement('div');
	div.style.width='100px';
	div.style.height='100px';
	div.style.background='green';
	document.body.appendChild(div);
}

* jQuery写法

$('#btn').click(function(){
	$('div').css({
		width:'100px',
		height:'100px',
		background:'green'
	}).appendTo('body');
});

>强大的选择器

<ul id="ulId" class="ulClass">
		<li>red</li>
		<li>green</li>
		<li name="blue">blue</li>
</ul>

		var li=$('ul li:nth-child(1)');
		var li=$('#ulId li:first-child');
		var li=$('.ulClass li:first-child + li');
		var li=$('li[name=blue]');
			//var li=document.querySelector('#ulId li:first-child');
			//li.style.background='green';

		li.css('background','green');

>链式操作
$('.text').html('陈学辉').css('border','1px solid #000').width(200).height(200).css('background','grey');

写一次无穷叠加buff


>原生js获取到的对象与jquery取到的对象的对比

console.log(h1==$h1);	//false


//h1.css('color','pink');	报错，原生对象不使用jquery方法

//$h1.style.color='pink';	报错，jquery的对象也不能使用最后方法

//原生转jquery
$(h1).css('color','blue');

//jquery转原生

$h1[0].style.color='purplue';

#### jquery选择器

$()中$符号选择的是集合

>基础选择器
$('#list').css('background','green');
$('.red').css('background','grey');
$('li').css('border','2px solid pink');
$('li,p').css('font-size','20px');		//和

>层级选择器
$('div a').css('color','green');		//div下面的a元素
$('div>a').css();						//div的子元素a
$('div a.link+a').css();				//div下面a.link再下一个a
$('div a.link~a').css();				//div下面a.link后面所有a标签

>属性选择器
$('#ulColor li[class]').css()			//id为ulcolor下面li带有class属性的
$('#ulColor li[title=blue]').css()		//id为ulcolor下面li属性title为blue的
$('#ulColor li[title!=blue]').css()		//id为ulcolor下面li属性title不为blue的
$('#ulColor li[title|=css]').css()		//id为ulcolor下面li属性title以前缀css-开头的
$('#ulColor li[id^=color]').css()		//id为ulcolor下面li的id属性为color的以属性值为开始(不需要-隔开)
$('#ulColor li[id$=color]').css()		//id为ulcolor下面li的id属性为color的以属性值为结尾(不需要-隔开)
$('#ulColor li[lang*=cn]').css()		//id为ulcolor下面li有lang且属性中包含cn
$('#ulColor li[lang~=cn]').css()		//id为ulcolor下面li有lang且属性中包含cn单词，用空格隔开
$('#ulColor li[class=cl][name=kaivon]').css()	//缩小范围进一步确认


>基础过滤选择器
$('#olColor li:eq(1)').css();			//根据索引过滤，选中索引为1的
$('#olColor li:gt(1)').css();			//根据索引过滤，选中索引大于1的
$('#olColor li:lt(1)').css();			//根据索引过滤，选中索引小于1的
$('#olColor li:not(#olColor li:eq(2))')	//排除
$('#olColor li:even').css();			//选中偶数
$('#olColor li:odd').css();				//选中奇数
$('#olColor li:first').css();			//选中第一个
$('#olColor li:last').css();			//选中最后一个
$('#olColor li:lang(en)').css();		//过滤选中lang为en的
$('#olColor li:target(tar)').css();		//锚点，id为tar的，导航栏#tar
$(':root').css();						//根节点
$(':header').css();						//所有h标签

>子元素过滤器
$('#paragraph p:first-child').css();	//第一个子元素必须是p标签
$('#paragraph span:first-of-type').css();	//选到第一个span标签
$('#paragraph span:last-child').css();
$('#paragraph p:last-of-type').css();

$('#paragraph p:nth-child(2)').css();				//选择到第二个子元素，并且这个子元素必需是p标签
$('#paragraph span:nth-of-type(2)').css();			//第二个span标签
$('#only p:only-child').css();						//选择到只有一个子元素的标签
$('#only-two span:only-of-type').css();				//选择到只有一个span子元素的标签


>内容过滤选择器
$('#content:contains(kaivon)').css();			//选中id为content内容包含了kaivon的
$('div:empty').css();							//选择到div里面属性为空的
$('#has:has(p)').css();							//选中id为has里包含p标签的
$('#title:parent').css();						//选中id为title的父级 


>表单过滤器
$(':button').css();							//选择到所有的按钮，包含button和input
$('#sex input:checkbox').wrap('<span></span>').parent().css();		//给input标签包一个父级元素添加样式
$(':checked').wrap('<span></span>').parent().css();					//同上给选中的添加父元素


#### DOM操作

>分类：class属性
$('.setClass li:first').addClass('red');			//添加属性
$('.setClass li:eq(1)').removeClass('green');		//移除属性
$('.setClass li:last').hasClass('green');			//判断是否有此属性
$('.setClass p').click(function(){					//点击事件切换
	$(this).toggleClass();
});

>DOM插入
//插入元素（内部插入）
		$('.insideAdd').append('<h2>append方法插入</h2>');	//append()，在元素里面的末尾插入DOM。这个与appendChild的方法是一样的。
		$('.insideAdd').append($('.insideAdd p'));
		$('<h2>appendTo方法插入</h2>').appendTo('.insideAdd');	
		//将匹配的元素插入到目标元素的最后面。这个与append一样，只不过内容和目标的位置相反。append方法里直接写一个标签的字符串，就相当于创建一个DOM对象
		$('.insideAdd').prepend('<h2>prepend方法插入</h2>');	//prepend()，与append的语法一样，只不过是插入到父级元素的前面
		$('<h2>prependTo方法插入</h2>').prependTo('.insideAdd');	//prependTo()，与appendTo是一样的，不同的也是插入的位置是在前面

//插入元素(外部插入)

$('.outsideAdd h2').after('<p>after方法添加到h2后面</p>');					//就相当于兄弟元素后面
$('<p>insertAfter方法添加到h2后面</p>').insertAfter('.outsideAdd h2');		//紧跟着h2

$('.outsideAdd h2').before('<p>before方法添加到h2前面</p>');				//就相当于兄弟元素前面
$('<p>insertBfter方法添加到h2前面</p>').insertBefore('.outsideAdd h2');		//紧跟着h2


//插入元素， html与text方法。相当于原生的innerHTML、innerText属性
		console.log($('.htmlText').html());//获取
		$('.htmlText').html('<h2>这是html方法添加的标题</h2><p>这是html方法添加的内容</p>');	//设置替换
		console.log($('.htmlText').text());	//获取
		$('.htmlText').text('<h2>这是text方法添加的标题</h2><p>这是<em>text</em>方法添加的内容</p>');	//原文本替换


//包裹元素
		$('.wrap span').wrap('<li>');	//wrap()，在每个匹配的元素外层包上一个html元素
		$('.wrap li').wrapAll('<ul>');	//wrapAll()，在所有匹配元素外面包一层HTML元素
		$('.wrap span').wrapInner('<strong>');	//wrapInner()，在匹配元素里的内容外包一层结构
		$('.wrap li').unwrap();	//.unwrap()，将匹配到的元素的父级删除


//删除元素
		//$('.del .title').remove();	//remove()，移除自己
		$('div').remove('.title');	//也可以添加参数。从div中移除一个.title的div
		$('.del ul').empty();	//empty()，清空子元素
		$('.del .end').click(function(){
			alert(1);
		});
		//detach()，与remove()一样，这两个方法都有一个返回值，返回被删除的DOM。它们的区别就在这个返回值身上
		var end=$('.del .end').detach();	//再次添加后是有事件的
		//var end=$('.del .end').remove();	//再次添加后没有事件
		setTimeout(function(){
			$('.del').append(end);	//1s后，被删除的那个元素会被重新添加上
		},1000);


//克隆与替换元素
		$('.clone p').click(function(){
			alert(2);
		});
		//$('.clone p').clone().appendTo('.clone');
		$('.clone p').clone(true).appendTo('.clone');	//clone的参数为true时表示，会把事件也克隆了
		$('<h3>使用replaceAll方法主动替换</h3>').replaceAll('.clone .replaceAll');//创建一个元素然后用它替换掉其它元素
		$('.clone .name2').replaceAll('.clone .name1');//使用已有的元素替换掉其它元素（剪切操作）
		$('.clone .replaceWidth').replaceWith('<h3>使用replaceWidth方法被动替换</h3>');



//属性操作-通用属性操作
		console.log($('.attr img').attr('src'));	//images/img_01.jpg（如果有多个img的话，它返回的是第一个img的src值）
		$('.attr img').attr('title','这是一张美食图片');	//如果有多个img的话，设置的是所有的img
		$('.attr img').attr({	//同时设置多个属性
			class:'delicious', 
			alt:'美食'
		});
		console.log($('.attr img').prop('src'));		//绝对地址
		console.log(
			$('.attr img').attr('kaivon'),	//liu
			$('.attr img').prop('kaivon'),	//undefined
		);
		$('.attr img').prop({
			id:'food',
			kaivon:'liuliu',	//自定义的属性prop并没有添加到DOM标签身上，但是它会添加到DOM对象身上	
		});
		$('.attr img').attr('kaivon','liuliuliu');
		$('.attr img').removeAttr('kaivon');
		$('.attr img').removeProp('id');	//删除的是DOM对象身上的属性，并不是DOM标签身上的属性
		$('.attr img').prop('index',5);
		console.log($('.attr img').prop('index'));	//5 这条属性是添加在DOM对象身上
		$('.attr img').removeProp('index');
		console.log($('.attr img').prop('index'));	//undefined removeProp是删除DOM对象身上的属性
		console.log($('.attr input').val());	//这是一个正经的输入框
		$('.attr input').val('这不是一个输入框');



//属性操作-css类属性操作
		console.log(
			$('.css').css('border'),	//2px solid rgb(0, 0, 0)
			$('.css').css('height'),	//19.9125px
		);
		$('.css h2').css('width','200px').css('height','100px').css('background','#ccc').text('插入一个标题');
		$('.css h2').css({
			color:'green',
			fontSize:'30px',
			'line-height':'100px',
		});
		$('.css p').css({
			width:'200px',
			height:'200px',
			padding:'20px',
			margin:'20px auto',
			border:'2px solid #f00',
		});
		console.log(
			$('.css p').width(),	//200
			$('.css p').height(),	//200
			$('.css p').innerWidth(),	//240	获取包含padding的宽度（clientWidth）
			$('.css p').innerHeight(),	//240
			$('.css p').outerWidth(),	//244	获取包含border的宽度（offsetWidth）
			$('.css p').outerHeight(),	//244
		);
		$('.css p').width(300).height(100).innerWidth(400).outerWidth(500);	//给width与给innerWidth设置的都是width属性的值。但是innerWidth与outerWidth都会动态的算出一个宽度值，赋给width属性

		$('.css').css('position','relative');	//先把父级设置成相对定位
		$('.css div').css({
			width:'100px',
			height:'100px',
			background:'green',
			position:'absolute',
			left:'100px',
			top:'200px'
		});



//相对于document
		console.log(
			$('.css div').offset().left,	//110
			$('.css div').offset().top,		//1648.3499755859375
			//此方法没有.right与.bottom
		);
		$('.css div').offset({
			left:200,
			top:1800,
		});



//获取相对于有定位的父级的位置信息
		console.log(
			$('.css div').position().left,
			$('.css div').position().top,
		);

		console.log(
			$(document).scrollTop(),
			$(document).scrollLeft(),
		);
		setTimeout(function(){
			$(document).scrollTop(300);
		},2000);



#### 遍历
<script>
//获取后代元素
		$('.child').children().css('border-color','green');	//.children()	获取所有子元素(第一层)
		$('.child').children(':eq(1)').css('border-width','3px');	//可以接收一个选择器的参数，这个选择器用来过滤子元素
		$('.child').find('span:eq(0)').css({	
			//.find()	获取匹配到的后代元素。它与children不同的地方为：children找到的是子元素，find找到的是后代元素
			'font-size':'30px',
			color:'red'
		});


//获取祖先元素
		$('.parent li ul li:first').parent('ul').css('border','4px solid blue');	//.parent()		获取父元素。也可以加一个参数.ul。就表示要找到父级必需有个class
		//$('.parent li ul li:first').parents().css('border','2px solid purple');
		console.log($('.parent li ul li:first').parents());//.parents()	获取祖先元素。所有祖先元素都会被找到，一直找到HTML
		$('.parent li ul li:first').parents('ul').css('border','2px solid purple');
		$('.parent li ul li:first').parentsUntil('li').css('border','5px solid purple');	
		//.parentsUntil()	获取祖先元素（但是有个范围，找到li就不再往上找了）
		$('.parent li ul li:first').offsetParent().css('border','5px solid teal');	//.offsetParent()	获取最近的有定位的祖先元素
		
//获取祖先元素.closest() 获取祖先元素，与parents有点像。但区别是closest会找自己，parents不会找自己
		$('.closest li ul li').closest('ul').css('border','2px solid purple');

		//$('.closest li ul li').parents('li').css('border','5px solid purple');
		$('.closest li ul li').closest('li').css('border','5px solid purple');	//会从自己查起，如果自己的标签满足的话，自己的标签就算


//获取后面的兄弟元素
		$('.next li:first').next('li').css('background','cyan');	//.next()	获取后面紧临的兄弟元素。参数也是个选择器，可选
		$('.next li:first').nextAll('li').css('border','5px solid #000');	//.nextAll()	获取后面所有的同辈兄弟元素
		$('.next li:first').nextUntil('div').css('border','5px solid red');	//获取后面所有的同辈兄弟元素（但是有个范围，找到div就不找了）


//获取前面的兄弟元素(与next一样)
		$('.prev li:last').prev('li').css('background','cyan');
		$('.prev li:eq(3)').prevAll('li').css('border','5px solid #000');
		$('.prev li:eq(3)').prevUntil('div').css('border','5px solid red');


//获取所有的兄弟节点
		$('.siblings li:eq(2)').siblings().css('border','5px solid skyblue');
		$('.siblings li:eq(2)').siblings('.select').css('background','yellow');	//添加了参数，进行过滤

</script>

#### 事件


#### ajax
//get请求
		$('#get').click(function () {
			$.get('http://api.duyiedu.com/api/student/findAll', { appkey: 'kaivon_1574822824764' }, function (data) {
				console.log(data);
			}, 'json');
		});
		$('#ajaxGet').click(function () {
			$.ajax({
				url: 'http://api.duyiedu.com/api/student/findAll',
				type: 'get',
				/* data:{
					appkey:'kaivon_1574822824764',
				}, */
				data: 'appkey=kaivon_1574822824764',
				dataType: 'json',
				success: function (data) {
					console.log(data);
				}
			});
		});


//post请求
		$('#loginBtn1').click(function () {
			var username = $('#login input[name=account]').val();
			var password = $('#login input[name=password]').val();

			$.post('http://api.duyiedu.com/api/student/stuLogin', { appkey: 'kaivon_1574822824764', account: username, password: password }, function (data) {
				console.log(data);
			}, 'json');

			//console.log(username,password);
		});

		$('#loginBtn2').click(function () {
			$.ajax({
				url: 'http://api.duyiedu.com/api/student/stuLogin',
				type: 'post',
				data: {
					appkey: 'kaivon_1574822824764',
					account: $('#login input[name=account]').val(),
					password: $('#login input[name=password]').val()
				},
				dataType: 'json',
				success: function (data) {
					console.log(data);
				},
				error: function (status) {
					console.log('错误原因：' + status);
				}
			});
		});


#### jsonp
$('#jsonp').click(function(){
	$.ajax({
		url:'http://developer.duyiedu.com/edu/testJsonp',
		dataType:'jsonp',
		method:'post',
		success:function(data){
			console.log(data);
		}
	});
});

function fn(data){
	console.log('kaivon');
	console.log(data);
}

var jp={
	ajax:function(options){
		var url=options.url;
		var dataType=options.dataType; //需求方式

		var targetProtocol=''; //用户地址的协议
		var targetHost='';	//用户地址的域名和端口

		if(url.index.Of('http://')==0||url.index.Of('https://')==0){
			//这个条件成立，说明传入的地址是一个绝对地址
			var targetUrl=new URL(url);
				//把用户传进来的地址(字符串变成一个真正的地址对象)
			targetProtocol=targetUrl.protocol;//返回地址对象协议
			targetHost=targetUrl.host;//返回对象的域名和端口
		}else{
			//代码走到这里说明，用户传入的地址是一个相对地址
			targetProtocol=location.protocol; //返回地址对象的协议
			targetHost=location.host;//返回地址对象的域名和端口
		}
		if(dataType!='jsonp'){
			//这个条件成立说明用户的请求方式不是jsonp，那就直接返回
			return;
		}

		if(location.protocol==targetProtocol&&location.host==targetHost){
			//这个条件成立说明现在是同域
			//ajax请求即可
		}else{
			//不同域jsonp请求
			var callback='cb'+Math.floor(Math.random()*100000);//随机生成一个函数名

			//把生成的方法定义到window身上
			window[callback]=options.success;

			//生成script标签
			var script=document.createElement('script');
			if(url.indexOf('?')>0){
				//这个条件成立说明用户传的url里面有参数(带问号了)
				script.src=url+'&callback'+callback;
			}else{
				script.src=url+'?callback'+callback;
			}

			document.head.appendChild(script);
		}
	}
}

jp.ajax({
	url:'https://developer.duyiedu.com/edu/testJsonp',
	dataType:'jsonp',
	success:function(data){
		console.log(data)
	}
});


#### jquery插件

https://plugins.jquery.com/
https://www.jq22.com/


#### jquery插件

//给jQuery对象本身扩展方法
$.extend({
	lg:function(value){
		console.log(value);
	}
});
$.lg('kaivon');   //kaivon

//给jquery DOM对象扩展方法
$.fn.extend({
		changeColor:function(){
			//$(this)指向使用的DOM对象
			return $(this);
		}
});
$.fn.changeSize=function(){
	$(this).css('fontSize',50);
	return $(this);
}
$('h1').changeColor().changeSize();


//封装拖拽的插件
```
<script>
//封装拖拽的插件
		$.fn.draggable = function (options) {
			options = options || {};
			options.limit = options.limit || false;

			var This = $(this);

			//修改DOM元素的样式
			$(this).css({
				position: 'absolute',
				left: 0,
				top: 0,
				cursor: 'move'
			});

			$(this).mousedown(function (ev) {
				var disX = ev.pageX - $(this).offset().left;
				var disY = ev.pageY - $(this).offset().top;

				$(document).mousemove(function (ev) {
					var l = ev.pageX - disX;
					var t = ev.pageY - disY;

					//如果用户传了limit:true，这个参数，就要处理拖拽的范围了
					if (options.limit) {
						if (l < 0) {
							l = 0;
						} else if (l > $(document).innerWidth() - This.outerWidth()) {
							l = $(document).innerWidth() - This.outerWidth();
						}

						if (t < 0) {
							t = 0;
						} else if (t > $(document).innerHeight() - This.outerHeight()) {
							t = $(document).innerHeight() - This.outerHeight();
						}
					}

					This.css({
						left: l,
						top: t
					});
				});

				$(document).mouseup(function () {
					$(this).off();
				});

				return false;
			});
		};


		$('#box').draggable({
			limit: true,
		});
<script/>
```

## lodash

### Array
		//chunk()   把数组拆分成一个二维数组，拆分后的第1个数组的长度为第二个参数的值
		console.log(_.chunk(['a', 'b', 'c', 'd'], 2));	//[["a", "b"],["c", "d"]]

		//compact() 过滤掉原数组里的非真（转布尔值后为false）数据
		console.log(_.compact([0, 1, false, 2, '', 3, null, NaN, undefined]));	//[1, 2, 3]

		//concat()  合并数组，与Array对象的方法一样

		//difference()  在第一个数组中把第二个数组里的数据都排除掉
		console.log(_.difference([1, 3, 5, 7, 9], [3, 7]));	// [1, 5, 9]

		//differenceBy	与上面的方法一样，只不过它可以再接收一个迭代器的函数做为参数
		console.log(_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor));	//[3.1, 1.3]

		//differenceWith()	与上面的方法一样，只不过它可以接收一个比较器的函数做为参数，对每个数据都要比较一下
		var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
		console.log(_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual));	//[{ 'x': 2, 'y': 1 }]

		//drop()    切掉数组的前n（第二个参数，默认为1）位
		console.log(_.drop(['a', 'b', 'c', 'd', 'e'], 2));	//['c', 'd', 'e']
		//dropRight()   切割数组，切掉数组的后n位

		//dropWhile()	去掉数组中，从起点到第二个方法返回假的数据。与Array对象身上的filter()方法一样
		//dropRightWhile()	与上面一样，不过它是从右边开始查，查到返回假的那个数据都去除

		//take()	提取数组的前n（第二个参数，默认为1）位。与drop方法相反
		console.log(_.take(['a', 'b', 'c', 'd', 'e'], 2));
		//takeRight()/takeWhile()/takeRightWhile()	与上面的一样

		//fill()    填充数组，与Array对象身上的fill()方法一样
		//findIndex()   查找到第一个满足条件的数据的索引值（从左往右查），没找到返回-1。与Array对象身上的findIndex()方法一样
		//findLastIndex()	这与上面的findIndex是一样的，区别是它是从右往左的查

		//flatten()	减少一级数组嵌套深度，与Array的flat()这个方法相似
		console.log(_.flatten(['a', ['b', ['c', ['d']]]]));

		//flattenDeep()	把数组递归为一维数组。相当于[].flat(Infinity)
		console.log(_.flattenDeep(['a', ['b', ['c', ['d']]]]));	//["a", "b", "c", "d"]

		//flattenDepth()	减少n（第二个参数）层数组的嵌套。相当于[].flat(2)
		console.log(_.flattenDepth(['a', ['b', ['c', ['d']]]], 2));	//["a", "b", "c", "d"]

		//fromPairs()	把数组转换为一个对象，与Object.fromEntries()方法一样
		//head()/first()	获取数组里第一个元素，就是取下标为0的那个数据
		//last()	取数组里的最后一位数据，取下标为length-1的那个数据

		//indexOf()	查找数据，并返回数据对应的索引值，与Array对象身上的indexOf()方法一样
		//lastIndexOf()	查找数据，并返回数据对应的索引值，与Array对象身上的lastIndexOf()方法一样
		//initial()	获取数组里除了最后一位的所有数据。相当于删除数组里的最后一个数据，与Array对象身上的pop()方法一样。区别在于pop方法会改变原数组，而这个方法不会改变原数组
		//tail()	获取除了array数组第一个元素以外的全部元素，想当于Array对象身上的shift()，与initial()相反

		//intersection()	取数组的交集
		console.log(_.intersection(['a', 'b'], ['b', 'c'], ['e', 'b']));	//['b']

		//union()	取数组的并集（合并起来，去掉重复的）
		console.log(_.union([2], [1, 2]));	//[2, 1]

		//xor()	删除数组的交集，留下非交集的部分
		console.log(_.xor(['a', 'b'], ['b', 'c'], ['e', 'b']));	//["a", "c", "e"]

		//join()	把数组转成字符串，这个方法原生的Array对象也有

		//nth()	取数组里的某个数据，就是通过下标取到某个数据。只不过它的数字可以为负。表示倒着找
		var array = ['a', 'b', 'c', 'd'];
		console.log(
			_.nth(array, 1),	//b
			_.nth(array, -3),	//c
		);

		//以下这几个方法，用后面remove的方法代替
		//pull()	根据给的参数（参数为数据）删除原数组里的对应数据
		//pullAll()	与上面的方法一样，就是参数为数组（好比call,apply这两个方法）
		//pullAllBy()\pullAllWith()	与前面方面的语法一样
		//pullAt()	根据给的参数（参数为索引）删除原数组里的对应数据

		//remove()	根据函数删除原数组里的数据
		var arr = ['a', 'b', 'c', 'd', 'e'];
		_.remove(arr, function (value, index, array) {
			return index > 2;
		});
		console.log(arr);	//["a", "b", "c"]

		//without()	根据给的参数（参数为数据）删除原数组里的对应数据
		var arr = ['a', 'b', 'c', 'd', 'e'];
		console.log(
			_.without(arr, 'b', 'c'),
			arr
		);

		//reverse()	颠倒数组，这个方法原生的Array对象也有
		//slice()	截取数组，这个方法原生的Array对象也有

		//uniq()
		console.log(_.uniq([1, 2, 2, 1]));	//[1, 2]
		//uniqBy()/uniqWith() 与前面的一样

		//zip()	把各数组中索引值相同的数据放到一起，组成新数组
		console.log(_.zip(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));	//[["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]

		//zipObject()	与上面方法一样，区别是它输出的是对象
		console.log(_.zipObject(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));	//{小明: "男", 小红: "女", 小刚: "男"}

		//zipWith()

		//unzip()	这个方法与zip相反，把每个数组里索引值一样的数据放在一起
		console.log(_.unzip([["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]));	//[['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]]
		//unzipWith()	与zipWidth()一样，接收了一个迭代器的函数


### collection方法

		//countBy()	按照一定规则统计数量，key循环次数，value为匹配到的数量
		console.log(_.countBy(['one', 'two', 'three'], 'length'));	//{3: 2, 5: 1}	按每个字符串的length进行统计，length为3的有两个数据。length为5的有1个数据

		//groupBy()	按照一定规则进行分组，key为循环次数，value为匹配到的数组
		console.log(_.groupBy(['one', 'two', 'three'], 'length'));	//{3: ["one", "two"], 5: ["three"]}

		//each()/forEach()	循环，与原生Array.forEach一样
		//eachRight()/forEachRight()	倒着循环
		//every()	与原生Array.every方法一样
		//filter()	过滤数组，与Array对象上的filter()方法一样
		//find()	查找数据，与Array对象上的find()方法一样
		//findLast()	与上面一样，区别在于它是从右往左查
		//flatMap()		生成一个扁平化的数组，与原生的flatMap()方法一样		
		//flatMapDeep()	与上面一样，不过它可以递归
		//flatMapDepth()	与上面一样，它可以递归，并且可以指定递归的深度
		//includes()	与Array对象上的includes()方法一样

		//invokeMap()	使用第二个参数（方法）去处理数组，返回处理后的结果（数组）
		console.log(
			_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort'),	//[ [1, 5, 7],[1, 2, 3]]
			_.invokeMap([123, 456], String.prototype.split, ''),	//[["1", "2", "3"],["4", "5", "6"]]
		);

		//keyBy()	创建一个对象，里面的key由第二个参数决定。value为原数组里对应的那条数据
		var array = [
			{ 'dir': 'left', 'code': 97 },
			{ 'dir': 'right', 'code': 100 }
		];
		var result = _.keyBy(array, function (o) {
			return String.fromCharCode(o.code);	//key为使用fromCharCode解析后的字符。value为它所在数组里的那条数据
		});
		console.log(result);

		//key为dir，value为key所在原数组里的那条数据
		console.log(_.keyBy(array, 'dir'));

		//orderBy()	排序，既能升序又能降序
		var users = [
			{ 'user': 'fred', 'age': 48 },
			{ 'user': 'barney', 'age': 34 },
			{ 'user': 'fred', 'age': 40 },
			{ 'user': 'barney', 'age': 36 }
		];
		console.log(
			_.orderBy(users, 'age', 'asc'),	//以age属性的值进行升序排序
			_.orderBy(users, 'user', 'desc'),	//以user属性的值进行降序排序
		);

		//sortBy()		排序，只能升序
		console.log(
			_.sortBy(users, function (o) {
				return o.user;
			}),
		);

		//partition()	根据第2个参数把一个数组分拆成一个二维数组
		var users = [
			{ 'user': 'barney', 'age': 36, 'active': false },
			{ 'user': 'fred', 'age': 40, 'active': true },
			{ 'user': 'pebbles', 'age': 1, 'active': false }
		];
		console.log(
			_.partition(users, function (o) {	//active为true的放在一起，active为false的放在一起
				return o.active;
			}),
			_.partition(users, { 'age': 1, 'active': false }),//把第二个参数对应的数据放一起，其余的放一起
		);
		
		//reduce()	与Array对象上的reduce()方法一样
		//reduceRight()	与Array对象上的reduceRight()方法一样
		
		//reject()
		var users = [
			{ 'user': 'barney', 'age': 36, 'active': false },
			{ 'user': 'fred', 'age': 40, 'active': true }
		];
		console.log(
			_.reject(users, function (o) {
				return o.active;	//barney
			}),
			_.reject(users, { 'age': 36, 'active': false }),	//fred
			_.reject(users, ['user', 'fred']),	//barney
			_.reject(users, 'age'),	//[]
		);

		//sample()	从数组中随机取一个数据
		console.log(_.sample(['a', 'b', 'c', 'd', 'e']));

		//sampleSize()	获得 n 个随机数据
		console.log(_.sampleSize(['a', 'b', 'c', 'd', 'e'], 3));

		//shuffle()	随机排序
		console.log(_.shuffle(['a', 'b', 'c', 'd', 'e']));

		//size()	返回集合长度
		console.log(
			_.size(['a', 'b', 'c', 'd', 'e']),	//5
			_.size({ a: 1, b: 2 }),	//2
			_.size('kaivon'),	//6
		);

		//some()	与Array对象上的some()方法一样


### Function方法

		//defer()	推迟调用函数，在第二次事件循环的时候调用 
		_.defer(function (text) {
			console.log(text);
		}, '第二次事件循环');
		console.log('第一次事件循环');

		//delay()
		_.delay(function (text) {
			console.log(text);
		}, 1000, '延迟一秒执行');

		//flip()	调用函数时翻转参数
		function fn1() {
			console.log(arguments);
		}
		fn1 = _.flip(fn1);
		fn1(1, 2, 3);

		//negate()	结果取反函数
		function fn2(n) {
			return n % 2 == 0;
		};
		console.log(_.filter([1, 2, 3, 4, 5, 6], _.negate(fn2)));	//[1, 3, 5]

		//once()	函数只能调用一次
		function fn3(){
			console.log('fn3');
		}
		var newFn3=_.once(fn3);
		newFn3();
		newFn3();



### Lang方法
	//castArray()	强制转为数组，其实就是在外面加一层方括号
		console.log(
			_.castArray('a'),	//["a"]
			_.castArray({ a: 1, b: 2 }),	//[{a: 1, b: 2}]
		);

		//clone()	浅拷贝
		var obj1 = {
			a: 1,
			b: {
				c: 2
			}
		};
		var obj2 = _.clone(obj1);
		console.log(obj1, obj2);
		obj2.b.c = 3, console.log(obj1, obj2);

		//cloneDeep()	深拷贝
		var obj3 = _.cloneDeep(obj1);
		obj3.b.c = 4, console.log(obj1, obj3);

		//conformsTo()	通过第二个参数来检测对象的属性值是否满足条件
		var object = { 'a': 1, 'b': 2 };
		console.log(
			_.conformsTo(object, { 'b': function (n) { return n > 1 } }),	//true
			_.conformsTo(object, { 'b': function (n) { return n > 2 } }),	//false
		);

		//ea()	比较两个值是否相等。与Object.is()这个方法一样
		console.log(
			_.eq(12, 12),	//true
			_.eq({ a: 1 }, { a: 1 }),	//false
			_.eq(NaN, NaN),	//true
		);

		//gt()	第一个值是否大于第二个值
		console.log(
			_.gt(3, 1),	//true
			_.gt(3, 3),	//false
		);
		//gte()	第一个值是否大于等于第二个值
		//lt()	小于
		//lte()	小于等于

		//isArray()
		console.log(
			_.isArray([1, 2, 3]),	//true
			_.isArray(document.body.children),	//false
			_.isObject({}),		//true
			_.isObject(null),	//false
		);

		//toArray()
		console.log(
			_.toArray({ a: 1, b: 2 }),	//[1, 2]
			_.toArray('abc'),	//["a", "b", "c"]
			_.toArray(null),	//[]
		);


### Object
		//assign()	合并对象，与Object.assign()方法一样
		//assignIn()/extend()	与上面一样，不过它能继承原型身上的属性
		//assignInWith()/extendWith()	与上面一样，接收一个比较器的函数做为参数
		//assignWith()	也是接收一个比较器的函数做为参数

		//at()	根据传入的属性创建一个数组
		var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
		console.log(_.at(object, ['a[0].b.c', 'a[1]']));	//[3, 4]

		//create()	与Object.create()一样

		//defaults()	合并对象，与assign()一样，不过assign方法合并时遇到相同的属性，后面的会覆盖前面的。defaults刚好相反，前面的覆盖后面的
		console.log(
			_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 }),	//{a: 1, b: 2}
			_.assign({ 'a': 1 }, { 'b': 2 }, { 'a': 3 }),	//{a: 3, b: 2}
		);

		//defaultsDeep()	与defaults一致，不过它会深递归

		//toPairs()/entries()	把对象里可枚举的属性(不包括继承的)创建成一个数组，与Object.entities()的方法一样
		//toPairsIn()/entriesIn()	与上面的一样，但它包括继承的属性

		//findKey()	与前面讲的find方法一样，只不过它返回的是key
		var users = {
			'barney': { 'age': 36, 'active': true },
			'fred': { 'age': 40, 'active': false },
			'pebbles': { 'age': 1, 'active': true }
		};
		console.log(_.findKey(users, { 'age': 1, 'active': true }));	//pebbles

		//findLastKey()	与上面一样，只不过它从反方向开始遍历

		//forIn()	与原生 的for...in循环一样，只不过它是一个函数，语法与forEach一样。它遍历的是自己的属性与继承的属性
		//forInRight()	与上面一样，只不过是反方向遍历
		//forOwn()	与forIn()一样，只不过forOwn只能遍历到自己的属性
		//forOwnRight()	与上面一样，只不过是反方向遍历

		//functions()/functionsIn()	这两个没有说？？？？？？

		//get()	获取属性的值，与Object.defineProperty()	属性描述对象上的get方法一致
		//set()	设置属性的值，与Object.defineProperty()	属性描述对象上的set方法一致
		//setWith()	与上面的一样，只不过可以给一个参数决定返回的是对象还是数组
		console.log(_.setWith({}, '[0][1]', 'a', Array));

		//has()	检查属性是否为对象的直接属性，与Object.hasOwnProperty()方法返回true一样
		//hasIn()	检查属性是对象的直接属性还是继承属性，也与Object.hasOwnProperty()一样，true表示直接属性，false表示继承属性

		//invert()	把对象的key与value颠倒，后面的属性会覆盖前面的属性
		var object = { 'a': 1, 'b': 2, 'c': 1 };
		console.log(_.invert(object));	//{1: "c", 2: "b"}

		//invertBy()	与上面一样，它遇到相同的值后不会覆盖，而是会把所有放在一个数组里。另外它多了一个遍历器方法

		//invoke()	调用方法去处理取到的属性值
		var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };
		console.log(_.invoke(object, 'a[0].b.c.slice', 1, 3)); //[2, 3]	用slice方法去截取a[0].b.c的1-3位

		//keys()	把对象的key放到一个数组里，与Object.keys()的方法一样
		//keysIn()	与上面一样，只不过它包含继承到的属性
		//values()	把对象的value放到一个数组里，与Object.value()的方法一样
		//valuesIn()	与上面一样，只不过它包含继承到的属性

		//mapKeys()	修改对象的key，value不会变
		var result = _.mapKeys({ 'a': 1, 'b': 2 }, function (value, key) {
			return key + value;
		});
		console.log(result);	//{a1: 1, b2: 2}

		//mapValues()	与上个方法一样，只不过它修改的是value，key不会变

		//merge()	它与assign一样，不过它遇到相同的属性名后并不会覆盖，它会合并
		var object = {
			'a': [{ 'b': 2 }, { 'd': 4 }]
		};
		var other = {
			'a': [{ 'c': 3 }, { 'e': 5 }]
		};
		console.log(_.merge(object, other));

		//mergeWith()	与上面的方法一致，不过多了接收一个比较器的函数做为参数

		//omit()	删除对象里的属性
		console.log(_.omit({ 'a': 1, 'b': '2', 'c': 3 }, ['a', 'c']));	//{b: "2"}

		//_.omitBy	与上面一样，不过是接收一个迭代器的函数做为参数

		//pick()	筛选对象里的属性
		console.log(_.pick({ 'a': 1, 'b': '2', 'c': 3 }, ['a', 'c']));	//{a: 1, c: 3}

		//pickBy()	与上面一样，不过是可接收一个迭代器的函数做为参数

		//result()	获取对象属性，它与get一样。只不过它遇到函数的属性时会调用函数，并且把this指向对象本身
		var obj = {
			a: 12,
			b: function () {
				console.log(this.a);
			}
		};
		console.log(_.result(obj, 'a'));	//12
		_.result(obj, 'b');	//12
		console.log(_.get(obj, 'b'));	//它只能取到这个函数，并不能执行

		//toPairs()	把对象的key与value一起放到数组里
		function Foo() {
			this.a = 1;
			this.b = 2;
		}
		Foo.prototype.c = 3;
		console.log(_.toPairs(new Foo()));
		console.log(_.toPairsIn(new Foo()));

		//unset()	删除属性
		var object = { 'a': [{ 'b': { 'c': 7 } }] };
		_.unset(object, 'a[0].b.c'), console.log(object);

		//update()	这个与set一样，不过它可以接收一个函数的参数
		var object = { a: 10 };
		_.update(object, 'a', function (n) { return n * n });
		console.log(object);	///{a: 100}

		//updateWith()	与上面的一样，不过可以接收一个路径的参数，决定生成的属性放在哪里
		var object = {};
		_.updateWith(object, '[a][b]', function () {
			return 12;
		}, Object);
		console.log(object);


### String
		//camelCase()	转换字符串为驼峰格式
		console.log(
			_.camelCase('kaivon_chen'),
			_.camelCase('kaivon chen'),
		);

		//capitalize()	首字母为大写
		console.log(_.capitalize('kaivon'));	//Kaivon

		//endsWith()	查检结尾的字符
		console.log(_.endsWith('abc', 'c'));	//true

		//escape()	把特殊字符转义成真正的HTML实体字符
		console.log(_.escape('ka<iv>on'));	//ka&lt;iv&gt;on

		//unescape()	与上面相反
		console.log(_.unescape('ka&lt;iv&gt;on'));	//ka<iv>on

		//kebabCase()	转换字符为加-的形式
		console.log(_.kebabCase('k a i'));	//k-a-i

		//lowerCase()/toLower()	转小写
		//upperCase()/toUpper()	转大写

		//lowerFirst()	首字符转小写
		//upperFirst()	首字符转大写

		//pad()	填充字符串到指定的长度(左右填充)
		console.log(_.pad('abc', 8, '-')); 	//--abc---

		//padEnd()
		console.log(_.padEnd('abc', 8, '-'));

		//padStart()
		console.log(_.padStart('abc', 8, '-'));

		//parseInt()	把字符串类型的数字转成数字，

		//repeat()	重复字符串
		console.log(_.repeat('kaivon', 2));	//kaivonkaivon

		//replace()	替换字符串
		console.log(_.replace('kaivon', 'von', '***'));	//kai***

		//snakeCase()	转换字符串为_的形式
		console.log(_.snakeCase('k a i'));	//k_a_i

		//split()	分隔字符串为数组，与原生String.split()一样

		//startCase()	转换字符串为+空格的形式，并且首字符大写
		console.log(
			_.startCase('kaivon-chen'),	//Kaivon Chen
			_.startCase('kaivonChen'),	//Kaivon Chen
			_.startCase('kaivon_chen'),	//Kaivon Chen
		);

		//startsWith()	检查字符串的开始字符
		console.log(_.startsWith('kaivon', 'k'));	//true

		//template()	编译模板
		var compiled = _.template('hello <%= user %>!');	//user为一个占位符
		console.log(compiled({ 'user': 'kaivon' }));	//拿到数据后，给user赋值，它就能正确解析出内容了

		//trim()	去除首尾空格，或者指定字符
		console.log(_.trim('kaivon-', '-'));	//kaivon
		//trimEnd()	去除后面的空格，或者指定字符
		//trimStart()	与上面的一样，只不过去除的是左边的

		//truncate()
		console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!'));	//Hi kaivon! How are you feel...
		console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!', {
			//'length': 10,	//限制固定的字符个数
			'separator': /!/	//加个正则，遇到第一个空格后就加三个点
		}));

		//words()	把字符串的单词拆分成数组
		console.log(_.words('kaivon chen'));	//["kaivon", "chen"]





## mock
Mock.js
生成随机数据，拦截Ajax请求


### mock语法规范

		//1. 属性值是字符串 String
		console.log(
			Mock.mock({
				'data1|1-4': '陈学辉',		//随机重复1-4次
				'data2|3': '好帅',	//固定重置3次
			})
		);

		//2. 属性值是数字 Number
		console.log(
			Mock.mock({
				'number1|+1': 100,	//整数，自动加1并且初始值为100
				'number2|1-100': 12,	//整数，1-100之间的随机数，包括1和100（1=<数字<=100）	12用来确定是数据为数字类型
				'number3|1-100.5': 12,	//小数，整数部分为为1-100间随机数，包括1和100；小数部分为固定5位随机数
				'number4|1-100.1-10': 12,	//小数，整数部分为为1-100间随机数，包括1和100；小数部分为1-10个随机数（位数随机，数字也随机）
				'number5|123.1-10': 12,	//数字123后面随机添加1-10位小数
				'number6|123.10': 12,	//数字123后面固定添加10位小数，但小数的值是随机的
			})
		);

		//3. 属性值是布尔型 Boolean
		console.log(
			Mock.mock({
				'b1|1': false,	//随机生成一个布尔值，true与false的概率各为一半
				'b2|1-5': true,	//随机生成一个布尔值，值为value的概率是min / (min + max)，值为!value的概率是max / (min + max)
			})
		);

		//4. 属性值是对象 Object
		console.log(
			Mock.mock({
				'num1|1-3': { a: 10, b: 20, c: 30, d: 40 },	//随机选取对象里1-3个属性
				'num2|2': { a: 10, b: 20, c: 30, d: 40 },	//随机选取对象里2个属性
			})
		);

		//属性值是数组 Array
		console.log(
			Mock.mock({
				'arr1|1': ['a', 'b', 'c', 'd', 'e'],	//随机选取数组里1个数据
				'arr2|1-3': ['a', 'b', 'c', 'd', 'e'],	//通过重复属性值生成一个新数组，min<=重复次数<=max
			})
		);

		//6. 属性值是函数 Function
		console.log(
			Mock.mock({
				'result': function () { return 1 + 2 }	//把函数的返回值当作属性的结果
			})
		)

		//7. 属性值是正则表达式 RegExp
		console.log(
			Mock.mock({
				'reg1': /[a-z][A-Z][0-9]/,
				'reg2': /\w\W\s\S\d\D/,
				'reg3': /\d{5,10}/
			})
		)

		//Mock.Random
		var Random = Mock.Random;
		// console.log(Random);

		//1、Basics	基础类里的方法，共7个

		//Random.boolean()		随机一个布尔值
		console.log(
			Random.boolean(),
			Random.boolean(1, 9, true),
			Random.boolean(1, 2, false),
		);

		//Random.natural()		随机一个自然数（大于等于 0 的整数）
		console.log(
			Random.natural(),
			Random.natural(100),
			Random.natural(0, 50),
		);

		//Random.integer()	随机一个整数（包含负数）
		console.log(
			Random.integer(),
			Random.integer(-100),
			Random.integer(-50, 50),
		);

		//Random.float()	随机一个小数
		console.log(
			Random.float(),
			Random.float(0),
			Random.float(-10, 10),
			Random.float(-10, 10, 3),
			Random.float(-10, 10, 2, 5),
		);

		//Random.character()	//随机一个字符
		console.log(
			Random.character(),
			Random.character('abc123'),
			Random.character('lower'),
			Random.character('symbol'),
		);

		//Random.string()	随机一个字符串
		console.log(
			Random.string(),
			Random.string(5),
			Random.string(7, 10),
			Random.string('symbol', 5),
			Random.string('abc123', 1, 3),
		);

		//Random.range()	随机一个整数数据的数组
		console.log(
			Random.range(7),
			Random.range(3, 7),
			Random.range(1, 10, 2),
		);



### mock方法

ajax请求需要后端

正常发请求，生成模拟数据，mock拦截发生的请求，生成的数据丢给ajax返回值


```
$('#btn').click(function () {
			$.ajax({
				url: 'js/data.json',
				type: 'get',
				dataType: 'json',
				success: function (data) {
					console.log(data);
					createDom(data.data);
				}
			});
		});

		function createDom(data) {
			var str = '';
			data.forEach(function (item, index) {
				str += `
					<tr>
						<td>${item.sNo}</td>
						<td>${item.name}</td>
						<td>${item.sex}</td>
						<td>${item.email}</td>
						<td>${item.birth}</td>
						<td>${item.phone}</td>
						<td>${item.address}</td>
						<td>
							<button>编辑</button>
							<button>删除</button>
						</td>
					</tr>
				`;
			});
			$('#table-body').html(str);
		};


		Mock.mock('js/data.json', {
			"status": "success",
			"msg": "查询成功",
			"data|10": [{
				"id|+1": 1,
				"name": "@cname",
				"birth": "@date",
				"sex|1": ['男', '女'],
				"sNo|+1": 11000,
				"email": "@email",
				"phone": "@natural(13000000000,19900000000)",
				"address": "@county(true) @ctitle(5,10)",
				"appkey": "@string(4,7)_@date(T)",
				"ctime": "@date(T)",
           		"utime": "@date(T)"
			}],
		});

		Mock.setup({
			timeout:5000,
		});

		//https://github.com/YMFE/yapi

```
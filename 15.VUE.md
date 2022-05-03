# 入门

## 核心概念

### 注入

vue 会将以下配置注入到 vue 实例

- data:和界面相关的数据
- computed：通过已有数据计算得来的数据
- methods：方法
  > 模板中可以使用 vue 实例中的成员

### 虚拟 DOM 树

直接操作真实的 DOM 会引发严重的效率问题
而 vue 使用虚拟 DOM(vnode)的方式来描述要渲染的内容。vnode 是一个普通的 js 对象

vue 模板不是真实的 dom，它会被编译为虚拟 dom。虚拟 dom 树会最终生成真实的 dom 树
文本模板编译成 vnode tree 生成 dom tree

当数据变化后将引发从新渲染，vue 会比较新旧 vnode tree 找出差异，仅把差异部分应用到真实 domtree 中

运行 render()函数返回结果生成虚拟 dom

```
render?有 运行render函数，将函数返回的结果直接作为虚拟节点树vnodetree
render?无 有没有template配置作为模板然后编译render函数
template? 无 将el配置的outerHTML作为模板
```

注意：虚拟节点树必须是单根的

### 挂载

将生成的真实 dom 树，放置到某个元素位置，称之为挂载

1. 通过 el:"css 选择器"进行配置
2. 通过 vue 实例.\$mount("css 选择器")进行配置

### 完整流程

- 实例被创建
- 注入
- 首次渲染
  编译生成虚拟的 dom 树
  挂载
  已挂载

数据变动，响应式重新渲染

- 重新生成虚拟 dom 树
- 对比新旧两树的差异
- 将差异应用到真实 dom

### vue 知识体系

模板
配置

### 组件

细粒度
组件出现是为了实现以下两个目标

1. 减低整体复杂度，提升代码的可读性和可维护性
2. 提升局部代码的可复用性

组件包含该区域的：

- 功能(JS 代码)
- 内容(模板代码)
- 样式(css 代码)

### 创建组件

组件是根据一个普通的的配置对象创建的，开发组件，只需要写一个配置对象即可
该配置对象和 vue 实例的配置是几乎一样的

```
var myComp={
    data(){
        return{
            //
        }
    },
    template:....
}
```

组件配置对象和 vue 实例有以下几点差异：

- 无 el
- data 必须是一个函数，该函数返回的对象作为数据
- 由于没有 el 配置，组件的虚拟 dom 必须定义在 template 或 render 中

#### 全局注册

Vue.component("MyButton",myComp);
在 newVue 中使用 template:'<div><MyButton /></div>',

```
<body>
    <div id="app"></div>
    <script scr="./vue.min.js"></script>
    <script>
    var myButton={
        data(){       //函数返回保护每个组件实例相互独立，用自己的数据
            return{
                count:0,
            };
        },
        template:'<button @click="count++">当前点击了{{count}}次</button>',
    };
    //全局注册一个组件
    Vue.component("MyButton",myButton);

    var vm =new Vue({
        template:'<div>
        <MyButton />
        <MyButton />
        </div>',
    });
    vm.$mount("#app");
    </script>
</body>
```

> 但在一些工程化的大型项目中，很多组件都不需要全局使用
> 除非组件特别通用，否则不建议使用全局注册

#### 局部注册 components

哪里需要用到组件，就在那里注册

```
<body>
    <div id="app"></div>
    <script scr="./vue.min.js"></script>
    <script>
    var myButton={
        data(){
            return{
                count:0,
            };
        },
        template:'<button @click="count++">当前点击了{{count}}次</button>',
    };
    //全局注册一个组件
    //Vue.component("MyButton",myButton);

    var vm =new Vue({
        components:{
            //局部注册组件
            MyButton：myButton，
        }，
        template:'<div>
        <MyButton />
        <MyButton />
        </div>',
    });
    vm.$mount("#app");
    </script>
</body>
```

#### 应用组件

- 组件必须有结束
  <MyButton />

- 组件的命名
  短横线命名法，大驼峰命名法

#### 组件树

props 声明组件的属性
主要就是开发组件
一个组件创建好后，往往会在各种地方使用它。
它可能多次出现在 vue 实例中，也可能出现在其他组件中，于是形成组件树
谁的数据谁负责
**组件中，属性是只读的，绝不可以更改，叫做单向数据流**

```
var Title={
    props:["tittle1","tittle2"],
    template:'<div><h1>{{tittle1}}</h1><h2>{{tittle2}}</h2></div>',
};
var vm=new Vue({
    components:{
        MyButton,
        Tittle,
    },
    template:
    '<div>
    <MyButton />
    <Title tittle="标题1" tittle2="标题1-1" />
    <Title tittle1="标题2" tittle2="标题2-1" />
    <Title tittle1="标题3" tittle2="标题3-1"/>
    </div>',
});

vm.$mount("#app");
```

### 搭建工程

**main.js 启动功能**

```
import Vue from 'vue'
import App from './App.vue'
import "./styles/global.less"
// Vue.config.productionTip = false

new Vue({
  //1 render(h){
  //   return h(App);   //组件也是虚拟节点对象，渲染的不是普通节点而是组件实例
  // },
  //2 components: {
  //   App
  // },
  // template: '<App />'
  render: h => h(App),
}).$mount('#app')

```

**App.js**

```
const template="";

export default{       //导出
  data(){
    return{

    };
  },
  template,
};
```

> vue cli
> 脚手架工具，内部使用了 webpack，并预置了诸多插件(plugin)，加载器(loader)以达到开箱即用的效果
> 预置了：babel webpack-dev-server eslint postcss less-loader

进入项目 cmd 窗口 npm run serve

> SFC

单文件组件，Single File Component,即一个文件就包含一个组件所需的全部代码

> 预编译

当 vue-cli 进行打包时，会直接把组件中的模板 template 转换成 render 函数，叫做模板预编译

- 运行时不再需要编译模板，提高运行效率
- 打包结果中不再需要 vue 的编译代码，控制打包体积
  源代码->打包->运行
  SFC 出 template 模板打包成 render 函数
  vue 出响应式系统和运行时系统
  凑成 bundle 运行
  舍弃 vue 编译代码和 vue 模板编译系统直接运行

### 计算属性

> 普通运用

考虑计算复杂写上方法 methods， 方法内部 this 指向 vue 实例，再调用方法(缺点：数值不变运行会多次重复计算浪费算力)

> 计算属性 当数据使用不是方法，后面不用加括号

根据已有数据得到新的数据
使用数据本质上是再调用方法得到结果，过程中记录缓存依赖，只要依赖不变，就不用重新计算

#### 计算属性和方法有什么区别：

计算属性本质上包含 getter 和 setter 方法
当获取计算属性时，实际上是在调用计算属性 getter 方法
vue 会收集计算属性的依赖，并缓存计算属性的返回结果。
只要依赖属性不变就一直使用缓存 缓存即 get 内部依赖变化后才重新进行计算
而方法没有缓存，每次调用方法都会导致重新执行

计算属性 getter 没有参数，setter 只有一个参数。而方法的参数不限
检测运行了 get 有缓存变化。则运行 set

计算属性通常是根据已有数据得到其他数据，并在数据的过程中不建议使用异步当前时间随机数等操作；注入数据只有响应式数据通知

> 最重要的区别是含义上的区别，计算属性含义上是一个数据，可读取可赋值；
> 方法含义上是一个操作，用于处理一些事情
> 注重含义，因为代表逻辑

```
<template>
    <p>全名:{{ getFullName() }}</p>
    <p>全名:{{fullName}}</p>
    <button @click="setNewName('姬'，'成')"> 修改名字为姬成 </button>
    <button @click="fullName='姬成'"> 修改名字为姬成 </button>
</template>

<script>
export default {
  data() {
    return {
      firstName:"袁",
      lastName:"进"，
    };
  },

  computed:{    //有缓存，重新渲染再加载
      fullName(){
          get(){
              console.log("fullName called");
              return this.firstName+" "+this.lastName;  //缓存依赖
          },
          set(val){
              console.log("正在设置全名",val)
              //没有改动依赖this.firstName,this.lastName;不影响重新渲染
            //this.firstName=val[0];
            //this.lastName=val.subStr(1);
          },
      },
  },

  methods:{
      getFullName(){    //方法每次都要加载
          console.log("method called");
          return this.firstName+" "+this.lastName;
      },

      setNewName(){
          this.firstName=first;
          this.lastName=last;
      }
  }

};
</script>
```

##### scoped

每个组件都有不同样式
加上 scoped 为其加上自定义属性，只会影响自己的东西
父组件的 scoped 外层属性会影响到组件里面的根元素
子组件根元素样式受两个自定义属性，父层 scoped，自身 scoped

### 组件事件

先写静态页面再动态

vue 渲染效率取决于渲染节点数量和渲染节点稳定

v-if 和 v-show 有什么区别：
v-if 能够控制是否生成 vnode，间接控制了是否生成对应的 dom。
v-show 始终生成 vonde，只是控制 dom 的 display 属性
v-if 可以有效减少树的节点渲染量，但也会导致树不稳定;而使用 v-show 可以保持树稳定不能减少树的节点和渲染量
变化频繁用 v-show 保持稳定
显示状态变化较少应该用 v-if 以减少树的节点和渲染量

组件事件
抛出事件：子组件在某个时候发生了一件事，但自身无法处理，以事件的发生通知父组件处理
事件参数：子组件抛出事件时，传递给父组件的数据
注册事件：父组件申明，当子组件发生某件事的时候，自身将做出的一些处理

实例成员：
$mount
$emit 在组件中抛出一个事件
父组件响应式改变@pageChange="pageChange=handlePageChange"再 methods 中写 handlePageChange 函数

> 父组件通过 props 像子组件传值，子组件通过 event 数据传递给父组件

```
注册事件<a @click="handleClick(current)"></a>

methods:{
  handleClick(newPage){
    console.log(newPage);
    //抛出一个事件
    this.$emit("pageChange",newPage);
  },
}
父组件响应式注册事件改变@pageChange="handlePageChange($event)"  手动传参event
methods：{
  handelePageChange(newPage){
    //console.log("页码变了"，newPage);
    this.currnet=newPage;   //数据一改引发重新渲染
    （若父组件数据还不是继续$emit上找）
  },
},
```

### 优化工程结构

单独测试 vue 组件：
并建一个同名文件夹子文件命名为 index.vue 可将原 vue 文件剪切过去。webpack 默认找 index 文件
可将测试代码写入新建的同名文件夹再 vue serve
vue serve 地址路径

https://cli.vuejs.org/zh/guide/prototyping.html
先安装 vue serve 快速原型开发 npm install -g @vue/cli-service-global

//组件练习 17：50

### 组件练习

> ---

<script> 
methods:{
  inSelected(item){
    var link=item.link.toLowerCase(); //菜单链接地址
    var curPathname=location.pathname.toLowerCase();//当前浏览器的访问路径
    if(item.startWith){
      return curPathname.startsWith(link);
    }
    else{
      return curPathname ===link;
    }
    return location.pathname.toLowerCase()===path.toLowerCase();
  },
}
</script>

### 插槽 slot

用于占位，需要父组件传递内容的区域
子组件：<slot name="header"></slot>
父组件：<template v-slot:header>页头</template>
v-slot:或#
默认插槽可不写

左右布局:flex 用法
.left,.right{
flex: 0 0 auto; //xy 不能增长也不能压缩
overflow:hidden
}

### 路由插件

1. 如何根据地址中的路径选择不同的组件
2. 把选择的组件放到哪个位置
3. 如何无刷新的切换组件

npm i vue-router

> vue-router:
> 组件 RouterView RouterLink
> 路由配置 routes(设置路由匹配规则) mode(配置匹配模式 hash history abstract)
> 注入的原型对象 \$route(提供路由信息)

#### 路由模式

决定了路由从哪里获取访问路径，路由如何改变访问路径

1. hash 默认
   路由从浏览器地址栏中 hash 部分获取路径 /# 只看#后面的

2. history
   从浏览器地址栏中获取路径，改变路径使用 H5 的 history api
   无刷新变化路径 H5 无刷新 history.pushState(null,null,"/blog")

3. abstract
   路由从内存中获取路径，改变路径也是改变内存中的值，通常应用到非浏览器中

刷新：
请求 index.html
请求各种.js
请求各种.css
执行 js
创建 vue 应用
渲染全部组件树
挂载到指定的 div 中

不刷新:
执行一行 js 代码：切换某个区域的组件

> 无刷新跳转 vue
> <RouterLink> </RouterLink >
> :href 改成:to
> 根据路由模式生成对应超链接地址"#/blog"或"/blog"
> vue-router 提供了全局的组件 RouterLink 渲染的结果是一个 a 元素
> mode：history 为避免刷新页面，vue-router 实际上为它添加了点击事件，并阻止了默认行为，在事件内部使用 hitory api 更改路径

##### 激活状态

默认情况 vue-router 会用当前路径匹配导航路径/blog

- 如果当前路径是以导航路径开头，则算作匹配，会为导航的 a 元素添加类名 router-link-active（以导航路径开头）
  / 类名 router-link-active
- 如果当前路径完全等于导航路径，则算作精确匹配，会为导航的 a 元素添加类名 router-link-exact-active（等于导航路径）
  /blog 类名 router-link-active router-link-exact-active

#### RouterLink 布尔属性 exact

将匹配规则改为必须要精确匹配才能匹配类名 router-link-active
例 当前访问路径是/blog
导航路径 exact 类名
/ true 无
/blog false router-link-active,router-link-exact-active

例 当前访问路径是/blog/fw/123/32
导航路径 exact 类名
/ true 无
/blog false router-link-active

类名太长可以在绑定时修改
router-link-active 对应 active-class="selected"
router-link-exact-active 对应 exact-active-class=""

#### 命名路由

router 中添加 name 属性
使用命名路由可解除系统与路径之间的耦合
<RouterLink :to=/foo>
向 to 属性传递路由信息对象 RouterLink 会根据你传递的信息以及路由配置生成对应的路径
<RouterLink :to="{name:'foo'}">
选择关联 name 和 path 改名

### 弹出消息

#### 使用 css module

避免类名重复冲突。会自动加上唯一类名

需要将样式文件命名为 xxx.module.ooo

xxx 为文件名
ooo 为样式文件后缀名，可以是 css、less
div.className = 获取或设置指定元素的 class 属性的值。

<script>
//手写纯DOM操作
import styles from "./styles/message.module.less";
console.log(styles);//不加module为空对象
const div = document.createElement("div");
div.className = styles.message;
div.innerText = "尹崽憨批眼里只有我哈哈";
document.body.appendChild(div);
</script>

#### 得到组件渲染的 Dom

<script>

//获取某个组件渲染的 Dom 根元素
function getComponentRootDom (comp, props) {// 组件 属性
  const vm = new Vue({
    render: (h) => h(comp, { props }),  //渲染组件，传组件的属性
  });
  vm.$mount();    //挂载生成真实DOM元素
  return vm.$el;  //挂载完实例属性叫el就是真实dom返回
}
import Inventory from "./components/Inventory"
console.log(Inventory);//对象
var dom = getComponentRootDom(Inventory, { title: "尹青" });
console.log(dom);

//扩展vue实例
Vue.prototype.sayHello =function(){ 
  //全局通用，组件实例的_proto_继承Vue.prototype
  console.log("Hello!!");
};
</script>

#### ref 拿到子元素 DOM 对象和实例

拿到子元素 DOM 对象和实例可以做很多事情
<template>

<div>
<p ref="para">some paragraph</p>
<ChildComp ref="comp" />
<button @click="handleClick">查看所有引用</button>

  </div>
</template>

<script>
  import ChildComp from "./ChildComp"
	export default {
    components:{
      ChildComp
    },
    methods:{
      handleClick(){
        // 获取持有的所有引用
        console.log(this.$refs.comp);
        this.$refs.comp.m1();
        /*
        {
        	para: p元素（原生DOM）,
        	comp: ChildComp的组件实例
        }
        */
      }
    }
  }
</script>

> 通过 ref 可以直接操作 dom 元素，甚至可能直接改动子组件，这些都不符合 vue 的设计理念(不要直接操作数据,谁的数据谁负责)。除非迫不得已，否则不要使用 ref

#### 弹出消息

//获取 dom 元素的外层结构
.outerHTML

//计算最终样式
getComputedStyle(container).position ==="static"

//过渡效果
transition:0.3s;
transform:translate(-50%,-50%) translateY(15px)
opacity:0

浏览器渲染是异步的，代码执行完才开始渲染
//浏览器强行渲染导致 feflow 重排
div.clientHeight

==>升起正常位置
div.style.transform:translate(-50%,-50%)
div.style.opacity:1

//等一段时间，消失
setTimeout(() => {
div.style.opacity = 0;
div.style.transform = `translate(-50%,-50%) translateY(-25px)`;
div.addEventListener(
"transitionend", function () { div.remove(); }, { once: true })
}, duration);

div.addEventListener( //消失后触发事件，将其移除
"transitionend", 注册 transitionend 事件监听
function(){
div.remove();
options.callback && options.callback(); // 如果有回调函数则运行它
},
{once:true}
);
},duration);

//运用模板
handleClick(){
showMessage({
content:"评论成功",
type:"success",
container:this.\$refs.container,
callback:function(){
console.log("完成!!");
},
});
}

//文件同时导入导出在一个文件
export{ default as showMessage} from "./showMessage";
==
import showMessage from "./showMessage"
export {showMessage}

导入使用时直接
import {showMessage} from "@/路径"

//全局使用 showMessage
import showMessage from "./utils/showMessage";
Vue.prototype.\$showMessage=showMessage;

### 获取远程数据

xhr XMLHttpRequest
fetch h5
axios

#### vue-cli 配置文件 vue.config.js

代理

```
module.exports={
  devServer:{
    proxy:{
      "/api":{
        target:"https://www.zhihu.com",   //已api开头的转到对应的服务
      },
      "/commercial_api":{
        target:"https://www.zhihu.com",
      }
    }
  }
}
```

#### axios 请求

```
import axios from "axios";

async function getNews(){
  const resp =await axios.get(
    "http://localhost:8080/api/v4/videos/1484885874358280192"
  )
}
```

- //浏览器请求这个地址
- //到开发服务器 vue.config.js 匹配规则路径以 api 开头转发到对应https://lens.zhihu.com
- //则开发服务器去请求https://lens.zhihu.com/api/v4/videos/1484885874358280192数据给浏览器

resp.data 响应体

#### mock 模拟数据

````拦截器api>request.js
import axios from "axios";
import showMessage from "../utils/showMessage";

const ins=axios.create(); //创建一个axios实例等同于添加拦截器
ins.interceptors.response.use(function(resp){    //实例运行得到的响应都将先运行这个函数
  //console.log("拦截器");
  if(resp.code!==0){
    showMessage({
      content:resp.data.msg,
      type:"error ",
      duration:1500,
    });
    return null;
  }
  return resp;//resp.data//resp.data.data
});

export default ins;



```1正常浏览器请求api>banner.js
import request from "./request";

export async function getBanners(){
  return await request.get("/api/banner");      //请求这个接口的时候mock直接拦截api/banner请求并且造假数据
}
//getBanners().then((r)=>{
//  console.log(r);
//});
````

```2mock伪造数据mock>banner.js
在main.js中import "./mock/index";  //mock要写在最前面才能提前拦截


import Mock from "mockjs";

Mock.mock("/api/banner","get",{
  code:0,
  msg:"",
  data:[
    {
      id:"1",
      midImg:"",
      bigImg:"",
      title:"凛冬将至",
      description:"人唯有恐惧的时候方能勇敢",
    },{
      id:"1",
      midImg:"",
      bigImg:"",
      title:"凛冬将至",
      description:"人唯有恐惧的时候方能勇敢",
    }
  ]
})
```

```index.js
import "./banner";
import "./blog";
Mock.setup({
    timeout:'200-600'
  })
```

```main.js
import "./mock"; //运行定义规则
~~~
~~~
```

### 组件生命周期

实例被创建
注入
首次渲染：
编译生成虚拟 DOM 树 vnode tree
挂载

已挂载数据变动，响应式
重新渲染生成 dom 树
对比新旧俩树的差异将差异应用到真实 dom

VUE'中
实例被创建 --> beforeCreate
注入 --> created
生成 VNode --> beforeMount
生成真实 DOM --> mounted

已挂载 数据变动 -->beforeUpdate 重新渲染 -->updated

-->beforeDestroy

销毁组件 -->destroyed

以销毁

#### 实例应用

加载远程数据

<script>
import {getBanners} from"@/api/banner";

export default{
  data(){
    return {
      banners:[],
    };
  },
  1:created(){
    getBanners().then((r)=>{
      this.banners=r;
    });
   }
  2:async created(){
    this.banners=await getBanners();
  }
};
</script>

> api>banner.js 需要俩次异步吗?

export async function getBanners(){
return await request.get("/api/banner");
}

直接操作 dom

<script>
export default{
  data(){
    return{
      containerWidth:0,
      containerHeight:0
    }
  },
  mounted(){
    this.containerWidth=this.$refs.container.clientWidth;
    this.containerHeight=this.$refs.container.containerHeight;
  }
}
</script>

时间计时器 app.vue
<template>

<div class="container">
  <Clock v-if="showClock" />
  <button @click="showClock=!showClock">切换显示</button>
</div>
</template>
<script>
import Clock from "./Clock";
export default{
  components:{
    Clock,
  },
  data(){
    return {
      showClock:true,
    };
  },
};
</script>

Clock.vue
<template>

<h1>当前时间：{{current}}</h1>
</template>
<script>
export default{
  data(){
    return{
      current:this.getCurrent(),
      timer:null,
    };
  },
  methods:{
    getCurrent(){
      return new Date().toLocaleTimeString();
    },
  },
  created(){        //生成虚拟dom vnode tree前
    console.log("created");
    this.timer=setInterval(()=>{
      console.log("更新了时间");
      this.current=this.getCurrent();
    },1000);
  },
  destroyed(){
    clearInterval(this.timer);  //销毁计时
  }
};
</script>

### 完成首页

> transform:translate(-50%,-50%); //左右居中

> 动画弹跳

```
&.icon-up{
  top:gap;
  animation: jump-up 2s infinite;
}

&.icon-down{
  top:auto;
  bottom:@gap;
  animation: jump-down 2s infinite;
}
@jump:5px;
@keyframes jump-up{
  0%{
    transform:translate(-50%,@jump);
  }
  50%{
    transform:translate(-50%,-@jump);
  }
  100%{
    transform:translate(-50%,@jump);
  }
}
@keyframes jump-down{
  0%{
    transform:translate(-50%,-@jump);
  }
  50%{
    transform:translate(-50%,@jump);
  }
  100%{
    transform:translate(-50%,-@jump);
  }
}
```

> 圆点样式

```
li{
  width:7px;
  height:7px;
  border-radius:50%;
  background:#333;
  cursor:pointer;
  margin-bottom:10px;
  border:1px solid #fff;
  box-sizing:border-box;
  transition:0.5s;
}
```

> 数据切换样式 index.vue

<template>
<div v-loading="isLoading" class="home-container" ref="container" @wheel="handleWheel">
  <ul
    class="carousel-container"
    :style="{
      marginTop,
    }"
    @transitionend="handleTransitionEnd"
  >
  <li v-for="item in banners" :key="item.id">
  <CarouselItem :carousel="item" ref="child" />   //父组件调用子组件方法
  </li>
  </ul>

  <div v-show="index>=1" class="icon icon-up" @click=switchTo(index-1)>
  <Icon type="arrowUp" />
  </div>
  <div v-show="index<banners.length -1" class="icon icon-down" @click=switchTo(index+1)>
  <Icon type="arrowDown" />
  </div>

  <ul class="indicator">
    <li
      :class="{
        active: i===index,
      }"
      v-for="(item,i) in banners"
      :key="item.id"
      @click=switchTo(i)
    ></li>
  </ul>
</div>
</template>
<script>
export default {
  data(){
    return {
      isLoading:true,
      banners:[],
      index:0, //当前显示的是第几张轮播图
      containerHeight:0,  //整个容器的高度
      switching:false,    //是否正在切換中
    };
  },
  async created() {
      this.banners=await getBanners();
      this.isLoading=false;
  },
  mounted(){
    this.containerHeight=this.$refs.container.clientHeight;
    window.addEventListener("resize",this.handleResize);  //添加监听事件观测视口变化
  },
  destroyed(){
    window.removeEventListener("resize",this.handleResize); //准备清除事件
  },
  computed:{
    marginTop(){
      return -this.index *this.containerHeight+"px";
    },
  },
  methods:{
    //切换轮播图
    switchTo(i){
      this.index=i;
    },
    handleWheel(e){
      if(this.switching){
        return;
      }
      if(e.deltaY<-5&&this.index>0){
        this.switching=true;
        this.index--;
      }else if (e.deltaY>5&&this.index<this.banners.length-1){
        this.switching=true;
        this.index++;
      }
    },
    handleTransitionEnd(){
      this.switching=false;
      this.$refs.child.showWords();  //父组件调用子组件方法refs //子组件调用父组件this.$parent.showWords();
    },
    handleResize(){
      this.containerHeight=this.$refs.container.clientHeight;
    }
  },
}
</script>

<style>
.home-container{
  width:100%;
  height:100%;
  position:relative;
  overflow:hidden;
  ul{
    margin:0;
    list-style:none;
    padding:0;
  }
}
.carousel-container {
  width:100%;
  height:100%;
  transition:500ms;
  li{
    width:100%;
    height:100%;
  }
}
</style>

> Carouselitem.vue

<template>
<div class="carousel-item-container" ref="container" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave">
  <div class="carousel-img" ref="image" :style="imagePosition">
    <ImageLoader  @load="this.showWords"  :src="carousel.bigImg" :placeholder="carousel.midImg" />
  </div>
  <div class="title" ref="title">{{carousel.title}}</div>
  <div class="desc" ref="desc">{{carousel.description}}</div>
</div>
</template>
<script>
export default{
  props:["carousel"],
  //  <li v-for="item in banners" :key="item.id">
  //  <CarouselItem :carousel="item" />
  //  </li>
  data(){
    return{
      titleWidth:0,
      descWidth:0,
      containerSize:null,//外层容器的尺寸
      innerSize:null,    //里层图片的尺寸
      mouseX:0,   //相对于div盒子的
      mouseY:0,
    };
  },
  computed:{
    //得到图片坐标
    imagePosition(){
      if(!this.innerSize ||!this.containerSize){
        return;
      }
      const extraWidth=this.innerSize.width-this.containerSize.width; //多出来的宽度
      const extraHeight=this.innerSize.height-this.containerSize.height;//多出来高度
      console.log(extraWidth,extraHeight);
      //x/mouseX=-extraWidth/container.width
      const left=-extraWidth/this.containerSize.width*this.mouseX
      const top=-extraHeight/this.containerSize.height*this.mouseY
      return{
        left:left+"px",
        top:top+"px",
        //或者为了缓加载
        //transform:`translate(${left}px,${top}px)`
      };
    },
    center(){
      return{
        x:this.containerSize.width/2,
        y:this.containerSize.height/2,
      };
    }
  },
  mounted(){
    this.titleWidth=this.$refs.title.clientWidth;
    this.descWidth=this.$refs.desc.clientWidth;
    this.setSize();
    //鼠标居中
    this.mouseX=this.center.x;
    this.mouseY=this.center.y;
    window.addEventListener("resize",this.setSize);
  },
  destroyed(){
    window.removeEventListener("resize",this.setsize)
  },
  methods:{
    //调用该方法，显示文字
    //文字渐进式显现
    showWords(){
        this.$refs.title.style.opacity=1;
        this.$refs.title.style.width=0;
        //强制渲染重排reflow
        this.$refs.title.clientWidth;
        this.$refs.title.style.transition="1s";
        this.$refs.title.style.width=this.titleWidth+"px";
        //描述
        this.$refs.desc.style.opacity=1;
        this.$refs.desc.style.width=0;
        //强制渲染重排reflow
        this.$refs.desc.clientWidth;
        this.$refs.desc.style.transition="2s 1s";//显示耗费两秒，延迟一秒显示
        this.$refs.desc.style.width=this.descWidth+"px";
    },
    //加餐：每翻动一页文字都缓慢加载?
    //添加监听事件index改变运行showWords方法？
    //vue父组件缓加载ref调用子组件方法showWords
    setSize(){
      this.containerSize={
        width:this.$refs.container.clientWidth,
        height:this.$refs.container.clientHeight,
      };
      this.innerSize={
        width:this.$refs.image.clientWidth,
        height:this.$refs.image.clientHeight,
      };
    },
    handleMouseMove(e){
      const rect=this.$refs.container.getBoundingClientRect();  //获取矩形相关信息
      this.mouseX=e.clientX-rect.left;    //相对于div盒子的
      this.mouseY=e.clientY-rect.top;
    },
    handleMouseLeave(){
      this.mouseX=this.center.x;
      this.mouseY=this.center.y;
    }
  },
};

</script>

> 定义的数据放 date-return 里面，页面效果 template 写好触发方法要求，计算属性 computed 写需要用到的值或属性，加载 dom 后操作 mounted 可写调用运行方法 destroyed 销毁组件，methods 写各种方法

> 文字描边加粗
> text-shadow:1px 0 0 rgba(0,0,0,0.5),-1px 0 0 rgba(0,0,0,0.5),0 1px 0 rgba(0,0,0,0.5),0 -1px 0 rgba(0,0,0,0.5);

> 文字渐进式显现 27.48
> props:["carousel"],传递属性：<CarouselItem :carousel="item" />

23.40 视口抖动问题

> container.width 鼠标位置 -extraWidth 图片坐标

> addEventListener 能监听什么事件：vuex

### 自定义指令

数据未到得需要加载中的图 Loading 组件
//注意相对于父组件中居中布局

全局注册 -->main.js
import vLoading from "./directives/loading";
Vue.directive("loading",vLoading);

局部注册指令

<script>
export default{
  //定义指令
  directives:{
    //指令名词
    mydirec1:{
        //指令配置
    }
  }
}
</script>

{
bind(){
//只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
},
inserted(){
//被绑定元素插入父节点时调用
},
update(){
//所在组件的 VNode 更新时调用
}
}

```
<div v-mydirec:a.b.c="2>1"></div>
指令名称:mydirec
="" js表达式决定value的值
arg指令参数:a
modifiers:{b,c}
```

> 导出指令的配置对象
> v-loading:="isLoading"

<script>
import loadingUrl from "@/assets/loading.svg";
import styles from "./loading.module.less";
//得到el中loading效果的img元素
function getLoadingImage(el){
  return el.querySelector("img[data-role=loading]")
}
function createLoadingImg(){
  const img=document.createElement("img")
  img.dataset.role="loading";
  img.src=loadingUrl;
  img.className=styles.loading;
  return img;
}
//export default{
  //bind(el,binding){
  //  //根据bingding.value的值,决定创建或删除img元素
  //}
  //update(el,binding){
  //  //根据bingding.value的值,决定创建或删除img元素
  //}
//}
//配置简化写法
export default function(el,binding){
//根据bingding.value的值,决定创建或删除img元素
  const curImg=getLoadingImage(el);
  if(binding.value){      //默认true转圈圈
    if(!curImg){
      const img=createLoadingImg();   //没有图片就创造图片
      el.appendChild(img);
    }
  }else{
    if(curImg){
      curImg.remove();    //false了有图片就删除图片
    }
  }
}
</script>

### 组件混入 4:38

抽离公共代码提高复用性

<scrip>
const common={
  data(){
    return{
      a:1,
      b:2
    }
  },
  created(){
    console.log("wofhoeiw")
  },
  computed:{
    sun(){
      return this.a+this.b;
    }
  }
}
const comp 1={
mixins:[common] //可混入多个配置代码
created(){
console.log("comefef,this.a,this.b,this.sum)  
 //先运行复用代码里的,还可调用参数
}
</script>

//公共的远程获取数据的代码

> mixins->fetchData.js

<script>
//具体的组件中，需要提供一个远程获取数据的方法 fetchData
export default function(defaultDataValue=null){ //默认远程数据为null
  data(){
    return{
      isLoading:true,
      data:defaultDataValue,
    };
  },
  async created(){
    this.data=await this.fetchData();
    this.isLoading=false;
  }
  //原本状态
    // async created() {
      // this.banners=await getBanners();
      // this.isLoading=false;
  // },
}
</script>

> index.vue

<script>
import {getBanners}from"@/api/banner";
import fetchData from "@/mixins/fetchData.js";
//实例用法mixins:[fetchData([])];

methods:{
  async fetchData(){
  return await getBanners();
  }
}
</script>

### 组件递归

RightList.vue

<template>
  <ul class="right-list-container">
    <li v-for="(item,i) in list"  :key="i">
      <span @click="handleClick(item)" :class="{active:item.isSelect}">{{item.name}}</span>
      显示当前组件
      <RightList :list="item.children" @select="handleClick"/>
    </li>
  </ul>
</template>

<script>
export default{
  name:"RightList",   //自己把自己导入进来注册
  props:{
    list:{
      type:Array,
      default:()=>[]
    },
  },
  methods:{
    handleClick(item){      //写个方法点了哪个元素丢给父级组件
    this.$emit("select",item);
  },
}
};
</script>

RightList-test.vue 父组件

<template>
  <RightList :list="list" @select="handleSelect" />
</template>
<script>
import Right from "./RightList";
export default{
  components:{
    RightList,
  },
  data(){
  },
  methods:{
    handleSelect(item){
      console.log(item);
    },
  },
}
</script>

### 开发文章列表页 1

> main.js 测试
> import \*as blogApi from "./api/blog";

blogApi.getBlogTypes().then((r)=>{
console.log("博客分类",r);
});

blogApi.getBlogs(2,10,3).then((r)=>{
console.log("博客",r)
})

> 根据接口写 api>blog.js
> mock 数据时需注意空格格式

<script>
import request from "./request";
//获取博客列表数据
export async function getBlogs(page=1,limit=10,categoryid=-1){
  return await request.get("/api/blog",{
    params:{
      page,
      limit,
      categoryid,
    }
  });
}
//获取博客分类
export async function getBlogTypes(){
  return await request.get("/api/blogtype");
}
</script>

然后 mock-js 拦截
写 mock 伪造数据模板 mock>blog

<script>
import Mock from "mockjs";
import qs from "querystring";
Mock.mock("/api/blogtpe","get",{
  code:0,
  msg:"",
  "data|10-20":[
    {
      "id|+1":1,
      name:"分类@id",
      "articleCount|0-300":0,
      "order|+1":1,
    },
  ],
});

//mock分页获取博客
Mock.mock(/^\/api\/blog(\?.+)?$/,"get",function(options){   //options请求的相关信息
//options.url有动态变化的数据，得提取出来
// 第三方库querystring处理地址栏参数
//npm i querystring再在头部导入
const query =qs.parse(option.url);
console.log(query);
return Mock.mock({
  code:0,
  msg:"",
  data:{
    "total|2000-3000":0,
    ['rows|${query.limit||10}']:[
      {
        id:"@guid",
        title:"@ctitle",
        description:"@cparagraph(1,10)",
        category:{
          "id|1-10":0,
          name:"分类@id",
        },
        "scanNumber|0-3000":0,
        "commentNumber|0-300":30,
        thumb:Mock.Random.image("300*250","#000","#fff","Random Image"),
        createDate:'@date('T')',
      }
    ],
  }
})

})

</script>

### 开发文章列表 2

Blog
地址栏双向绑定响应式
BlogList 根据路由路径地址栏参数显示文章列表，完成分页  
BlogCategory 显示文章分类，根据路由信息，显示激活状态
兄弟节点也要相互通信

#### 路由跳转逻辑

> 动态路由
> 路由中动态可用 :属性名 xxx 绑定表达内容变化
> 在 vue-router 中，将变化的这一部分 xxx 称为 params 可通过 vue 组件中通过 this.\$route.params 获取

vue-router 注入的原型对象 \$route 提供路由所有信息比 router 少一个 s

- fullPath 完整路径
- hash ""
- name 匹配到的路由名称
- params 动态绑定对象 xxx:"值"
- path 路径
- query 地址栏参数对象 limit page

<script>
  export default{
    created(){
      console.log(this.$route);
    },
  };
</script>

> 模板用的是组件里面的东西

#### BlogList.vue 组件

根据路由信息，显示文章列表，并完成分页

导航页
D:\VScode\vue\attempts\src\assets\BlogList.vue 思路

> 根据计算出路由中的各种信息，
> 获取数据，传入 fetchData 渲染显示
> 给分页组件提供数据，触发 pageChange 事件调用 handlePageChange router.push 改变导航的值
> watch 检测\$route 路由信息是否变化重新调用 fetchData 方法获取数据渲染
> 两组件完成间接通信

#### BlogCategory.vue 组件

显示所有文章分类根据路由信息，显示激活状态

22 节 38.46

### \$listeners 和 v-model

#### \$listeners 是 vue 的一个实例属性,用于获取父组件传来的所有事件函数

父组件
<child @event1="handleEvent1" @event2="handleEvent2" />

子组件
this.\$listeners //{event:handleEvent1,event:handleEvent2}

$emit 和$listeners 通信的异同
相同点：均可实现子组件向父组件传递消息

差异点：

- $emit更加符合单向数据流，子组件仅发出通知，由父组件监听做出改变；
而$listeners 则是在子组件中直接使用父组件的方法。
- 调试工具可以监听到子组件$emit的事件，但无法监听到$listeners 中的方法调用
- 由于$listeners中可以获得传递过来的方法，因此调用方法可以得到其返回值。但$emit 仅仅是向父组件发出通知，无法知晓处理结果

#### v-model 数据双向绑定

v-model="formData.loginId"
:value="formData.loginId"
@input="formData.loginId=\$event.target.value"

- .stop 阻止事件冒泡
- .prevent 阻止事件默认行为
- .capture 捕获阶段运行事件
- .self 事件只能发生在当前元素
- .passive 提高效率

  33.17

### 事件总线

11：55
事件总线监听和卸载 event1 不同的组件和普通模块
别的组件可触发事件 event1 从而处理监听的组件
分类继承传 Data

12.：36

- 提供监听某个事件的接口
- 提供取消监听的接口
- 触发事件的接口(可传递数据)
- 触发事件后会自动通知监听者

### 开发文章详情页 part5

17.16

### 代码优化

mixins 混入公共代码
事件总线跨页面组件监听处理问题

- mixins 监听滚动 emit 提交事件总线 mainScroll 以滚动,Top.vue\$on 收到滚动执行方法(判断是否滚动距离满足大于显示条件)
- Top.vue 点击事件 emit 提交事件总线 setMainScroll，mixins 收到监听执行方法(改变高度)
- 以及对应的销毁事件

### 图片懒加载

自定义指令 lazy 传入图片 inserted 处理后放入 imgs 并立马处理设置图片(setImage(img))
换页 unbind 指令与元素解绑时调用从 imgs 中删除 img
事件总线监听滚动就会调用是否需要处理设置图片(setImages)并防抖
setImages 遍历出 img 交给 setImage 处理
setImage 关键判断图片是否在视口中
先同一设定 img.src 为一张图
当 img.dom.top>图片高度 height 时说明 img.dom 露出一点在视口里,以及 img.dom.top<视口高度就需要加载真实图片
真实图片加载完成后触发事件将其 img.src 改为 tempImg.src
只要处理完就不再考虑将 img 从 imgs 中删除,其判断 i 为对象改变其中属性即改变

### 数据共享

#### 问题

Vue 中遇到共享数据
例如 1.当前登入的用户 2.网站的全局设置 3.用户偏好设置

- 如何保证数据的唯一性??
  如果数据不唯一会浪费大量内存资源降低运行效率，就肯出现不统一的数据难以维护
- 某个组件改动数据后，如何让其他用到该数据的组件知道数据变化??
  事件总线貌似可以解决该问题，但需要在组件中手动的维护监听，极其不方便而事件总线的目的在于通知，而不是共享数据

错误示范：把所有的共享数据全部提升到根组件，如何通过属性不断下发，当某个组件需要修改数据时，又不断向上抛出事件，直到根组件完成对数据的修改
缺陷：需要编写大量代码层层下发上抛数据，很多组件被迫拥有了自己根本不需要的数据，很多组件被迫注册了自己根本处理不了的事件

#### Vuex 独立的数据仓库

可用 js 写，仓库数据响应式
组件树或者其他 js 代码需要什么共享数据就拿什么，
组件可以自由改变仓库中的数据，仓库数据变化的话依赖的组件都要重新渲染更新

安装 vuex
npm i vuex
在 src 目录下新建 store 文件夹 index.js

```
import Vuex form "vuex";
import Vue from "vue";
Vue.use.(Vuex);//应用vuex插件

function delay(duration) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, duration);
  });
}

const store=new Vuex.Store({
  //仓库的配置

  state:{ //仓库的初始状态(数据)
  count:0
  },
  mutations: {
    /**
     * 每个mutation是一个方法，它描述了数据在某种场景下的变化
     * increase mutation描述了数据在增加时应该发生的变化
     * 参数state为当前的仓库数据
     */
    increase(state){
      state.count++;
    },
    decrease(state){
      state.count--;
    },
    /**
     * 求n次幂
     * 该mutation需要一个额外的参数来提供指数
     * 我们把让数据产生变化时的附加信息称之为负荷（负载） payload
     * payload可以是任何类型，数字、字符串、对象均可
     * 在该mutation中，我们约定payload为一个数字，表示指数
     */
    power(state, payload){
      state.count **= payload;
    }
  },
   actions: {
    async asyncIncrease(ctx) {
      await delay(1000);
      ctx.commit("increase");
    },
    async asyncDecrease(ctx) {
      await delay(1000);
      ctx.commit("decrease");
    },
    async asyncPower(ctx, payload) {
      await delay(1000);
      ctx.commit("power", payload);
    },
  },
})
export default store;
```

想要在组件中使用还在 main.js 中向 vue 注入仓库(和 router 一样)
即可通过实例的\$store 的属性访问到仓库

#### 数据的变更

尽管可以利用数据响应式的特点直接变更数据，
但这样做法在大型项目中会遇到问题(如果有一天，你发现共享数据是错的，而一百多个组件都有可能变更过这块数据，你该如何知道是哪一步数据变更出现了问题？)
为了能够更好的跟踪数据的变化，vuex 强烈建议使用 mutation 来更改数据
在 vuex mutation 中列出可能出现的情况
当我们有了 mutation 后，就不应该直接去改动仓库的数据了
而是通过 store.commit 方法提交一个 mutation，具体做法是
store.commit("mutation 的名字", payload);

**特别注意： **

1. mutation 中不得出现异步操作

在实际开发的规范中，甚至要求不得有副作用操作
副作用操作包括：
异步
更改或读取外部环境的信息，例如 localStorage、location、DOM 等

2. 提交 mutation 是数据改变的唯一原因

#### 如果在 vuex 中要进行异步操作，需要使用 action

触发 action 为 dispatch
store.dispatch("asyncIncrease").then(()=>console.log("变化完成"));

1.06

### 打包结果分析

发现问题 分析问题 设想方案 尝试解决 测试
原理灵活应用

#### 分析打包结果

vue-cli 是利用 webpack 打包 //见官网
加入 webpack 插件 webpack-bundle-analyzer 来分析

> npm i webpack-bundle-analyzer -D //不加-D 生产环境，加了开发环境

避免在开发环境中启动 webpack-bundle-analyzer
新建 webpack.config.js 导入 vue.config.js 中

#### 优化服务包体积

##### 使用 CDN

- 用了没全用可树苗优化(具名)vuex
- 而 router vue axios vuex 可使用 cdn(内容分发网络)来优化

1. 首先告诉 webpack 不要对公共库进行打包
2. 在 public 里 index 的页面中导入免费 cdn(bootcdn)找到对应版本和 mian.js、、
   public 里 index 被 html-webpack-plugin 读取
   开发环境不能用 cdn 否则 vue 工具无法识别
3. 代码变动//不存在 cdn 就默认

##### 启用现代模块

为了兼容各种浏览器，vue-cli 在内部使用了@babel/present-env 来对代码降级，可通过.browserlistrc 配置来设置兼容的目标浏览器
只配置现代浏览器，把.browserlistrc 删掉就不会考虑兼容性

偷懒：因为现代浏览器的用户也被迫使用了降级后的代码而降低代码中包含了大量的 polyfill，从而提升包的体积

1. 降级后的包(大)，提供给旧浏览器使用
2. 未降级的包(小)，提供给现代浏览器用户使用

除应用 webpack 进行多次打包，还可利用 vue-cli 给文明提供的命令
在 packjson 中修改 build：vue-cli-service build --modern
可是 vue2 中加--modern 好像不适用，袁说报错不用管！！

打包后的 index 中属性 rel="preload"预加载暂时不用
现代浏览器看到 module 就会把同是 moduledpreload 的预加载
旧浏览器看到 nomodule 很兴奋就去加载
当 ESmodule 处理

#### 优化项目包体积

指 src 目录中的打包结果

##### 页面分包

默认情况下，vue-cli 会利用 webpack 将 src 目录中的所有代码打包成一个 bundle
这样就导致访问一个页面时，需要加载所有页面的 js 代码
我们可以利用 webpack 对动态 import 的支持，从而达到把不同页面的代码打包到不同文件中
每一个页面进行单独打包 公共代码提出来.总体积变大，每一次加载变少
dist 目录下 index 的 prefetch(没用到慢慢加载) 比 preload 优先级要低
// routes 路由懒加载
export default [
{
name: "Home",
path: "/",
component: () => import(/* webpackChunkName: "home" */ "@/views/Home"),
},
{
name: "About",
path: "/about",
component: () => import(/* webpackChunkName: "about" */"@/views/About"),
}
];

##### 优化首屏响应 47.18

首页白屏受很多因素的影响

vue 页面需要通过 js 构建，因此在 js 下载到本地之前，页面上什么也没有

一个非常简单有效的办法，即在页面中先渲染一个小的加载中效果，等到 js 下载到本地并运行后，即会自动替换
public 里 index 插入

<div id="app">
  <img src="loading.gif" />
</div>

放 public 新建 img 文件夹

- static 纯静态资源原封不动
- assets 嵌入式参与打包

### 异步组件

> component: () => import(/_ webpackChunkName: "home" _/ "@/views/Home"),

本质就是函数调用返回 promise，result 后变成组件配置对象
在代码层面 vue 组件就是配置对象
可能发生场景一时半会拿不到对象(异步)
例如：

- ajax 加载拿到数据
- 为合理分包，组件配置对象需通过 import()动态导入加载

```异步组件可更多配置
const AsyncComponent = () => ({
  // 需要加载的组件 (应该是一个 `Promise` 对象)
  component: import('./MyComponent.vue'),
  // 异步组件加载时使用的组件
  loading: LoadingComponent,
  // 加载失败时使用的组件
  error: ErrorComponent,
  // 展示加载时组件的延时时间。默认值是 200 (毫秒)
  delay: 200,
  // 如果提供了超时时间且组件加载也超时了，
  // 则使用加载失败时使用的组件。默认值是：`Infinity`
  timeout: 3000
})
```

process.env.NODE_ENV 可能 production 生产环境或 development 开发环境
本身 node 环境，vue-cli 望浏览器里注入些代码

function getPageComponent(pageCompResolver) { //不能直接用 path 因为要交给 webpack，动态依赖关系可能分辨不出，所以写出函数
return async () => {
start();// console.log("组件开始加载");
if (process.env.NODE_ENV === "development") {
await delay(2000);
}
const comp = await pageCompResolver();
done();// console.log("组件结束加载");
return comp;
};
}

> 异步组件好处加载完不会重复加载
> 再用第三方库 NProgress 假装加载进度笑死

# 组件通信总结

## 父子组件通信

> 面试题：vue 组件之间有哪些通信方式？
> 绝大部分`vue`本身提供的通信方式，都是父子组件通信

### prop

最常见的组件通信方式之一，由父组件传递到子组件

### event

最常见的组件通信方式之一，当子组件发生了某些事，可以通过`event`通知父组件

### style 和 class

父组件可以向子组件传递`style`和`class`，它们会合并到子组件的根元素中

**示例**
父组件

```vue
<template>
	<div id="app">
		<HelloWorld style="color:red" class="hello" msg="Welcome to Your Vue.js App" />
	</div>
</template>
<script>
	import HelloWorld from './components/HelloWorld.vue';
	export default {
		components: {
			HelloWorld,
		},
	};
</script>
```

子组件

```vue
<template>
	<div class="world" style="text-align:center">
		<h1>{{ msg }}</h1>
	</div>
</template>

<script>
	export default {
		name: 'HelloWorld',
		props: {
			msg: String,
		},
	};
</script>
```

渲染结果：

```html
<div id="app">
	<div class="hello world" style="color:red; text-aling:center">
		<h1>Welcome to Your Vue.js App</h1>
	</div>
</div>
```

### attribute

如果父组件传递了一些属性到子组件，但子组件并没有声明这些属性，则它们称之为`attribute`，这些属性会直接附着在子组件的根元素上(可通过\$attrs 得到父组件传来的所有 attribute)

> 不包括`style`和`class`，它们会被特殊处理
> **示例**
> 父组件

```vue
<template>
	<div id="app">
		<!-- 除 msg 外，其他均为 attribute -->
		<HelloWorld data-a="1" data-b="2" msg="Welcome to Your Vue.js App" />
	</div>
</template>

<script>
	import HelloWorld from './components/HelloWorld.vue';

	export default {
		components: {
			HelloWorld,
		},
	};
</script>
```

子组件

```vue
<template>
	<div>
		<h1>{{ msg }}</h1>
	</div>
</template>

<script>
	export default {
		name: 'HelloWorld',
		props: {
			msg: String,
		},
		created() {
			console.log(this.$attrs); // 得到： { "data-a": "1", "data-b": "2" }
		},
	};
</script>
```

渲染结果：

```html
<div id="app">
	<div data-a="1" data-b="2">
		<h1>Welcome to Your Vue.js App</h1>
	</div>
</div>
```

子组件可以通过`inheritAttrs: false`配置，禁止将`attribute`附着在子组件的根元素上，但不影响通过`$attrs`获取

### natvie 修饰符

在注册事件时，父组件可以使用`native`修饰符，将事件注册到子组件的根元素上
**示例**
父组件

```vue
<template>
	<div id="app">
		<HelloWorld @click.native="handleClick" />
	</div>
</template>

<script>
	import HelloWorld from './components/HelloWorld.vue';

	export default {
		components: {
			HelloWorld,
		},
		methods: {
			handleClick() {
				console.log(1);
			},
		},
	};
</script>
```

子组件

```vue
<template>
	<div>
		<h1>Hello World</h1>
	</div>
</template>
```

渲染结果

```html
<div id="app">
	<!-- 点击该 div，会输出 1 -->
	<div>
		<h1>Hello World</h1>
	</div>
</div>
```

### \$listeners

子组件可以通过`$listeners`获取父组件传递过来的所有事件处理函数

### v-model

### sync 修饰符

和`v-model`的作用类似，用于双向绑定，不同点在于`v-model`只能针对一个数据进行双向绑定，而`sync`修饰符没有限制

示例

子组件

```vue
<template>
	<div>
		<p>
			<button @click="$emit(`update:num1`, num1 - 1)">-</button>
			{{ num1 }}
			<button @click="$emit(`update:num1`, num1 + 1)">+</button>
		</p>
		<p>
			<button @click="$emit(`update:num2`, num2 - 1)">-</button>
			{{ num2 }}
			<button @click="$emit(`update:num2`, num2 + 1)">+</button>
		</p>
	</div>
</template>

<script>
	export default {
		props: ['num1', 'num2'],
	};
</script>
```

父组件

```vue
<template>
	<div id="app">
		<Numbers :num1.sync="n1" :num2.sync="n2" />
		<!-- 等同于 -->
		<Numbers :num1="n1" @update:num1="n1 = $event" :num2="n2" @update:num2="n2 = $event" />
	</div>
</template>

<script>
	import Numbers from './components/Numbers.vue';

	export default {
		components: {
			Numbers,
		},
		data() {
			return {
				n1: 0,
				n2: 0,
			};
		},
	};
</script>
```

### $parent和$children

在组件内部，可以通过`$parent`和`$children`属性，分别得到当前组件的父组件和子组件实例

### $slots和$scopedSlots

### ref

父组件可以通过`ref`获取到子组件的实例

## 跨组件通信

### Provide 和 Inject

示例

```js
// 父级组件提供 'foo'
var Provider = {
	provide: {
		foo: 'bar',
	},
	// ...
};

// 组件注入 'foo'
var Child = {
	inject: ['foo'],
	created() {
		console.log(this.foo); // => "bar"
	},
	// ...
};
```

详见：https://cn.vuejs.org/v2/api/?#provide-inject

### router

如果一个组件改变了地址栏，所有监听地址栏的组件都会做出相应反应

最常见的场景就是通过点击`router-link`组件改变了地址，`router-view`组件就渲染其他内容

### vuex

适用于大型项目的数据仓库

### store 模式

适用于中小型项目的数据仓库

```js
// store.js
const store = {
  loginUser: ...,
  setting: ...
}

// compA
const compA = {
  data(){
    return {
      loginUser: store.loginUser
    }
  }
}

// compB
const compB = {
  data(){
    return {
      setting: store.setting,
      loginUser: store.loginUser
    }
  }
}
```

### eventbus

组件通知事件总线发生了某件事，事件总线通知其他监听该事件的所有组件运行某个函数

# 虚拟 DOM 详解

> 面试题：请你阐述一下对 vue 虚拟 dom 的理解

1. 什么是虚拟 dom？

   虚拟 dom 本质上就是一个普通的 JS 对象，用于描述视图的界面结构

   在 vue 中，每个组件都有一个`render`函数，每个`render`函数都会返回一个虚拟 dom 树，这也就意味着每个组件都对应一棵虚拟 DOM 树

   <img src="http://mdrs.yuanjin.tech/img/20210225140726.png" alt="image-20210225140726003" style="zoom:30%;" align="left" />

2. 为什么需要虚拟 dom？

   在`vue`中，渲染视图会调用`render`函数，这种渲染不仅发生在组件创建时，同时发生在视图依赖的数据更新时。如果在渲染时，直接使用真实`DOM`，由于真实`DOM`的创建、更新、插入等操作会带来大量的性能损耗，从而就会极大的降低渲染效率。
   因此，`vue`在渲染时，使用虚拟 dom 来替代真实 dom，主要为解决渲染效率的问题。

3. 虚拟 dom 是如何转换为真实 dom 的？
   在一个组件实例首次被渲染时，它先生成虚拟 dom 树，然后根据虚拟 dom 树创建真实 dom，并把真实 dom 挂载到页面中合适的位置，此时，每个虚拟 dom 便会对应一个真实的 dom。
   **_但界面只需要渲染一次后面不需要重新渲染 vue 效率低，多一步生成虚拟 dom 再转换真实 dom 比直接生成 dom 费力，vue 优势在与多次渲染能提高效率_**

   如果一个组件受响应式数据变化的影响，需要重新渲染时，它仍然会重新调用 render 函数，创建出一个新的虚拟 dom 树，用新树和旧树对比，通过对比，vue 会找到最小更新量，然后更新必要的虚拟 dom 节点，最后，这些更新过的虚拟节点，会去修改它们对应的真实 dom
   `实际上是直接使用新树，抛弃旧树，然后只更新必要的正式DOM详见diff算法`
   这样一来，就保证了对真实 dom 达到最小的改动。

   <img src="http://mdrs.yuanjin.tech/img/20210225144108.png" alt="image-20210225144108143" style="zoom:33%;" align="left" />

4. 模板和虚拟 dom 的关系

   vue 框架中有一个`compile`模块，它主要负责将模板转换为`render`函数，而`render`函数调用后将得到虚拟 dom。

   编译的过程分两步：

   1. 将模板字符串转换成为`AST抽象语法树`
   2. 将`AST`转换为`render`函数

   如果使用传统的引入方式，则编译时间发生在组件第一次加载时，这称之为运行时编译。
   如果是在`vue-cli`的默认配置下，编译发生在打包时，这称之为模板预编译。
   编译是一个极其耗费性能的操作，预编译可以有效的提高运行时的性能，而且，由于运行的时候已不需要编译，`vue-cli`在打包时会排除掉`vue`中的`compile`模块，以减少打包体积

   模板的存在，仅仅是为了让开发人员更加方便的书写界面代码

   **vue 最终运行的时候，最终需要的是 render 函数，而不是模板，因此，模板中的各种语法，在虚拟 dom 中都是不存在的，它们都会变成虚拟 dom 的配置**

# v-model

> 面试题：请阐述一下 `v-model` 的原理

`v-model`即可以作用于表单元素，又可作用于自定义组件，无论是哪一种情况，它都是一个语法糖，最终会生成一个属性和一个事件
**当其作用于表单元素时**，`vue`会根据作用的表单元素类型而生成合适的属性和事件。例如，作用于普通文本框的时候，它会生成`value`属性和`input`事件，而当其作用于单选框或多选框时，它会生成`checked`属性和`change`事件。

`v-model`也可作用于自定义组件，**当其作用于自定义组件时**，默认情况下，它会生成一个`value`属性和`input`事件。

```html
<Comp v-model="data" />
<!-- 等效于 -->
<Comp :value="data" @input="data=$event" />
```

开发者可以通过组件的`model`配置来改变生成的属性和事件

```js
// Comp
const Comp = {
	model: {
		prop: 'number', // 默认为 value
		event: 'change', // 默认为 input
	},
	// ...
};
```

```html
<Comp v-model="data" />
<!-- 等效于 -->
<Comp :number="data" @change="data=$event" />
```

# 数据响应原理

Observer 负责把原始对象变为变成一个响应式对象 (getter 和 setter)
属性，数组加上 Dep
render 函数需要执行，就交给 watcher 执行，设置全局变量运行 render 函数
执行过程中用到响应式对象中的属性，就会依赖收集[记录依赖 dep.depend()]。
(当读取对象,属性,数组就记录什么东西[render]在用)**界面渲染出来**
触发事件改变数据就派发更新,通知 watcher 有变化[派发更新 dep.notify()]
watcher 不会立即执行 render 函数，而是交给调度器 Scheduler 处理添加到队列中，
把队列执行生成函数交给 nextTick 队列通过 Promise 放到微队列里面异步执行
重新执行 watcher，相当于又运行 render 函数，又得用到响应式数据的依赖收集**界面更新渲染出来**
将来依赖数据变化，再次派发更新走流程

**_Dep 怎么知道是谁再用我?把函数交给 watcher 去处理_**

当读取一个属性(发生记录依赖)，dep 对象检查全局变量就知道 watcher 在用
当派发更新通知找到用到的 watcher，就重新运行之前的 render 函数重新渲染(watcher 监听 render 函数重新渲染再次收集依赖)
watcher 收到派发更新后，不立即执行，把自己交给调度器(维护一个执行队列),通过 nextTick(Promise 异步)把需要执行的 watcher 放到微队列中

> 面试题：请阐述`vue2`响应式原理

> vue 官方阐述：https://cn.vuejs.org/v2/guide/reactivity.html

**响应式数据的最终目标**，是当对象本身或对象属性发生变化时，将会运行一些函数，最常见的就是 render 函数。

在具体实现上，vue 用到了**几个核心部件**：

1. Observer
2. Dep
3. Watcher
4. Scheduler

## Observer

Observer 要实现的目标非常简单，就是把一个普通的对象转换为响应式的对象

为了实现这一点，Observer 把对象的每个属性通过`Object.defineProperty`转换为带有`getter`和`setter`的属性，这样一来，当访问或设置属性时，`vue`就有机会做一些别的事情。

<img src="http://mdrs.yuanjin.tech/img/20210226153448.png" alt="image-20210226153448807" style="zoom:50%;" />

Observer 是 vue 内部的构造器，我们可以通过 Vue 提供的静态方法`Vue.observable( object )`间接的使用该功能。

在组件生命周期中，这件事发生在`beforeCreate`之后，`created`之前。

具体实现上，它会递归遍历对象的所有属性，以完成深度的属性转换。

**_由于遍历时只能遍历到对象的当前属性_**，因此无法监测到将来动态增加或删除的属性，因此`vue`提供了`$set`和`$delete`两个实例方法，让开发者通过这两个实例方法对已有响应式对象添加或删除属性。

**_对于数组，`vue`会更改它的隐式原型，之所以这样做，是因为 vue 需要监听那些可能改变数组内容的方法_**

<img src="http://mdrs.yuanjin.tech/img/20210226154624.png" alt="image-20210226154624015" style="zoom:50%;" />

总之，Observer 的目标，就是要让一个对象，它属性的读取、赋值，内部数组的变化都要能够被 vue 感知到。

## Dep

这里有两个问题没解决，就是读取属性时要做什么事，而属性变化时要做什么事，这个问题需要依靠 Dep 来解决。

Dep 的含义是`Dependency`，表示依赖的意思。

`Vue`会为响应式对象中的每个属性、对象本身、数组本身创建一个`Dep`实例，每个`Dep`实例都有能力做以下两件事：

- 记录依赖：是谁在用我
- 派发更新：我变了，我要通知那些用到我的人

当读取响应式对象的某个属性时，它会进行依赖收集：有人用到了我

当改变某个属性时，它会派发更新：那些用我的人听好了，我变了

<img src="http://mdrs.yuanjin.tech/img/20210226155852.png" alt="image-20210226155852964" style="zoom:50%;" />

## Watcher

这里又出现一个问题，就是 Dep 如何知道是谁在用我？
要解决这个问题，需要依靠另一个东西，就是 Watcher。
当某个函数执行的过程中，用到了响应式数据，响应式数据是无法知道是哪个函数在用自己的
因此，vue 通过一种巧妙的办法来解决这个问题
我们不要直接执行函数，而是把函数交给一个叫做 watcher 的东西去执行，watcher 是一个对象，每个这样的函数执行时都应该创建一个 watcher，通过 watcher 去执行
window.currentWatcher=this//接下来在执行我
watcher 会设置一个全局变量，让全局变量记录当前负责执行的 watcher 等于自己，然后再去执行函数，在函数的执行过程中，**如果发生了依赖记录`dep.depend()`，那么`Dep`就会把这个全局变量记录下来，表示：有一个 watcher 用到**了我这个属性

当 Dep 进行派发更新时，它会通知之前记录的所有 watcher：我变了

<img src="http://mdrs.yuanjin.tech/img/20210226161404.png" alt="image-20210226161404327" style="zoom:50%;" />

每一个`vue`组件实例，都至少对应一个`watcher`，该`watcher`中记录了该组件的`render`函数。

**`watcher`首先会把`render`函数运行一次以收集依赖，于是那些在 render 中用到的响应式数据就会记录这个 watcher。**

当数据变化时，dep 就会通知该 watcher，而 watcher 将重新运行 render 函数，从而让界面重新渲染同时重新记录当前的依赖。

## Scheduler

现在还剩下最后一个问题，就是 Dep 通知 watcher 之后，如果 watcher 执行重运行对应的函数，就有可能导致函数频繁运行，从而导致效率低下

试想，如果一个交给 watcher 的函数，它里面用到了属性 a、b、c、d，那么 a、b、c、d 属性都会记录依赖，于是下面的代码将触发 4 次更新：

```js
state.a = 'new data';
state.b = 'new data';
state.c = 'new data';
state.d = 'new data';
```

这样显然是不合适的，因此，watcher 收到派发更新的通知后，实际上不是立即执行对应函数，而是把自己交给一个叫调度器的东西

调度器维护一个执行队列，该队列同一个 watcher 仅会存在一次，队列中的 watcher 不是立即执行，它会通过一个叫做`nextTick`的工具方法，把这些需要执行的 watcher 放入到事件循环的微队列中，nextTick 的具体做法是通过`Promise`完成的

> nextTick 通过 `this.$nextTick` 暴露给开发者
>
> nextTick 的具体处理方式见：https://cn.vuejs.org/v2/guide/reactivity.html#%E5%BC%82%E6%AD%A5%E6%9B%B4%E6%96%B0%E9%98%9F%E5%88%97

也就是说，当响应式数据变化时，`render`函数的执行是异步的，并且在微队列中

## 总体流程

![image-20210226163936839](http://mdrs.yuanjin.tech/img/20210226163936.png)

# diff 算法

调用 render 生成虚拟 dom 树得到根节点传入 update 里 watcher 下
update 传入新的 vnode,新 vnode 赋给 this.\_vnode 虚拟节点指向新的树(现虚拟 dom 正确真实 dom 不正确)
搞定真实 dom 进行 diff 比较，把旧的树暂存起来，对比 oldVnode 和新虚拟 dom 对比的目的是为了更新真实 dom

```js
function update(vnode) {
	//vnode:新
	//this._vnode:旧
	var oldVnode = this._vnode;
	this._vnode = vnode;
	//对比的目的：更新真实dom。diff,patch算法
}
```

判断旧树是否存在(可能第一次渲染)

- 没有旧 dom 树，按新 vnode 循环遍历生成真实 dom 挂载(patch 渲染新 dom)。this.**patch**(this.\$el,vnode) //(挂载位置，dom 树)

- 旧树存在，patch 核心根据旧树和新树生成真实 dom

  1. 对比根节点，判断两个节点是不是同一个节点(元素类型相同，key 值相同)
     - 不相同直接递归创建一个新的真实节点 dom 树，原来 dom 直接销毁(vnode.elm.remove())
     - 相同进入更新阶段，原来的 dom 需要重复使用，新节点指向原来真实 dom。对比新旧节点属性，有变化更新到真实 dom 中(类样式，自定义属性等)。旧节点不需要与 dom 断开，旧树用不到过一会垃圾回收机制会回收掉
  2. 对比子节点(深度优先同层比较)两个指针不断向中间靠拢来进行对比，这样做的目的是尽量复用真实 dom，尽量少的销毁和创建真实 dom。如果发现相同，则进入和根节点一样的对比流程，如果发现不同，则移动真实 dom 到合适的位置。
     尽量啥也别做，尽量仅改动元素属性，尽量移动元素，还不行的话，删除和创建元素
     30.42

> 面试题：请阐述 vue 的 diff 算法
>
> 参考回答：
>
> 当组件创建和更新时，vue 均会执行内部的 update 函数，该函数使用 render 函数生成的虚拟 dom 树，将新旧两树进行对比，找到差异点，最终更新到真实 dom
>
> 对比差异的过程叫 diff，vue 在内部通过一个叫 patch 的函数完成该过程
>
> 在对比时，vue 采用深度优先、同层比较的方式进行比对。
>
> 在判断两个节点是否相同时，vue 是通过虚拟节点的 key 和 tag 来进行判断的
>
> 具体来说，首先对根节点进行对比，如果相同则将旧节点关联的真实 dom 的引用挂到新节点上，然后根据需要更新属性到真实 dom，然后再对比其子节点数组；如果不相同，则按照新节点的信息递归创建所有真实 dom，同时挂到对应虚拟节点上，然后移除掉旧的 dom。
>
> 在对比其子节点数组时，vue 对每个子节点数组使用了两个指针，分别指向头尾，然后不断向中间靠拢来进行对比，这样做的目的是尽量复用真实 dom，尽量少的销毁和创建真实 dom。如果发现相同，则进入和根节点一样的对比流程，如果发现不同，则移动真实 dom 到合适的位置。
>
> 这样一直递归的遍历下去，直到整棵树完成对比。

1. `diff`的时机

   当组件创建时，以及依赖的属性或数据变化时，会运行一个函数，该函数会做两件事：

   - 运行`_render`生成一棵新的虚拟 dom 树（vnode tree）
   - 运行`_update`，传入虚拟 dom 树的根节点，对新旧两棵树进行对比，最终完成对真实 dom 的更新

   核心代码如下：

   ```js
   // vue构造函数
   function Vue() {
   	// ... 其他代码
   	var updateComponent = () => {
   		this._update(this._render());
   	};
   	new Watcher(updateComponent);
   	// ... 其他代码
   }
   ```

   `diff`就发生在`_update`函数的运行过程中

2. `_update`函数在干什么

   `_update`函数接收到一个`vnode`参数，这就是**新**生成的虚拟 dom 树

   同时，`_update`函数通过当前组件的`_vnode`属性，拿到**旧**的虚拟 dom 树

   `_update`函数首先会给组件的`_vnode`属性重新赋值，让它指向新树

   <img src="http://mdrs.yuanjin.tech/img/20210301193804.png" alt="image-20210301193804498" style="zoom:50%;" />

   然后会判断旧树是否存在：

   - 不存在：说明这是第一次加载组件，于是通过内部的`patch`函数，直接遍历新树，为每个节点生成真实 DOM，挂载到每个节点的`elm`属性上

     <img src="http://mdrs.yuanjin.tech/img/20210301194237.png" alt="image-20210301194237825" style="zoom:43%;" />

   - 存在：说明之前已经渲染过该组件，于是通过内部的`patch`函数，对新旧两棵树进行对比，以达到下面两个目标：

     - 完成对所有真实 dom 的最小化处理
     - 让新树的节点对应合适的真实 dom

     <img src="http://mdrs.yuanjin.tech/img/20210301195003.png" alt="image-20210301195003696" style="zoom:50%;" />

3. `patch`函数的对比流程

   **术语解释**：

   1. 「**相同**」：是指两个虚拟节点的标签类型、`key`值均相同，但`input`元素还要看`type`属性
   2. 「**新建元素**」：是指根据一个虚拟节点提供的信息，创建一个真实 dom 元素，同时挂载到虚拟节点的`elm`属性上
   3. 「**销毁元素**」：是指：`vnode.elm.remove()`
   4. 「**更新**」：是指对两个虚拟节点进行对比更新，它**仅发生**在两个虚拟节点「相同」的情况下。具体过程稍后描述。
   5. 「**对比子节点**」：是指对两个虚拟节点的子节点进行对比，具体过程稍后描述

   **详细流程：**

   1. **根节点比较**

      <img src="http://mdrs.yuanjin.tech/img/20210301203350.png" alt="image-20210301203350246" style="zoom:50%;" />

      `patch`函数首先对根节点进行比较

      如果两个节点：

      - 「相同」，进入**「更新」流程**

        1. 将旧节点的真实 dom 赋值到新节点：`newVnode.elm = oldVnode.elm`

        2. 对比新节点和旧节点的属性，有变化的更新到真实 dom 中
        3. 当前两个节点处理完毕，开始**「对比子节点」**

      - 不「相同」

        1. 新节点**递归**「新建元素」
        2. 旧节点「销毁元素」

   2. **「对比子节点」**

      在「对比子节点」时，vue 一切的出发点，都是为了：

      - 尽量啥也别做
      - 不行的话，尽量仅改动元素属性
      - 还不行的话，尽量移动元素，而不是删除和创建元素
      - 还不行的话，删除和创建元素

# 生命周期函数

> 面试题：`new Vue`之后，发生了什么？数据改变后，又发生了什么？

设置私有属性到实例中，
beforeCreate，
注入流程用 observe 变成响应式，Object.defineProperty 挂载实例
created(可以拿到各种响应式数据，实例中拿到方法。异步处理前置事情)
拿到 render 函数(vue-cli 工程不用做自动生成 render)，针对于模板字符串 script 导入 vue 编译成 render
beforeMount
创建一个 Watcher，监测 updateComponent 函数，其中包含 render 的虚拟节点 vnode 传给 update 函数进行 diff 算法比较

```js
var updateComponent = () => {
	this._update(this._render());
};
new Watcher(updateComponent);
```

在执行 render 函数中，会搜集依赖，依赖变化会重新运行 updateComponent 函数

在执行 update 函数中接受 vnode 参数，触发 patch 函数对比，
没有旧树，以新树的**每一个普通节点**生成真实 dom
如果遇到创建组件的 vnode，new Vue(vnode.componentOptions)传入配置创建组件
则会进入组件实例化流程(和创建 vue 实例流程基本相同)，最终把创建好的组件实例挂载在 vnode 的 componentInstance[指向新组件] 属性中(复用)
mounted(可以拿到 ref,真实 dom)
重新渲染?改变 data 数据变化，updateComponent 有变化通知 watcher
watcher 会被调度器放到 nextTick 中运行，微队列避免多次执行
beforeUpdate
updateComponent 函数重新执行，丢掉以前依赖，重新收集所有依赖(依赖变化重新 updateComponent)
执行 update 函数触发 patch 函数
新旧两棵树对比，\_vnode 指向新树
再 diff 流程更新 dom 和组件(创建，删除，移动，更新)
新组件创建，再次实例化流程
旧组件删除，调用旧组件的$destroy方法删除组件(该方法会先触发beforeDestroy,然后递归调用子组件的$destroy 方法，触发 destroyed)
组件更新，又相当于组件的 updateComponent 函数被重新触发，又进入重新渲染
updated

> 例：render:(h)=>h(App)

vue 实例中 render 渲染虚拟节点(组件)
render 中传入 componentOptions 组件配置(属性，事件监听函数等)创建虚拟节点 vnode(新组件)
像 vnode 里面添加 componentInstance(组件实例)指向新组件
组件中夹杂其他组件即渲染对应流程
<img src="http://mdrs.yuanjin.tech/img/20210302155735.png" alt="image-20210302155735758" style="zoom: 33%;" />

![image-20210226163936839](http://mdrs.yuanjin.tech/img/20210226163936.png)

1. 创建 vue 实例和创建组件的流程基本一致

   1. 首先做一些初始化的操作，主要是设置一些私有属性到实例中

   2. **运行生命周期钩子函数`beforeCreate`**

   3. 进入注入流程变成响应式：**处理属性、computed、methods、data、provide、inject**，最后使用代理模式将它们挂载到实例中

   4. **运行生命周期钩子函数`created`**

   5. 生成`render`函数：如果有配置，直接使用配置的`render`，如果没有，使用运行时编译器，把模板编译为`render`

   6. **运行生命周期钩子函数`beforeMount`**

   7. 创建一个`Watcher`，传入一个函数`updateComponent`，该函数会运行`render`，把得到的`vnode`再传入`_update`函数执行。

      在执行`render`函数的过程 中，会收集所有依赖，将来依赖变化时会重新运行`updateComponent`函数

      在执行`_update`函数的过程中，触发`patch`函数，由于目前没有旧树，因此直接为当前的虚拟 dom 树的每一个普通节点生成 elm 属性，即真实 dom。

      如果遇到创建一个组件的 vnode，则会进入组件实例化流程，该流程和创建 vue 实例流程基本相同，最终会把创建好的组件实例挂载 vnode 的`componentInstance`属性中，以便复用。

   8. **运行生命周期钩子函数`mounted`**

2. 重渲染？

   1. 数据变化后，所有依赖该数据的`Watcher`均会重新运行，这里仅考虑`updateComponent`函数对应的`Watcher`

   2. `Watcher`会被调度器放到`nextTick`中运行，也就是微队列中，这样是为了避免多个依赖的数据同时改变后被多次执行

   3. **运行生命周期钩子函数`beforeUpdate`**

   4. `updateComponent`函数重新执行

      在执行`render`函数的过程中，会去掉之前的依赖，重新收集所有依赖，将来依赖变化时会重新运行`updateComponent`函数

      在执行`_update`函数的过程中，触发`patch`函数。

      新旧两棵树进行对比。

      普通`html`节点的对比会导致真实节点被创建、删除、移动、更新

      组件节点的对比会导致组件被创建、删除、移动、更新

      当新组件需要创建时，进入实例化流程

      当旧组件需要删除时，会调用旧组件的`$destroy`方法删除组件，该方法会先触发**生命周期钩子函数`beforeDestroy`**，然后递归调用子组件的`$destroy`方法，然后触发**生命周期钩子函数`destroyed`**

      当组件属性更新时，相当于组件的`updateComponent`函数被重新触发执行，进入重渲染流程，和本节相同。

   5. **运行生命周期钩子函数`updated`**

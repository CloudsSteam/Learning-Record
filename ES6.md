# ES6 课程概述

1. ECMAScript JavaScript NodeJs 它们区别是什么?
   ECMAScript:简称 ES,是一个语言标准(循环，判断，变量，数组等数据方式)

JavaScript :运行在浏览器的语言 ，该语言使用 ES 标准。ES+ wb api =JavaScript

NodeJs: 运行在服务器段的语言，该语言使用 ES 标准。 ES+node api =JavaScript

无论 JavaScript 还是 nodejs，他们都是 ES 的超集(super set)

2. ECMAScript 有哪些版本

ES3.0: 1999
ES5.0: 2009
ES6.0: 2015,从该版本开始，不再使用数字作为编号而是使用年份
ES7.0：2016

3. 为什么 ES6 如此重要?
   ES6 解决 JS 无法开发大型应用的语言层面的问题。

4. 如何应对兼容性问题?
   有工具

# 块级绑定

## 声明变量的问题

使用 var 声明变量

1. 允许重复的变量声明：导致数据被覆盖
2. 变量提升：怪异数据访问，闭包问题
3. 全局变量挂载到全局对象：全局对象成员污染问题

var 允许重复的变量声明：会覆盖同一个变量

- 变量提升：怪异的数据访问，未定义就使用，
- 闭包问题(定义的量会提升，)
  调用还是外部数据(解决方法立即执行函数)

```
(function(i){
   btn.onclick=function(){
     console.log(i)
   }
 })(i)
```

## 使用 let 声明变量

ES6 不仅引入 let 关键字用于解决变量声明的问题，同时引入块级作用域的概念

> 块级作用域：代码执行时遇到花括号，会创建一个块级作用域，花括号结束块级作用域销毁(里面可以用外面，外面不能用里面)

声明变量的问题

1. 全局变量挂载到全局对象：全局对象成员污染问题
   let 声明的变量不会挂载到全局对象
2. 允许重复的变量声明：导致数据被覆盖
   let 声明的变量，不允许当前作用域范围内重复声明
3. 变量提升：怪异的数据访问，闭包问题
   使用 let 不会有变量提升，因此不能在定义 let 变量之前使用它

底层实现上，let 声明的变量实际上也会有提升，但是，提升后会将其放入到"暂时性死区"，如果访问变量位于暂时性死区，会报错。当代码运行到该变量的声明语句时，会将其从暂时性死区中移除

在循环中，用 let 声明的循环变量，会特殊处理，每次进入循环体，都会开启一个新的作用域，并且将循环遍历绑定到该作用域(每次循环，使用的是一个全选的循环变量)

在循环中使用的 let 声明的循环变量，在循环结束后会销毁

## 使用 const 声明变量

const 和 let 完全相同，仅在于用 const 声明的变量，必须在声明时赋值，而且不可以重新赋值。
实际上在开发中，应该尽量使用 const 来声明变量，以保证变量的值不会随意篡改
原因如下：

1. 根据开发经验，开发中的很多变量，都是不会更改，也不应该更改。
2. 后续的很多框架都是第三方 js 库，都要求数据不可变，使用常量可以一定程度上保证这一点

注意的细节：

1. 常量不可变，是指声明的常量的内存空间不可变，并不保证内存空间中的地址指向的其他空间不可变.例 const main={}内部可变只是指向不变
2. 常量的命名
   1. 特殊的常量：该常量从字面意义上，一定是不可变的，比如圆周率，月底距地或其他一些绝不可能变化的配置。通常该常量的名称全部使用大写，多个单词之间用下划线分割
   2. 普通的变量：使用和之前一样的命名即可
3. for 循环中不可用 const 的值 for in 循环可以改变

# 字符串和正则表达式

## 更好的 Unicode 支持

早期由于存储空间宝贵，unicode 使用 16 位二进制来存储文字，我们将一个 16 位的二进制叫做码元(code Unit)

后来由于技术的发展，Unicode 对文字编码进行了扩展，将某些文字扩展到了 32 位(占用两个码元),并且，将某个文字对应的二进制数字叫做码点(Code Point )

js 根据码元(字节)来取长度
现 ES6 为解决困扰，为字符串提供了方法：codePointAt
text.codePointAt(0),会表示码点，
text.codePointAt(1),会表示后面码元

//得到一个字符串码点真实长度

```
//判断是否为汉字
function is32bit(char){
   //如果码点大于了16位二进制的最大值，则其是32位的，判断是否为汉字
   return char.codePointAt(0)>0xffff;
}
//得到一个字符串码点真实长度
function getLengthOFCodePoint(str){
   var len=0;
   for (let i =0;i<str.length;i++){
      if(is32bit(str,i)){
         //当前字符串在i这个位置，占用了两个码元
         i++;
      }
      len++
   }
   return len;
}
console.log("判断字符串码点的长度"，getLengthOfCodePoint("oWWwg我是2"))
```

同时,ES6 为正则表达式添加了一个 (flag:)u 就使用码点(字节)匹配,(例如正则 g)

## 更多的字符串 API

字符串实例原型方法

- includes
  判断字符串中是否包含指定的字符串
  第二个参数可传指定下标开始查找

- startsWith
  是否以指定字符串开头
  第二个参数可传指定下标开始查找
- endsWith
  是否以指定字符串结尾
  第二个参数可传指定下标开始查找
- repeat
  将字符串重复指定的次数，然后返回一个新字符串 text.repeat(4)重复 4 次

## 正则中的粘连标记

标记名：y
含义：匹配时完全按照正则对象中的 lastIndex 位置开始匹配，并且匹配的位置必须在 lastIndex 位置

加了 y 就是以开头开始匹配，也可以改变 reg.lastIndex 从而开始匹配

## 模板字符串

ES6 之前处理字符串繁琐的两个方面

1. 多行字符串
2. 字符串拼接

在 ES6 中，提供了模板字符串的书写，可以非常方便的换行和拼接，要做的，仅仅是将开头或结尾改为`符号 ` `里头样式都会输出

\${}里面可以是任何有意义的数据
表达式是可以嵌套的

## 模板字符串标记

```
var love1 = "秋葵";
var love2 =  "香菜";
var text = myTag`邓哥喜欢${love1}，邓哥也喜欢${love2}。`;
//相当于
text= myTag(["邓哥喜欢","邓哥也喜欢","。"],"秋葵","香菜");
Arguments第一个参数就是myTag的数组

除Arguments之外可const rest= Array.prototype.slice.apply(arguments).slice(1);
function myTag(parts,arg1,arg2){
   console.log(parts)
   console.log(arg1)
   console.log(arg2)
  // part.length= rest.length+1
}

```

String.raw'abc\t\bac'; //api 表示忽略转义字符

//特殊处理用户输入标签

```
container.innerHTML=safe`<p>${txt.value}</p>`;

function safe(parts){
   const values=Array.prototype.slice.apply(arguments).slice(1);
   let str ="";
   for (let i=0;i<values.length;i++){
      const v=values[i].replace(/</g,"&lt;").replace(/>/g,"&gt;");
      str +=parts[i]+v;
      if(i===values.length-1){
         str+=parts[i+1];
      }
   }
   return str;
}

```

# 函数

## 参数默认值

在书写形参时，直接给形参赋值，赋的值即为默认值

这样一来，当调用函数时，如果没有给对应的参数赋值(就为 undefined)则会自动使用默认值

### 扩展对 arguments 的影响

严格模式？
只要给函数加上参数默认值，该函数会自动变量严格模式下的规则：arguments 和形参脱离

### 留意暂时性死区

形参和 ES6 中的 let 和 const 声明一样具有作用域，并且根据参数的声明顺序，存在暂时性死区

## 剩余参数

写函数就是让调用的时候爽舒服
arguments 的缺陷:

1. 如果和形参配合使用，容易导致混乱
2. 从语义上，使用 arguments 获取参数，由于形参缺失，无法从函数定义上理解函数的真实意图

ES6 的剩余参数专门用于手机末尾的所有参数，将其放置到一个形参数组中。
function sum(...args){
//args 收集了所有参数，形成的一个数组
}

1. 一个函数，仅能出现一个剩余参数
2. 剩余参数必须是最后一个形参

## 展开运算符 ES6

也是三个点...要展开的东西
和剩余函数一样，只不过剩余参数用到形参指收集剩余参数
[]{}表新数组或对象

## 展开对象 ES7

浅克隆
展开对象中有对象 obj1.address{}对象
方法操作
obj2={
...obj1,
address:{
...obj1.address
}
}
深克隆需在里面重新创建对象或数组

### 剩余参数和运算符展开

//curry:柯里化,用户固定某个函数的前面的参数，得到一个新的函数，函数调用时，接受剩余的参数

## 明确函数的双重用途

ES6 提供特殊 API 可以在该 ap 内部，判断是否使用的 new 来调用

> new.target
> 得到的是：如果没有使用 new 来调用函数，则返回 undefined
> 如果使用 new 调用函数，则得到的是 new 关键字后面的函数本身

## 箭头函数

回顾：this 指向

1. 通过对象调用函数，this 指向对象
2. 直接调用函数，this 指向全局对象
3. 如果通过 new 调用函数，this 指向新创建的对象
4. 如果通过 apply,call， bind 调用函数，this 指向指定的数据
5. 如果是 DOM 事件函数，this 指向事件源

箭头函数是函数表达式，理论上任何使用函数表达式的场景都可以使用箭头函数

解决闭包问题，或 this 指向
完整语法

```
(参数1，参数2，...)=>{
   //函数体
}
```

如果参数只有一个，可以省略小括号
如果箭头函数只有一条返回语句，可以省略大括号，和 return 关键字

```
const numbers=[3,7,78,3,5,345];
const result=numbers.filter(num=>num%2!==0)
         .map(num=>num*2).reduce((a,b)=>a+b)
console.log(result);
```

### 注意细节

- 箭头函数的函数体中的 this，取决于箭头函数定义的位置的 this 指向，而与如何调用无关
- 箭头函数中，不存在 this,arguments,new.target,如果使用了，则使用的是函数外层的对应的 this,arguments,new.target
- 箭头函数没有原型
- 箭头函数不能作为构造函数使用
- 对象的属性不用箭头函数

### 应用场景

1. 临时性使用的函数，并不会可以可以调用它，比如：
   1. 事件处理函数
   2. 异步处理函数
   3. 其他临时性的函数
2. 为绑定外层 this 函数
3. 在不影响其他代码的情况下，保持代码的简洁，最常用的，数组方法中的回调函数

# 对象

## 新增对象字面量语法

1. 成员速写
   如果对象字面量初始化时，成员的名称来自于一个变量，并且和变量的名称相同，则可以进行简写
2. 方法速写
   对象字面初始化时，方法可以省略冒号和 function 关键字
3. 计算属性名
   有的时候，初始化对象时，某些属性名可能来自某个表达式的值，在 ES6，可以使用中括号来表示该属性名是通过计算得到的

## Object 的新增 API

1. Object.is
   用于判断两个数据是否相等，基本上更严格相等(===)是一致的，除了以下两点：
   NaN 和 NaN 相等
   +0 和-0 不相等

2. Object.assign
   将 obj2 的数据，覆盖到 obj1，并且回对 obj1 产生改动，然后返回 obj1
   const obj =Object.assign(obj1,obj2);

3. Object.getOwnPropertyNames 的枚举顺序
   Object.getOwnPropertyNames 方法之前就存在，只不过官方没有明确要求，对属性的顺序如何排序,如何排序，完全由浏览器厂商决定。
   ES6 规定了该方法返回的数组的排序方式如下：

- 先排数字，并安装升序排序
- 再排其他，按照书写顺序排序

4. Object.setPrototypeOf
   该函数用于设置某个对象的隐式原型

比如 Object.setPrototypeOf(obj1,obj2),
相当于：`obj1.__proto__=obj2`

## 面向对象简介

面向对象：一种编程思想，跟具体的语言

对比面向过程：

- 面向过程：思考的切入点是功能的步骤
- 面向对象：思考的切入点是对象的划分

## 类:构造函数的语法糖

面向对象中，将下面对一个对象的所有成员的定义，统称为类

### 传统的构造函数的问题

```
class Animal{
   constructor(type,name,age,sex){
      this.type=type;
      this.name=name;
      this.age=age;
      this.sex=sex;
   }
   print(){
      console.log(`[种类]:${this.type`);
      console.log(`[名字]:${this.name`);
      console.log(`[年龄]:${this.age`);
      console.log(`[性别]:${this.sex`);
   }
}
const a=new Animal("狗","旺财","3","男")
```

1. 属性和原型方法定义分离，降低了可读性
2. 原型成员可以被枚举
3. 默认情况下，构造函数仍然可以被当作普通函数使用

### 类的特点

1. 类声明不会被提升，与 let 和 const 一样，存在暂时性死区
2. 类中所有代码均在严格模式下执行
3. 类的所有方法都是不可枚举的
4. 类的所有方法内部都无法被当作构造函数使用
5. 类的构造器，必须使用 new 来调用

## 类的其他书写方式

1. 可计算的成员名

2. getter 和 setter
   Object.defineProperty 可定义某个对象成员属性的读取和设置
   使用 getter 和 setter 控制的属性，不在原型上
3. 静态成员
   构造函数本身的成员
   使用 static 关键字定义的成员即静态成员

4. 字段初始化器(ES7)
   使用 static 的字段初始化器，添加的是静态成员
   没有使用 static 的字段初始化器，添加的成员位于对象上
   箭头函数指向当前对象
5. 类表达式
6. [扩展]装饰器(ES7)(Decorator)

## 类的继承

```
function Dog(name,age,sex){
   //借用父类的构造函数
   Animal.call(this,"犬类",name,age,sex);
}
Object.setPrototypeOf(Dog.prototype,Animal.prototype);
```

```
class Dog extends Animal{
   constructor(name,age,sex){
      super("犬类",name,age,sex)
   }
}
```

如果两个类 A 和 B，如果可以描述为：B 是 A，则，A 和 B 形成继承关系
如果 B 是 A，则：

1. B 继承自 A
2. A 派生 B
3. B 是 A 的子类
4. A 是 B 的父类

如果 A 是 B 的父类，则 B 会自动拥有 A 中所有实例成员

新的关键字：

- extends：继承，用于类的定义
- super
  - 直接当作函数调用，表示父类构造函数

注意：ES6 要求，如果定义了 constructor，并且该类是子类，则必须在 constructor 的第一行手动调用父类的构造函数

如果子类不写 constructor，则会有默认的构造器，该构造器需要的参数和父类一致，并且自动调用父类构造器

[ 冷知识]

- 用 js 制作抽象类
  - 抽象类：一般是父类，不能通过该类创建对象
- 正常情况下，this 的指向，this 始终指向具体的类的对象

# 解构

## 对象结构

let name,age,sex,address;
({name,age,sex,address}=user);
或
let{name,age,sex,address}=user //先定义 4 个变量，然后从对象中读取同名属性，放到变量中

### 什么是结构

使用 ES6 的一种语法规则，讲一个对象或数组的某个属性提取到某个变量中

### 在结构中使用默认值

```
{同名变量=默认值}
```

### 非同名属性结构

：

## 数组结构

## 参数结构

# 符号

## 普通符号

符号是 ES6 新增的一个数据类型，它通过使用函数`symbol符号名`来创建
const syb1 =Symbol();
const syb2 =Symbol("abc");
符号设计的初衷，是为了给对象设置私有属性

符号具有以下特点：

- 没用字面量
- 使用 typeof 得到的类型是 symbol
- **每次调用 Symbol 函数得到的符号永远不相等，无论符号名是否相同**
- 符号可以昨晚对象的属性名存在，这种属性称之为符号属性
  - 开发者可以通过精心的设计，让这些属性无法通过常规方式被外界访问
  - 符号属性是不能枚举的，因此在 for-in 循环中无法读取到符号属性，Object.keys 方法也无法读取到符号属性
  - Object.getOwnPropertyNames 尽管可以得到所有无法枚举的属性，但是仍然无法读取到符号属性
  - Es6 新增 object.getOwnPropertySymbols 方法，可以读取符号
- 符号无法被隐式转化，因此不能被用于数学运算，字符串拼接或其他隐式转化的场景，但符号可以以显式的转化为字符串，通过 String 构造函数进行转化即可，console.log 之所以可以输出符号，是它在内部进行了显式转换

## 共享符号

根据某个符号名称(符号描述)能够得到同一个符号

```
Symbol.for("符号名/符号描述") //获取共享符号
```

## 知名(公共，具名)符号

知名符号是一些具有特殊含义的共享符号，通过 Symbol 的静态属性得到
Es6 延续了 ES5 的思想：减少魔法，暴露内部实现！
因此，ES6 用知名符号暴露了某些场景的内部实现

1. Symbol.hasInstance
   该符号用于定义构造函数的静态成员，它将影响 instanceof 的判定

```
obj instanceof A
//等效于
A[Symbol.hasInstance](obj)
```

2. [扩展]Symbol.isConcatSpreadable
   该知名符号会影响数组的 concat 方法
3. [扩展]Symbol.toPrimitive
   该知名符号会影响类型转换的结果
4. [扩展]Symbol.toStringTag
   该知名符号会影响 Object.prototype.toString 的返回值
5. 其他知名符号

# 异步处理

异步一定放在事件队列中

## 事件循环

JS 运行的环境称之为宿主环境。
执行栈：call stack 一个数据结构，用于存放各种函数的执行环境，每一个函数执行之前他的相关信息会加入到执行栈。函数调用之前，创建执行环境，然后加入到执行栈；函数调用之后，销毁执行环境

JS 引擎永远执行的是执行栈的最顶部。

异步函数：某些函数不好立即执行，需要等到某个时机到达后才会执行，这样的函数称之为异步函数。比如时间处理函数。异步函数的执行时机，会被宿主环境控制。

浏览器宿主环境中包含 5 个线程

1. JS 引擎：负责执行执行栈的最顶部代码
2. GUI 线程：负责渲染页面
3. 事件监听线程：负责监听各种事件
4. 计时线程：负责计时
5. 网络线程：负责网络通信

异步函数要进入事件队列

当上面的线程发生了某些事情，如果该线程发现，这件事情有处理程序，它会将该处理程序加入一个叫做事件队列的内存。当 js 引擎发现，执行栈中已经没有了任何内容后，会将事件队列中的第一个函数加入到执行栈中执行。

JS 引擎对事件队列的取出执行方式，以及与宿主环境的配合，称之为事件循环

事件队列在不同的宿主环境中有所差异，大部分宿主环境的配合，称之为事件循环

事件队列在不同的宿主环境中有所差异，大部分宿主环境会将事件队列进行细分。在浏览器中，事件队列分为两种：

- 宏任务(队列)：macroTask,计时器结束的回调，事件回调，http 回调等等绝大部分异步函数进入宏队列
  - setTimeout 的回调
  - setInterval 的回调
  - 事件处理函数
- 微任务 (队列)：MutationObserver ,Promise 产生的回调进入微队列
  > MutationObserver 用于监听某个 DOM 对象的变化
  - Promise 的 then 函数会回调
  - requestAnimationFrame 的回调

const observer=new MutationObserver(()=>{
//当监听的 dom 元素发生变化时运行的回调函数
console.log()
})

> 当执行栈清空时，JS 引擎首先会将微任务中的所有任务依次执行结束，如果没有微任务，则执行宏任务

## Promise 基础

一层层回调嵌套，形成回调地狱 callback hell
Promise 出马

### Promise 规范

一套专门处理异步场景的规范，它能有效避免回调地狱的产生，使异步代码更加清晰，简洁，统一
Promise(承诺)

1. 所有的异步场景，都可以看作是一个异步任务，每个异步任务，在 js 中应该表现为一个对象，该对象称之为 Promise 对象，也叫做任务对象

2. 每个任务对象，都应该有**两个阶段，三个状态**

- 未决阶段 unsettled

  - 挂起状态 pending

- 已决阶段 settled
  - 完成状态 fulfilled
  - 失败状态 rejected

以下逻辑：

> 任务总是从未决阶段变到已决阶段，无法逆行
> 任务总是从挂起状态到完成或失败状态，无法逆行
> 时间不能倒流，历史不可改写，任务一旦完成或失败，状态就固定下来，永远无法改变

3. 挂起到完成，resolve 过程完成状态；挂起到失败称之为 reject。
   任务完成就有一个相关数据 data，任务失败可能有失败原因 reason

4. 可以针对任务进行后续处理.针对完成状态后续处理称为 onFulfilled(data).针对失败后续处理称之为 onRejected(reason)

const pro =new Promise((resolve,reject)=>{
//立即执行,执行过程描述任务
成功调第一个参数，失败调第二个
})

pro.then(data=>{},reason=>{})  
//then 方法表示然后呢
//第一个参数成功之后干啥，第二个失败干啥

## Promise 的链式调用

### catch 方法

.catch(onRejected)=.then(null,onRejected)
针对错误

### 链式调用

28.00

1. then 方法必定会返回一个新的 promise
   可理解为后续处理也是一个任务
2. 新任务的状态取决于后续处理：
   - 若没有相关的后续处理，新任务的状态和前任务一致，数据为前任务的数据
   - 若有后续处理但还未执行，新任务挂起
   - 若后续处理执行了，则根据后续处理的情况确定新任务的状态
     - 后续处理执行无错，新任务的状态为完成，数据未后续处理的返回值
     - 后续处理执行有错，新任务的状态为失败，数据为异常对象
     - 后续执行后返回的是一个任务对象，新任务的状态与数据与该任务对象一致

由于链式任务的存在，异步代码拥有了更强的表达力

```
//任务成功后，执行1失败执行2
pro.then(处理1).catch(处理2)
//任务成功，依次处理1，2
pro.then(处理1).then(处理2)
//任务成功后，依次执行处理1，2 若任务失败或前面的处理有错执行处理3
pro.then(处理1).then(处理2).catch(处理3)
```

### 3.邓哥处理

56.40

## Promise 静态方法

- Promise.resolve(data) //直接返回一个完成状态的任务
- Promise.reject(reason) //直接返回一个拒绝状态的任务
- Promise.all(任务数组) //返回一个任务，任务数组全成功则成功，任何一个失败则失败
- Promise.any(任务数组) //返回一个任务，任务数组任一成功则成功，全部失败才失败
- Promise.allSettled(任务数组) //返回一个任务，任务数组全部已解决成功，该任务会不会失败
- Promise.race(任务数组) //返回一个任务，任务数组，任务数组一已决，状态和其一致

## async 和 await

有 Promise 异步任务就有了一种统一的处理方式
ES7 推出两个关键字 async 和 await,更加优雅表达 Promise

### async

被修饰的函数一定返回 Promise

### await

await 表某个 promise 完成，必须用于 async 函数中

29.44 练习题

## 手写 Promise

# Fetch Api

## Fetch Api 概述

**XMLHttpRequest 的问题**

1. 所有的功能全部集中在同一个对象上，容易书写出混乱不宜维护的代码
2. 采用传统的事件驱动模式，无法适配新的 Promise Api

**Fetch Api 的特点**

1. 并非取代 AJAX，而是对 AJAX 传统 API 的改进
2. 精细的功能分割：头部信息，请求信息，响应信息等均匀分布到不同的对象，更利于处理各种复杂的 Ajax 场景
3. 使用 Promise Api 更利于异步代码的书写
4. Fetch Api 并非 ES6 的内容，属于 HTML5 新增的 Web Api
5. 需要掌握网络通信知识

## Fetch Api 基本使用

### 参数

该函数又两个参数

1. 必填，字符串，请求地址
2. 选填， 对象，请求配置

**请求配置对象**

- method:字符串，请求方法，默认 GET
- headers：对象，请求头信息(配置请求头格式"Content-Type":"application/json")
- body： 请求体的内容，必须匹配请求头中的 Content-Type
- mode：字符串，请求模式
  - cors:默认值，配置为该值，会在请求头中加入 origin 和 referer
  - no-cors：配置为该值，不会在请求头中加入 origin 和 referer，跨域的时候可能会出现问题
  - same-origin:指示请求必须在同一个域中发生，如果请求其他域，则会报错
- credentials:如何携带凭据 cookie
  - omit：默认值，不携带 cookie
  - same-origin：请求同源地址时携带 cookie
  - include：请求任何地址都携带 cookie
- cache：配置缓存模式
  - default：表示 fetch 请求之后将检查下 http 的缓存
  - no-store：表示 fetch 请求将完全忽略 http 缓存的存在。这意味着请求之前将不再检查下 http 的缓存，拿到响应后，它也不会更新 http 缓存
  - no-cache：如果存在缓存，那么 fetch 将发送一个条件查询 request 和一个正常的 request，拿到响应后，它会更新 http 缓存
  - reload：表示 fetch 请求之前将忽略 http 缓存的存在，但是请求拿到响应后，他将自动更新 http 缓存
  - force-cache：表示 fetch 请求不顾一切的依赖缓存，即使缓存过期了它依然从缓存中读取，除非没有任何缓存，那么它将发送一个正常的 request。
  - only-if-cached:表示 fetch 请求不顾一切的依赖缓存，及时缓存过期了，它依然从缓存中读取，如果没有缓存，它将抛出网络错误(该设置只在 mode 为 same-orgin 有效)

### 返回值

- 当收到服务器的返回结果后，Promise 进入 resolved 状态，状态数据为 Response 对象
- 当网络发生错误(或其他导致无法完成交互的错误)时，Promise 进入 rejected 状态，状态数据为错误信息

fetch(url,config).then(resp=>{
console.log(resp)
}).catch(err=>{
console.log(err)
})

**Response 对象**

- ok：boolean，当响应消息码在 200~299 之间时为 true，其他为 false
- status：number,响应的状态码
- text():用于处理文本格式的 Ajax 响应，它从响应中获取文本流，将其读完，然后返回一个被解决为 string 对象的 Promise。
- blob()：用于处理二进制文件格式(比如图片或者电子表格)的 Ajax 响应，它读取文件的原始数据，一旦读取完整个文件，就返回一个被解决为 blob 对象的 Promise
- json()：用于处理 JSON 格式的 Ajax 响应，它将创建一个新的 Promise，已解决来自重定向的 URL 的响应

### Request 对象

除了使用基本的 fetch 方法，还可以通过创建一个 Request 对象来完成请求(实际上，fetch 的内部会帮你创建一个 Request 对象)

```
new Request(url地址，配置)
```

注意点：尽量保证每次请求都是一个新的 Request 对象

### Response 对象

### Headers 对象

- has(key):检查请求头中是否存在指定 key 值
- get(key):得到请求头中对应的 key 值
- set(key,value):修改对应的键值对
- append(key,value):添加对应的键值对
- keys():得到所有请求头键的集合
- values()：得到所有的请求头中的值的集合
- entries():得到所有请求头的键值对的集合

# 迭代器和生成器

## 迭代器

1. 什么是迭代?
   从一个数据集合中按照一定顺序，不断取出数据的过程
2. 迭代和遍历的区别?
   迭代强调的是依次取数据，并不保证取多少，也不保证把所有的数据取完
   遍历强调的是要把整个数据依次全部取出
3. 迭代器
   对迭代过程的封装，在不同的语言下有不同的表现形式，通常为对象
4. 迭代模式
   一种设计模式，用于统一迭代过程，并规范了迭代器规格：

- 迭代器应该具有的到下一个数据的能力
- 迭代器应该具有判断是否还有后续数据的能力

```
<script>
   const arr=[1,2,3,4,5];
   //迭代器创建函数

   function createIterator(arr){
      let i=0;//当前数组下标
      return{
         next(){
           var result ={
               value:arr[i],
               done:i>=arr.length
           }
            i++;
            return result;
         }
      }
   }

   const iterator ={
     i:0,
      next(){
         var result={
            value:arr[this.i],
            done:this.i>=arr.length
         }
         this.i++;
         return result;
      }
   }

   console.log(iterator.next());
</script>
```

## 可迭代协议与 for-of 循环

### 可迭代协议

**概念回顾**

- 迭代器(iterator):一个具有 next 方法的对象，next 方法返回下一个数据并且能指示是否迭代完成
- 迭代器创建函数(iterator creator):一个返回迭代器的函数

**可迭代协议**
ES6 规定，如果一个对象具有知名符号属性`Symbol.iterator`,并且属性值是一个迭代器创建函数，则该对象是可迭代的(iterable)
const iterator = arr[Symbol.iterator]()

数组属性 Symbol.iterator 表示可迭代

> 思考:如何知晓一个对象是否可迭代的?
> 思考:如何遍历一个可迭代对象?

```
const arr =[5,3,5,6,1,9];

const iterator =arr[Sybol.iterator](); //相当于这里代码
let result=iterator.next();
while(!result.done){
   const item=result.value;//取出数据
   console.log(item);
   //下一次迭代
   result=iterator.next();
}
```

### for-of 循环

语法糖
for-of 循环用于遍历可迭代对象，格式如下

```
//迭代完成后循环结束
for(const item in iterable){  //相当于上面代码
   //iterable:可迭代对象
   //item：每次迭代得到的数据

}
```

自己造一个可迭代对象

```
var obj={
   a:1,
   b:2,
   [Symbol.iterator](){
      const keys=Object.keys(this);
      //console.log(keys);
      let i=0;
      return {
         next()=>{
            const propName =keys[i];
            const propValue=this[propName];
            const result ={
                  value:{
                     propName,
                     propValue
                  },
                  done:i>=keys.length
            }
         }
      }
   }
}

for (const item of obj){
   console.log(item);   //{propName:"a",propValue:1}
}
```

### 展开运算符与可迭代对象

展开运算符可以作用于可迭代对象，这样就可以轻松的将可迭代对象转化为数组

## 生成器(Generator)

1. 什么是生成器
   初衷是为了简便书写迭代器函数，后发现有别用处对 React 重要

生成器是一个通过构造函数 Generator 创建的对象，生成器既是一个迭代器，同时又是一个可迭代对象

2. 如何创建生成器?

生成器的创建，必须使用生成器函数(Generator Function)

3. 如何书写一个生成器函数呢
   生成器函数一定返回一个生成器

   //对象里面方法没有 function，匿名函数没有 method

```
function *method(){

}
```

4. 生成器函数内部是如何执行的?

可以调用 next，以及 form
调用生成器函数只是产生生成器，不会运行里面代码

生成器函数内部只是为了给生成器每次提供迭代数据的

每次调用生成器的 next 方法，将导致生成器函数运行到下一个 yield 关键字位置

yield 是一个关键字，该关键字只能在生成器函数内部使用，表达"产生"一个迭代数据

```
function* test(){
   console.log("第一次运行")
   yield 1;
   console.log("第二次运行")
   yield 2;
   console.log("第三次运行")
   yield 3;
}

const generator=test();

generator.next()  //调用迭代
```

```
const arr1=[2,4,3,6,7,5]
function* createIterator(arr){
   for (const item of arr){
      yield item;
   }
}
const iter1=createIterator(arr1)
```

5. 有哪些需要注意的细节?
   1).生成器函数可以有返回值，返回值出现在第一次 done 为 true 时的 value 属性中
   2).生成器调用 next 方法时可以传入参数，传递的参数会交给 yield 表达式的返回值
   3).第一次调用 next 方法时，传参没有任何意义'
   4).在生成器函数内部，可以调用其他生成器函数，但是要注意加上\*号

6. 生成器的其他 API

- return 方法：调用该方法，可以提前结束生成器函数，从而提前让整个迭代过程结束(done 变 true)
- throw 方法：调用该方法，可以在生成器中产生一个错误[.throw(new Error ("在上一次迭代位置报错"))]

## 生成器应用-异步任务控制

<script>
   function *task(){
      const d=yield 1;
      console.log(d)
      const a =yield "abc";
      console.log(a)
      // //d:1
      const resp =yield fetch("http://101.132.72.36:5100/api/local")
      const result = yield resp.json();
      console.log(result);
   }

   run (task)

   function run (generatorFunc){
      const generator = generatorFunc();
      let result = generator.next();   //启动任务(开始迭代)，得到迭代数据
      handleResult();
      //对result进行处理
      function handleResult(){
         if(result.done){
            return;//迭代完成，不处理
         }
         //迭代没有完成，分两种情况
         //1. 迭代的数据是一个Promis
         //2. 迭代的数据是其他数据
         if(typeof result.value.then==="function"){
            //1.迭代的数据是一个Promise
            //等待Promise完成后，再进行下一次迭代
            result.value.then(data=>{
               result=generator.next(data)
               handleResult();
            },err=>{
               result=generator.throw(err);
               handleResult();
            })
         }else{
            //2. 迭代的数据是其他数据，直接进行下一次迭代
            result=generator.next(result.value)
            handleResult();
         }
      }
   }

</script>

# 更多的集合类型

## set 集合

> 一直以来，js 只能使用数组和对象来保存多个数据，缺乏像其他语言那样拥有丰富的集合类型。因此 ES6 新增了两种集合类型(set 和 map)，用于在不同的场景中发挥作用。

**set 用于存放不重复的数据**
自动可迭代对象(数组)去重

1. 如何创建 set 集合

```
new Set();//创建一个没有任何内容的set集合

new Set(iterable);//创建一个具有初始内容的set集合，内容来自于可迭代对象每一次迭代的结果
```

2. 如何对 set 集合进行后续操作

- add(数据)：添加一个数据到 set 集合末尾，如果数据已存在，则不进行任何操作
  - set 使用 Object.is 的方式判断两个数据是否相同，但是针对+0 和-0，set 认为是同一个数据
- has(数据)：判断 set 中是否存在对应的数据
- delete(数据)：删除匹配的数据，返回是否删除成功
- clear():清空整个 set 集合
- size：获取 set 集合中的元素数量，只读属性无法重新赋值

3. 如何与数组进行相互转换

数组处理下再还原成数组

```
const arr=[1,2,1,66,55,48,66,2,56,55];
//set本身也是一个可迭代对象，每次迭代的结果就是每一项值
const result=[...new Set(arr)].join("");
console.log(result);
```

4. 如何遍历
   1).使用 for-of 循环
   2).使用 set 中的实例方法 forEach

注意 set 集合中不存在下标,因此 forEach 中的回调的第二个参数和第一个参数是一致的，均表示 set 中的每一项

```
for(const item of s1){
   console.log(item)
}

s1.forEach((item,index,s)=>{
   console.log(item);
})
```

## set 应用

//并集
const s=new Set(arr1.concat(arr2));
const result =[...s];
console.log(result);

//交集
const s1 =new Set(arr1);
const s2 =new Set(arr2);
[...s1].filter(item=>s2.has(item)) //箭头函数只有一句话

//差集
arr1 有的且 arr2 没有，arr2 有的且 arr1 没有
合并数组.filter(item=>arr1.indexOf(item)>=0)

## 手写 set

## map 集合

键值对(key value pair)数据集合的特点：键不可重复

map 集合专门用于存储多个键值对数据。

在 map 出现之前，我们使用的是对象的方式来存储键值对，键是属性名，值是属性值。

使用对象存储有以下问题：

1. 简明之恩那个是字符串
2. 获取数据的数量不方便
3. 键名容易更原型上的名称冲突

到底对象存储键值对还是 map 存储?

- 完整的东西构成完整的整体就用对象存储(共同描述一个完整的整体，信息不能随意添加和删除)

- 有一些数据，键值对可能会随意添加和删除用 map

1. 如何创建 map
   new Map(); //创建一个空的 map
   new Map(iterable); //创建一个具有初始内容的 map，初始内容来自于可迭代对象每一次迭代的结果，但是，它要求每一次迭代的结果必须是一个长度为 2 的数组，数组第一项表示键，数组第二项表示值

   ```
      const mp1=new Map([["a",3],["b",4],["c",5]])
   ```

2. 如何进行后续操作

- size:只读属性，获取当前 map 中键的数量
- set(键，值)：设置一个键值对，键和值可以是任何类型
  - 如果键不存在，则添加一项
  - 如果键已存在，则修改它的值
  - 比较键的方式和 set 相同
- get(键)：根据一个键得到对应的值
- has(键)：判断某个键是否存在
- delete(键)：删除指定的键
- clear():清空 map

3. 和数组互相转换
   和 set 一样

4. 遍历

- for-of 每次迭代得到的是一个长度为 2 的数组

```
for(const[key,value]of mp){
   console.log(key,value)
}

```

- forEach，通过回调函数遍历
  - 参数 1：每一项的值
  - 参数 2：每一项的键
  - 参数 3：map 本身
  ```
     mp1.forEach((value,key,mp)=>{
        console.log(value,key,mp)
     })
  ```

## 手写 map

## WeakSet 和 WeakMap

### WeakSet

```
let obj={
   name:"yj",
   age:18
};
const set =new Set();   //换成weakSet内部就没数据
set.add(obj);

obj=null;
console.log(set)
```

使用该集合，可以实现和 set 一样的功能，不同的是：

1. **它内部存储的对象地址不会影响垃圾回收**
2. 只能添加对象
3. 不能遍历(不是可迭代的对象)，没有 size 属性，没有 forEach 方法

### WeakMap

类似于 map 的集合，不同的是：

1. **它的键存储的地址不会影响垃圾回收**
2. 它的键只能是对象
3. 不能遍历(不是可迭代的对象)，没有 size 属性，没有 forEach 方法

# 代理和反射

## [回顾]属性描述符

Property Descriptor 属性描述符 是一个普通对象，用于描述一个属性的相关信息

通过`Object.getOwnPropertyDescriptor(对象，属性名)`可以得到一个对象的某个属性的属性描述符

- value:属性名
- configurable:属性描述符能否被修改
- writable：属性的值能否被修改
- enumerable:该属性是否可以被枚举

> `Object.getOwnPropertyDescriptors(对象)`可以得到某个对象的所有属性描述符

如果需要为某个对象添加属性或修改属性时，配置其属性描述符，可以使用下面的代码

```
Object.defineProperty(对象，属性名，描述符)
Object.defineProperties(对象,多个属性的描述符)
```

### 存取器属性

属性描述符中，如果配置了 get 和 set 中的任何一个，则该属性，不再是一个普通属性，而变成了存取器属性。

get 和 set 配置均为函数，如果一个函数是存取器属性，则读取该属性时，会运行 get 方法，将 get 方法得到的返回值作为属性值；如果给改属性赋值，则会运行 set 方法。
obj.a 实际上是运行 obj 里面 get 方法，改变 obj.a 实际上是运行 obj 里面的 set 方法

存取器属性最大的意义，在于可以控制属性的读取和赋值

存取器应用：todo 表单，vue 响应式修改数据

## Reflect

1. Reflect 是什么?

Reflect 是一个内置的 JS 对象，它提供了一系列方法，可以让开发者通过调用这些方法，访问一些 JS 底层功能

由于它类似于其它语言的**反射**，因此取名为 Reflect

2. 它可以做什么?
   使用 Reflect 可以实现诸如 属性的赋值与取值，调用普通函数，调用构造函数，判断属性是否存在于对象中 等等功能

3. 这些功能不是已经存在了吗?为什么还需要用 Reflect 实现一次?

有一个重要的理念，在 ES5 就被提出：减少魔法，让代码更加纯粹

这种理念很大程度上是受函数式编程的影响

ES6 进一步贯彻了这种理念，它认为，对属性内存的控制，原型链的修改，函数的调用等等，这些都属于底层实现，属于一种魔法，因此，需要将它们提取出来，形成一个正常的 API，并高度聚合到某个对象中，于是，就造就了 Reflect 对象

因此，你可以看到 Reflect 对象中有很多的 API 都可以使用过去的某种语法或其他 API 实现。

4. 它里面到底提供了哪些 API 呢?

- Reflect.set(target 对象,propertyKey 名,value 值):设置对象 target 的属性 propertyKey 的值为 value,等同于给对象的属性赋值
- Reflect.get(target,propertyKey 名):读取对象 target 的属性 propertyKey，等同于读取对象的属性值
- Reflect.apply(target,thisArgument 绑定 this,argumentsList 参数):调用一个指定的函数，并绑定 this 和参数列表。等同于函数调用
- Reflect.deleteProperty(target,propertyKey):删除一个对象的属性
- Reflect.defineProperty(target,propertyKey,attributes):类似于 Object.defineProperty,不同的是如果配置出现问题，返回 false 而不是报错
- Reflect.construct(target,argumentsList):用构造函数的方式创建一个对象
- Reflect.has(target,propertyKey):判断一个对象是否拥有一个属性
- 其他 Api 见 mdn

## Proxy

中间人 为了访问目标对象，只有通过代理打交道，全权由代理接收返回

代理：提供了修改底层实现的方法
得用到反射里面的 api 来处理底层实现

不能重写目标对象的底层实现，需写代理的底层实现

```
//代理一个目标对象
//target:目标对象
//handler:是一个普通对象，其中可以重写底层实现
//返回一个代理对象
new Proxy (target,handler)
```

> 示例

```
const obj={
   a:1,
   b:2
}
const proxy=new Proxy(obj,{         //其中反射的底层实现在代理中统统适用
   set(target,propertyKey,value){
      //console.log(target,propertyKey,value);
      //target[propertyKey]=value;
      Reflect.set(target,propertyKey,value);
   }
});
console.log(proxy);
proxy.a=10;
console.log(proxy.a);
```

## Proxy 观察者模式

有一个对象，是观察者，它用于观察另外一个对象的属性值变化，当属性值变化后会收到一个通知，可能会做一些事

> vue2 采用 Object.defineProperty 响应式观察监听数据，vue3 改用 proxy

**Object.defineProperty 响应式**
//无法监听底层赋值，

<script>
//创建一个观察者
function observer(target){
   const div=document.getElementById("container");
   const ob={};
   const props=Object.keys(target);
   for(const prop of props){
      Object.defineProperty(ob,prop,{
         get(){ 
            return target[prop];
         },
         set(val){
            target[prop]=val;
            render();
         },
         enumerable:true   //可以枚举
      })
   }
   render();
   function render(){
      let html="";
      for(const prop of Object.keys(ob)){
         html+='<p><span>${prop}:</span><span>${ob[prop]}</span></p>';
      }
      div.innerHTML=html;
   }
   return ob;
}

   const target={ //直接修改target没响应
      a:1,
      b:2
   }
   const obj=observer(target) //得观察者修改 

//两次内存空间浪费

</script>

**proxy 实现响应式**

<script>
//
function observer(target){
   const div=document.getElementById("container");
   const proxy=new Proxy(target,{   //重写底层实现
      set(target,prop,value){ //捕获底层实现
         Reflect.set(target,prop,value);
         render();
      },
      get(target,prop){
         return Reflect.get(target,prop);
      }
   })
   render();
   function render(){
      let html="";
      for(const prop of Object.keys(target)){
         html+='<p><span>${prop}:</span><span>${target[prop]}</span></p>';
      }
      div.innerHTML=html;
   }
   return proxy;
}

   const target={ 
      a:1,
      b:2
   }
   const obj=observer(target) //都可以监听(无论是给观察者obj还是target赋值)


</script>

## 偷懒的构造函数

用 construct 构造函数创建一个对象，给类赋值
//08.06

<script>
class User{

}

function ConstructorProxy(Class, ...propNames){
   return new Proxy(Class,{   //用构造函数的方式创建一个对象
      construct(target,argumentsList){ //UserProxy当构造函数使用可以捕获
         const obj=Reflect.construct(target,argumentsList)  //通过原来构造函数创建对象
         propNames.forEach((name,i)=>{ //再把属性加上
            obj[name]=argumentsList[i];//属性名对应到属性值
         })
         return obj;
      }
   })
}

const UserProxy = ConstructorProxy(User,"firstName","lastName","age")  //通过代理告诉有三个属性

const obj=new UserProxy("袁","进",18); //对应的三个参数
console.log(obj)
</script>

## 可验证的函数参数

防止类型不匹配

<script>
function sum (a,b){
   return a+b;
}

function validatorFunction(func,...types){
   const proxy =new Proxy(func,{
      apply(target,thisArgument,argumentsList){
         types.forEach((t,i)=>{
            const arg =argumentsList[i]
            console.log(arg,t,i)
            if(typeof arg!==t){
               throw new TypeError(`第${i+1}参数${argumentsList[i]}不满足类型${t}`)
            }
         })
         Reflect.apply(target,thisArgument,argumentsList);
      }
   })
}

const sumProxy =validatorFunction(sum,"number","number")
console.log(sumProxy("1","2"))
</script>

# 新增数组功能

## 新增的数组 API

**静态方法**

- Array.of(...args):使用指定的数组项创建一个新数组
  //不同于 new Array(100)只传一个数表达数组长度
- Array.from(arg):通过给定的类数组，或可迭代对象，创建一个新数组(类数组放进去变真数组)
  //ES6 前强行把类数组变成数组 Array.prototype.slice.call(divs,0);

**实例方法**

- find(callback):用于查找满足条件的第一个元素 //filter 找全部，find 找一个
- findIndex(callback):用于查找满足条件的第一个元素下标
- fill(data):用于指定的数据填充满数组所有的内容
- copyWithin(target,start?,end?):在数组内部完成复制
- includes(data):判断数组中是否包含某个值，使用 Object.is 匹配 //不用 indexOf 匹配下标是否大于 0

## 类型化数组

### 数字存储的前置知识

1. 计算机必须使用固定的位数来存储数字,无论存储的数字是大是小，在内存中占用的空间是固定到底
2. n 位的无符号的整数能表示的数字是 2^n 个，取值范围是：0~2^n -1
3. n 位的有符号整数能表示的数字是 2^n 个，取值范围：-2^(n-1)~2^(n-1)-1
4. 浮点数表示法可以用于表示整数和小数，目前分为两种标准:
   1. 32 位浮点数：又称为单精度浮点数，它用 1 位表示符号，8 位表示阶码，23 位表示尾数
   2. 64 位浮点数：又称为双精度浮点数，它用 1 位表示符号，11 位表示阶码，52 位表示尾数
5. js 中的所有数字，均使用双精度浮点数保存

### 类型化数组

类型化数组：用于优化多个数字的存储
具体分为：

- Int8Array: 占用 8 位内存空间。8 位有符号整数(-126~127)
- Uint8Array:8 位无符号整数(0~255)
- Int16Array:...
- Uint16Array
- Int32Array
- Uint32Array
- Float32Array
- Float64Array

1. 如何创建数组
   new 数组构造函数(长度)
   数组构造函数.of(元素...)
   数组构造函数.from(可迭代对象)
   new 数组构造函数(其他类型化数组)

2. 得到长度
   数组.length //得到元素数量
   数组.byteLength //得到占用的字节数

3. 其他的用法跟普通数组一致

- 不能增加和删除数据，类型化数组的长度固定
- 一些返回数组的方法，返回的数组是同类型化的新数组

## ArrayBuffer

缓冲区
ArrayBuffer:一个对象，用于存储一块固定内存大小的数据。

```
//创建了一个用于存储10个字节的内存空间
const bf=new ArrayBuffer(10);
```

可以通过属性`byteLength`得到字节数，可以通过方法`slice`得到新的 ArrayBuffer

### 读写 ArrayBuffer

1. 使用 DataView
   通常会在需要混用多种存储格式时使用 DataView
2. 使用类型化数组
   实际上，每一个类型化数组都对应一个 ArrayBuffer,如果没有手动指定 ArrayBuffer,类型化数组创建时，会新建一个 ArrayBuffer

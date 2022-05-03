# Javascript 详细版

## 概述

- 细化目标

正面反馈 成就感

- 重视练习

### 语言简史

1. 95 年网景公司
   **Brendan Eich**
   10 天新语言诞生
   LiveScript->Javascript

2. 浏览器大战

ie3 发布绑定 windows 操作系统
**97 年 ECMA 收录了 Javas，并提交给 ISO，经过修改，成为第一个 JS 标准版本，成为 ECMAScript 简称 ES**

3. 第二次浏览器大战

IE4IE5IE6(windows xp)，觉得浏览器没有进步的可能了，微软决定解散浏览器团队。

Brendan Eich， 带领团队成立 Mozilla 基金会，并讲网景浏览器开源
长时间世界技术爱好者对网景浏览器维护补丁

2002 年 Mozilla 推出 firefox 浏览器

2008，谷歌推出 chrome 浏览器，苹果推出 safari，ASA 推出 opera

chrome 浏览器搭载 js 执行引擎 V8(V8 引擎，可将 js 代码直接转化字节码，理论上，js 代码执行熟读接近汇编语言)
于是 js 具备了编写大型应用程序的能力，甚至服务器应用

> Ryan Dahl 准备写一个服务器段框架，直接利用 V8 引擎完成了该框架，称为 nodejs

**V8，将 js 执行推向了一个新的台阶**

4. Es 标准的发展

ES1,1997
ES2,1998
ES3,1999
ES5,2009.习惯上不再区分 JavaScript(js)和 ECMAScript（ES)
ES6,2015.ECMA 宣布，从 ES6 开始，使用年号作为版本号，ES6 真正称呼蔚 ES2015
ES7,2016

深谋远虑，前瞻性眼光
正是因为 ES 避免了运行环境，才让 ES 有机会在各种环境中执行
**非常重要:ES 的语言标准，不涉及语言的运行环境**

学习的是：ES 通用语法，浏览器环境为其注入的新功能

通常把 ES 运行的环境称为宿主环境

### JS 语言特性

- 解释性语言

编译型语言：c,c++,java,c#

编译型语言会经过一个翻译的过程，负责翻译的叫做编译器
优点：执行速度快
缺点：某个编译结果，难以适用于各种环境(跨平台)；部署繁琐

解释型语言：js，php

解释性语言没有编译结果
优点：跨平台，部署简单
缺点：执行速度稍慢

- 弱类型语言
  弱类型：存放数据类型可变优点：灵活，易上手，不严谨

强类型：存放的数据类型不可变。严谨，不灵活，不易上手

> 通常将弱类型的解释性语言，称为脚本语言

- 单线程
  同步现象：上一件事没做完，下一件事必须等待

- 异步
  提高单线程的执行效率

### 开发环境准备

chorme
visual studio code 可视化开发工具

## Js 语法基础

### 第一个 js 程序

#### 浏览器环境中，代码书写位置

1. 直接书写页面中的 script 元素内部
2. 书写到外部的 js 文件，在页面中引用[推荐]
   代码分离：内容，样式，功能，三者分离，更加容易维护和阅读

- 页面中，可以存在多个 script 元素，执行顺序从上到下，单线程执行
- 如果一个 script 元素引用了外部文件，内部不能书写任何代码
- script 元素有一个可选属性，type，该属性用于指定代码的类型，该属性值是 MIME 格式`type="text/javascript"`

#### 认识基本语法

- 语法必须都是英文符号
- js 代码由多条语句构成，每个语句用英文分号结束
- js 代码从上到下同步执行
- js 语言大小写敏感

所有的输出语句都不是 ES 标准。

- document.write 该语句用于将数据输出到页面
- alert 该语句用于将数据弹窗的形式显示到页面
- console.log 该语句用于将数据显示到控制台

注释为两个斜杠

### JS 数据类型

#### 原始类型

原始类型值不可再细分的类型

不同类型的数据的字面量表示法

1. 数字类型 number
   直接书写即可
   数字类型前加前缀，表不同进制
   0 表示 8 进制，0x 表示 16 进制，0b 表示 2 进制

2. 字符串类型 string

- 单引号 '
- 双引号 "
- ` 模板字符串，也就是包代码块的吧 在字符串中，任何表示一个特殊字符，可以使用转义字符`\`

3. 布尔类型 boolean
   表达真或假

4. undefined 类型

5. null 类型
表示空，不存在。
<!-- null的tpyeof表object -->

#### 引用类型

- 对象 object(事物，东西)
  可以认为对象，是由多个基本类型组合而成。
  描述一个东西的集合

- 函数
  (见后两章)

**属性**：对象的成员
typeof 展示数据类型

> 直接书写的具体数据，叫做**字面量**

### 变量

变量是一块内存空间，用于存储数据

计算机程序的运行，仅与内存打交道

```
var pid；
```

//声明个变量后，名称为 pid，值为 undefined

- 变量可以重新赋值

- 标识符的规范： 1)只能以英文字母，下划线，$开头
2)其他位置可以出现数字，英文字母，下划线$ 3)标识符应该做到望文思意 4)如有多个单词，使用驼峰命名发，单词首字母大写

语法糖仅仅是为了方便代码书写或记忆，不会有实质性的改变

- JS 中存在变量提升
  所有的变量的声明，会自动提到代码的最顶部，不会在超越脚本块

### 变量和对象

原始类型：number,string,boolean,null,undefined
引用类型：object，funciotn 函数

> 在变量中存放对象

1. 通过变量，读取对象中某个属性
   变量名.属性名
   若读取的属性不存在时，会得到 undefined
   当读取属性的对象不存在(undefined 或 null)时，程序报错

```
有区别
var user2;       没有定义的本身就是undefined，读其属性自然报错
var user2={}
```

2. 通过变量，更改对象中某个属性
   当赋值的属性不存在，会添加该属性
   给 underfined 添加也自然会报错

3. 删除属性
   delete 变量名.属性名
   变量名.属性名=undefined；

4. 属性表达式

给属性赋值，或读取属性时，可以使用下面的格式操作

```
对象变量["属性名"]
```

- 某些属性名中包含特殊字符

实际上，js 对属性名的命名要求并不严格，属性可以是任何形式等待名字

属性的名字只能是字符串，如果书写是数字，会自动转化为字符串

> 全局对象
> JS 大部分的宿主环境都会提供一个特殊的对象，该对象可以直接在 JS 代码中访问，该对象叫做全局对象

浏览器环境中，全局对象为 window，表示整个窗口

全局对象中的所有属性都可以直接使用，而不需要写上全局对象名。

**开发者定义的所有变量，实际上，会成为 window 对象的属性**

### 引用类型

```
var obj1={
    name:"123"  //出现对象字面量的位置，会新开辟一块内存空间，用于存放对象内容，再把新开辟的内存地址交给对象
};
var obj2=obj1;      //obj1和obj2指向同一个对象，持有相同的引用
obj2.name="456"
console.log(obj1.name,obj2.name);
居然两个都是456???
```

> 解释

**
原始类型的变量存放的具体的值
引用类型的变量，存放的是内存地址
凡是出现对象字面量的位置，都一定在内存出现一个新的对象，有几个创建几个新的空间**

例 obj2=obj1，(赋值) 修改自身属性则会改变引用值，
有大括号才是创建对象，创建对象则改变自身(若是给其属性赋值除外)

```
var obj1={
    a:"123",
    b:"456",
    sub:{
        s1:"abc".
        s2:"bcd"
    }
};
var temp=obj1.sub;
var obj2=obj1;
obj2.sub={
    s1:"s",
    s2:"ddd"
};

console.log(obj1.sub.s1,obj2.sub.s1.temp.s1);
//s s(之前sub还在，只不过换了地址), abc(原始类型存放具体的值)

```

凡是出现对象字面量的位置，都一定在内存出现一个新的对象，有几个创建几个新的空间

<!-- 引用类型 24.30 -->

扩展知识：JS 中的垃圾回收
JS 引擎，会定期的发现内存中无法访问到的对象，该对象称之为垃圾
JS 引擎会在合适的时候将其占用的空间释放

补充：在 js 中变量在使用时可以不写 var
不写 var 直接赋值，相当于给 window 的某个属性直接赋值

## 运算符

### 运算符概述

操作符：运算符，参与运算的符号
操作数：参与运算的数据，也称之为元
操作符不一定只有一个符号
操作符出现在不同的位置可能不同含义

`=` 赋值符号，将右边赋值给左边
`.`访问符号，用于访问对象属性
`[]`访问对象属性
`()`函数调用

#### 分类

按操作数数量区分
用操作符需要几个操作数来分

功能区分

1. 算术运算符(数学)
2. 比较运算符
3. 逻辑运算符
4. 位运算符
5. 其他

#### 表达式

表达式=操作符+操作数
每个表达式都有一个运算结果，该结果叫做**返回值**，返回值的类型叫做返回类型
所有表达式可以当作数据使用

运算符返回值的类型
`=` 返回赋值的结果
`.`返回属性的值
`[]`返回属性的值
`()`返回取决于函数的运行
如果是声明加赋值的表达式，返回结果为 undefined

console.log 函数的返回结果为 undefind

```
chrome浏览器控制台的环境是REPL环境
REPL：Read Eval Print Loop 读-执行-打印-循环
当直接在控制台书写代码时，除了运行代码之外，还会输出该表达式的返回值
```

### 算术运算符

`+ - * / % ++ -- **(指数) `

1. 数字运算是不精确的
2. 除数为 0
   如果被除数是正数，得到结果为 Infinity(正无穷)
   如果被除数是负数，得到结果为-Infinity(负无穷)
   如果被除数是 0，得到结果 NaN (Not a Number，是数字类型)
   > NaN 虽然是数字，但它和任何数字做任何运算，得到的结果都是 NaN

三个特殊值 正无穷 负无穷 NaN
typeof1/0 返回类型为 NaN

> isNaN 函数,该函数用于判断一个数据是否是 NaN，返回 boolean
> isFinite 函数，该函数用于判断一个数据是否是有限的，返回 boolean

3. 求余
   % 也为求模
   余数的符号，与被除数相同

#### 其他类型使用算术运算

1. 除加号之外的算术运算符

将原始类型转化为数字类型(自动完成转化)，然后进行运算

- boolean true->1 ,false->0
- string :如果字符串内部是一个正常的数字，直接变成数字，
  如果是一个非数字则得到 NaN(能识别 Infinity，不能把字符串内部的东西当作表达式)
  如果字符串是一个空字符串，转换为 0.字符串转化时，会忽略前后空格
- null:null ->0
- undefined: undefined->NaN

将对象类型先转化为字符串类型，然后再将该字符串转化为数字类型

对象类型->"[object object]"\*5 ->NaN
对象转化为数字是 NaN

2. 加号运算符

- 加号一边有字符串，含义变成字符串拼接

将另一边的其他类型，转化为字符串

数字->数字字符串
boolean->boolean 字符串
null->"null"
undefined->"undefined"
对象->"[object object]"

- 加号两边都没有字符串，但一边有对象，将对象转化为字符串，然后按照上面的规则进行

- 其他情况和上面的数学运算一致

### 自增自减

从高到低依次是：

- `++ --`
- `* / %`
- `+ -`
  优先级的运算细节：

1. 从左到右依次查看
2. 如果遇到操作数，将数据的值直接取出
3. 如果遇到相邻的两个运算符，并且左边的运算符优先级大于等于右边运算符，则直接运行作变的运算符

### 比较运算符

大小比较: > < >= <=

相等比较：== != ===严格相等 !==严格不相等

比较运算符返回类型是 boolean
算术运算符的优先级高于比较运算符

大小比较

- 两个字符串比较大小，比较的是字符串的字符编码
- 如果一个不是字符串，并且两个都是原始类型，将它们都转化为数字进行比较
  NaN 与任何数字比较，得到的结果都是 false
  Infinity 比任何数字都大
  Infinity 比任何数字都小

- 如果其中一个是对象，将对象转化为原始类型然后，按照规则 1 或规则 2 进行比较

目前，对象转化为原始类型后，是字符串"[object object]"

相等比较

1. 两端的类型相同，直接比较两个数据本身是否相同(两个对象比较的地址)
2. 两端的类型不同

1). null 和 undefined，它们之间相等，和其他原始类型比较，则不相等
2).其他原始类型，比较是先转换为数字，再进行比较
3).NaN 与任何数字比较，都是 false，包括自身
4).Infinity 和-Infinity，自能和自身相等
5).对象比较时，要先转化为原始类型后，再进行比较

**由于相等和不相等比较，对于不同类型的数据比较违反直觉，因此，通常我们不适用这种比较方式，而是使用更加接近直觉的严格相等和严格不相等比较**

===：两端的数据和类型必须相同
!==:两端的数据或类型不相同

### 逻辑运算符

#### 与(并且)

符号：&&
有一个假就是假

书写方式：表达式 1&&表达式 2

1. 将表达式 1 进行 boolean 判定

以下数据均判定为 false：

1. null
2. undefined
3. false
4. NaN
5. ''
6. 0

其他数据全部为真

2.  <!-- 左边为假结束运算，直接为假 -->

如果表达式 1 的判定结果为假,则直接返回表达式 1,而不执行表达式 2;
否则返回表达式 2 的结果

#### 或

符号：||
有一个真就是真

书写方式：表达式||表达式

1. 将表达式 1 进行 boolean 判定

以下数据均判定为 false：

1. null
2. undefined
3. false
4. NaN
5. ''
6. 0

其他数据全部为真

2.  <!-- 左边为假结束运算，直接为假 -->

如果表达式 1 的判定结果为真,则直接返回表达式 1,而不执行表达式 2;
否则返回表达式 2 的结果

应用(取默认值)

#### 非

符号:!
写法:!数据

将数据的 boolean 判定结果直接取反,非运算符一定返回 boolear 类型

优先级很高

```
应用求是否闰年
var year=2000

//逻辑判断是否是闰年

//闰年规则:4年一闰,百年不闰,400年一闰
var result= year%4===0 && year%100!==0 || year % 400 === 0;
//如果是闰年,则输出闰年,否则输出平年
result&&console.log("闰年");
result||console.log("平年");

```

### 三目运算符

? :

### 运算符补充

- 模板字符串

```
${user.name}        //在代码块里面在${}可直接书写js表达式
```

- 类型转换
  运算时把表达式运算出来参与运算，不会改变原来的值和类型

- 复合的赋值运算符
  += -= /= \*= %= \*\*=

- void 运算符
  写法：

1. 普通写法：`void表达式`
2. 函数写法：`void(表达式)`

运行表达式，然后返回 undefined

- 逗号运算符
  写法：表达式 1，表达式 2
  依次运行两个表达式，返回表达式 2

逗号运算符比赋值运算符更低

### 数字的存储

在对精度要求很高的系统中，或要对小数的运算结果进行比较时，需要特别谨慎

1. Js 中的小数运算是精确的吗
   不一定
2. Js 中整数运算时精确的吗
   不一定
3. Js 中表示的整数是连续的吗
   不是，当 js 的数字很大的时候，不再连续

4. Js 中表示的最大数字是多少
   最大连续整数：9007199254740991
5. Js 中能表示的数字的有效位数是多少
   16~17 位

**进制转化**
十进制转化为二进制后，可能是无限小数，但是计算机对数字的存储能力有限，因此会丢失一些数据

```
var a =0.3
a.toString(2)；
查看该数的二进制格式
```

**Js 如何存储数字**

整数法，浮点法
Js 中，存储的所偶数在，都按照浮点法存放叫 float
浮点数分为单精度和双精度
使用双精度存放浮点数，IEEE 754。

**存放方式**
Js 在计算机中，给每个数字开辟一块内存空间，尺寸固定为 64 位
在计算机中位(bit)是最小的存储单位，简称为 bit
1 byte=8bit
1kb=1024byte
1mb=1024kb
1gb=1024mb
分三段
第 1 段：1 位，表示符号位，1 为负，0 为正
第 2 段：11 位，表示指数位，在这里的指数是 2 为底的指数，而不是 10 2^11=2048
第 3 段：52 位，表示有效数字

举例

```
0   0000 0000 011     1111 0000 0000 0000....
```

相当于：$1.1111*2^3$

为了考虑其负值则采用$1.1111 *2^{1027-1023}$ //其 1023 恰好为 2048 的一半

> 特殊情况

1. 指数为 0 ，尾数为 0，表示数字 0
2. 符号为 0， 指数为 2047，尾数为 0，表示正无穷 //正常数指数最多取到 2046

```
Infinity:0 11111111111 0000000000..
```

3. 符号为 1，指数为 2047，尾数为 0，表示负无穷

```
-Infinity:1 11111111111 000000000..
```

4. 指数为 2047 ，尾数不为 0，表示 NaN

```
NaN: 1 11111111111 01001010000..

```

**一个正常数字，指数部分最多取到 2046**

> 能表示最大的数字

```
0 11111111110 111111111..

```

相当于：$1.111111111...*2^1023$

> 能表示的最大安全整数
> 安全数字：从 1 开始到该数字，均是连续的整数，并且该数字的下一个整数时存在的

```
0 xxxx 111111111111..
```

相当于：$1.111111111..*2^52$ //指数为 52 是为了去除前面的小数点

即$2^53-1$ //??

### 位运算符

将一个整数的二进制格式进行运算

js 中如果对一个数据进行位运算，它首先会将其转化为一个整数，并且按照 32 位的整数二进制排列

举例

```
2.7-> 2 ->0000 0000 0000 0000 0000 0010

NaN-> 0

Infinity -> 0

-Infinity ->0
```

> 与运算
> 符号：&
> 写法：整数 1&整数 2
> 将数字转化为 32 位的二进制 位运算
> 两个为 1 才是 1(同时为真才真)

> 或运算
> 符号：|
> 写法：整数 1|整数 2
> 将数字转化为 32 位的二进制 位运算
> 两个为 0 才是 0(同时为假才假)

> 否(非)运算
> 符号：~
> 写法：~整数
> 将该整数按位取反

**负数的存储方式**
计算机做不了减法，只能做加法

-1
真码：1000 0000 0000 0000 0000 0000 0000 0001
反码：1111 1111 1111 1111 1111 1111 1111 1110 真码取反
补码：1111 1111 1111 1111 1111 1111 1111 1111 反码加 1
只针对于负数计算机才这样存储方案

取反的快速运算：-数字 -1

快速取整(~~3.76237)

> 异或运算

符号：^
写法：整数 1^整数 2
将数字 1 和数字 2 按位比较，不同取 1，相同取 0

应用
交换两个值

```
1.
a=a+b;
b=a-b;
a=a-b;
console.log(a,b);

2.
a=a^b;
b=a^b;
a=a^b;
```

> 应用场景：位的叠加(开关)

```
文件权限添加124
var perm ={
    read:0b001,     //读权限
    write:0b010,    //写(修改)权限
    create:0b100    //创建权限
}；

//变量p中保存可读可写
var p =perm.read |perm.write ;

//去掉可读权限
//011^001=010
p=p|perm.read^perm.read;    //或运算是确保本来没有权限

//判断权限：p中是否有可读元素
// p:011& 001= 001

p & perm.read ===perm.read ?console.log("可读")：console.log("不可读")

```

> 位移运算

左位移：<<
写法：数字 1<<数字 2
将数字 1 的二进制(除符号之外，左移数字 2 的次数)

右位移：>>
写法：数字 1>>数字 2 结果：整数(数字 1/2^数字 2)

全右位移：>>>
与有位移的区别，在于全右位移会导致符号位跟着位移

### 求余和求模

%:求余
x%y
**求余符号与被除数一致**

1. 求余 x rem y: x-n\*y,n 表示商取整(直接去掉小数，向 0 取整)

```
x=7, y=3    x rem y=x-n*y=7-2*3=1
n=x/y=2.333直接取2
```

```
x=7,y=-3
n=7/-3=-2.3333取-2
x rem y =x-n*y=7-(-2)*(-3)=7-6=1
```

2. 求模 x mod y:x-n\*y, n 表示商取整(向下取整)
   向下取整始终靠进 x 左侧

**求模符号与除数相同**

## 流程控制

### 流程图

if 判断
switch 开关
循环

### 数组

数组的本质是一个对象

- length 属性：数组的长度，自动变化，值为最大下标+1
- 数字字符属性：下标也叫做索引。相当于每个数据的编号，下标从 0 开始排列

连续下标的取值范围：0~lenght -1，如果给 lenght 直接赋值，会导致数组被截断

实际开发中，不要给 length 赋值

> 下标
> 通常情况下，下标是连续的
> 下标不连续的数组，叫稀松数组

> 常见操作
> 添加数组项

- 数组 [长度] =数据：像数组末尾添加一个数据
- 数组.push(数据),向数组末尾添加一个数据
- 数组.unshift(数据)：向数据起始位置添加一个数据，会导致每一项的下标向后移动
- 数组.splice(下标，0，添加到数据)：从指定下标位置开始，删除 0 个，然后在那个位置添加插入的数据，如果下标超出范围，则按照范围的边界进行处理

push 和 unshift，splice 可以添加多个数据

> 删除数据

- delete 数组[下标]：这种做法不会导致数组其他的属性发生变化，因此会导致产生稀松数组。
- 数组.pop()：删除数组的最后一项，该表达式返回最后一项数据
- 数组.shiift()：删除数组的第一页，该返回值返回第一项的数据
- 数组.splice(下标，删除的数量，添加的数据)：从指定下标位置开始，删除指定数量，然后再该位置插入添加的数据，如果下标超过范围，则按照范围的边界进行处理，返回一个新数组，该数组记录被删除的数据

> 其他操作

- 数组.slice(起始位置下标，结束位置下标):将起始位置到结束位置之间的数据拿出来，得到一个新数组，该函数不会改变原数组；注意：结束下标取不到

下标可以写负数，如果是负数，则从数组的末尾开始计算
如果不写下标，则直接取到末尾

- 数组清空

数组.splice(0,数组.length)；
数组.length =0；

- 查找数组中某一项的下标

数组.indexOf(数据)

从数组中一次就查找对应的数据，查找时使用严格相等进行比较，找到第一个匹配的下标，返回。如果没有找到，则得到-1；

数组.lastIndexOf(数据)
只是查找的是最后一个匹配的下标

数组.fill(数据)：将数组的所有项，填充为指定数据
数组.fill(数组，开始下标)：将数组从开始下标起，到数组的末尾，填充为指定点数据
数组.fill(开始下标，结束下标)：将数组从开始下标起，到数组的结束下标(取不到)，填充为指定点数据

arr1.concat(arr2) 拼接数组，产生新数组返回

- 补充

in 关键字：判断某个属性在对象中是否存在

"属性名" in 对象

for-in 循环

## 函数

主要用于减少重复代码

创建定义声明函数

函数体的代码不会直接运行，必须要手动调用函数，才能运行其中的代码

运行函数体

通过字面量声明的函数，会提升到脚本块的顶部

通过字面量声明的函数，会成为全局对象的属性

函数内部声明的变量：

1. 如果不使用 var 声明，和全局变量一致，表示给全局对象添加属性
2. 如果使用 var 声明，变量提升到所在函数的顶部，函数外部不可以使用该变量

函数中声明的变量，仅能在函数中使用，在外部无效

### 作用域和闭包

1. 全局作用域
   直接在脚本中书写的代码
   在全局作用域中声明的变量，会被提升到脚本块的顶部，并且会成为全局对象的属性

2. 函数作用域
   函数中的代码
   在函数作用域中声明的变量，会被提升到函数顶部，并且不会成为全局对象的属性

因此函数的声明变量不会导致全局对象的污染
尽可能把功能封装在函数中

当函数成为表达式时，既不会提升，也不会污染全局对象

将函数变为一个函数表达式的方法之一，将函数用小括号起来
然而，这样一来函数无法通过名称调用，

不污染全局变量且能调用函数

```
(function test(){

})();
```

如果书写一个函数表达式，然后将立即调用，该函数称为立即执行函数 IIFE(Imdiately Invoked Function Expression)

大部分情况下，函数表达式的函数名没有实际意义，因此可以忽略函数名
没有名字的函数叫做，称为匿名函数

#### 作用域中可以使用的变量

全局作用域只能使用全局作用域中声明的变量(包括函数)

函数作用域不仅能使用自身作用域中声明的变量(包括函数)，还能使用外部环境的变量(包括函数)

有时候，某个函数比较复杂，在编写的过程，可能需要另外一些函数和来辅助它完成一些功能，而这些函数仅仅会被该函数使用，不会在其他位置使用,则可以将这些函数声明到该函数的内部。

```
外面不能调用只能通过该函数父函数调用使用
(function(){
    function helper1(){
        function subHelper1(){

        }
    }
    function helper2(){

    }
})();
```

函数内部声明的变量和外部冲突时，使用内部的

```
function A(){
    var a ="bcd";
    functionB(){
        console.log(a);
    }
    B();
}

var a ="abc";
function B(){

}
A();


//分析bcd
全局环境：
A:函数
B:函数
a：abc

函数A的环境：
a：bcd
B：函数

函数B的环境：
```

#### 闭包

闭包(closure)
现象，内部函数使用外部环境中的变量就有闭包

自身被回收，而创建的变量还有用，则不会销毁

### 函数表达式和 this

> 函数表达式
> js 中，函数也是一个数据，语法上，函数可以用于任何需要数据的地方

函数是一个引用类型，将其赋值给某个变量时，变量中保存的是函数的地址

> 作业:
> **回调函数**
> 当你写一个函数时，在完成函数功能时候，有些条件未知是参数，但参数不是具体数据，而是做一件具体的事。函数就是做一件事功能，判断是否满足条件这个功能的条件缺失故用回调函数，就是做一件事功能

1. 新建 BetterFunction.js,将之前的 MyFunction.js 改造成为单对象模式

2. 写一个函数为数组排序，考虑这个数组所有可能 sort

```
length 5
i1++
j   4  01 12 23 34
j   3  01 12 23
j   2  01 12
j   1  01

sort(arr,compare){
    for(var i=1;i<arr.length;i++){      //循环排序！！！
        for(var j=0;j<arr.length-i;j++){
            if(compare(arr[j],arr[j+1])>0){
                var temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
    }
}

var arr={
    {name:"张三",age:18,weight:60},
    {name:"李四",age:15,weight:75},
    {name:"王五",age:120,weight:65}

};
MyFunction.sort(arr,function(a,b){
    retuen a.age-b.age;          //只需要切换这就可以灵活改变排序条件
})
```

3. 写一个函数按照指定的条件对数组进行筛选 filter

```
filter(arr,callback){
    var newArr=[];
    for(var i=0;i<arr.length;i++){
        if(callback(a[i],i)  //arr[i]是否满足条件){
            newArr.push(arr[i]);
        }
    }
    return newArr;
}

var arr=[151,51,5,,1,15,156,656,51]
var newArr=MyFunctions.filter(arr,function(item,index){
    return itme%2!===0;
})
```

4. 写一个函数，按照指定条件，得到某个数组中第一个满足条件的元素 find

```
find(arr,callback){
     var newArr=[];
    for(var i=0;i<arr.length;i++){
        if(callback(a[i],i)  //arr[i]是否满足条件){
            return arr[i];
        }
    }
}
var newArr=Myfunctions.find(arr,function(item,index){
    return item%12===0;
})
```

5. 得到某个数组中满足条件的元素数量 count

```
count(arr,callback){
    var nember=0;
    for(var i=0;i<arr.length;i++){
        if(callback(a[i])){
            nember++;
        }
    }
    return nember;
}

var num =Myfunctions.count(arr,function(a[i]){
    reture a[i]%2===0;
})
console.log(num);
```

> this

this 无法赋值

1. 在全局作用域中，this 关键字固定指向全局对象
2. 在函数作用域中，取决于函数是如何被调用的
   当调用时才知道 this 指向谁，初始不知 1. 函数直接调用，this 指向全局对象 2. 通过一个对象的属性调用，格式为`对象.属性() ` `对象["属性"]() `this 指向对象

### 构造函数

> 对象中的属性，如果是一个函数，也称该属性为对象的方法

构造函数取决于怎么调用

#### 用于创建对象的函数

用函数创建对象，可以减少繁琐的对象创建流程

1. 函数返回一个对象

```
function createUser(){
    reture{
        name:"abc",
        age:10,
        gender:"男",
        sayHello:function(){
                console.log('我叫${this.name},年龄${this.age}岁,性别${this.gender}');
        }
    };
}

var u1 = createUser();
u1.sayHello();
```

> 进阶传参用函数自动创建

```
function createUser(name,age,gender){
    reture{
        name:name,
        age:age,
        gender:gender,
        sayHello:function(){
                console.log('我叫${this.name},年龄${this.age}岁,性别${this.gender}');
        }
    };
}

var u1 = createUser("张三",18,"男");
u1.sayHello();

var u2 = createUser("姬成",20,"男");
u2.sayHello();
```

2. 构造函数
   构造函数专门用于创建对象

```
new 函数名(参数)；

function User(name,age,gender){
    this.name=name;
    this.age=age;
    this.gender=gender;
    this.sayHello=function(){
        console.log('我叫${this.name},年龄${this.age},性别${this.gender}');
    }
}
var u1 = new User("张三",18,"男");
console.log(u1);
u1.sayHello();
```

如果是使用上面的格式创建对象，则该函数叫做构造函数

1. 函数命使用大驼峰命名法
2. 构造函数内部，会自动创建一个新对象，this 指向新创建的对象并且自动返回新对象
   3）构造函数中如果出现返回值，如果返回的是原始类型，则直接忽略；如果返回的是引用类型，则使用返回的结果(返回对象即对象结果，返回函数则调用函数的结果)

3. 所有的对象，最终都是通过构造函数创建的

```
var arr =new Array(3,4,5);相当于arr=[3,5,7,2];
var obj={
    name:"asdf",
    age:234,
    gender:"男"
};语法糖
相当于
var obj=new Object();
obj.name="asdf";
obj.age=234;
obj.gender="男";
```

#### new.target

该表达式在函数中使用，返回的是当前的构造函数，但是，如果该函数不是通过 new 调用，则返回 undefined

通常用于判断某个函数是否通过 new 在调用

```
function User(name,age,gender){

    var temp=function(){
            console.log('我叫${this.name},年龄${this.age},性别${this.gender}');
        }

    if(new.target ===User){     //正常的构造函数调用
        this.name=name;
        this.age=age;
        this.gender=gender;
        this.sayHello=temp;
    }else{
        return{
            name,age,gender,
            sayHello:temp        //直接调用返回对象
        }
    }

}
var u1=new User("ss",18,"女")； //if判断可以无论是否通过new调用都正确返回
console.log(u1);

```

可写函数专门帮助创建对象

#### 英雄打怪兽小游戏

```
英雄和怪兽都具有攻击力，防御力，生命值，暴击几率(暴击时伤害翻倍)
攻击伤害=攻击力-防御力
攻击力最少为1.
创建一个英雄和一个怪兽，让它们互相攻击，直到一方死亡，输出整个攻击过程。

见项目英雄打怪兽.html
```

### 函数的本质

函数的本质就是对象.

某些教材将构造函数称为构造器

> 所有的对象都是通过关键字 new 出来的`new 构造函数()`

**那么函数是不是通过 new 关键字创建的?**

```
示例
//      function sum(a,b){
//          return a+b;     //语法糖
//      }

var sum =new Function("a","b","return a+b");
console.log(typeof sum);
console.log(sum(3,5));

```

故
所有的函数，都是通过`new Function`创建。

Function V8 引擎起动就写好了放在内存中，供使用

Function ->产生函数对象 ->产生普通对象

```
Function 创建函数User 再new出用户对象
function User(firstName,lastName){
    this.firstName=firstName;
    this.lastName=lastName;
    this.fullName=this.firstName+ this.lastName;
}
console.log(new User("袁"+"进"))；
```

new 一个 function 产生的对象一定是函数？ //对

> Function
> 由于函数本身就是对象，因此函数中，可以拥有各种属性。

#### 包装类

Js 为了增强原始类型的功能，为 boolean，string，number 分别创建了一个构造函数：

1. Boolean
2. String
3. Number

如果语法上，将原始类型当作对象使用时(一般是在使用属性时)，Js 会自动在该位置利用对应的构造函数，创建对象来访问原始类型的属性

> 类：在 js 中，可以认为，类就是构造函数

> 成员属性(方法)，实例属性(方法)：表示该属性是通过构造函数的对象调用的。
> 静态属性(方法)，类属性(方法)：表示该属性是通过构造函数本身调用的。

### 递归

函数直接或间接调用自身

避免无限递归，无限递归会导致执行栈溢出

对比死循环

- 死循环不会报错，也不会导致栈溢出

```
//求斐波拉契数列第n位值

1 1 2 3 5 8 13 21
f(n)=f(n-1)+f(n-2)

function f(n){
    if(n===1||n===2){
        return 1;
    }
    return f(n-1)+f(n-2);
}
console.log(f(7);)
```

#### 执行栈

任何代码的执行都必须有一个执行环境，执行环境为代码的执行提供支持

执行环境是放到执行栈中

每个函数的调用，都需要创建一个函数的执行环境，函数调用结束，执行环境销毁。

执行栈有相对固定的大小，如果执行环境太多，执行栈无法容纳，会报错

#### 尾递归

如果一个函数最后一条语句是调用函数，并且调用函数不是表达式的一部分，则该语句称之为尾调用，如果尾调用是调用自身函数，则称为尾递归。
某些语言或执行环境会对尾调用进行优化，它们会理解销毁当前函数，避免执行栈空间被占用

遗憾的是在浏览器执行环境中，尾调用没有优化，但在 nodejs 环境中有优化。

## 标准库

标准库(标准 API)

- 库：liberary
- API： 应用程序编程接口，Application Programing Interface
- 标准：ECMAScript 标准

### Object 和 Function

Object 构造函数为给定值创建一个对象包装器。Object 构造函数，会根据给定的参数创建对象

> Object 构造函数的属性

静态属性：通过构造函数名字调用的属性
静态方法：通过类名调用
**静态成员(构造函数找到成员)**
构造函数 Object.进行调用

Object.Keys() 得到所有属性名组成的数组 //(键值对：数组名数组值)
Object.values() 得到所有属性值的数组  
Object.entries() 既包含属性名又包含属性值

> Object 实例 和 Object 原型对象

**实例成员**

> 实例成员可以被重写

通过对象 obj.进行调用，而不是构造函数 Object.

obj.prototype.toString() 返回该对象字符串格式 //[object object]
obj.prototype.valueOf() 得到某个对象的值 //默认情况下，返回该对象本身

> 在 JS 中，挡自动的进行类型转换时，如果要对一个对象进行转换，实际上是先调用对象的 valueOf 方法，然后调用返回结果的 toString 方法，将得到的结果进行进一步转换

> 如果调用了 valuOf 已经得到了原始类型，则不再调用 toString

```
var obj={
    x:13,
    y:34534,
    valueOf{
        renturn 123;
    }
}
console.log(obj+1);     ---->124
```

**所有对象，都拥有 Object 的所有实例成员**

> Function
> 构造函数创建一个新的 Function 对象，每个函数实际上都是一个 function 对象
> 所有函数都具有 Function 中的实例成员

arguments：在函数中使用，获取该函数调用时，传递的所有参数
arguments 类数组也称伪数组：没有通过 Array 构造创建的类似数组结构的对象，会缺少大量的数组实例方法
arguments 数组中的值会与对应的形参映射对应

#### 实例成员(Function 的对象，函数)

obj.length 参数个数
sayHello.apply() //调用函数改变 this 指向，参数以数组传递
obj.call() //参数以列表传递
.bind //需 new 一个新函数，该函数中的 this 始终指向指定的值。可直接多次调用函数

通常以 apply，call 方法，将某个伪数组转换伪真数组

[].slice() //不传参，表完整新数组
//将 arguments 转换为真数组
var newArr=[].slice.call(arguments) /// !!

var newFunc=sayHello.bind(user1,1,2);

### Array 构造器

```
abc是Array的静态方法    //实例调用
Array.abc();


abc是Array的实例方法    //对象调用
var aa=new Array();
aa.abc;

```

凡是通过 Array 构造函数创建的对象，都是数组

#### 静态成员

- Array.from() //伪数组转化为真数组
  var newArr =Array.from(arguments);

- Array.isArray(arguments) 判断是否是数组

- Array.of() //类似中括号创建数组，依次赋予数组每一项的值

#### 实例成员

- arr.fill(abc)：填充替换为固定值

- arr.pop 从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。

- arr.push 将一个或多个元素添加到数组的末尾，并返回该数组的新长度。

- arr.reverse 将当前数组颠倒顺序

- arr.shift 从数组中删除第一个元素，并返回该元素的值。

- arr.sort 对数组元素进行排序，并返回当前数组(按照编码排序，而不是数组大小排)
  arr.sort(function(a,b){return a-b}) //可传回调函数进一步判断
  随机打乱顺序 return Math.random()-0.5

- arr.splice myFish.splice(2, 1, "trumpet");  
  //从索引 2 的位置开始删除 1 个元素，插入“trumpet”

- arr.unshift 将一个或多个元素添加到数组的开头，并返回该数组的新长度(该方法修改原有数组)。

> 纯函数，无副作用函数：不会导致当前对象发生改变

- concat var newArr =arr1.concat(arr2,arr3);
  把 arr2 arr3 拼接到 arr1 并且赋值给新数组，不改变 arr1 的值

- includes  
  arr.includes(valueToFind[,fromIndex]) //.fromIndex 可选传入  
   arr.includes(67,3);从数组下标 3 的位置开始寻找，目标是 67
  值，[，指定位置开始寻找]
  数组中是否包含满足条件的元素

- join 连接所有数组元素组成一个字符串

- slice 抽取当前数组中的一段元素组合成一个新数组

- arr.forEach 遍历数组
  forEach 方法中的 function 回调有三个参数：
  第一个参数是遍历的数组内容，第二个参数是对应的数组索引，第三个参数是数组本身

```
var arr = [1,2,3,4];
var sum =0;
arr.forEach(function(value,index,array){

 array[index] == value; //结果为true

 sum+=value;

 });

console.log(sum); //结果为 10


```

arr.forEach(function(item){
console.log(item);
});

- every 所有都满足条件

- some 至少有一个同学及格

- filter 在所有过滤函数中返回 true 的数组元素放进一个新数组中并返回

- find 查找第一个满足条件的元素，返回元素本身，如果没有找到，返回 undefind
  var rusult =arr.find(function(item){
  return item.score>=60
  });

- map 映射

```
var newArr =arr.map(function(item,i){
    return{
        name:"学生"+(i+1),
        score：item
    }
})；

newArr=newArr.map(function(item){
    return item.name;
});

```

- reduce 统计(相加相乘)相加

var sum =reduce(function(s,item){
console.log(s,item);
return s+item;
})

> 链式编程，每个函数调用返回的类型一致
> var arr=[22,33,44,55,66,77,88];
> 先对数组随机排列
> 只取及格的分数
> 得到学生对象的数组(每个学生对象包含姓名和分数)

```
var result=arr.sort(function(){
    return Math.random()-0.5;
}).filter(function(item){
    return item>=60;
}).map(function(item,i){
    reutrn{
        name:'学生'${i+1},
        score:item
    }
});
console.log(result);

```

> 作业
> var arr=[1,2,3,4,5,6,-1,-2,-3,-4,-5,-6];
> 去掉数组中的负数，然后对每一项平方，然后再对每一项翻倍，然后求和

```
var result=arr.filter(function(item){
    return item>=0;
}).map(function(item){       //为什么不是reduce而是map(区别)
    return item*item*2;
}).reduce(function(s,item){
    return s+item;
})；
```

### 原始类型包装器

- new 包装器(值)：返回的是一个对象
- 包装器(值)：返回的是一个原始类型

#### Number

**静态成员**

- isNaN

- isFinite 是否是有限数

- isInteger 确定是 number 且是整数

- parseFloat 将一个数据转化为小数 //先转化为字符串再转化为数字

- parseInt 将数据转化为整数，可传第二个参，表将给定的字符串识别为多少进制
  //从字符串开始位置进行查找，找到第一个有效数字进行转换，如果没有找到，则返回 NaN

> 得到一个最小值到最大值之间的随机整数

```
举例
Math.random()   0/1
Math.random()*11   0/11
Math.random()*11+1   1/12
Math.random()*7+3      3/10
Math.random()*(max-min)+min  min/max


getRandom:function(min,max){
    ret.urn parseInt(Math.random()*(max-min)+min);
}
```

**实例成员**

- toFixed 保留几位小数 会四舍五入

- toPrecision 以指定精度返回 ，保留几位数

#### Boolean

#### String

**静态方法**
String.fromCharCode() //通过 Unicode 编码创建字符串

String.fromCodePoint() //通过一串码点创建字符串

**实例方法**

- length() 字符串长度

- charAt() 返回指定位置的字符

- charCodeAt() 返回给定索引的字符的 Unicode 值

- concat() 连接两个字符串文本，并返回一个新字符串

- includes() 判断一个字符串是否包含其他字符串

- endsWith() 判断结尾是否以其字符串结尾

- startsWith() 判断是否以其字符串开头

- indexOf() 返回首个被发现给定值的索引值，如果没有找到返回-1

- padStart(7，\*) 不足 7 位前面填充\*

- padEnd( , ) 末尾填充

- repeat() 返回指定重复次数由元素组成的字符串对象

- slice() 从某个位置取到某个位置，位置可以是负数

- substr(a,b) 从 a 开始取长度为 b 字符串 ，位置可以是负数

- substring(a，b) 从 a 开始取到 b 结束的字符串，不可以是负数，参数位置是可调换

- toLowerCase() 将字符串转化为小写

- toUpperCase() 将字符串转化为大写

- trim() 去掉首尾空格，账户密码校验

- split() 分隔字符串组成数组

> 作业：以下练习使用之前的通用函数

1. 找到某个字符串中出现最多的字符，打印字符和它出现的次数

```
getTopFreqInArray:function(arr){
    var records ={};
    for(var i=0;i<arr.length;i++){
        var n=arr[i];
        if(records[n]){
            records[n]++;
        }else{
            records[n]=1;
        }
    }
    var result;
    for (var prop in records){
        if(!result||records[prop]>result.frequency){
            result={
                number:prop,
                frequency:records[prop]
            };
        }
    }
    return result;
}

var s="ofoivjsojdijwfpefjwf"
var arr=Array.from(s);      //伪变成真数组
var obj=getTopFreqInArray(arr);
console.log(obj);

```

2. 将一个字符串中单词之间的空格去掉，然后把每个单词首字母转化成大写

```
1.
var s="hello\t world\n  \rjs";

function bigCamel(s){
    var result="";
    var empties=" \t\r\n";
    for(var i=0;i<s.length;i++){
        if(!empties.includes(s[i])){        //要是有空白字符就进不了
            //判断s[i]是否为首字母
            //s[i-1]是否是空白字符
            if(empties.includes(s[i-1])|| i==0){
                result+=s[i].toUpperCase();
            }else{
                result+=s[i];
            }
        }
    }
    return result;
}

```

```
2.
var s="hello  woRldd   js";
function bigCamel(s){
    //只考虑空格
    return s.split(" ").filter(function(item){
        return item.length>0;
    }).map(function(item){
        return item[0].toUpperCase()+item.substring(1).toLowerCase();
    }).join("");
}

console.log(bigCamel(s));
```

3. 书写一个函数，产生一个指定长度的随机字符串，字符串中只能包含大写字母，小写字母，数字

```
getRandom:function(min,max){
    return parseInt(Math.random()*(max-min)+min);
}

function getRandomString(len){
    var template="";    //字符串模板
    for(var i=65;i<65+26;i++){
        template +=String.fromCharCode(i);
    }
    for(var i=97;i<97+26;i++){
        template +=String.fromCharCode(i);
    }
    for(var i=48;i<48+10;i++){
        template +=String.fromCharCode(i);
    }
    console.log(template);

    var result="";
    for(var i=0;i<len;i++){
            //从模板中随机取出一位字符
            var index =getRandom(0,template.length-1);
            result+=template[index]；
    }
    return result;

}

console.log(getRandomString(6));

```

4. 将字符串按照字符编码的顺序重新升序排序

```
var s="bafosfwefsdfsdfoij";
var result=Array.from(s).sort().join("");
```

5. 从一个标准身份证号中提取用户的出生年月和性别，保存到对象中
   例如，"524713199703020014"
   得到对象
   birthYear:1997
   birthMonth:3
   birthDay:2
   gender:男 //倒数第二位，奇为男偶为女

```
function getInfoFromPID(pid){
    return{
        birthYear:parseInt(pid.substr(6.4)),
        birthMonth:parseInt(pid.substr(10,2)),
        birthDay:parseInt(pid.substr(12,2)),
        gender:pid[pid.length-2]%2===0?"女"："男"
    }
}

console.log(getInfoFromPID("524713199703020014"))

```

### Math 对象

- Math.randown 方法 产生一个 0-1 之间的随机数

- Math.PI 圆周率

- Math.abs(x)方法 返回 x 的绝对值

- Math.floor()方法 返回小于 x 的最大整数(向下取整)

- Math.ceil 方法 对一个数向上取整

- Math.max 方法 得到一组数字的最大值

- Math.min 方法 得到一组数字的最小值

- Math.pow(x,y) 返回 x 的 y 次幂

- Math.round(x) 返回四舍五入后的整数

### Date 构造器

1. 时间单位
   年(year)
   月(month)
   日(date)
   小时(hour)
   分钟(minute)
   秒(second) =1000ms
   毫秒(millisecond) =1000us
   微秒(microsecond) =1000ns
   纳秒(nanosecond)

2. UTC 和 GMT
   世界划分为 24 个时区，北京在东八区，格林威治在 0 时区

GMT：Greenwish Mean Time 格林威治世界时。太阳时，精确到毫秒。
UTC：Universal Time Coodinated 世界协调时。以原子时间为计时标准，精确到纳秒

UTC 和 GMT 之间误差不超过 0.9 秒

3. 时间戳
   数字

1970-1-1 凌晨 到 某个时间 所经过的毫秒数
2 的 32 次方 68 年后 现内存变大为 2 的 64 次方

#### 创建时间对象

- 直接调用函数(不适用 new)，忽略所有参数，直接返回当前时间的字符串
- newDate():创建日期对象

1. 无参，当前时间
2. 1 个参数，参数为数字，表示传入的是时间戳
3. 两个参数以上，分别表示年,月,日,时,分,秒,毫秒

注意：月份的数字从 0 开始计算

如果缺失参数，日期部分默认为 1，时分秒毫秒默认为 0

月，日，时，分，秒，毫秒，均可传递负数，如果传递负数，会根据指定日期进行计算。

#### 实例成员

- .getDate()方法 //得到今天多少号 (.getUTCDate(格林威治时间))

- .getDay()方法 //得到今天星期几 (0/6，星期天是 0 开始)

- .getFullyear //得到年份

- .getMonth //得到月，从 0 开始计算

- .getHours //得到小时

- .getMinutes //得到分钟

- .getSeconds //得到秒

- .getMilliseconds //得到毫秒

- .getTime //得到时间戳

get 变成 set

- toDateString:将日期部分转换为可读的字符串

- toISOString:将整个对象转化为标准的 ISO 格式

- toLocaleDateString:根据本地系统的地区设置将日期部分来转换为可读的字符串

- toLocaleString:根据当前系统的地区设置，将整个日期对象转化为可读的字符串

### 正则表达式

正则表达式是国际标准，跨越语言

正则表达式是一个规则，用于验证字符串

#### 基础

1. 字面量匹配
   规则中直接书写字面量字符

2. 特殊字符

```
.   //匹配所有字符(除换行符之外)
^   //匹配字符串开始
$   //字符串末尾结束

```

3. 转义符

\n //换行符
\r //回车符
\s //任何空白字符(空格，制表符，换页符)[\f\n\r\t\v]
\S //匹配任何非空白字符[^\f\n\r\t\v]
\t //制表符
\v //垂直制表符
\b //单词边界
\d //匹配数字
\D //非数字
\w //字母数字下划线 [A-Za-z0-9]
\u //Unicode 编码

转义字符可将特殊字符转义 \.

4. 字符集
   [0-9a-zA-Z_]
   字符范围

[^字符范围]加在中括号前面是对字符范围取反

匹配中文：`[\u4e00-\u9FA5]`

5. 量词

前面的规则出现的次数

```
*   //匹配0次或多次任意次数
+   //匹配1个或多个
?   //匹配0个或1个
{n} //匹配n个
{n,}//匹配>=n个
{n,m}//匹配n-m个
括号只针对于前面一项

```

6. 或者
   多个规则之间，适用或者`|`一条竖线，表示多个规则任选其一

> 作业

1. 写一个正则表达式匹配手机号
   11 位，第一位是 1
   ^[1\d{10}]\$
2. 姓名必须是 3-6 位的中文
   ^[(\u4e00-\u9FA5){3,6}]\$
3. 密码必须是 6-12 位的字符，只能包含数字，字母，下划线
   ^\w{6,12}\$
4. 写一个正则表达式匹配邮箱
   xxxxxx@xxxx.xxxx.xxx
   ^[0-9a-zA-Z]+@[0-9a-zA-Z]+.[0-9a-zA-Z]+(.[0-9a-zA-Z])?\$

^\w+@\w+(\.\w+){1,2}\$

5. 匹配一个座机号
   xxx-xxxxxxx
   前面：1-3 位数
   后面：4-8 位数

^[0-9]{1,3}-[0-9]{4,8}\$

^\d{1,3}-\d{4,8}$
6. 匹配一个正数
^\d+(\.\d+)?$

7. 匹配一个小数
   ^-?\d+\.\d+\$

8. 匹配一个整数

^-?\d+(.\0+)\$

#### JS 中的应用

js 中，正则表达式表现为一个对象，该对象是通过构造函数 RegExp

> 创建正则对象

/pattern/
new RegExp(pattern [,flags]) //新的对象规则一样地址改变不一致
RegExp(pattern[,flags])

标志位 flags g i m  
global 全局搜索 ignoreCase 大小写 multiline 多行匹配
同传字符串没问题
但如果把字符串赋值当参数传入，则用 new 好

> 正则实例成员

- global 是否开启了全局属性(只读)

- ignoreCase 是否开启了大小写

- multiline 是否开启多行匹配

- source 目前规则(源模式文本)

- lastIndex 下次匹配开始字符串索引位置

- test 方法 测试当前正则是否能匹配目标字符串
  (全局模式下和非全局模式不一样却全局输数)且在全局属性下，往后面移动影响下一次匹配位置，匹配不了才复位
  \d+正则表达式默认情况，适用贪婪模式。\d+?取消贪婪模式

```
var reg=/abc/g;             //关键在于有没有开启全局匹配
var s="111abc111abc111";
//判断匹配多少处
var n=0；
while(reg.test(s)){
    n++;
}
console.log('匹配了${n}次')

console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
console.log(s,reg.lastIndex,reg.test(s),reg.lastIndex);
```

- exec 方法：execute,执行匹配，得到匹配结果
  (匹配结果，下标，输入字符)

//得到所有的匹配结果和位置

1.  while(true){
    var result= reg.exec(s);
    if(!result){
    break;
    }
    console.log('匹配结果:${result[0]},出现位置：${result.index}');
    }
2.  var result;
    while(result=reg.exec(s)){
    console.log('匹配结果:${result[0]},出现位置：${result.index}');
    }

#### 字符串对象中的正则方法

- string.match()
  字符串匹配表达式

```
var s="1234abc123aaa";
var result=s.match(/\d+/g)
console.log(s,result);
//1234abc123aaa (2)["1234","123"]
```

- string.search() //对正则表达式和指定字符串进行匹配，返回第一个出现的匹配项下标

```
var s="1234abc123aaa";
var result=s.search(/\d+/g)
console.log(s,result);
//1234abc123aaa 0
```

- string.split() //分隔字符

```
var result=s.split(/[, \-\s]/);
console.log(s,result);
```

- string.replace() //替换字符串

```
//将空白字符替换为逗号
console.log(s);
s=s.replace(/\s/g,",");
console.log(s);

2.首字母变大写(第二个参数传函数)
s=s.replace(/\b[a-z]/g,function(match){
    return match.toUpperCase();
});
console.log(s);

3.驼峰命名法            //***********************************************
s=s.replace(/\s*\b[a-z]\s*/g,function(match){
    console.log(math,match.length);
    return match.toUpperCase().trim();
});
console.log(s);
```

> 作业

1. 书写一个正则表达式，去匹配一个字符串，得到匹配的次数，和匹配的结果

```
var reg=/\d{3}/g;
var s="1321wfef123wfewf132";
var n=0;
var str="";
while(result=reg.exec(s)){
    n++;
    str+=result[0]+"\n";
}
str='匹配${n}次\n'+str;
console.log(str);
```

2. 得到一个字符串中中文字符的数量

```
var reg=/[\u4e00-\u9fa5]/g;
var s="放假哦按双方13412aaa"
var n=0;
while(reg.test(s)){
    n++;
}
console.log(n);
```

3. 过滤敏感词，有一个敏感词数组，需要将字符串中出现的敏感词替换成四个星号
   ["共产党","too young too simple","营销"]

```
var senWords=["色情","暴力,"卢本伟","贸易战","毒品"]；
将字符串中敏感词汇替换成为指定的字符串
function removeSensitiveWords(s,rep){
    var reg=new RegExp(senWords.join("|"),"g");             //g什么意思********************************
    return s.replace(reg,rep);
}

console.log(removeSensitiveWords("ihwe色情暴力gioi贸易战ui菲【4毒品"，iii))；


连着的直接用一次(贪婪匹配)
function removeSensitiveWords(s,rep){
    var reg=new RegExp('(${senWords.join("|")})+',"g");
    return s.replace(reg,rep);
}
```

4. 得到一个 html 字符串中出现的章节数量

```
var reg=/<h2>第\d+章<\/h2>/g;
var result=html.match(reg);
if(result){
    console.log(result.length)
}
else{
    console.log(0);
}

```

正则表达式 3 .。。。

#### 进阶

##### 捕获组

用小括号包裹的部分叫做捕获组，捕获组会出现在匹配结果中?数组形式
捕获组可以命名?<\*\*\*>具名捕获组

```
var s="2015-5-1,2019-4-19,2000-04-28"
得到每一个日期，并得到每个日期的年月日

var reg=/(?<year>\d{4})-(?<month>\d{1,2})-(?<day>\d{1,2})/g;
while(result=reg.exec(s)){
    console.log(result[0],result.groups.year,result.groups.month,result.groups.day)
}
```

```
var s="2015-5-1,2019-4-19,2000-04-28";
var reg=/(\d{4})-(\d{1,2})-(\d{1,2})/g;
s=s.replace(reg,function(match,g1,g2,g3){   //第二个参数传"$1/$2/$3"表捕获组
    console.log(match,g1,g2,g3);
    return'${g1}/${g2}/${g3}';
})
console.log(s);

```

非捕获组(加小括号只是为了变一个整体，不是真正捕获)
(?:\d{4})

##### 反向引用

在正则表达式中，使用某个捕获组 \捕获组编号

```
var reg=/(\d{2})\1/;        //重复捕获1313才满足条件
var s ="1312"；
console.log(reg.test(s));
```

```
var s="aaaaaaaabbbbbbbbbbbccccccccdefgggg";
//找出该字符串中连续的字符
var reg=/(\w)\1+/g;
while(result=reg.exec(s)){
    console.log(result[1]);
}
```

##### 正向断言(预查)

检查某个字符后面的字符是否满足某个规则，该规则不称为匹配结果，并且不称为捕获组
只做检查满足条件不作为输出(?=\d+)

```
var s="sdfasfs2afsdfef223ewef223";
var reg=/[a-zA-Z](?=\d+)/g;
while (result=reg.exec(s)){
    console.log(result);
}
```

```
面试题
var s="6266515";
//var result="6,266,515";
var reg=/\B (?=(\d{3})+$)/g;   //检查空字符后面得出现三个数的倍数****************************
s=s.replace(reg,",");
console.log(s);

```

##### 负向断言(预查)

检查某个字符后面的字符是否不满足某个规则，该规则不成为匹配结果，并且不称为捕获组
只做检查不满足条件不作为输出()

```
var s="fw16255fwioje443";
var reg=/[a-zA-Z](?!\d+)/g;
while (result=reg.exec(s)){
    console.log(result);
}
```

```
密码判断
要求密码中必须出现小写字母，大写字母，数字，特殊字符(!@#_,.) ,6-12位
正向预查检查空字符后面是否出现了满足条件的，检查通过再匹配任意字符出现次数
var s="154dfA51.";
var reg=/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#_.]).{6,12}$/;     //(?=.*[a-z])只是检查是否存在，不管之前有什么，位数要满足
console.log(reg.test(s));
```

```
判断密码强度
密码长度必须是6-12位
出现小写字母，大写字母，数字，特殊字符  强
出现小写字母，大写字母，数字           中
出现小写字母，大写字母                 轻
其他                                不满足要求

function judgePwd(pwd){
   if(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#_.])/).{6,12}$/.test(pwd){
       return "强";
   }else if(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{6,12}$/.test(pwd)){
       return"中";
   }else if(/^(?=.*[a-z])(?=.*[A-Z]).{6,12}$/.test(pwd)){
       return"轻";
   }else{
       return "不满足";
   }
}
console.log(judgePwd("pwd"))
```

### 错误处理

Js 中的错误分为：

1. 语法错误:会导致整个脚本块无法执行。 //Uncaught SyntaxError:Unexpected token
2. 运行错误
   1. 运行报错:会导致当前脚本块后续代码无法执行 //Uncaught ReferenceError:
   2. 运行结果不符合预期

#### 调试错误

1. 控制台打印
2. 断点调试

#### 抛出错误

错误在 js1 中本质是一个对象，抛出错误的语法为

```js
throw 错误对象;
```

throw new Error
错误堆栈：isPrie->全局环境->浏览器

#### 捕获错误

```
try{
    //代码一
}
catch(错误对象){
    //代码2
}
finally{
    //代码块3
}
```

当运行代码 1 的时候，如果发生错误，立即停止代码 1 的执行，转而执行代码 2，错误对象为抛出的错误对象，无论代码 1 和代码 2 是否，最终都要执行代码 3.

## dom 核心

### web api 概述

标准库：ECMAScript 中的对象和函数

浏览器宿主环境

web Api:浏览器宿主环境中的对象和函数

1. 知识繁杂

2. 成体系的知识

3. 程序思维

4. 兼容性：了解，不记忆

webApi:

- BOM:Browser Object Model ，浏览器对象模型
- Dom:Document ObjectModel, 文档对象模型

BOM 控制浏览器本身
Dom 控制 HTML 文档

ES 由 ECMAScript 规定的
WebApi 由 W3C 万维网联盟制定

**DOM 是什么**
Dom 的核心理念，将一个 html 或 xml 文档，用数字称为 dom 对象
dom 对象又称之为节点 Node
节点类型：

- DocumentType,文档类型节点
- Document，文档节点，表示整个文档
- Comment,注释节点
- Element，元素节点
- Text：文本节点
- Attribute，属性节点
- DocumentFragment，文档片段节点

dom 树：文档中不同节点形成的树形结构

### 获取 dom 节点

获取 dom 对象

> 全局对象 window 中有属性 document，代表的是整个文档节点

#### 旧的获取元素节点的方式

dom 0

- document.body:获取 body 元素节点

- document.head：获取 head 元素节点

- document.links:获取页面上所有的超链接元素节点，类数组

- document.anchrors：获取页面上所有的锚链接(具有 name 属性)元素节点

- document.forms：获取页面中所有的 form 元素节点

#### 新的获取元素节点的方式

##### 通过方法获取

- document.getElementById:通过 id 获取对应 id 的元素

- document.getElementsByTagName:通过元素名称获取元素

- document.getElementsByClassName:通过元素的类样式获取元素，IE9 以下无效

- document.getElementsByName:通过元素的 name 属性值获取元素

- document.querySelector:通过 css 选择器获取元素，得到匹配的第一个，IE8 以下无效

- document.querySelectorAll:通过 css 选择器获取元素，得到所有匹配的结果，IE8 以下无效

- doucument.documentElement:获取根元素

细节：

1. 在所有的得到类数组的方法中，除了 querySelectorAll，其他地方都是实时更新。
2. getElementByID 得到元素执行效率最高
3. 书写了 id 的属性，会自动成为 window 对象的属性。它是一个实时的单对象，事实上的标准不推荐使用
4. getElementsByTagName，getElementsByClassName，querySelector，querySelectorAll，可以作为其他元素节点对象的方法使用

##### 根据节点关系获取节点

- parentNode:获取父节点，父元素

- previousSibling：获取上一个兄弟节点

- nextSibling：获取下一个兄弟节点

- childNodes： 获取所有的子节点

- firstChild ：获取第一个子节点

- lastChild:获取最后一个子节点

- attributes:获取某个元素的属性节点

获取元素节点

- parentElement:获取父元素

- previousElementSibling:获取上一个兄弟元素

- nextElementSibling:获取下一个兄弟元素

- children：获取子元素

- firstElementchild：获取第一个子元素

- lastElementChild：获取最后一个子元素

#### 获取节点信息

- nodeName：获取节点名称
- nodeValue：获取节点的值
- nodeType:节点类型，是一个数字

> 作业

1. //得到某个元素下面的所有 a 元素的内容数组

```
function getLinkContents(dom){
    return Array.from(dom.getElementsByTagName("a")).map(function(a){
        return a.firstChild.nodeValue;
    })
//    var arr=dom.getElementsByTagName("a");//a元素数组
//    var newArr=[];
//    for(var i=0;i<arr.length;i++){
//        var a =arr[i];
//        newArr.push(a.firstChild.nodeValue);
//    }
//    return newArr;
}
list1Links=getLinkContents(document.getElementById("list1"))
console.log(list1Links);
```

2. //写入一个函数，传入一个 dom 对象，返回该对象的第一个 div 容器

```
function getDivContainer(dom){
    var parent =dom.parentElement;
    while (parent&&parent.nodeName !=="DIV"){
        parent=parent.parentElement;
    }
    return parent;
}

var div=getDivContainer(document.querySelector(".container").getElementsByTagName("a")[2]);
console.log(div);
```

### dom 元素操作

#### 初始元素事件

元素事件：某个元素发生一件事(被点击 click)
事件处理程序：发生了一件事，应该做什么事情
注册事件：将事件处理程序与某个事件关联

#### 获取和设置元素属性

- 通用方式：getAttribute，setAttribute

1. 可识别属性
   正常的 HTML 属性

- dom 对象.属性名：推荐

```
//获取文本框内容，设置文本框内容
<input type="text"value="abcsf">
<button id="btnGetTxt">获取文本框内容</button>
<button id="btnSetTxt">设置文本框内容</button>
<script>
    var input=document.querySelector("input[type=text]");
    document.getElementById("btnGetTxt").onclick=function(){
        //获取文本框的值
        console.log(input.value);
    }
    document.getElementById("btnSetTxt").onclick=function(){
        input.value="请输入文本";
    }
</script>
```

```
//点击切换图片
var i=1;
var img=document.querySelector("img");
img.onclick=function(){
    i++;
    if(i===3){
        i=1;
    }
    img.src=i+".jpg";
}
```

细节： 1. 正常的属性即使没有辅助，也有默认值 2. 布尔属性在 dom 对象中，得到的是 boolean 3. 某些表单元素可以获取到某些不存在的属性 4. 某些属性与标识符冲突，此时，需要更换属性名

```for属性点性别也可选中表单
<input id="asdfg" type="checkbox"><label for="asdfg">男</label>
```

2. 自定义属性

HTML5 建议自定义属性使用`data-`作为前缀
如果遵从 HTML5 自定义属性规范，可以使用`dom对象.dataset.属性名`控制属性
删除自定义属性

- removeAttribute("属性名");
- delete dom.dataset.属性名

#### 获取和设置元素的内容

- innerHTML:获取和设置元素内部 HTML 文本
- innerText:获取和设置元素内部的纯文本，仅得到元素内部部分得到文本
- textContent：获取和设置元素内部的纯文本，textContent 得到的是内部所有的文本

#### 元素结构重构

- 父元素.appendChlid(元素):在某个元素末尾加入一个子元素

```
var li=ul1.getElementsByTagName("li")[3]
ul2.appendChild(li);
```

- 父元素.insertBefore(待插入的元素，哪个元素之前)
- 父元素.replaceChild(替换的元素，被替换的元素)

细节：
更改元素结构效率较低，尽量少用。

#### 创建和删除元素

1. 创建元素
   document.createElement("元素名")：创建一个元素对象
   - document.createTextNode("文本")
   - document.createDocumentFragment()：创建文档片段

```
var ul =document.getElementById("ul1");
var frag=document.createDocumentFragment();
for (var i=1; i<=100;i++){
    var li=document.createElement("li");
    li.innerText="选项"+i;
    frag.appendChild(li);
}
ul.appendChild(frag);
```

2. 克隆元素

- dom 对象.cloneNode(是否深度克隆)：复制一个新的 dom 对象

> chidNodes 也是实时集合

3. 删除元素

- removeChild:父元素调用，传入子元素
- remove：把自己删除

> 作业

```
    <div class="container">
        <p>
            <button id="btnClear">清空</button>
        </p>
        <ul class="list">
            <li>项目1<button>删除</button></li>
            <li>项目2<button>删除</button></li>
            <li>项目3<button>删除</button></li>
            <li>项目4<button>删除</button></li>
            <li>项目5<button>删除</button></li>
        </ul>
    </div>
    <script>
        //得到ul下的所有按钮**************************************
        var btnClear = document.getElementById("btnClear");
        var ul = document.querySelector(".list");
        btnClear.onclick = function() {
            ul.innerHTML = "";
        }


        var btns = ul.querySelectorAll("button");
        Array.from(btns).forEach(function(b) {
            b.onclick = function() {
                b.parentNode.remove();
            }
        })

        // for (var i = 0; i < btns.length; i++) {
        //     var b = btns[i]; //得到当前按钮
        //     // (function(b) {
        //     //     b.onclick = function() {
        //     //         b.parentNode.remove();
        //     //     }
        //     // }(b));

        for (var i = 0; i < btns.length; i++) {
        //     var b = btns[i]; //得到当前按钮
               regEvent(b);//通过函数固定变量值
        }
        function regEvent(btn){
            btn.onclick=function(){
                console.log(btn,btn.parentNode);
            }
        }


        1.
        //     b.onclick = function() {
        //         this.parentNode.remove();
                    //b.parentNode不行有变量提升
        //     }
        // }
    </script>
```

```库存添加器
//
    <p>
        库存的最小值为0
    </p>
    <div>
        库存：
        <button data-plus="-1000">-1000</button>
        <button data-plus="-100">-100</button>
        <button data-plus="-10">-10</button>
        <button data-plus="-1">-</button>
        <span id="spanNumber">10</span>
        <button data-plus="1">+</button>
        <button data-plus="10">+10</button>
        <button data-plus="100">+100</button>
        <button data-plus="1000">+1000</button>
    </div>

    <script>
        var btns = document.querySelectorAll("button");
        var span = document.getElementById("spanNumber");
        for (var i = 0; i < btns.length; i++) {
            var b = btns[i];
            b.onclick = function() {
                var num = parseInt(span.innerText);
                //加某个数
                var plus = parseInt(this.dataset.plus);
                var result = num + plus;
                if (result < 0) {
                    result = 0;
                }
                span.innerHTML = result;
            }
        }
    </script>


```

```添加列表
//
  <div class="container">
        <p>不能添加空的文本</p>
        <div class="input">
            <input type="text">
            <button id="btnAdd">添加</button>
        </div>
        <ul class="list">
            <li>项目1</li>
            <li>项目2</li>
        </ul>
    </div>
    <script>
        var btnAdd = document.getElementById("btnAdd");
        var ul = document.querySelector(".list");
        var inp = document.querySelector("input");
        var p = document.querySelector("p");
        btnAdd.onclick = function() {
            if(!inp.value.trim()){
                p.className = "error";
                return;
            }
            p.className = "";
            var li = document.createElement("li");
            li.innerText = inp.value;
            inp.value = "";
            ul.appendChild(li);
        }

```

```穿梭框，点击左右移动
//
    <div class="container">
        <div class="left">
            <h2>成哥的现任女友</h2>
            <select id="sel1" multiple>
                <option value="1">幂幂</option>
                <option value="2">花花</option>
                <option value="3">春春</option>
                <option value="4">盈盈</option>
                <option value="5">红红</option>
            </select>
        </div>
        <div class="left mid">
            <p>
                <button id="btnToRight" title="右移动选中的">&gt;&gt;</button>
            </p>
            <p>
                <button id="btnToRightAll" title="右移动全部">&gt;&gt;|</button>
            </p>
            <p>
                <button id="btnToLeft" title="左移动选中的">&lt;&lt;</button>
            </p>
            <p>
                <button id="btnToLeftAll" title="左移动全部">|&lt;&lt;</button>
            </p>
        </div>
        <div class="left">
            <h2>成哥的前女友</h2>
            <select id="sel2" multiple>
                <option value="6">坤坤</option>
            </select>
        </div>

    </div>

    <script>
        var btnLeft = document.getElementById("btnToLeft"),
            btnRight = document.getElementById("btnToRight"),
            btnLeftAll = document.getElementById("btnToLeftAll"),
            btnRightAll = document.getElementById("btnToRightAll"),
            selLeft = document.getElementById("sel1"),
            selRight = document.getElementById("sel2");

        //得到某个select元素内部被选中的option数组
        function getSelectedOptions(sel) {
            return Array.from(sel.children).filter(function(item) {
                return item.selected;
            });
            // var opts = [];
            // for (var i = 0; i < sel.children.length; i++) {
            //     if (sel.children[i].selected) {
            //         opts.push(sel.children[i]);
            //     }
            // }
            // return opts;
        }

        //将option数组中的东西添加到制定的select中
        //opts: 要添加的option数组
        //sel：要添加到的select元素
        function appendToSelect(opts, sel) {
            opts = Array.from(opts);
            var frag = document.createDocumentFragment();
            for (var i = 0; i < opts.length; i++) {
                opts[i].selected = false;
                frag.appendChild(opts[i]);
            }
            sel.appendChild(frag);
        }

        btnLeft.onclick = function() {
            //获取右边选中的
            var opts = getSelectedOptions(selRight);
            //循环将该数组添加到左边的select中
            appendToSelect(opts, selLeft);
        }

        btnRight.onclick = function() {
            //获取右边选中的
            var opts = getSelectedOptions(selLeft);
            //循环将该数组添加到左边的select中
            appendToSelect(opts, selRight);
        }

        btnLeftAll.onclick = function() {
            appendToSelect(selRight.children, selLeft);
        }

        btnRightAll.onclick = function() {
            appendToSelect(selLeft.children, selRight);
        }
    </script>
```

### dom 元素样式

- className:获取或设置元素的类名
- classList：dom4 的新属性，是一个用于控制元素类名的对象
  - add:用于添加一个类名
  - remove：用于移除一个类名
  - contains:用于判断一个类名是否存在
  - toggle:用于添加/移除一个类名

#### 获取样式

**css 的短横线命名法需要转换为小驼峰命名**

- dom.style:得到**行内样式**对象
- window.getComputedStyle(dom 元素)：得到某个元素最终计算的样式

#### 设置样式

dom.style.样式名=值
设置的是行内样式

> 作业

1. 选中效果

2. 随机背景色

3. 放大和缩小

4. 扑克牌

```
 <div id="divcontainer">

    </div>

    <script>
        var div = document.getElementById("divcontainer");
        var imgs = [];
        for (var i = 1; i <= 13; i++) {
            for (var j = 1; j <= 4; j++) {
                imgs.push(createImg(`pokers/${i}_${j}.jpg`));
            }
        }
        imgs.push(createImg(`pokers/14_1.jpg`));
        imgs.push(createImg(`pokers/15_1.jpg`));
        imgs.sort(function() {
            return Math.random() - 0.5;
        });

        imgs.forEach(function(img){
            div.appendChild(img);
        });

        function createImg(src) {
            var img = document.createElement("img");
            img.src = src;
            img.style.margin = "30px";
            return img;
        }
    </script>
```

5. 拼图

##### 拼图********\*\*********\*\*********\*\*********

```
/**
 * 游戏配置
 */
var gameConfig = {
    width: 500,
    height: 500,
    rows: 3, //行数
    cols: 3, //列数
    isOver: false, //游戏是否结束
    imgurl: "img/lol.png", //图片路径，注意：相对的是页面路径
    dom: document.getElementById("game") //游戏的dom对象
};
//每一个小块的宽高
gameConfig.pieceWidth = gameConfig.width / gameConfig.cols;
gameConfig.pieceHeight = gameConfig.height / gameConfig.rows;
//小块的数量
gameConfig.pieceNumber = gameConfig.rows * gameConfig.cols;

var blocks = []; //包含小方块信息的数组

function isEqual(n1, n2) {
    return parseInt(n1) === parseInt(n2);
}

/**
 * 小方块的构造函数
 * @param {*} left
 * @param {*} top
 * @param {*} isVisible 是否可见
 */
function Block(left, top, isVisible) {
    this.left = left; //当前的横坐标
    this.top = top; //当前的纵坐标
    this.correctLeft = this.left; //正确的横坐标
    this.correctTop = this.top; //正确的纵坐标
    this.isVisible = isVisible; //是否可见
    this.dom = document.createElement("div");
    this.dom.style.width = gameConfig.pieceWidth + "px";
    this.dom.style.height = gameConfig.pieceHeight + "px";
    this.dom.style.background = `url("${gameConfig.imgurl}") -${this.correctLeft}px -${this.correctTop}px`;
    this.dom.style.position = "absolute";
    this.dom.style.border = "1px solid #fff";
    this.dom.style.boxSizing = "border-box";
    this.dom.style.cursor = "pointer";
    // this.dom.style.transition = ".5s"; //css属性变化的时候，在0.5秒中内完成
    if (!isVisible) {
        this.dom.style.display = "none";
    }
    gameConfig.dom.appendChild(this.dom);

    this.show = function () {
        //根据当前的left、top，重新设置div的位置
        this.dom.style.left = this.left + "px";
        this.dom.style.top = this.top + "px";
    }
    //判断当前方块是否在正确的位置上
    this.isCorrect = function () {
        return isEqual(this.left, this.correctLeft) && isEqual(this.top, this.correctTop);
    }

    this.show();
}

/**
 * 初始化游戏
 */
function init() {
    //1. 初始化游戏的容器
    initGameDom();
    //2. 初始化小方块
    //2.1 准备好一个数组，数组的每一项是一个对象，记录了每一个小方块的信息
    initBlocksArray();
    //2.2 数组洗牌
    shuffle();
    //3. 注册点击事件
    regEvent();

    /**
     * 处理点击事件
     */
    function regEvent() {
        //找到看不见的方块
        var inVisibleBlock = blocks.find(function (b) {
            return !b.isVisible;***********************************************把flase的isVisible给return返回(是真的才返回)
        });
        blocks.forEach(function (b) {
            b.dom.onclick = function () {
                if (gameConfig.isOver) {
                    return;
                }
                //判断是可以交换(横纵坐标为0.1，1.0)
                if (b.top === inVisibleBlock.top &&
                    isEqual(Math.abs(b.left - inVisibleBlock.left), gameConfig.pieceWidth) ||
                    b.left === inVisibleBlock.left &&
                    isEqual(Math.abs(b.top - inVisibleBlock.top), gameConfig.pieceHeight)) {
                    //交换当前方块和看不见的方块的坐标位置
                    exchange(b, inVisibleBlock);
                    //游戏结束判定
                    isWin();
                }

                //交换当前方块和看不见的方块的坐标位置
                // exchange(b, inVisibleBlock);
                // //游戏结束判定
                // isWin();
            }
        })
    }

    /**
     * 游戏结束判定
     */
    function isWin() {
        var wrongs = blocks.filter(function (item) {
            return !item.isCorrect();******************************************************不匹配的return返回，ruturn的值是真的，那么item的值是假的
        });
        if (wrongs.length === 0) {
            gameConfig.isOver = true;
            //游戏结束，去掉所有边框
            blocks.forEach(function (b) {
                b.dom.style.border = "none";
                b.dom.style.display = "block";
            });
        }
    }

    /**
     * 随机数，能取到最大值
     * @param {*} min
     * @param {*} max
     */
    function getRandom(min, max) {
        return Math.floor(Math.random() * (max + 1 - min) + min);
    }

    /**
     * 交换两个方块的left和top
     * @param {*} b1
     * @param {*} b2
     */
    function exchange(b1, b2) {
        var temp = b1.left;
        b1.left = b2.left;
        b2.left = temp;

        temp = b1.top;
        b1.top = b2.top;
        b2.top = temp;

        b1.show();
        b2.show();
    }

    /**
     * 给blocks数组洗牌
     */
    function shuffle() {
        for (var i = 0; i < blocks.length - 1; i++) {
            //随机产生一个下标
            var index = getRandom(0, blocks.length - 2);
            //将数组的当前项与随机项交换left和top值
            exchange(blocks[i], blocks[index]);
        }
    }

    /**
     * 初始化一个小方块的数组
     */
    function initBlocksArray() {
        for (var i = 0; i < gameConfig.rows; i++) {
            for (var j = 0; j < gameConfig.cols; j++) {
                //i 行号，j 列号
                var isVisible = true;
                if (i === gameConfig.rows - 1 && j === gameConfig.cols - 1) {
                    isVisible = false;
                }
                var b = new Block(j * gameConfig.pieceWidth, i * gameConfig.pieceHeight, isVisible);
                blocks.push(b);
            }
        }
    }

    /**
     * 初始化游戏容器
     */
    function initGameDom() {
        gameConfig.dom.style.width = gameConfig.width + "px";
        gameConfig.dom.style.height = gameConfig.height + "px";
        gameConfig.dom.style.border = "2px solid #ccc";
        gameConfig.dom.style.position = "relative";
    }
}

init();


```

## dom 事件

- 事件：发生一件事
- 事件类型：点击鼠标按下，鼠标抬起，鼠标移入鼠标移出键盘按下，键盘抬起……

- 事件处理程序：一个函数，，当某件事情发生时运行
- 事件注册，将一个事件处理程序，挂载到某个事件上。

### 事件流

当某个事件发生的时候，哪些元素会监听到该事件发生，这些元素发生该事件的顺序。

事件冒泡：先触发最里层的元素，然后再依次触发外层元素
事件捕获：先触发外层的元素，然后再依次触发里面元素

目前，标准规定，默认情况下，事件是冒泡的方式触发。

捕获(body->btn)->源事件->冒泡(btn->body)

事件源，事件目标：事件目标阶段的元素

### 事件注册

事件绑定

#### dom0

将事件名称前面加上 on，作为 dom 的属性名，给该属性赋值为一个函数，即为事件注册

移除：重新给事件属性赋值，通常赋值为 null 和 undefined

#### dom2

dom 对象.addEventListener:(注册事件,函数，是否开启捕获)

与 dom0 的区别

1. dom2 可以为某个元素的同一个事件，添加多个处理程序按照注册的先后顺序运行
2. dom2 允许开发者控制事件处理的阶段(第三个参数控制捕获阶段)

如果元素是目标元素(事件源，最底层)，第三个参数无效

事件的移除：dom 对象.removeEventListener(事件名，处理函数)
dom2 中如果要移除事件，不能使用匿名函数，而是把函数写外面，传函数名

**细节**

1. dom2 在 IE8 以下不兼容，需要使用 attachEvent,datachEvent 添加和移除事件
2. 添加和移除事件时，可以将第三个参数写为一个对象，进行相关配置(onece 是否只运行一次，capture 是否开启捕获)

### 事件对象

事件对象封装了事件的相关信息

#### 获取事件对象

- 事件处理函数获取

```
打印事件对象event
var btn =document.querySelector("button")
btn.onclick=function(e){
    console.log(e);
}
```

- 旧版本的 IE 浏览器通过 window.event 获取
  e=e||window.event

#### 事件对象的通用成员

- target&srcElement
  事件目标(事件源)
  事件委托：通过给祖先元素注册事件，在程序处理程序中判断事件源进行不同的处理

通常，事件委托用于动态生成元素的区域

```
//点button删除语句
var div= document.querySelector("div")
div.onclick=function(e){
    if(e.target.tagName==="BUTTON"){
        e.target.parentElement.remove();
    }
}
```

- currentTarget
  当前目标：获取绑定事件的元素，等效于 this

- type
  字符串，得到事件的类型

- preventDefault&returnValue

e.preventDefault()方法，阻止默认浏览器行为

returnValue 配置 ie 浏览器已过时
dom0 中用 return false;

针对 a 元素，可以设置为功能性链接解决跳转问题
`<a href="javascript:;">baidu</a>`

- stopPropagation 方法

阻止事件冒泡

- eventPhase

得到事件所处的阶段

1. 事件捕获
2. 事件目标
3. 事件冒泡

> ##### 作业

```
2
```

### 鼠标事件

#### 事件类型

- click:用户单击主鼠标按钮(一般是左键)或者在聚焦时按下回车键时触发

- dbclick:用户双击主鼠标按键触发(频率取决于系统配置)

- mousedown：用户按下鼠标任意按键时触发

- mouseup：用户抬起鼠标任意按键时触发

- mousemove：鼠标在元素上移动时触发

- mouseover:鼠标在进入元素时触发
- mouseout：鼠标离开元素时触发

- mouseenter：鼠标进入元素时触发，该事件不会冒泡
- mouseleave:鼠标离开元素时触发，该事件不会冒泡
  区别: over 和 out 不考虑子元素，从父元素移动到子元素，对于父元素而言，仍算离开
  enter 和 leave，不考虑子元素，子元素仍然是父元素的一部分
  mouseenter 和 mouseleave 不会冒泡

##### 事件对象

所有的鼠标事件，事件处理程序中的事件对象，都为 MouseEvent

- altKey：触发事件时，是否按下了键盘的 alt 键
- ctrlKey:触发事件时，是否按下了键盘的 ctrl 键
- shiftKey：触发事件时，是否按下了 shift 键
- button：触发事件时，鼠标按键类型
  0 左键 1 中键 2 右键

位置：

- page:pageX，pageY，当前鼠标距离页面的横纵坐标
- client:clientX,clientY,鼠标相对于视口的坐标
- offset:offsetX,offsetY,鼠标相对于事件源的内边距的坐标(父元素左上角)
- screen:screenX,screenY,鼠标相对于屏幕
- x,y 等同于 clientX,clientY
- movement:movementX,movementY,只在鼠标移动事件中有效，相对于上一次鼠标位置，偏移的距离(移动的速度大小有关)

> 作业

1. 拖拽效果

###### 拖拽效果

      <style>
        div {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: rgb(247, 93, 93);
            cursor: move;
            position: absolute;
            left: 100px;
            top: 100px;
        }

        p {
            width: 100px;
            height: 100px;
            background: lightblue;
        }
    </style>

    <div>
        <!-- <p></p> -->
    </div>

    <script>
        var div = document.querySelector("div");
        div.onmousedown = function(e) {
            if (e.button !== 0) { //如果不是鼠标左键
                return;
            }
            var pageX = e.pageX;
            var pageY = e.pageY;
            var style = getComputedStyle(div);
            var divLeft = parseFloat(style.left);
            var divTop = parseFloat(style.top);
            window.onmousemove = function(e) {
                var disX = e.pageX - pageX;
                var disY = e.pageY - pageY;
                div.style.left = divLeft + disX + "px";
                div.style.top = divTop + disY + "px";
            }
        window.onmouseup = window.onmouseleave = function(e) {  //onmouseleave有必虑吗
                if (e.button === 0) {
                    window.onmousemove = null; //移除鼠标移动事件
                }
            }
        }

        // var div = document.querySelector("div");
        // var style = getComputedStyle(div);
        // var divLeft = parseFloat(style.left);
        // var divTop = parseFloat(style.top);
        // div.onmousedown = function(e) {
        //     if (e.button !== 0) { //如果不是鼠标左键
        //         return;
        //     }
        //     window.onmousemove = function(e) {
        //         divLeft += e.movementX;
        //         divTop += e.movementY;
        //         div.style.left = divLeft + "px";
        //         div.style.top = divTop + "px";
        //     }
        //     window.onmouseup = window.onmouseleave = function(e) {
        //         if (e.button === 0) {
        //             window.onmousemove = null; //移除鼠标移动事件
        //         }
        //     }
        // }
    </script>

2. 星星打分

##### 星星打分

```
    <style>
        .left {
            float: left;
            margin-left: 10px;
            line-height: 30px;
        }
    </style>

    <div id="divstars" class="left">
        <img src="images/empty.png" alt="">
        <img src="images/empty.png" alt="">
        <img src="images/empty.png" alt="">
        <img src="images/empty.png" alt="">
        <img src="images/empty.png" alt="">
    </div>
    <div id="divword" class="left">

    </div>
    <script>
        var words = ["满意", "一般满意", "还不错", "很满意", "非常满意"];
        var divstars = document.getElementById("divstars");
        var divword = document.getElementById("divword");
        var star = -1;
        divstars.onmouseover = function (e) {
            if (e.target.tagName === "IMG") {
                e.target.src = "images/shining.png";
                //处理之前的
                var prev = e.target.previousElementSibling;
                while (prev) {
                    prev.src = "images/shining.png";
                    prev = prev.previousElementSibling;
                }
                //处理之后的
                var next = e.target.nextElementSibling;
                while (next) {
                    next.src = "images/empty.png";
                    next = next.nextElementSibling;
                }
                //处理文字
                var index = Array.from(divstars.children).indexOf(e.target)
                divword.innerHTML = words[index];
            }
        }
        divstars.onclick = function (e) {
            if (e.target.tagName === "IMG") {
                star = Array.from(divstars.children).indexOf(e.target);
            }
        }
        divstars.onmouseleave = function () {
            divword.innerHTML = words[star] || " ";
            for (var i = 0; i < divstars.children.length; i++) {
                if (i <= star) {
                    divstars.children[i].src = "images/shining.png";
                } else {
                    divstars.children[i].src = "images/empty.png";
                }
            }
        }
    </script>
```

3. 放大镜
   24.51

##### 放大镜

```
1
```

### 键盘事件

#### 事件类型

- keydown：按下键盘上任意键触发，如果按住不放，会重复触发此事件
- keypress：按下键盘上一个**字符集**时触发
- keyup：抬起键盘上任意键触发

keydown,keypress 如果阻止了事件默认行为，文本不会显示

#### 事件对象

- keyboardEvent.charCode() //得到字符 unicode 编码 keypress 中
- code //得到按键字符串，适配键盘布局
- key //得到按键字符串，不适配键盘布局。能得到打印字符

- keyCode,which:得到键盘编码 //已弃用

### 其他事件

#### 表单事件

- focus：//元素聚焦的时候触发(能与用户发生交互元素，都可以聚焦)该事件不会冒泡

- blur //失去焦点触发，该事件不会冒泡

- submit //提交表单事件，仅在 form 元素有效

- change //文本改变事件

- input //文本改变事件，即使触发

##### window 事件

- load,DOMContentLoaded,readystatechange

window 的 load:页面中所有志愿全部加载完毕的事件
图片的 load：图片资源加载完毕的事件

```
var img=document.querSeleector("img");
img.onload=function(){
    console.log(this.width,this.height);
}
```

- document.DOMContentLoaded //dom 树构建完成后发生(异步加载的资源还没有加载完)

- readystate:loading,interactive,complete
- interactive:触发 DOMContentLoaded 事件
- complete:触发 window 的 load 事件

浏览器渲染页面的过程：

1. 得到页面源代码
2. 创建 document 节点
3. 从上到下，将原始依次添加到 dom 树中，每添加一个元素，进行预渲染
4. 按照结构，依次渲染子节点

link script 元素同步渲染
**js 代码应该尽量写到页面底部**

- css 应该写到页面顶部：避免出现闪烁(如果放到页面底部，会导致元素先没有样式，使用丑陋的默认样式，然后当读到 css 文件后，重新改变样式)图片视频元素异步加载

- js 应该写到页面底部：避免阻塞后续渲染，也避免运行 js 时，得不到页面中的元素

```
                                    //异步加载完图片callback函数回调返回宽高
function getImgSize(img,callback){
    if(img.width===0&&img.height===0){
        img.onload=function(){
            callback{
                width:img.width,
                height:img.height
            }
        }
    }
}
```

#### 其他事件

- beforeunload:window 事件,关闭窗口时运行，可以阻止关闭窗口
- unload:window 事件，关闭窗口时运行弹出字符串确定关闭

- scroll：滚动事件

```
window.onscroll=function(){
    console.log("滚动了！！！")；
}
var p=document.querySelector("p");
p.onscroll=function(){
    console.log(this.scrollTop,this.scrollLeft);
}
document.querSelector("button").onclick=function(){
    p.scrollTop=0;
    p.scrollLeft=0;         //可以获取和设置滚动距离
}

document.documentElement.scrollTop+document.body.scrollTop
浏览器兼容性问题，两个中有一个一定为0
```

- resize 窗口尺寸发生改变时运行的事件

1.  window.screen.height-window.screen.width //获取屏幕高和宽

window.outerWidth-window.outerHeight //浏览器窗口外尺寸

window.innerWidth-window.innerHeight //浏览器窗口内尺寸(包含滚动条)

document.documentElement.clientWidth //视口宽高

2.  div.offsetWidth div.offsetHeight //包含其边框和滚动条
    div.clientWidth div.clientWidth //不包含边框和滚动条，包含内边距内容

3.  div.scrollHeight Width //实际内容的宽高，不含边框

```回到顶部或底部
document.getElementsByTagName("button")[1].onnclick=function(){
    p.scrollTop=p.scrollHeight;
    p.scrollLeft=p.scrollWidth;
}

```

- contextmenu //点击右键出现的菜单，给 window 和 div 注册事件

div.oncontextmenu=function(e){
e.preventDafalut(); //阻止默认事件
}

- paste 粘贴事件
  //这两个事件都可以阻止默认行为
- copy 复制事件

- cut 剪切事件

> 元素位置

- offsetParent

获取某个元素第一个祖先定位元素，如果没有则得到 body

body 的 offsetParent 为 null

- offsetLeft,offsetTop
  相对于该元素的 offsetParent 坐标

如果 offsetParent 是 body，则将其当作是整个网页

- getBoundingClientRect 方法

该方法得到一个对象，该对象记录了该元素相对于视口的距离

> 事件模拟

- click:
- sumbit
- dispatchEvent

- window.scrollX,window.pageXOffset,

- window.scrollY,window.pageYOffset:

- scrollTo,scrollBy
  设置滚动条位置
  resizeTo,resizeBy
  窗口尺寸

> 作业

1. 自定义右键菜单

2. 许愿墙

```
1.

```

## bom

Browser Object Model

### 计时器

计时器是异步的，当时机成熟后才会执行
计算机会返回一个数字，该数字表示计时器的编号

- setTimeout 方法

```
btn.onclick=function(){
    setTimeout(function(){

    },3000)
}
```

- clearTimeout 方法：清除计时器
  回调函数

```
function interval(callback,duration){
    time1=setTimeout(function(){
        callback();
        interval(callback,duration);
    },duration);
}
```

- setInterval 方法：指定间隔时间到达后运行某个函数

```
btn1.onclick=function(){
    timer1=setInterval(function(){
        num++;
        h1.innerHTML=num;
    },300);
}
```

> 作业
> 无缝轮播图 详情轮播图难度指数五颗星 **********\*\*\*\***********\*\*\*\***********\*\*\*\***********

```
1
右边移动：
        目标的left<当前的left
        移动距离,目标的left-当前的left

        目标的left>当前的left
        移动距离,-(整个长度-|目标的left-当前的left|)

左边移动：
        目标的left>当前的left
        移动距离,目标的left-当前的left

        目标的left<当前的left
        移动距离,整个长度-|目标的left-当前的left|
```

### window 对象

> 自身方法

- open
  打开一个新窗口
  open(" 页面路径","打开目标","配置")

- alert
- confirm 是否确定
- prompt

> 对象属性

- document

  - document.write
    在当前文档流中写入内容，如果当前文档流不存在，则新开一个文档流

- location：地址栏对象
  href：当前地址栏对象
  hash：返回一个 url 锚部分
  host：返回一个 url 的主机名和端口
  hostname：返回 url 的主机名
  href：返回完整的 url
  pathname：返回 url 路径名
  port：返回 url 服务器使用端口号
  protocol：返回一个 url 协议
  search：返回一个 url 的查询部分
  reload 方法：刷新当前页面

- navigator //呜呜骗人的
  appCodeName:返回浏览器的代码名
  appMinorVersion:返回浏览器的次级版本
  appName:返回浏览器名称
  appVersion:返回浏览器的平台和版本信息
  browserLanguage：返回当前浏览器语言
  cookieEnabled：返回当前浏览器中是否启动 cookie 的布尔值
  cpuClass：返回浏览器的 CPU 等级
  onLine:返回指明系统是否处于脱机模式的布尔值
  platform：返回运行浏览器的操作系统平台
  systemLanguage：返回 OS 使用的默认语言
  userAgent：返回由客户机发送服务器的 user-agent 头部的值
  userLanguage:返回 os 的自然语言设置

- history
  go(d)
  back 方法
  forword 方法

- console

log 方法：打印对象的 valueof 的返回值
dir 方法：打印对象结构
time 方法和 timeEnd 方法：用于计时

### 提示插件

太他妈的强了，写好了轮子，后续用的轻松

1. 通用性
2. 易用性
3. 尽量不要与其他功能冲突

> 作业 提示插件

```
1
```

## JS 进阶

### 原型和原型链

- 所有对象都是通过`new函数`创建
- 所有的函数也是对象
- 函数中可以有属性
- 所有对象都是引用类型

#### 原型 prototype

所有函数都有一个属性：prototype，称之为函数原型
默认情况下，prototype 是一个普通的 object 对象
默认情况下，prototype 中有一个属性，constructor，它也是一个对象，它指向构造函数本身

```add 对象的隐式原型__proto__指向add原型      add new出对象
         prototype
        <--------
add原型              add
        --------->
         constructor

add.prototype=对象.__proto__ =add原型
```

![image-20210812164255317](C:\Users\licensor\AppData\Roaming\Typora\typora-user-images\image-20210812164255317.png)

#### 隐式原型 **proto**

两个下划线系统变量不要轻易适用

所有的对象都有一个属性：`__proto__`称之为隐式原型
默认情况下，隐式原型指向创建该对象的函数的原型。

```
function test(){

}
var obj=new test();
obj.__proto__===test.prototype          ==>true
```

```面试题
function create(){
    if(Math.random()<0.5){
        return new A();
    }else{
        return new B();
    }
}

var obj=create();
//如何得到创建obj的构造函数名称
console.log(obj.__proto__.constructor.name);

```

当访问一个对象的成员时：

1. 看该对象自身是否拥有该成员，如果有直接使用
2. 在原型链中依次查找是否拥有该成员，如果有直接使用

猴子补丁：在函数原型中加入成员，以增加对象的功能，猴子补丁会导致原型污染，使用需谨慎

#### 原型链

特殊点：

1. Function 的**proto**指向自身的 prototype
2. Object 的 prototype 的**proto**指向 null

```面试题*****************************************
function User(){
    User.prototype.sayHello=function(){}
    var u1=new User();
    var u2=new User();

    console.log(u1.sayHello===u2.sayHello);     //true
    console.log(User.prototype.constructor);    //User Function1
    console.log(User.prototype===Function.prototype);   //false
    console.log(User.__proto__===Function.prototype);   //true********
    console.log(User.__proto__===Function.__proto__);   //true********
    console.log(u1.__proto__===u2.__proto__);   //true
    consoel.log(u1.__proto__===User.__proto__); //false
    console.log(Function.__proto__===Object.__proto__);     //true
    console.log(Function.prototype.__proto__===Object.prototype.__proto__); //false
    console.log(Function.prototype.__proto__===Object.prototype);   //true
}

```

### 原型链的应用

#### 基础方法

**Object.getPrototypeOf(对象)**==对象.**proto**
获取对象的隐式原型

**Object.prototype.isPrototypeOf(对象)**
判断当前对象(this)是否在指定对象的原型链上

**对象 instanceof 函数**
判断函数的原型是否在对象的原型链上

**Object.create(对象)**
创建一个新对象，其隐式原型指向指定的对象

**Object.prototype.hasOwnProperty(属性名)**
判断一个对象自身是否拥有某个属性

#### 应用·

**类数组转化为真数组**

```
Array.prototype.slice.call(类数组);
```

**实现继承**

### 属性描述符

属性描述符：它表达了一个属性的相关信息(元数据)，它本质上是一个对象

1. 数据属性
2. 存取器属性
   1. 当给它赋值，会自动运行一个函数
   2. 当获取它的值时，会自动运行一个函数

```
Object.defineProperty(obj,"x",{
    //属性描述符value=1;
    get:function(){
        //当读取属性x时，运行的函数
        console.log("读取属性X");
        //该函数的返回值，将作为属性的值
        return 2;
    },
    set:function(){
        //当给该属性赋值时，运行的函数
        //val:表示要赋的值
        console.log("给属性赋值为"+val)；
    }
});

obj.x=3;    //相当于运行了set(3)

console.log(obj.x);

===>
给属性赋值为3
读取属性x
2

```

value 默认为 undefined

存取性配置 get,set 的 value 无效

```年龄存取判断
function User(name,age){
    this.name=name;var _age;
Object.defineProperty(this,"age",{
    get:function(){
        console.log("运行了age的get");
    },
    set:function(val){
        console.log("运行了age的set:"+val);
        if(val<0){
            val=0;
        }else if(val>100){
            val=100;
        }
        _age=val;
    }
})
this.age=age;
}

var ucnew User("abc",10000);

```

其他的属性描述符

**Object.getOwnPropertyDescriptor**
Object.getOwnPropertyDescriptor(obj,"x")
获取某个对象的某个属性的属性描述符对象(该属性必须直接属于该对象)

### 执行上下文

执行上下文：一个函数运行之前，创建的一块内存空间，空间中包含有该函数执行所需要的数据，为该函数执行提供支持

执行上下文栈：call stack，所有执行上下文组成的内存空间。

栈：一种数据结构，先进后出，后进先出。

全局执行上下文：所有的 js 代码执行之前，都必须有该环境

js 引擎始终执行的是栈顶的上下文。

#### 执行上下文中的内容

1. this 指向

1).直接调用函数，this 指向全局对象
2).在函数外，this 指向全局对象
3).通过对象调用或 new 一个函数，this 指向调用的对象或新对象

2. VO 变量对象
   关键在于分析 VO 中各项的变化
   variable Object:VO 中记录了该环境中所有声明的参数，变量和函数

之所以在全局环境中能使用这些定义的值是因为执行上下文中的 VO 指向了 window 对象
才能直接使用 window 里面的东西

Global Object:Go，全局执行上下文中的 VO

Active Object :AO,当前正在执行的上下文中的 VO

1).确定所有形参值以及特殊变量 arguments
2).确定函数中通过 var 声明的变量，将它们的值设置为 undefined,如果 VO 中已有该名称，则直接忽略。
3).确定函数中通过字面量声明的函数，将它们的值设置为指向函数对象，如果 VO 中已存在该名称，则覆盖

```
function A(a,b){
    console.log(a,b);
    var b=123;

    function b(){}
    var a=function(){}
    console.log(a,b);
}
先确认var声明的,已有则忽略
函数b存在即覆盖b的值
从上到下一步一步执行
遇到var的则重新赋值
```

当一个上下文中代码执行的时候，如果上下文中不存在某个属性，则会从之前的上下文寻找

```
console.log(foo);   //fn C
var foo="A";
console.log(foo)    //A
var foo=function(){
    console.log("B");
}
console.log(foo);   //fn B
foo();  //B
function foo(){
    console.log("C");
}
console.log(foo)    //fn    B
foo();  //B

```

```
var foo=1;

function bar (a){
    var a1=a;
    var a=foo;
    function a(){
        console.log(a);
    }
    a1();
}

bar(3);
```

### 作用域链

1. VO 中包含一个额外的属性，该属性指向创建该 vo 的函数本身
2. 每个函数在创建时，会有一个隐藏属性`[[scope]]`,它指向创建该函数时的 AO
3. 当访问一个变量时，会先查找自身 VO 中是否存在，如果不存在，则依次查找[[scope]]属性

某些浏览器会优化作用域链，函数的`[[scope]]`中仅保留需要用到的数据

# JavaScript [ 1995  Brendan Eich ]

> 好的文章推荐

[Javascript诞生记 -阮一峰]:http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html

[ TS 实现设计模式 ]:https://refactoringguru.cn/design-patterns/typescript

## 一: 了解 JS

### 1. 历史和发展

> `JavaScript` 的定位

- `JavaScript` 是脚本编程语言
- `JavaScript` 是弱类型语言
- `JavaScript` 是动态类型的
- `JavaScript` 是单线程的
- `JavaScript` 解释型语言
- `JavaScript` 具有良好的跨平台性

> `JavaScript` 和 `ECMAScript` 的区别，以及和 `DOM` 、`BOM` 的关系, 

`ECMAScript `是由网景的`布兰登·艾奇`开发的一种脚本语言`JavaScript`的`标准化规范`；

- 1995年12月，升阳与网景联合发表了`JavaScript`。
- 1996年11月，网景公司将`JavaScript`提交给[欧洲计算机制造商协会](https://baike.baidu.com/item/欧洲计算机制造商协会/2052072)进行标准化。
- 1997年6月, `ECMA-262`的第一个版本被`Ecma`组织采纳。`ECMAScript`是`ECMA-262`标准化的脚本语言的名称。
- 最初命名为`Mocha`，后来改名为`LiveScript`，最后重命名为`JavaScript`。

`ECMAscript`由于**只是语法的标准**, 所以在很多地方也都有了实现甚至超越了浏览器本身的存在.

- `ECMAscript`在浏览器中的实现`JavaScript`

- `ECMAscript`在`flash`中的实现`ActionScript`

- `ECMAscript`在服务器端的实现`Nodejs`

`JavaScript`包含

- `DOM`（文档对象模型），提供了与网页内容交互的 `方法` 和 `接口`
- `BOM`（浏览器对象模型），提供了与浏览器交互的 `方法` 和 `接口`
- `ECMAScript` 描述了 `JavaScript` 的语法和基本对象 (核心)

> `ECMAScript` 的版本

`ES5` 也称为 `ECMAScript 2009`，是`ECMAScript`的第5版, 是现在浏览前兼容性较好的一个版本

`JS版本` 主要还是用的`5.1 `和 `6.0`

`ECMAScript 2018 ` 是最新版

> `JavaScript `和 `java `的关系

首先在在概念和设计方面，`Java `和 `JavaScript `是两种完全不同的语言。

`JavaScript`语言最初出现在`Netscape Navigator 2浏览器`中。当时它叫**`LiveScript`**。

然而，由于当时`Java`技术如日中天，`Netscape`公司觉得改为`JavaScript`这个名字会更吸引人注目, 所以就是这么草率, 没有什么特殊的关系

### 2. 基础使用

> `script` 标签

`JavaScript`是脚本语言, 所以是可以和`HTML`进行混编的一种语言,使用通常也都是混入`HTML`中进行的.

`HTML`中使用`script`标签引入`JS文件或者代码.`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        // 在这里写代码
    </script>
    <script src = "tools.js"></script>
</head>
<body>
    <button onclick="alert('不推荐, 也别这么玩')">别闹</button>
    <script>
        // 也可以在这里写代码
    </script>
    <script>
        // 可以有多个 script 标签
    </script>
</body>
</html>
```

> `script `标签的属性

|            |                                                              |
| ---------- | ------------------------------------------------------------ |
| `src`      | 用于引入`JS文件的地址`                                       |
| `language` | 用于设置脚本的类型 (废弃)                                    |
| `type`     | 用于设置引入文件的`MIME类型`                                 |
| `charset`  | 用于设置引入文件的字符集类型                                 |
| `defer`    | **延时执行属性**, 可以是`JS`加载完毕后执行, 只对外部文件有效 |
| `async`    | **异步加载属性**, 可以改变`JS`文件的下载顺序, 但是不改变执行顺序 |

> `script` 标签的三中使用方式

1. 外链式

```html
<script src = "tools.js"></script>
```

2. 嵌入式

```html
<script>
    console.log('hello ximingx');
</script>
```

3. 内联式

```html
<button onclick="alert('不推荐, 也别这么玩')"></button>
```

> 三种输出方式

`JavaScript `中内置有一些调试代码时的工具

1. 控制台输出 `console.log()`

```js
console.log('hello ximingx');
```

2. 弹窗输出 `alert()`

```js
alert('hello ximingx');
```

3. 文档输出 `document.write()`

```js
document.write('hello ximingx');
```

> 语法结构
>
> ​		`JS`是以分号作为语句的结束, 但是如果你不写分号，也能够正常执行, 但是它相当于没有结束符, 在某些特定特殊的情况下运行会报错

## 二: 基础语法

### 1. 变量常量

> 变量就是可以变化的量, 是内存中可以存储数据内容的代号, 一个变量名, 对应一个变量的值
>
> 与常量不同, 常量必须在声明的时候赋予一个值, 且不能更改

#### 1.1 var

> 使用 `var` 进行变量的声明的三种方式

1. 声明并同时赋值

```js
var a = "a";
```

2. 声明但不赋值

```js
var a;
```

3. 没有声明, 直接使用 (唔, 有弊端,劝你别用,会被别人骂屎一样的代码)

```js
a = "a"
```

> 命名规则

1. 由`字母`, `数字`, `下划线`, `$`组成, 但是不可以用数字开头
2. 变量名严格区分大小写
3. 变量名不能和系统的保留关键字冲突

> `JS` 关键字

```html
break、delete、if、this、while、case、do、in、throw、with、catch、else、instanceof、try、continue、finally、new、typeof、for、return
```

> `JS` 保留字

```js
abstract、double、goto、native、static、boolean、enum、implements、package、super、byte、char、class、const、public
```

总结: 平常 `JS` 见不到的, 但是在 `java` 中有的, 谨慎使用它作为变量名, 之后一部分我们可以在 `TS` 中看到

> 驼峰命名法

`骆驼式命名法（Camel-Case）`又称`驼峰式命名法`，是电脑程式编写时的一套命名规则。

是指混合使用大小写字母来构成变量和函数的名字, 第一个单词以小写字母开始, 第二个单词的首字母大写, 以此类推

也是一般情况下 `JS` 的命名规范

```js
var oldPeople = '阿翔'
```

#### 1.2 let



留坑



#### 1.3 const



留坑



### 2. 注释

在编程语言中基本都有注释的存在, 没必要行行都加, 在一些很难想得通的地方加就好

单行注释: 用于对一行的内容进行注释操作.

```js
// 嗷呜, 这是注释
```

多行注释: 一次对连续的多行进行注释操作

```js
/*
	嗷呜, 这是注释	
	嗷呜, 这是注释
	嗷呜, 这是注释
	水代码
*/
```

在`JS`中多行注释禁止嵌套使用,因为多行注释的开头符号`/*` 是查找最近的`*/`作为结束的, 所以多行注释嵌套会出错的!

### 3. 转义字符

```html
<h1><</h1>
<h1>></h1>
<!-- 上面这么写会出 bug -->
```

因为标签之间 `<` 会产生歧义,  这个时候我们需要使用到转义符, 而这也正是我们需要使用转义字符的常见需求

| 转义字符 | 含义           |
| -------- | -------------- |
| `\n`     | 换行           |
| `\r`     | 回车           |
| `\t`     | 缩进           |
| `\\`     | 表示一个`\`    |
| `\'`     | 表示一个单引号 |
| `\"`     | 表示一个双引号 |

## 三. 数据类型

根据语言特征: `JS` 是基于对象的语言, 所有的数据都是对象

根据内存特征, `JS `分为

1. 基本数据类型
2. 引用数据类型

### 1. 类型检测

> `instanceof`

用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。关于原型和原型链可以先不懂, 具体看`8. Object`中的原型介绍

```
object instanceof constructor
```

- `object`：某个实例对象
- `constructor`：某个构造函数

```js
function fn(a, b, c) {
  console.log(arguments instanceof Array);
  console.log(arguments instanceof Object);
  // false
  // true
  // 一个不大不小的知识点: 函数中的默认属性arguments是一个伪数组的形式
}

fn(1, 2, 3);
```

> `typeof`

`typeof`运算符用于判断对象的类型，但是对于一些创建的对象，它们都会返回`object`'

`typeof`还可以判断是否为`function`

### 2. Null

`null `专门用来定义一个空对象。

```js
let a = null
```

如果你想定义一个变量用来保存引用类型，但是还没想好放什么内容，这个时候，可以在初始化时将其设置为 `null`。

你可以把 `null `理解为：`null `虽然是一个单独的数据类型，但`null `相当于是一个 `object`，只不过地址为空（是一个空指针）而已。

比如：

```js
let myObj = null;
cosole.log(typeof myObj); // 打印结果：object
```

补充：

-   `Null `类型的值只有一个，就是 `null`。
-   使用 `typeof `检查一个 `null `值时，会返回 `object`。

### 3. Undefined

与 `null` 有一些区别, 他是一个未定义的值, 下面都是他可能出现的场景

> 变量已声明，未赋值时

声明了一个变量，但没有赋值，此时它的值就是 `undefined`。举例：

```js
let name;
console.log(name); // 打印结果：undefined
console.log(typeof name); // 打印结果：undefined
```

补充：

-   `Undefined `类型的值只有一个，就是 `undefind`

-   使用 `typeof `检查一个 `undefined `值时，会返回 `undefined`

> 变量未声明

如果你从未声明一个变量，就去使用它，则会报错（这个大家都知道）；此时，如果用 `typeof` 检查这个变量时，会返回 `undefined`。举例：

```js
console.log(typeof a); // undefined
console.log(a); // 打印结果：Uncaught ReferenceError: a is not defined
```

> 数无返回值时

如果一个函数没有返回值，那么，这个函数的返回值就是 `undefined`。

或者，也可以这样理解：在定义一个函数时，如果末尾没有 `return `语句，那么，其实就是 `return undefined`。

```js
function foo() {}
console.log(foo()); // 打印结果：undefined
```

> 调用函数时，未传参

调用函数时，如果没有传参，那么，这个参数的值就是 `undefined`。

```js
function foo(name) {
    console.log(name);
}
foo(); // 调用函数时，未传参。执行函数后的打印结果：undefined
```

实际开发中，如果调用函数时没有传参，我们可以根据需要给形参设置一个默认值：

```js
function foo(name) {
    name = name || 'qianguyihao';
}
foo();
```

等学习了 ES6 之后，上方代码也可以这样写：

```js
function foo(name = 'qianguyihao') {}

foo();
```

### 4. String

#### 4.1 声明字符串的方式

```js
// 一: 以使用一对单引号或者一对双引号来定义一个字符串
let str1 = "str1"
console.log(str1) // str1
let str2 = 'str2'
console.log(str2) // str2
// 1. 在 JavaScript 中双引号定义的字符串和单引号定义的字符串没有本质区别

// 2. 无论是单引号还是双引号，都必须配对使用，不能一个单引号和双引号配对
let str3 = "str3'"
console.log(str3) //str'
// 3. 单引号中的字符串中不能出现单引号，可以出现双引号
//    双引号中的字符串中不能出现双引号，可以出现单引号

// 4. 单引号和双引号定义字符串时，须在一行内完成,不能换行

// 二: 使用模板字符串的方式定义字符串：我们可以使用一对反引号来定义字符串 (tab 键上面的 ``)
let str4 = `这是一个普通的字符串`
let str5 = `这是一个换行的 
字符串`
let str6 = 7
let str7 = 6
// 模板字符串利用 ${} 使用变量
let str8 = `这是一个可以解析变量的字符串，例如：${str6 + str7}`
console.log(str4) // 这是一个普通的字符串
console.log(str5) /* 这是一个换行的 
字符串 */
console.log(str6) // 7
console.log(str7) // 6
console.log(str8) // 这是一个可以解析变量的字符串，例如：13
// ${varName}或${value}。即${}中可为变量名，也可直接为字面量值(如${123}或${asd})。
```

#### 4.2 转义符串

转义符: `\`

```js
// 在定义一个字符串的时候，有些特殊字符并不适合直接出现。例如：换行符、单引 号（不能出现在单引号内）、双引号（不能出现在双引号内）
```

例如 下面是错误的

```js
let str = " " " 
// 会直接报语法错误
```

但是我们需要这样去使用 , 这个时候可以我们就需要使用 `\` 转义符，例如： 

```js
// 在这里使用了\n 来代表换行符
// 在这里使用了\"来代表双引号。
let str1 = '这是一个换行的\n字符串'
let str2 = '这是一个换行的\' 字符串'
console.log(str1)
console.log(str2)
/* 这是一个换行的
字符串 */
// 这是一个换行的' 字符串
let str3 = `123 
str3 \"\'`
// 如果使用模板字符串的方式定义字符串，可以直接使用回车换行。但是要在其中使用 反引号`，也必须转义
console.log(str3)
// 123
// str3 "'
```

#### 4.3 数据类型转换

> `toSring()`

`toString()`方法，该方法不会影响到原变量，会将转换后的结果返回，需要定义新的变量接收，或者将值赋予已有变量。
但是需要注意的是，`null`和`undefined`这两个类型的值是没有`toString()`方法的。

### 5. Number

`Number` 其实就是数字类型

#### 5.1 分类

> 整形



> 浮点型



> NaN

获得`NaN`的方式:

```JS
var val = 5 - 'a'; // 数字和字符串进行了乘法运算.(错误运算)
var val = NaN; // 直接赋值为 NaN
```

尽量避免获得`NaN`值, 因为`NaN`是个错误, 你应该反思一下为什么会算出来 `NaN`

`NaN `不等于任何数值,包括`NaN `自己

`NaN`具有传染性, 任何和`NaN`之间运算的结果都是`NaN`.

唯一检测`NaN`的办法是使用`isNaN()`功能

#### 5.2 NaN遇到的坑

```js
var a = 'abc';
a++;
console.log(a); // NaN
console.log(typeof a); // number
console.log(a); // NaN, 因为 Number('abc')的结果为 NaN，再自增后，结果依然是 NaN

// 这里自己有个误区

var a = 'abc';
a = a + 1;
console.log(a); // abc1
console.log(typeof a); // string
console.log(a); // abc1
```

#### 5.3 数据类型转换

> `parseInt() ` `parseFloat()`

1. `parseInt()`、`parseFloat()`会将传入的数据当作字符串来处理。
2. 也就是说，如果对`非String`使用 `parseInt(`)、`parseFloat()`，它会先将其转换为 `String `然后再操作。如果不是数值开头的字符串, 转换结果永远为`NaN`

```javascript
var a = 168.23;
console.log(parseInt(a)); //打印结果：168  （因为是先将 a 转为字符串"168.23"，然后然后再操作）

var b = true;
console.log(parseInt(b)); //打印结果：NaN （因为是先将 b 转为字符串"true"，然后然后再操作）

var c = null;
console.log(parseInt(c)); //打印结果：NaN  （因为是先将 c 转为字符串"null"，然后然后再操作）

var d = undefined;
console.log(parseInt(d)); //打印结果：NaN  （因为是先将 d 转为字符串"undefined"，然后然后再操作）
```

2. 只保留字符串最开头的数字，后面的中文自动消失。例如：

```javascript
console.log(parseInt('2017在公众号上写了6篇文章')); //打印结果：2017

console.log(parseInt('2017.01在公众号上写了6篇文章')); //打印结果仍是：2017   （说明只会取整数）

console.log(parseInt('aaa2017.01在公众号上写了6篇文章')); //打印结果：NaN （因为不是以数字开头）
```

3. 自动截断小数：取整，不四舍五入。

```javascript
var a = parseInt(5.8) + parseInt(4.7);
console.log(a); //9
a = parseInt(5.8 + 4.7);
console.log(a); //10;
```

4. 带两个参数时，表示在转换时，包含了进制转换。

```javascript
var a = '110';

var num = parseInt(a, 16); // 【重要】将 a 当成 十六进制 来看待，转换成 十进制 的 num

console.log(num); //272
```

就是说，无论 `parseInt()` 里面的进制参数是多少，最终的转换结果是十进制。

```javascript
var a = '5';

var num = parseInt(a, 2);
 // 将 a 当成 二进制 来看待，转换成 十进制 的 num

console.log(num);
 // 打印结果：NaN。因为 二进制中没有 5 这个数，转换失败。
```

---

> `Number()`

就拿`Number(true)` 和 `parseInt(true)/parseFloat(true)`来举例，二者在使用时，是有区别的：

-   `Number(true)` ：千方百计地想转换为数字；如果转换不了则返回 `NaN`。

-   `parseInt(true)/parseFloat(true) `：提取出最前面的数字部分；没提取出来，那就返回 `NaN`。

```js
console.log(Number(true)); 
console.log(parseInt(true));
// 1
// NaN
```

`Number()` 函数的转换规则

`Boolean	 ` `true `转换为 1 `false `转换为 0

`function     `转换为 `NaN		 `

`Object     `有值转换为 `NaN `为 `null  `转换为 `0`

`undefined   `转换为  `NaN`

### 6. Boolean

布尔类型只有2个值: `true  `和 `false`

系统中的所有布尔值都是有系统隐式的调用当前对象创建

#### 6.1 数据类型转换

其他的数据类型都可以转换为 `Boolean `类型。无论是隐式转换，还是显示转换，转换结果都是一样的。

> 情况一：`Number `转 `Boolean `

`0` 和 `NaN`是 `false`，其余的都是 `true`。比如 `Boolean(NaN)`的结果是 `false`。

> 情况二：`String `转 `Boolean `

空串是`false`，其余的都是 `true`。全是空格的字符串，转换结果也是 `true`。字符串`'0'`的转换结果也是 `true`。

> 情况三: `null `和 `undefined `都会转换为 `false`。

```js
var a = null;
if (!a) {
    a = {
        name: 'ximingx'
    }
}
```

> **引用数据类型会转换为 `true`。**

**注意，空数组`[]`和空对象`{}`，转换结果也是 `true`, 但是为 null 的时候为 `false`**

```js
if (Boolean(null)) {
    console.log('true + ' + null);
}
if (Boolean({})) {
    console.log('true + {}');
}
// true + {}
```

### 7. Function

函数：就是将一些功能或语句进行封装，在需要的时候，通过调用的形式，执行这些语句。

- **函数也是一个对象**

- 使用`typeof`检查一个函数对象时，会返回 `function`

函数的作用：

- 将大量重复的语句抽取出来，写在函数里，以后需要这些语句的时候，可以直接调用函数，避免重复劳动。

- 简化编程，让编程模块化。高内聚、低耦合。

来看个例子：

```javascript
console.log("你好");
sayHello();	// 调用函数

// 定义函数
function sayHello(){
	console.log("欢迎");
	console.log("welcome");
}
```

#### 7.1 函数的定义/声明

> 方式一：利用函数关键字自定义函数（命名函数）

使用`函数声明`来创建一个函数（也就是 `function `关键字）。

```javascript
function 函数名([形参1,形参2...形参N]){  // 备注：语法中的中括号，表示“可选”, 参数的选取是任意的
	
}
```

举例：

```javascript
function fun1(a, b){
	return a + b;
}
```

解释如下：

- `function`：是一个关键字。

- 函数名字：命名规定和变量的命名规定一样。只能是字母、数字、下划线、美元符号，不能以数字开头。

- 参数：可选。

- 大括号里面，是这个函数的语句。

> 方式二：函数表达式（匿名函数）

使用`函数表达式`来创建一个函数。语法：

```javascript
var 变量名  = function([形参1,形参2...形参N]){
	语句....
}
```

举例：

```javascript
var fun2 = function() {
	console.log("我是匿名函数中封装的代码");
};
```

解释如下：


- 上面的 `fun2 `是变量名，不是函数名。

- 函数表达式的声明方式跟声明变量类似，只不过变量里面存的是值，而函数表达式里面存的是函数。

- 函数表达式也可以传递参数。

从方式二的举例中可以看出：所谓的“函数表达式”，其实就是将匿名函数赋值给一个变量。

> 方式三：使用构造函数 `new Function()`

使用构造函数`new Function()`来创建一个对象。这种方式，用的少。

语法：

```javascript
var 变量名/函数名  = new Function('形参1', '形参2', '函数体');
```

注意，`Function `里面的参数都必须是字符串格式。

也就是说，形参也必须放在字符串里, 而且是在最前面的几位参数；

函数体也是放在字符串里包裹起来，放在 `Function `的最后一个参数的位置。

- **所有函数都是 `Function `的实例(对象)  **
- 函数也属于对象

代码举例：

```javascript
var fun3 = new Function('a', 'b', 'console.log("我是函数内部的内容");  console.log(a + b);');
fun3(1, 2); // 调用函数
```

打印结果：

```js
我是函数内部的内容
3
```

**分析**：

方式3的写法很少用，原因如下：

- 不方便书写：写法过于啰嗦和麻烦。

- 执行效率较低：首先需要把字符串转换为 `js `代码，然后再执行。

> 总结

1、所有的函数，都是 `Fuction` 的实例。函数本质上都是通过 `new Function` 得到的。

2、函数既然是实例对象，那么，函数也属于“对象”。还可以通过如下特征，来佐证函数属于对象：

我们直接打印某一个函数，比如 `console.log(fun2)`，发现它的里面有`__proto__`。

们还可以打印 `console.log(fun2 instanceof Object)`，发现打印结果为 `true`。

### 8. Object

对象就是数据和功能的集合.

#### 1. 对象的基本操作

> 创建对象

使用 `new `关键字调用的函数，是构造函数 `constructor` 来创建的对象。构造函数是专门用来创建对象的函数。

```javascript
var obj = new Object();
```

记住，使用`typeof`检查一个对象时，会返回`object`。

使用对象字面量

```js
var 变量  =  {};
```

创建对象时添加成员

```js
var 变量  = {
    成员名: 值,
    成员名: 值,
}
```

无论哪种方式以上方式创建的对象都是由`Object原型`创建的.

> 向对象添加属性

```javascript
对象.属性名 = 属性值;
```

> 删除对象的成员

```js
delete 对象变量.成员名称
```

> 获取属性

`.`的形式

```js
对象.属性名;
```

也可以使用`[]`这种形式去操作属性

```js
对象['属性名'] = 属性值;
```

`Object.keys()`获取到当前对象中的属性名 ，返回值是一个数组

```js
 var obj = {
     id: 1,
     pname: '小米',
     price: 1999,
     num: 2000
};
var result = Object.keys(obj)
console.log(result) // [id，pname,price,num]
```

> 修改

对象.属性名 = 新值;

```javascript
obj.name = 'tom';
```

`defineProperty`

```js
Object.defineProperty(对象，修改或新增的属性名，{})
// 三个参数都是必填
```

```js
Object.defineProperty(对象，修改或新增的属性名，{
		value: 1,// value: 修改或新增的属性的值,
		writable:true/false, // 如果值为false 不允许修改这个属性值
		enumerable: false, // enumerable 如果值为false 则不允许遍历, 默认为false
         configurable: false  // configurable 如果为false 则不允许删除这个属性 属性是否可以被删除或是否可以再次修改特性
})	
```

> 检查一个对象中是否含有指定的属性

通过 `in` 运算符可以检查一个对象中是否含有指定的属性。如果有则返回 `true`，没有则返回 `false`。

```javascript
'属性名' in 对象;
```

```javascript
// 检查对象 obj 中是否含有name属性
console.log('name' in obj);
```

#### 2. 构造函数原型 prototype

构造函数方法的使用存在浪费内存的问题, 例如创建实例对象方法的重复会占用内存

`JavaScript `规定，每一个`构造函数`都有一个`prototype `属性，指向另一个对象。

注意这个`prototype`就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。

我们可以把那些不变的方法，直接定义在 `prototype `对象上，这样所有对象的实例就可以共享这些方法。

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
```

#### 3. 对象原型  `__proto__`

对象都会有一个属性 `__proto__` 指向构造函数的 `prototype `原型对象，之所以我们对象可以使用构造函数 `prototype `原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。

`__proto__` 对象原型和原型对象 `prototype `是等价的

`__proto__` 对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象 `prototype`

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201412866.png)

#### 4. constructor 

对象原型（`__proto__` ）和构造函数（`prototype`）原型对象里面都有一个属性 `constructor `属性 ，`constructor `我们称为构造函数，因为它指回构造函数本身。

`constructor `主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。

一般情况下，对象的方法都在构造函数的原型对象中设置。

如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 `constructor  `就不再指向当前构造函数了。

此时，我们可以在修改后的原型对象中，添加一个 `constructor `指向原来的构造函数。

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
 }
 // 很多情况下,我们需要手动的利用constructor 这个属性指回 原来的构造函数
 Star.prototype = {
   // 如果我们修改了原来的原型对象,给原型对象赋值的是一个对象,则必须手动的利用constructor指回原来的构造函数
   constructor: Star, // 手动设置指回原来的构造函数
   sing: function() {
     console.log('我会唱歌');
   },
   movie: function() {
     console.log('我会演电影');
   }
}
var zxy = new Star('张学友', 19);
console.log(zxy)
```

#### 5.  原型链

每一个实例对象有一个__`proto`__属性，指向的构造函数的原型对象，构造函数的原型对象也是一个对象，也有__`proto`__属性，这样一层一层往上找就形成了原型链。

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201418663.png)

#### 6. js 成员查找机制

- 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
- 如果没有就查找它的原型（也就是 __`proto`__指向的 `prototype `原型对象）。
- 如果还没有就查找原型对象的原型（`Object`的原型对象）。
- 依此类推一直找到 `Object `为止（`null`）。
- __`proto`__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。





### 9. global

> 固有对象

固有对象就是系统已经实例化完毕的对象, 只可以使用不可以创建





### 10. Math





### 11. Date

内置对象 `Date `用来处理日期和时间。

需要注意的是：与 `Math `对象不同，`Date `对象是一个构造函数 ，需要先实例化后才能使用

#### 1. 创建Date对象的两种写法

- 写法一：如果`Date()`不写参数，就返回当前时间对象

- 写法二：如果`Date()`里面写参数，就返回括号里输入的时间对象

> 不传递参数时

获取系统的当前时间对象

```javascript
var date1 = new Date();
console.log(date1);
console.log(typeof date1);
// 2022-05-27T00:36:08.262Z
// object
```

代码解释：不传递参数时，表示的是获取系统的当前时间对象。

也可以理解成是：获取当前代码执行的时间。

当然你可能会发现, `new Date` 的时候会将时间按照`ISO`格式日期，东八区加上八个小时

> 传递参数

传递参数时，表示获取指定时间的时间对象。参数中既可以传递`字符串`，也可以传递`数字`，也可以传递`时间戳`。

通过传参的这种写法，我们可以把时间字符串/时间数字/时间戳，按照指定的格式，转换为时间对象。

参数是字符串

```js
const date11 = new Date('2020/02/17 21:00:00');
console.log(date11); // Mon Feb 17 2020 21:00:00 GMT+0800 (中国标准时间)

const date12 = new Date('2020/04/19'); // 返回的就是四月
console.log(date12); // Sun Apr 19 2020 00:00:00 GMT+0800 (中国标准时间)

const date13 = new Date('2020-05-20');
console.log(date13); // Wed May 20 2020 08:00:00 GMT+0800 (中国标准时间)

const date14 = new Date('Wed Jan 27 2017 12:00:00 GMT+0800 (中国标准时间)');
console.log(date14); // Fri Jan 27 2017 12:00:00 GMT+0800 (中国标准时间)
```


参数是多个数字

```js
const date21 = new Date(2020, 2, 18); // 注意，第二个参数返回的是三月，不是二月
console.log(date21); // Wed Mar 18 2020 00:00:00 GMT+0800 (中国标准时间)

const date22 = new Date(2020, 3, 18, 22, 59, 58);
console.log(date22); // Sat Apr 18 2020 22:59:58 GMT+0800 (中国标准时间)

const params = [2020, 06, 12, 16, 20, 59];
const date23 = new Date(...params);
console.log(date23); // Sun Jul 12 2020 16:20:59 GMT+0800 (中国标准时间)
```


参数是时间戳

```js
const date31 = new Date(1591950413388);
console.log(date31); // Fri Jun 12 2020 16:26:53 GMT+0800 (中国标准时间)

// 先把时间对象转换成时间戳，然后把时间戳转换成时间对象
const timestamp = new Date().getTime();
const date32 = new Date(timestamp);
console.log(date32); // Fri Jun 12 2020 16:28:21 GMT+0800 (中国标准时间)
```

#### 2. 日期的格式化

上一段内容里，我们获取到了 `Date` 对象，但这个对象，打印出来的结果并不是特别直观。

如果我们需要获取日期的指定部分，就需要用到 `Date`对象自带的方法。

获取了日期指定的部分之后，我们就可以让日期按照指定的格式，进行展示（即日期的格式化）。比如说，我期望能以 `2020-02-02 19:30:59` 这种格式进行展示。

`Date `对象 有如下方法，可以获取日期和时间的指定部分：

| 方法名              | 含义              | 备注          |
| ------------------- | ----------------- | ------------- |
| `getFullYear()`     | 获取年份          |               |
| `getMonth()`        | **获取月： 0-11** | 0代表一月     |
| `getDate()`         | 获取日：1-31      | 获取的是几号  |
| `getDay()`          | **获取星期：0-6** | **0代表周日** |
| `getHours()`        | 获取小时：0-23    |               |
| `getMinutes()`      | 获取分钟：0-59    |               |
| `getSeconds()`      | 获取秒：0-59      |               |
| `getMilliseconds()` | 获取毫秒          | 1s = 1000ms   |

> 年月日的格式化

```js
console.log(formatDate());

/*
    方法：日期格式化。
    格式要求：今年是：2020年02月02日 08:57:09 星期日
*/
function formatDate() {
    var date = new Date();

    var year = date.getFullYear(); // 年
    var month = date.getMonth() + 1; // 月
    var day = date.getDate(); // 日

    var week = date.getDay(); // 星期几
    var weekArr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];

    var hour = date.getHours(); // 时
    hour = hour < 10 ? '0' + hour : hour; // 如果只有一位，则前面补零

    var minute = date.getMinutes(); // 分
    minute = minute < 10 ? '0' + minute : minute; // 如果只有一位，则前面补零

    var second = date.getSeconds(); // 秒
    second = second < 10 ? '0' + second : second; // 如果只有一位，则前面补零

    var result = '今天是：' + year + '年' + month + '月' + day + '日 ' + hour + ':' + minute + ':' + second + ' ' + weekArr[week];

    return result;
}

```

#### 3. 时间戳

时间戳：指的是从格林威治标准时间的`1970年1月1日，0时0分0秒`到当前日期所花费的毫秒数（1秒 = 1000毫秒）。

计算机底层在保存时间时，使用的都是时间戳。时间戳的存在，就是为了统一时间的单位。

我们经常会利用时间戳来计算时间，因为它更精确





### 12. RegExp

#### 1. 正则表达式基础使用

> 正则表达式的创建

在 `JavaScript `中，可以通过两种方式创建一个正则表达式。

方式一：通过调用`RegExp`对象的构造函数创建 

```js
var regexp = new RegExp(/123/);
console.log(regexp);
```

方式二：利用字面量创建 正则表达式

```js
 var rg = /123/;
```

> 测试正则表达式

`test()` 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 `true`  或 `false`，其参数是测试字符串。

```js
var rg = /123/;
console.log(rg.test(123)); // 匹配字符中是否出现123  出现结果为true
console.log(rg.test('abc')); // 匹配字符中是否出现123 未出现结果为false
```

> 匹配模式

/正则表达式/匹配模式 

- `i` 忽略大小写。这里的 `i `指的是 `ignore`。

- `g` 全局匹配模式。这里的 `g` 指的是 `global`。

#### 2. 正则表达式字符匹配

正则表达式是匹配模式，要么匹配字符，要么匹配位置。

##### 1 两种匹配

如果正则只有精确匹配是没多大意义的，比如 `/hello/`，也只能匹配字符串中的 "hello" 这个子串。

```js
var regex = /hello/;

console.log( regex.test("hello") );

// => true
```

正则表达式之所以强大，是因为其能实现模糊匹配。

> 横向模糊匹配

横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。

其实现的方式是使用量词。譬如 `{m,n}`，表示连续出现最少 m 次，最多 n 次。

比如`/ab{2,5}c/`表示匹配这样一个字符串：第一个字符是“a”，接下来是2到5个字符“b”，最后是字符“c”。测试如下：

```js
var regex = /ab{2,5}c/g;

var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc";

console.log( string.match(regex) );

// => ["abbc", "abbbc", "abbbbc", "abbbbbc"]
```

注意：案例中用的正则是`/ab{2,5}c/g`，后面多了`g`，它是正则的一个修饰符。表示全局匹配，即在目标字符串中按顺序找到满足匹配模式的所有子串，强调的是“所有”，而不只是“第一个”。`g`是单词global的首字母。

> 纵向模糊匹配

纵向模糊指的是，一个正则匹配的字符串，**具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。**

其实现的方式是使用字符组。譬如`[abc]`，表示该字符是可以字符“a”、“b”、“c”中的任何一个。

比如`/a[123]b/`可以匹配如下三种字符串："a1b"、"a2b"、"a3b"。测试如下：

```js
var regex = /a[123]b/g;

var string = "a0b a1b a2b a3b a4b";

console.log( string.match(regex) );

// => ["a1b", "a2b", "a3b"]
```

检查一个字符串中是否包含 a或b

**写法1**：

```javascript
	var reg = /a|b/;
```

解释：使用 `|` 表示`或`的意思。

**写法2**：

```javascript
	var reg = /[ab]/;  // 跟上面的那行语法，是等价的
```

解释：这里的`[]`也是表示`或`的意思。

一些规则：

- `/[ab]/` 等价于 `/a|b/`：检查一个字符串中是否包含 **a或b**

- `/[a-z]/`：检查一个字符串那种是否包含**任意小写字母**

- `/[A-Z]/`：任意大写字母

- `/[A-z]/`：任意字母

- `/[0-9]/`：任意数字

- `/a[bde]c/`：检查一个字符串中是否包含 abc 或 adc 或 aec

`[]`这个符号在正则还是比较常用的。

> 精确匹配

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| `^`    | 表示匹配行首的文本（以谁开始） |
| `$`    | 表示匹配行尾的文本（以谁结束） |

如果` ^`和 `$` 在一起，表示必须是精确匹配。

##### 2. 字符组

需要强调的是，虽叫字符组（字符类），但只是其中一个字符。例如`[abc]`，表示匹配一个字符，它可以是“a”、“b”、“c”之一。

> 范围表示法

如果字符组里的字符特别多的话，怎么办？可以使用范围表示法。

比如[123456abcdefGHIJKLM]，可以写成[1-6a-fG-M]。用连字符`-`来省略和简写。

因为连字符有特殊用途，那么要匹配“a”、“-”、“z”这三者中任意一个字符，该怎么做呢？

不能写成[a-z]，因为其表示小写字符中的任何一个字符。

可以写成如下的方式[-az]或[az-]或[a\-z]。即要么放在开头，要么放在结尾，要么转义。总之不会让引擎认为是范围表示法就行了。

> 排除字符组

纵向模糊匹配，还有一种情形就是，某位字符可以是任何东西，但就不能是"a"、"b"、"c"。

此时就是排除字符组（反义字符组）的概念。例如`[ ^abc ]`，表示是一个除"a"、"b"、"c"之外的任意一个字符。字符组的第一位放`^`（脱字符），表示求反的概念。

当然，也有相应的范围表示法。

> 常见的简写形式

预定义类指的是某些常见模式的简写方式.

有了字符组的概念后，一些常见的符号我们也就理解了。因为它们都是系统自带的简写形式。

`\d`就是[0-9]。表示是一位数字。记忆方式：其英文是digit（数字）。

`\D`就是[ ^0-9]。表示除数字外的任意字符。

`\w`就是[0-9a-zA-Z_]。表示数字、大小写字母和下划线。记忆方式：w是word的简写，也称单词字符。

`\W`是[ ^0-9a-zA-Z_]。非单词字符。

`\s`是[ \t\v\n\r\f]。表示空白符，包括空格、水平制表符、垂直制表符、换行符、回车符、换页符。记忆方式：s是space character的首字母。

`\S`是[ ^ \t\v\n\r\f]。 非空白符。

.就是[ ^\n\r\u2028\u2029]。通配符，表示几乎任意字符。换行符、回车符、行分隔符和段分隔符除外。记忆方式：想想省略号...中的每个点，都可以理解成占位符，表示任何类似的东西。

如果要匹配任意字符怎么办？可以使用[\d\D]、[\w\W]、[\s\S]和[^]中任何的一个。

```js
var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
console.log(rg.test('andy'));//true
console.log(rg.test('baby'));//true
console.log(rg.test('color'));//true
console.log(rg.test('red'));//false
var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
console.log(rg1.test('aa'));//false
console.log(rg1.test('a'));//true
console.log(rg1.test('b'));//true
console.log(rg1.test('c'));//true
console.log(rg1.test('abc'));//true
----------------------------------------------------------------------------------
var reg = /^[a-z]$/ //26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
console.log(reg.test('a'));//true
console.log(reg.test('z'));//true
console.log(reg.test('A'));//false
-----------------------------------------------------------------------------------
//字符组合
var reg1 = /^[a-zA-Z0-9]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
------------------------------------------------------------------------------------
//取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。
var reg2 = /^[^a-zA-Z0-9]$/;
console.log(reg2.test('a'));//false
console.log(reg2.test('B'));//false
console.log(reg2.test(8));//false
console.log(reg2.test('!'));//true
```

##### 3. 量词

量词也称重复。掌握{m,n}的准确含义后，只需要记住一些简写形式。

> 简写形式

| 量词        | 说明                               |
| ----------- | ---------------------------------- |
| `*`         | 重复0次或更多次                    |
| `+`         | 重复1次或更多次                    |
| `?`         | 重复0次或1次                       |
| `{n}`       | 重复n次                            |
| `{n,}`      | 量词符用来设定某个模式出现的次数。 |
| 量词`{n,m}` | 说明重复n到m次                     |

> 贪婪匹配和惰性匹配

看如下的例子：

```js
var regex = /\d{2,5}/g;

var string = "123 1234 12345 123456";

console.log( string.match(regex) );

// => ["123", "1234", "12345", "12345"]
```

其中正则``/\d{2,5}/``，表示数字连续出现2到5次。会匹配2位、3位、4位、5位连续数字。

但是其是贪婪的，它会尽可能多的匹配。你能给我6个，我就要5个。你能给我3个，我就3要个。反正只要在能力范围内，越多越好。

我们知道有时贪婪不是一件好事。而惰性匹配，就是尽可能少的匹配：

```js
var regex = /\d{2,5}?/g;

var string = "123 1234 12345 123456";

console.log( string.match(regex) );

// => ["12", "12", "34", "12", "34", "12", "34", "56"]
```

其中`/\d{2,5}?/`表示，虽然2到5次都行，当2个就够的时候，就不在往下尝试了。

通过在量词后面加个问号就能实现惰性匹配，因此所有惰性匹配情形如下：

```js
{m,n}?
{m,}?
??
+?
*?
```

对惰性匹配的记忆方式是：量词后面加个问号，问一问你知足了吗，你很贪婪吗？

##### 4. 多选分支

一个模式可以实现横向和纵向模糊匹配。而多选分支可以支持多个子模式任选其一。

具体形式如下：(p1|p2|p3)，其中p1、p2和p3是子模式，用|（管道符）分隔，表示其中任何之一。

例如要匹配"good"和"nice"可以使用`/good|nice/`。测试如下：

```js
var regex = /good|nice/g;

var string = "good idea, nice try.";

console.log( string.match(regex) );

// => ["good", "nice"]
```

但有个事实我们应该注意，比如我用`/good|goodbye/`，去匹配"goodbye"字符串时，结果是"good"：

```js
var regex = /good|goodbye/g;

var string = "goodbye";

console.log( string.match(regex) );

// => ["good"]
```

而把正则改成/goodbye|good/，结果是：

```js
var regex = /goodbye|good/g;

var string = "goodbye";

console.log( string.match(regex) );

// => ["goodbye"]
```

也就是说，分支结构也是惰性的，即当前面的匹配上了，后面的就不再尝试了。

#### 3. 正则表达式位置匹配

在ES5中，共有6个锚字符：

```js
^ $ \b \B (?=p) (?!p)
```

##### 1. ^和$

`^`（脱字符）匹配开头，在多行匹配中匹配行开头。

`$` (美元符号）匹配结尾，在多行匹配中匹配行结尾。

```js
var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型
// /abc/ 只要包含有abc这个字符串返回的都是true
console.log(rg.test('abc'));
console.log(rg.test('abcd'));
console.log(rg.test('aabcd'));
console.log('---------------------------');
var reg = /^abc/;
console.log(reg.test('abc')); // true
console.log(reg.test('abcd')); // true
console.log(reg.test('aabcd')); // false
console.log('---------------------------');
var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
console.log(reg1.test('abc')); // true
console.log(reg1.test('abcd')); // false
console.log(reg1.test('aabcd')); // false
console.log(reg1.test('abcabc')); // false
```

比如我们把字符串的开头和结尾用"`#`"替换（位置可以替换成字符的！）：

```js
var result = "hello".replace(/^|$/g, '#');

console.log(result);

// => "#hello#"
```

多行匹配模式时，二者是行的概念，这个需要我们的注意：

```js
var result = "I\nlove\njavascript".replace(/^|$/gm, '#');

console.log(result);

/*
#I#
#love#
#javascript#
*/
```

##### 4. 位置的特性

对于位置的理解，我们可以理解成空字符""。

比如"hello"字符串等价于如下的形式：

```js
"hello" == "" + "h" + "" + "e" + "" + "l" + "" + "l" + "o" + "";

"hello" == "" + "" + "hello"
```

因此，把`/^hello$/`写成`/^^hello$$$/`，是没有任何问题的：

````js
var result = /^^hello$$$/.test("hello");

console.log(result);

// => true
````

甚至可以写成更复杂的:

```js
var result = /(?=he)^^he(?=\w)llo$\b\b$/.test("hello");

console.log(result);

// => true
```

也就是说字符之间的位置，可以写成多个。

把位置理解空字符，是对位置非常有效的理解方式。





## 四: 运算

操作数：参与运算的数据

操作符：参与运算的符号

表达式：操作符 + 操作数

每一个表达式都有一个运算结果，这个结果就叫返回值，所有的表达式都可以当作数据使用。

### 1. 算数运算符

| 运算符 | 含义 |
| ---- | ---- |
| `+` |		加法运算|
| `-` |		减法运算|
| `*` | 		 乘法运算|
| `/` |		除法运算|
| `%`	|		取余/求模运算|
| `++` |	自增运算|
| `--` |	自减运算|

### 2. 比较运算符


| 运算符 | 含义 |
| ---- | ---- |
| `=` | 普通赋值 |
| `+=` | 加等运算 |
| `-=` | 减等运算 |
| `*=` | 乘等运算 |
| `/=` | 除等运算 |
| `%=` | 取余等运算 |
| `.=` | 点等运算 |

### 3. 赋值运算符

| 运算符 | 含义 |
| ---- | ---- |
| `>` |  大于 |
| `<` | 小于 |
| `==` | 等于 |
| `>=` | 大于等于 |
| `<=` |	小于等于 |
| `!=` | 不等 |
| `===` | 全等于 |
| `!==` | 非全等于 |

### 4. 字符串运算

\`+`  字符串连接运算

```js
console.log('嗷呜' + '123');
// 嗷呜123
```

### 5. 逻辑运算

`&&`	逻辑与运算  (有假则假)

`||`	逻辑或运算  (有真则真)

`!`      逻辑非运算  (真变假,假变真)

抑或运算的特征:(相同为假,不同为真)

`? `三目运算符  判断条件 ? 真值 : 假值;

### 6. 位运算

进行位运算时，都会将数字转化为二进制再做运算， `1`表示`true   ``0` 表示`false`

> 按位与 `&`

将数字转化之后的每一位比较，如果都是`1`，结果为`1`，否则为`0`

> 按位或` |`

将数字转化之后的每一位比较，如果都是`0`，结果为`0`，否则为`1`

> 否 `~`

将该整数按位取反，转化为二进制之后，将`1`改为`0`，`0`改为`1`

> 异或  `^`

按位比较，相同取`0`，不同取`1`

>左移 `<<`

左移操作符用两个小于号（ `<<` ）表示，会按照指定的位数将数值的所有位向左移动。

> 右移 `>>` 

右移操作符用两个小于号（ `>>` ）表示，会按照指定的位数将数值的所有位向右移动。

```js
let a = 5
console.log(a)
console.log(a << 1)
console.log(a << 2)
console.log(a << 3)
// 5              5 的二进制为 101 
// 10             1010 的十进制是 10
// 20             10100 的十进制是 20
// 40             101000 的十进制是 40
```

## 五: 流程控制

### 1. 顺序结构

计算机自上而下执行代码的流程

### 2. 分支结构

> `if`    `else `       `else if`

```js
if(条件表达式) {
    
} else if (条件表达式) {
    
} else {
    
}
```

>`switch`

```js
switch(变量){
    case 值1: JS语句;
    case 值2: JS语句;
    case 值3: JS语句;
    default: JS语句;
}
```

`switch() `内放的是一个变量而不是一个表达式, 根据他来进行下面的匹配

`case `的选值必须是字符串, 整型或者布尔值其中的一种

### 3. 循环结构

> `for`

```js
// 打印 0 - 100 的数子
for (var i = 0; i <= 100; i++) {
    console.log(i)
}
```

> `while`

达到条件跳出循环

> `do while`

先执行一遍, 直到达到条件跳出循环

> `for in`

专门用于遍历对象的循环方式.

```js
let passage = {
    author: 'author: ximingx',
    Github: 'Github:https://github.com/ximingx',
    csdn: 'csdn: https://ximingx.blog.csdn.net/'
}
for (const passageKey in passage) {
    console.log(passageKey)
    console.log(passage[passageKey] + ': ')
}
// author
// author: ximingx:
// Github
// Github:https://github.com/ximingx:
// csdn
// csdn: https://ximingx.blog.csdn.net/:
```

### 4. 跳出判断循环

> `break `：

结束当前的循环体（如` for、while`）

> `continue `：

跳出本次循环，继续执行下次循环（如 `for`、`while`）

> `return `：

1、退出循环。

2、返回 `return `语句中的值，同时结束当前的函数体内的代码，退出当前函数。

## 六: 函数

### 1. 函数的定义

> 函数名: 函数的标识

使用英文命名

可以使用数字,但是不能以数字开头

不可以使用特殊字符,除了`$`和`_`

函数名严格区分大小写.

函数允许同名, 后出现的函数会覆盖前面的函数的功能

> 参数名: 函数的形参

函数的参数分为实参和形参, 实参是在调用函数时传递的参数, 形参是函数定义时使用的参数

> `return `返回值

每个函数都具有返回值, 默认为 `undefined`, 我们可以通过使用 `return `返回结果, 并且终止函数的执行, 当然函数也可以没有 `return`

在函数中，`return` 后的语句都不会执行（函数在执行完 `return `语句之后停止并立即退出函数）

```js
function 函数名(参数,参数...){
    // 函数体
    // return 结果;
}
```

eg: 

```js
function add(a = 2, b = 1) {
  return a + b;
}
var a = add();
var b = add(3);
var c = add(3, 4);
console.log(a, b, c);
// add 是一个求和函数
// 3 4 7
```

### 2. 函数作用域

> 函数中声明的变量为局部变量, 不可以被全局访问

但是在函数内部声明变量没有使用 `var` 关键字, 那么这个变量会被系统默认为全局变量, 会造成全局变量的污染

函数的形参都属于当前函数本身, 所以函数的形参都是局部变量.



### 3. 回调函数

把一个函数作为参数传递到另外一个函数中使用

```js
function foo(number, success, fail) {
    setTimeout(() => {
      console.log(number);
      if (number >= 0) {
        success(number);
      } else {
        fail(number);
      }
    })
}

function success(data) {
    console.log(`success: ${data}`);
}

function fail(data) {
    console.log(`fail: ${data}`);
}

foo(10, success, fail);
```

### 4. 递归函数

在函数内部调用当前函数本身的函数

```js
function get(number) {
  number++
  console.log(number)
  if (number <= 0) {
    return get(number)
  } else {
    return number
  }
}

console.log(get(-3));
// -2
// -1
// 0
// 1
// 1
```

在递归函数中使用 `arguments.callee` 表示当前函数

```js
function get(number) {
  number++
  console.log(number)
  if (number <= 0) {
    return arguments.callee(number)
  } else {
    return number
  }
}

console.log(get(-3));
// -2
// -1
// 0
// 1
// 1
```

> 利用递归求1~n的阶乘

```js
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
function fn(n) {
  if (n === 1) { //结束条件
    return 1;
  }
  return n * arguments.callee(n - 1);
}
console.log(fn(4));
```

> 利用递归求斐波那契数列

```js
// 利用递归函数求斐波那契数列(兔子序列)  1、1、2、3、5、8、13、21...
// 用户输入一个数字 n 就可以求出 这个数字对应的兔子序列值
// 我们只需要知道用户输入的n 的前面两项(n-1 n-2)就可以计算出n 对应的序列值
function fb(n) {
  if (n === 1 || n === 2) {
    return 1;
  }
  return arguments.callee(n - 1) + arguments.callee(n - 2);
}
console.log(fb(5));
```



### 5. 内部函数

在函数内部声明的函数就是内部函数, 相当于函数的局部变量

```js
function f() {
  var id = 20201613118;
  function getId() {
    return id;
  }
  return getId();
}

console.log(f())
```





### 6. 函数表达式

在定义表达式函数之后才可以调用当前表达式.

``` js
var foo = function() {
    return 'aw';
}
```





### 7. arguments

在调用函数时，浏览器每次都会传递进两个隐含的参数：

- 函数的上下文对象 `this`

- 封装实参的对象 `arguments`

每个函数中都包含 `arguments` 对象, 包含传递的所有实参

例如：

```javascript
function foo() {
    console.log(arguments);
    console.log(typeof arguments);
}

foo();
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205262234998.png)

`ES5` 中，在定义方法时，参数要确定个数，如下：（程序会报错）

```javascript
function fn(a, b, c) {
    console.log(a);
    console.log(b);
    console.log(c);
    console.log(d);
}

fn(1, 2, 3);
```

上方代码中，因为方法的参数是三个，但使用时是用到了四个参数，所以会报错：

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205262228702.png)

所以我们可以通过 `arguments` 对象来获取我们需要的实参, 通过 `arguments.length` 获取实参长度







### 8. 闭包

闭包：指有权访问另一个函数作用域中变量的函数。

本质是通过将函数从一个函数内部返回到函数外部成为一个全局变量, 借由函数原有的位置, 将函数内部的变量可以在函数外部得意访问.

让局部变量可以在函数外部访问

> 通过全局变量到函数中获取内部函数

```
// 声明全部变量
var a;
function fn1(){
	a  =  12;
	inner = function (){
		return a;
	}
}

fn1();
```

> 通过函数返回值的方式获取内部函数

```
function fn1() {
    let a = 10;
    return function fn2() {
        console.log(a);
    }
}
fn1();
```

闭包效果会长时间占用内存而不进行清除操作,降低程序效率.



### 9. 函数参数的默认值

> `ES5` 写法

```javascript
function fn(param) {
    let p = param || 'hello';
    console.log(p);
}
```

上方代码中，函数体内的写法是：如果 `param `不存在，就用 `hello`字符串做兜底。但是这样写比较啰嗦。

> **`ES6 `** （参数默认值的写法，很简洁）

```javascript
function fn(param = 'hello') {
    console.log(param);
}
```

在 `ES6 `中定义方法时，我们可以给方法里的参数加一个默认值（缺省值）：

-   方法被调用时，如果没有给参数赋值，那就是用默认值；

-   方法被调用时，如果给参数赋值了新的值，那就用新的值。

```js
var fn2 = (a, b = 5) => {
    return a + b;
};
console.log(fn2(1)); //第二个参数使用默认值 5。 输出结果：6

console.log(fn2(1, 8)); //输出结果：9
```

默认值的后面，不能再有没有默认值的变量。比如`(a,b,c)`这三个参数，如果我给 b 设置了默认值，那么就一定要给 c 设置默认值。

除此之外还应该注意

```js
let x = 'smyh';
function fn(x, y = x) {
    console.log(x, y);
}
fn('vae');
```

注意第二行代码，我们给 y 赋值为`x`，这里的`x`是括号里的第一个参数，并不是第一行代码里定义的`x`。打印结果：`vae vae`。

如果我把第一个参数改一下，改成：

```javascript
let x = 'smyh';
function fn(z, y = x) {
    console.log(z, y);
}
fn('vae');
```

此时打印结果是：`vae smyh`。

### 10. 函数与方法的区别

函数也可以成为对象的属性。如果一个函数是作为一个对象的属性保存，那么，我们称这个函数是这个对象的方法。

调用这个函数就说调用对象的方法。函数和方法，有什么本质的区别吗？它只是名称上的区别，并没有其他的区别。

函数举例：

```javascript
	// 调用函数
	fn();
```

方法举例：

```javascript
	// 调用方法
	obj.fn();
```

我们可以这样说，如果直接是`fn()`，那就说明是函数调用。如果是`XX.fn()`的这种形式，那就说明是方法调用。

### 11. 立即执行函数

现有匿名函数如下：

```javascript
	function(a, b) {
		console.log("a = " + a);
		console.log("b = " + b);
	};
```

立即执行函数如下：

```javascript
	(function(a, b) {
		console.log("a = " + a);
		console.log("b = " + b);
	})(123, 456);
```

立即执行函数：函数定义完，立即被调用，这种函数叫做立即执行函数。

立即执行函数往往只会执行一次

### 12. fn()  和 fn 的区别

- `fn()`：调用函数。调用之后，还获取了函数的返回值。

- `fn`：函数对象。相当于直接获取了整个函数对象。

我们要记住：函数名 == 整个函数。举例：

```javascript
// 定义fn方法
function fn(){
	alert(1)
};

console.log(fn == fn()); // false
```

我们知道，当我们在调用一个函数时，通常使用`函数()`这种格式；可如果，我们是直接使用`函数`这种格式，它的作用相当于整个函数。












































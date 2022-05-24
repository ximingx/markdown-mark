# TypeScript

> 在学习的时候, 我一度想起了大一时学的 `java`, 后悔当时没好好听 ~ ~ ~
>
> 提高了代码的可读性以及质量。我们在编译时就可以发现部分错误。这是我们选择TS的一个很大的原因

`TypeScript`是由`Microsoft`开发和维护的开源面向对象语言，他是`Javascript`的超集，不能直接在浏览器上运行，需要编译成`Javascript`。

在平常我们使用 `ES6/7/8/9` 语法用于开发中, 要想让具有新特性的代码顺利运行在非现代浏览器，需要借助`Babel`这种编译工具，将代码转为`ES5`版本。

**而 TypeScript，可以完全不用 `Babel`，就能将你的代码编译为指定版本标准的代码**。

**TypeScript 作为 JavaScript 的超集**，但是始终紧跟 `ECMAScript `标准，所以` ES6/7/8/9` 等新语法标准都是支持的，而且我还在语言层面上，对一些语法进行拓展。

`TypeScript`通过数据类型，类和其他带有类型检查的面向对象特性来扩展`Javascript`。例如类的私有/公有/保护。

- **``TypeScript`` 会在编译时对代码进行严格的静态类型检查，可以在编码阶段就发现问题**，而不是在上线运行时才发现
- ``TypeScript``语法遵循`ES`规范，更细速度快，不断支持最新的`ECMAScript`新特性，如装饰器、public/private修饰符
- ``TypeScript`` 支持 `OOP`（面向对象）的接口，抽象类，多态特性
- ``TypeScript``可以为 `IDE `提供更好的代码补全、接口提示、跳转到定义
- 还有重要一点是众多科技公司已经采用 ``TypeScript`` 进行开发，也是前端工程师需要掌握的就业技能
- ``TypeScript`` 是 `javascript `的一个超集，``TypeScript`` 可以运行于任何系统，并且是开源免费的。

> 历史版本


|  版本  | 发布日期 |
| ---- | ---- |
|`TypeScript 0.8`|	2012 年 10 月|
|`TypeScript 0.9`|	2013年六月|
|`TypeScript 1.0`	|2014 年 10 月|
|`TypeScript 2.0`|	2016 年 9 月|
|`TypeScript 3.0`|	2018 年 7 月|
|`TypeScript 4.0` - 最新版本|	2020 年 8 月|




## 1. 编译环境

> 安装 ``TypeScript``

```bash
# 全局安装
## win 系统
$ npm install ``TypeScript`` -g
$ yarn add ``TypeScript`` -g
## mac 系统
$ brew install ``TypeScript``	

# 项目中独立安装
$ yarn init -y
$ yarn add ``TypeScript`` -D

# 版本验证
$ tsc -v
```

> 编译

```bash
# tsc 就是 TypeScript Compile
# 编译 tsc 文件名
$ tsc 1.ts

# 修改 ts 文件后再执行命令编译会过于繁琐，可以执行以下命令自动监听ts 文件内容并自动生成 js 文件
$ tsc 1.ts -w

# tsc -w 会使用配置文件, 单独指定不会使用配置文件
```

## 2. 类型注解

**`TypeScript `里的类型注解是一种轻量级的为函数或变量添加约束的方式。** 

**`TypeScript `提供了静态的代码分析，它可以分析代码结构和提供的类型注解。**

但要注意的是, 就算你的代码里有错误，你仍然可以使用`TypeScript`。但在这种情况下，`TypeScript`会警告你代码可能不会按预期执行。

两种形式:

- 值类型 :限制固定的几个值
  - 宽泛类型 :`string` 这样的固定类型


举例: 

下面没有使用类型限制时，我们想要做一个求和函数, 函数参数传入字符串也是可以执行的，显示这个结果是不符合我们想法的

```js
function sum(a,b){
	return a+b;
}

console.log(sum('a',3)); //结果为 a3
```

但是在我们加上严格类型后，在编译环节就会提示错误

```js
function sum(a:number,b:number){
	return a+b;
}

console.log(sum('a',3)) 
//报错 Argument of type 'string' is not assignable to parameter of type 'number'.
```

**值得注意的是, 当没有明确设置类型时，系统会根据值推断变量的类型**

而这就体现了 `TypeScript `的严谨

> 布尔值

最基本的数据类型就是简单的 `true/false` 值

值为 `true `或 `false `会被推断为 `boolean`类型

```js
let isDone: boolean = false;
```

> 数值

和JavaScript一样，TypeScript 里的所有数字都是浮点数, 这些浮点数的类型是 `number`。 

除了支持十进制和十六进制字面量，`TypeScript `还支持 `ECMAScript 2015 `中引入的二进制和八进制字面量。

```js
let decLiteral: number1 = 6;
let hexLiteral: number2 = 0xf00d;
let binaryLiteral: number3 = 0b1010;
let octalLiteral: number4 = 0o744;
number1 = 123
```

> 字符串

`JavaScript `程序的另一项基本操作是处理网页或服务器端的文本数据。 像其它语言里一样，我们使用 `string`表示文本数据类型。 和JavaScript一样，可以使用双引号（ `"`）或单引号（`'`）表示字符串。

```js
let name: string = "bob";
name = "smith";
```

你还可以使用*模版字符串*，它可以定义多行文本和内嵌表达式。 这种字符串是被反引号包围，并且以`${ expr }`这种形式嵌入表达式

```js
let name: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ name }. I'll be ${ age + 1 } years old next month.`;
```

> 数组

TypeScript像JavaScript一样可以操作数组元素。 有两种方式可以定义数组。 第一种，可以在元素类型后面接上 `[]`，表示由此类型元素组成的一个数组：

```js
// 这时候会推断数组的内容值的类型是 number
let list = [1, 2, 3];
// 等同于
let list: number[] = [1, 2, 3];

let list1 = [1, "aw"]
// 等同于
let list1: (number | string)[] = [1, "aw"]
```

第二种方式是使用数组泛型，`Array<元素类型>`：

```js
let list: Array<number> = [1, 2, 3];
```

> 元组 Tuple

明确数组每个成员值类型的数组为元组

比如，你可以定义一对值分别为 `string`和`number`类型的元组。

```js
// Declare a tuple type
let x: [string, number];

x = ['hello', 10]; // OK

x = [10, 'hello']; // Error

x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型

console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString

x[6] = true; // Error, 布尔不是(string | number)类型
```

```js
// 顺序是固定的, 可以改值, 但是不可以更改类型
let tuple: [string, number] = ['John', 30];
tuple[0] = 123;
```

![image-20220505140938059](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220505140938059.png)

> 枚举

`enum`类型是对`JavaScript`标准数据类型的一个补充。 

枚举在程序语言及`mysql `等数据库中广泛使用

像`C#`等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

```js
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下，从`0`开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从 `1`开始编号：

当某个字段设置数值类型的值后，后面的在它基础上递增

```js
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```

枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：

```js
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName);  // 显示'Green'因为上面代码里它的值是2, 顺序递增
```

> any

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 

**这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。** 那么我们可以使用 `any`类型来标记这些变量：

- 使用`any `类型等同于使用纯 `JavaScript `的开发方式
- `any `类型是顶部类型，所有其他类型是他的子类型
- 使用`any`类型将失去 `typescript `静态类型的强制检测
- 只有在描述一个根本不知道的类型时使用 any

```js
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; 

let list: any[] = [1, true, "free"];
list[1] = 100;

let ximingx:any
//以下赋值不会报错
hd='ximingx'
hd=2002
hd=true
hd=[]
hd ={}
hd= class{}
```

**一个类型如果为 any, 和直接写 js 没有区别, 麻烦少用, 好去装B**

**any 为顶级类型, 失去了 ts 的严格类型保护, 所以any不进行类型检查，等于关闭了 TS 对该变量的严格类型校验**

```json
// 可以在 tsconfig.json 配置, 关闭 any 类型的使用
"noImplicitAny": true,
```

> void

某种程度上来说，`void`类型像是与`any`类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 `void`：

```js
function warnUser(): void {
    console.log("This is my warning message");
}
```

声明一个`void`类型的变量没有什么大用，因为你只能为它赋予`undefined`和`null`：

但是在严格模式下只能是 `undefined`

````js
let unusable: void = undefined;
````

> null 与 undefined

TypeScript里，`undefined`和`null`两者各自有自己的类型分别叫做`undefined`和`null`。 和 `void`相似，它们的本身的类型用处不是很大：

```js
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

**默认情况下`null`和`undefined`是所有类型的子类型。** 就是说你可以把 `null`和`undefined`赋值给`number`类型的变量。

开启对 null 与 undefined 的严格校验

```js
"strictNullChecks": true,
```

> never

`never`类型表示的是那些永不存在的值的类型。 

例如， **`never`类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型；** 变量也可能是 `never`类型，当它们被永不为真的类型保护所约束时。

```js
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

> Object

`object`表示非原始类型，也就是除`number`，`string`，`boolean`，`symbol`，`null`或`undefined`之外的类型。

`TypeScript` 也可以推断字面量类型

```js
const user = {name:'ximingx',age:18,open:true} 
// 推断结果
const user: {
  name: string;
  age: number;
  open: boolean;
} 

```

![image-20220507084444827](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220507084444827.png)

如果向对象中添加类型中不存在的属性将报错

```js
const user = {name:'ximingx',age:18,open:true}
// 将报错
user.aw = "aw"
```

![image-20220507084707856](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220507084707856.png)

```js
// 即使是深层次的属性也可以判断类型
const user = {
    name: 'ximingx',
    age: 18,
    open: true,
    lessons: [
        {title: 'vue', score: 100},
        {title: 'TS', score: 90},
    ]
}
console.log(user)
```

![image-20220507084838964](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220507084838964.png)

> unknown

`unknown` 不知道什么类型, 但是有一个类型, 不可以随意的赋值

- 与 `any `的区别是 any `不`进行 `TS `校验，**`unknown `类型要安全得多，会进行 TS 的类型检查**
- 使用 `unknown `类型时一般需要 as **类型断言**来转换类型
- `unknown `类型也是顶部类型这与 `any `一样

```js
let a:unknown = "1";
let b:string =  a as string;
// unknow 作为中间值 可以进行类型的转换
let a:unknown = "1";
let b:number =  a as unknown as number;
```

>  union

可以同时为声明联合类型，下面是为变量声明字符串或数值类型

```js
let ximingx:string | number = 'ximingx.com'
ximingx = 2010
ximingx = 'ximingx.com'
// 将会报错
ximingx = false

let aw:(string | number | boolean)[]  = []
hd.push('aw',2002,true)
```

> function

下面是 TS 自动推断的函数类型

```js
let ximingx = ()=> 'ximingx'

hd = false //更改类型为 false 后将报错
```

下面是使用显示类型定义函数 ，注意类型要使用大写的`Function` 这与 `string/number/boolean` 是有区别

```js
let ximingx:Function = ()=> 'ximingx'
```

如果函数的参数是可选的，使用 `?` 修饰

- 下面的*cc* 参数可以不传
- 不传时*cc* 值为`undefined`

```js
function sum(a: number, b: number, c?: number) {
    return a + b;
}

console.log(sum(3, 3));
```

如果参数设置默认值了就不需要可选参数符号`?`了

```js
function sum(a: number, b: number, c: number = 10) {
    return a + b;
}

console.log(sum(3, 3));
```

返回值类型也会自动推断

```js
function sum(a: number, b: number) {
    return a + b;
}
// 函数结构为 function sum(a: number, b: number): number
```

当函数没有明确返回值时，使用 `void `类型。`TS `会自动推断，建议明确声明 `void `类型

相同类型的参数我们可以使用 `type`

```js
type userType = { name: string; age: number }

let addUser = (user: userType): void => {
  console.log('添加用户')
}

let updateUser = (user: userType): void => {
  console.log('更新用户')
}
```



## 3. 类型断言

有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。

> as 断言

下例中TS 会根据函数推断变量 a 的类型是 number | string

```js
function one(x: boolean): number | string {
    return x ? 12 : "字符串";
}
let a = one(true)
```

![image-20220507103720863](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220507103720863.png)

我们可以由开发者来断定（断言）这就是字符串，这就是断言

```js
function one(x: boolean): number | string {
    return x ? 12 : "字符串";
}
let a = one(true) as number
```





## 4. 配置文件

在 `TypeScript `开发中，``tsconfig.json` 是个不可或缺的配置文件，它是我们在 `TypeScript`项目中最常见的配置文件, `TypeScript `支持对编译过程使用配置项自定义

当一个目录中存在  `tsconfig.json` 文件，则认为该目录为 `TypeScript `项目的根目录。

通常  `tsconfig.json` 文件主要包含两部分内容：**指定待编译文件**和**定义编译选项**。

```bash
# ts 初始化 tsconfig.json 文件。
$ tsc --init

# 在不指定输入文件的情况下执行 tsc 命令，默认从当前目录开始编译，编译所有 .ts 文件，并且从当前目录开始查找 tsconfig.json 文件，并逐级向上级目录搜索。
$ tsc
```

目前 tsconfig.json 文件有以下几个顶层属性：

- compileOnSave
- compilerOptions
- exclude
- extends
- files
- include
- references
- typeAcquisition

> 常见配置

```js
{
  "compilerOptions": {
    "target": "es5",          
    "module": "commonjs",       
    "noImplicitAny": true,     
    "removeComments": true,     
    "preserveConstEnums": true
    "removeComments": true,
    "strictNullChecks": true,
    "noImplicitThis": true
  },
  "files": [   // 指定待编译文件
    "./src/index.ts"  
  ]
}
```

 `files` 配置项值是一个**数组**，用来指定了待编译文件，即**入口文件**。

> compileOnSave

`compileOnSave` 属性作用是**设置保存文件的时候自动编译，但需要编译器支持**。

```js
{
 // ...
  "compileOnSave": false,
}
```

> compilerOptions

`compilerOptions` 属性作用是**配置编译选项**。

若 `compilerOptions` 属性被忽略，则编译器会使用默认值

```js
{
  // ...
  "compilerOptions": {
    "incremental": true, // TS编译器在第一次编译之后会生成一个存储编译信息的文件，第二次编译会在第一次的基础上进行增量编译，可以提高编译的速度
    "tsBuildInfoFile": "./buildFile", // 增量编译文件的存储位置
    "diagnostics": true, // 打印诊断信息 
    "target": "ES5", // 目标语言的版本
    "module": "CommonJS", // 生成代码的模板标准
    "outFile": "./app.js", // 将多个相互依赖的文件生成一个文件，可以用在AMD模块中，即开启时应设置"module": "AMD",
    "lib": ["DOM", "ES2015", "ScriptHost", "ES2019.Array"], // TS需要引用的库，即声明文件，es5 默认引用dom、es5、scripthost,如需要使用es的高级版本特性，通常都需要配置，如es8的数组新特性需要引入"ES2019.Array",
    "allowJS": true, // 允许编译器编译JS，JSX文件
    "checkJs": true, // 允许在JS文件中报错，通常与allowJS一起使用
    "outDir": "./dist", // 指定输出目录
    "rootDir": "./", // 指定输出文件目录(用于输出)，用于控制输出目录结构
    "declaration": true, // 生成声明文件，开启后会自动生成声明文件
    "declarationDir": "./file", // 指定生成声明文件存放目录
    "emitDeclarationOnly": true, // 只生成声明文件，而不会生成js文件
    "sourceMap": true, // 生成目标文件的sourceMap文件
    "inlineSourceMap": true, // 生成目标文件的inline SourceMap，inline SourceMap会包含在生成的js文件中
    "declarationMap": true, // 为声明文件生成sourceMap
    "typeRoots": [], // 声明文件目录，默认时node_modules/@types
    "types": [], // 加载的声明文件包
    "removeComments":true, // 删除注释 
    "noEmit": true, // 不输出文件,即编译后不会生成任何js文件
    "noEmitOnError": true, // 发送错误时不输出任何文件
    "noEmitHelpers": true, // 不生成helper函数，减小体积，需要额外安装，常配合importHelpers一起使用
    "importHelpers": true, // 通过tslib引入helper函数，文件必须是模块
    "downlevelIteration": true, // 降级遍历器实现，如果目标源是es3/5，那么遍历器会有降级的实现
    "strict": true, // 开启所有严格的类型检查
    "alwaysStrict": true, // 在代码中注入'use strict'
    "noImplicitAny": true, // 不允许隐式的any类型
    "strictNullChecks": true, // 不允许把null、undefined赋值给其他类型的变量
    "strictFunctionTypes": true, // 不允许函数参数双向协变
    "strictPropertyInitialization": true, // 类的实例属性必须初始化
    "strictBindCallApply": true, // 严格的bind/call/apply检查
    "noImplicitThis": true, // 不允许this有隐式的any类型
    "noUnusedLocals": true, // 检查只声明、未使用的局部变量(只提示不报错)
    "noUnusedParameters": true, // 检查未使用的函数参数(只提示不报错)
    "noFallthroughCasesInSwitch": true, // 防止switch语句贯穿(即如果没有break语句后面不会执行)
    "noImplicitReturns": true, //每个分支都会有返回值
    "esModuleInterop": true, // 允许export=导出，由import from 导入
    "allowUmdGlobalAccess": true, // 允许在模块中全局变量的方式访问umd模块
    "moduleResolution": "node", // 模块解析策略，ts默认用node的解析策略，即相对的方式导入
    "baseUrl": "./", // 解析非相对模块的基地址，默认是当前目录
    "paths": { // 路径映射，相对于baseUrl
      // 如使用jq时不想使用默认版本，而需要手动指定版本，可进行如下配置
      "jquery": ["node_modules/jquery/dist/jquery.min.js"]
    },
    "rootDirs": ["src","out"], // 将多个目录放在一个虚拟目录下，用于运行时，即编译后引入文件的位置可能发生变化，这也设置可以虚拟src和out在同一个目录下，不用再去改变路径也不会报错
    "listEmittedFiles": true, // 打印输出文件
    "listFiles": true// 打印编译的文件(包括引用的声明文件)
  }
}
```

> exclude

`exclude` 属性作用是**指定编译器需要排除的文件或文件夹。**

默认排除 `node_modules` 文件夹下文件。

```js
{
 // ...
  "exclude": [
    "src/lib" // 排除src目录下的lib文件夹下的文件不会编译
  ]
}
```

和 `include` 属性一样，支持 glob 通配符：

- `*` 匹配0或多个字符（不包括目录分隔符）
- `?` 匹配一个任意字符（不包括目录分隔符）
- `**/` 递归匹配任意子目录

> extends

`extends` 属性作用是**引入其他配置文件，继承配置**。
默认包含当前目录和子目录下所有 TypeScript 文件。

```js
{
 // ...
  // 把基础配置抽离成tsconfig.base.json文件，然后引入
 "extends": "./tsconfig.base.json"
}
```

> files

`files` 属性作用是**指定需要编译的单个文件列表**。
默认包含当前目录和子目录下所有 TypeScript 文件。

```js
{
 // ...
  "files": [
    // 指定编译文件是src目录下的leo.ts文件
    "scr/leo.ts"
  ]
}
```

>  include

`include` 属性作用是**指定编译需要编译的文件或目录**。

```js
{
 // ...
  "include": [
    // "scr" // 会编译src目录下的所有文件，包括子目录
    // "scr/*" // 只会编译scr一级目录下的文件
    "scr/*/*" // 只会编译scr二级目录下的文件
  ]
}
```

> references

`references` 属性作用是**指定工程引用依赖。**

```js
{
 // ...
  "references": [ // 指定依赖的工程
     {"path": "./common"}
  ]
}
```

> typeAcquisition

`typeAcquisition` 属性作用是**设置自动引入库类型定义文件(.d.ts)相关。**

- `enable` : 布尔类型，是否开启自动引入库类型定义文件(.d.ts)，默认为 false；
- `include` : 数组类型，允许自动引入的库名，如：["jquery", "lodash"]；
- `exculde` : 数组类型，排除的库名。

```js
{
 // ...
  "typeAcquisition": {
    "enable": false,
    "exclude": ["jquery"],
    "include": ["jest"]
  }
}
```

## 5. 声明变量

> let const

`let`和`const`是JavaScript里相对较新的变量声明方式。 像我们之前提到过的， `let`在很多方面与`var`是相似的，但是可以帮助大家避免在JavaScript里常见一些问题。 `const`是对`let`的一个增强，它能阻止对一个变量再次赋值。

因为TypeScript是JavaScript的超集，所以它本身就支持`let`和`const`。

当用`let`声明一个变量，它使用的是*词法作用域*或*块作用域*。 不同于使用 `var`声明的变量那样可以在包含它们的函数外访问，块作用域变量在包含它们的块或`for`循环之外是不能访问的。

在`catch`语句里声明的变量也具有同样的作用域规则。

`const` 声明是声明变量的另一种方式。与`let`声明相似，但是就像它的名字所表达的，它们被赋值后不能再改变。 换句话说，它们拥有与 `let`相同的作用域规则，但是不能对它们重新赋值。

> 解构数组

```js
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2
```

作用于函数参数：

```js
function f([first, second]: [number, number]) {
    console.log(first);
    console.log(second);
}
f(input);
```

你可以在数组里使用`...`语法创建剩余变量：

```js
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]

let [firsts] = [1, 2, 3, 4];
console.log(firsts); // outputs 1
```

> 解构对象

```js
// 这通过 o.a and o.b 创建了 a 和 b 。 注意，如果你不需要 c 你可以忽略它。
let o = {
    a: "foo",
    b: 12,
    c: "bar"
};
let { a, b } = o;
```

> 属性重命名

```js
let { a: newName1, b: newName2 } = o;
```

> 默认值

```js
function keepWholeObject(wholeObject: { a: string, b?: number }) {
    let { a, b = 1001 } = wholeObject;
}
```

> 展开

展开操作符正与解构相反。 它允许你将一个数组展开为另一个数组，或将一个对象展开为另一个对象。

```js
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
```

## 6. 类 (class)

> 下面是使用 `TS `约束属性并实例化对象

```js
class User {
    name: string
    age: number
    constructor(n: string, a: number) {
        this.name = n
        this.age = a;
    }

    info(): string {
        return `${this.name}的年龄是 ${this.age}`
    }
}
```

通过约束数组的类型为`User`，使其成员只能是 `User `类型对象

```js
new ximingx = new User("ximingx",20)  
new haosilu = new User("haosilu",19)
const users: User[] = [ximingx, haosilu];
console.log(users);
```

### 6.1 修饰符

> public

访问修饰符 `public`，指**公开**的属性或方法

- 默认情况下的属性是 `public `（公开的），即可以在类的内部与外部进行修改和访问
- 不明确设置修饰符即为 `public`

上面的代码等同于

```js
class User {
    name: string
    age: number
    constructor(n: string, a: number) {
        this.name = n
        this.age = a;
    }

    info(): string {
        return `${this.name}的年龄是 ${this.age}`
    }
}

=>

class User {
    public name: string
    public age: number
    constructor(n: string, a: number) {
        this.name = n
        this.age = a;
    }

    public info(): string {
        return `${this.name}的年龄是 ${this.age}`
    }
}
```

> protected

- protected 修饰符指**受保护**的，只允许在父类与子类中使用，不允许在类的外部使用

```js
class Person {
    protected name: string
    constructor(name: string) {
        this.name = name
    }
}
class Man extends Person {
    constructor(name: string) {
        super(name)
    }

    public info(): string {
        return `你好 ${this.name}`
    }
}

const ximingx = new Man('ximingx')
console.log(ximingx.name); //属性被 protected 修饰, 在类的外面不允许访问
```

> private

- `protected` 修饰符指**私有**的，不允许在子类与类的外部使用
- 父类声明 `private `属性或方法子类不允许覆盖

```js
class Person {
    private name: string
    constructor(name: string) {
        this.name = name
    }
}
class Man extends Person {
    constructor(name: string) {
        super(name)
    }

    public info(): string {
        return `你好 ${this.name}` ///属性被 private 修饰,不允许子类访问
    }
}
```

子类更改父类方法或属性的访问修饰符有些限制的

- 父类的 `private` 不允许子类修改
- 父类的 `protected` 子类可以修改为 `protected `或 `public`
- 父类的 `public `子类只能设置为 `public`

> readonly

`readonly `将属性定义为只读，不允许在类的内部与外部进行修改, 类似于其他语言的 const 关键字

但是可以在构造函数的时候设置初始值

```js
class Axios {
    readonly site: string = 'https://ximingx.com/api'
    constructor(site?: string) {
        this.site = site || this.site
    }
    public get(url: string): any[] {
        console.log(`你正在请求 ${this.site + '/' + url}`)
        return []
    }
}

const instance = new Axios('https://www.123.com')
```

### 6.2 constructor

构造函数是初始化实例参数使用的，在 `TS `中有些细节与其他程序不同

我们可以在构造函数 `constructor` 中定义属性，这样就不用在类中声明属性了，可以简化代码量, 但是必须要在属性前加上` public、private、readonly` 等修饰符才有效

```js
class User {
    constructor(
        public name: string,
        public age: number
    ) {}

    public info(): string {
        return `${this.name}的年龄是 ${this.age}`
    }
}
```

### 6.3 static

`static `用于定义静态属性或方法，属性或方法是属于构造函数的

静态属性是属于构造函数的，不是对象独有的，所以是所有对象都可以共享的

```js
class Site {
    static url: string = 'https://ximingx.com/api'

    static getSiteInfo() {
        return Site.url
    }
}

// 通过 类名.方法 使用
console.log(Site.getSiteInfo());
```

> 单例模式
>
> - 最后只会实例化一个对象

```js
class User {
    static instance: User | null = null;
    protected constructor() { }

    public static make(): User {
        if (User.instance == null) User.instance = new User;
        return User.instance;
    }
}

const x = User.make();
console.log(x);
```

### 6.4 get set

使用 `get `与 `set `访问器可以动态设置和获取属性，类似于 `vue `中的计算属性

```js
class User {
    private _name
    constructor(_name: string) {
        this._name = _name
    }
    public get name() {
        return this._name;
    }
    public set name(value) {
        this._name = value
    }
}
```

### 6.5 abstract

抽象类定义使用`abstract `关键字，抽象类除了具有普通类的功能外，还可以定义抽象方法

- 抽象类可以不包含抽象方法，但抽象方法必须存在于抽象类中
- **抽象方法是对方法的定义，子类必须实现这个方法**
- 抽象类不可以直接使用，只能被继承
- 抽象类类似于类的模板，**实现规范的代码定义**
- 抽象方法只能定义，不能实现，即没有函数体
- 必须由子类实现抽象方法

```js
abstract class Animation {
    abstract move(): void
}

class Anim1 extends Animation {
    public move(): void {

    }
}

class Anim2 extends Animation {
    public move(): void {

    }
}
```

## 7. 接口

接口用于描述类和对象的结构

- 使项目中不同文件使用的对象保持统一的规范
- 使用接口也会支有规范更好的代码提示

> 如果有额外的属性，使用以下方式声明，这样就可以添加任意属性了

```js
interface UserInterface {
    name: string;
    age: number;
    isLock: boolean;
    // 可以添加任意属性, 如果不加, 必须一一对应
    [key:string]:any
}
```

> 接口继承

对象也可以使用实现多个接口，多个接口用逗号连接

```js
class Tank implements Interface1, Interface2{
    
}
```

## 8. type

`type `与 `interface `非常相似都可以描述一个对象或者函数，使用 `type `用于定义类型的别名，是非常灵活的类型定义方式。

- `type `与 `interface `都是可以进行扩展
- 使用 `type `相比 `interface `更灵活
- 使用类(`class`) 时建议使用接口，这可以与其他编程语言保持统一
- `class `可以使用 `implements `来实现 `type` 或 `interface`

> `class `可以使用 `implements `来实现 `type `或 `interface`

```js
type Member = {
    name: string
}

class User implements Member {
    name: string = 'ximingx'
}
```

### 8.1 基本使用

```js
// 1. 基本类型别名
type IsAdmin = boolean

// 2. 定义联合类型
type Sex = 'boy' | 'girl'

// 3. 组合
type User = {
    isAdmin: IsAdmin,
    sex: Sex
}

// 4. 使用 type 声明对象类型
type User = {
    name: string,
    age: number
}
const hd: User = { name: 'ximingx', age: 20 }

//  5. type 声明函数的方式
type Pay = (price: number) => boolean
const pay: Pay = (price: number) => {
    console.log(`支付${price}`);
    return true;
}

// 6. 索引
interface User {
    [key: string]: any
}

type UserTYpe = {
    [key: string]: any
}
```

### 8.2 声明继承

`typescript `会将同名接口声明进行合并

```js
interface User {
    name: string
}
interface User {
    age: number
}
const hd: User = {
    name: 'ximingx',
    age: 20
}
```

`interface`也可以使用 `extends `继承

```js
interface Admin {
    role: string
}
interface User extends Admin {
    name: string
}
```

`interface `也可以 `extends `继承 `type`

```js
type Admin = {
    role: string
}
interface User extends Admin {
    name: string
}
```

`type `与 `interface `不同，存在同名的 `type `时将是不允许的

```js
// 错误
type User {
    name: string
}
type User {
    age: number
}
```

使用 `&` 来进行合并

```tsx
interface Name {
    name: string
}
interface Age {
    age: number
}
type User = Name & Age


type Admin = {
    role: string,
    isSuperAdmin: boolean
}
type Member = {
    name: string
}
// 声明合并
type User = Admin & Member;
//满足任何一个 type 声明即可
type User = Admin | Member;
```

## 9. 泛型 Generics

泛型指使用时才定义类型，即类型可以像参数一样定义，主要解决类、接口、函数的复用性，让它们可以处理多种类型。

### 9.1 基本使用

下面示例返回值类型是 `any`，这不是我们想要的，因为我们想要具体返回类型

```js
function dump(arg: any) {
    return arg;
}

let hd = dump('123') //类型为 any
let xj = dump(123) //类型为 any
```

使用了泛型定义后，返回值即为明确的类型

```js
function dump<T>(arg: T): T {
    return arg;
}
let hd = dump<string>('123')
```

### 9.2 类型继承

下面的代码是不严谨的，我们不需要处理数字，因为数字没有 `length `属性，同时我们希望返回类型不是 `any`

```js
function getLength(arg: any) {
    return arg.length;
}
console.log(getLength('123')); //3
console.log(getLength(['123'])); //1
console.log(getLength(123)); //undefined
```

泛型是不确定的类型，所以下面读取 `length `属性将报错

```js
function getLength<T>(arg: T): number {
    return arg.length; // 类型“T”上不存在属性“length”
}
```

我们可以通过继承来解决这个问题

```js
function getLength<T extends string>(arg: T): number {
    return arg.length; 
}

// 或使用

function getLength<T extends { length: number }>(arg: T): number {
    return arg.length;
}

// 或使用 interface 或 type

type LengthType = { length: number }
function getLengthAttribute<T extends LengthType }>(arg: T): number {
    return arg.length;
}

// 如果你的类型只是字符串或数组，也可以使用联合类型


function getLength<T extends string | any[]>(arg: T): number {
    return arg.length
}
```

## 10. 装饰器

装饰器（`Decorators`）为我们在类的声明及成员上通过编程语法扩展其功能，装饰器以函数的形式声明。

对功能进行扩展, 可以很方便的添加或者取消这个装饰的功能

> `Decorators `是实验性的功能，所以开发时会提示错误，我们需要启动 `Decorator `这个实验性的功能。 
>
> 这里需要我们在 `tsconfig.js `中进行修改后才可以使用

```bash
# 首先创建配置文件 tsconfig.js
$ tsc --init

# tsconfig.js 中将下面两行解除注释
"experimentalDecorators": true,
"emitDecoratorMetadata": true

# 执行命令
$ tsc -w
```

> 可用装饰器包括以下几种

| 装饰器             | 说明       |
| ------------------ | ---------- |
| ClassDecorator     | 类装饰器   |
| MethodDecorator    | 方法装饰器 |
| PropertyDecorator  | 属性装饰器 |
| ParameterDecorator | 参数装饰器 |

### 10.1 类装饰器

类装饰器是对类的功能进行扩展

- 首先执行 装饰器，然后执行类的构造函数
- **装饰器会优先执行，这与装饰器与类的顺序无关**

> **装饰器参数**

| 参数   | 说明                                                       |
| ------ | ---------------------------------------------------------- |
| 参数一 | 普通方法是构造函数的原型对象 Prototype，静态方法是构造函数 |

```js
/**
 * author: ximingx
 * Github:https://github.com/ximingx
 * csdn: https://ximingx.blog.csdn.net/
 */

// 2. 在类的前面添加 @装饰器名字, 这是语法糖
// 用 Decorator 装饰 Person 类
@Decorator
class Person {
    constructor() {
        console.log('构造函数');
    }
}

// 1. 定义
// 它的定义可以在任意的位置, 即使把装饰器定义放在类的后面也是先执行装饰器
const Decorator: ClassDecorator = (constructor: Function): void => {
    console.log(constructor);
}

// 3. 使用
const p1 = new Person;
```

> 原型对象

**因为可以装饰器上得到构造函数**，所以可以通过原型对象来添加方法或属性，供实例对象使用

```js
/**
 * author: ximingx
 * Github:https://github.com/ximingx
 * csdn: https://ximingx.blog.csdn.net/
 */

const MoveDecorator: ClassDecorator = (constructor: Function): void => {
    constructor.prototype.author = '机器人';
    console.log(constructor.toString())
}

// 装饰器的语法糖, 等同于
// MoveDecorator(Tank);
@MoveDecorator
class Person {
    constructor() {
        console.log('构造函数');
    }
}

const p1 = new Person;
// 直接使用 p1.author 会报错, 解决方法
// 1. 可以通过为类添加默认属性来解决这个错误
// 2. 在调用时使用断言处理

console.log((<any>p1).author);
// class Person {
//     constructor() {
//         console.log('构造函数');
//     }
// }
// 构造函数
// 机器人
```

> 装饰器叠加

```js
@MoveDecorator
@EatDecorator
@SleepDecorator
class Person {
    constructor() {
    }
}
```

### 10.2 方法装饰器

装饰器也可以修改方法

| 参数   | 说明                                                       |
| ------ | ---------------------------------------------------------- |
| 参数一 | 普通方法是构造函数的原型对象 Prototype，静态方法是构造函数 |
| 参数二 | 方法名称                                                   |
| 参数三 | 属性描述                                                   |

### 10.3 属性装饰器

| 参数   | 说明                                                       |
| ------ | ---------------------------------------------------------- |
| 参数一 | 普通方法是构造函数的原型对象 Prototype，静态方法是构造函数 |
| 参数二 | 属性名称                                                   |

### 10.4 参数装饰器

| 参数   | 说明                                                       |
| ------ | ---------------------------------------------------------- |
| 参数一 | 普通方法是构造函数的原型对象 Prototype，静态方法是构造函数 |
| 参数二 | 方法名称                                                   |
| 参数三 | 参数所在索引位置                                           |

### 10.5 装饰器工厂

有时有需要根据条件返回不同的装饰器，这时可以使用装饰器工厂来解决。可以在类、属性、参数等装饰器中使用装饰器工厂。

下例根据工厂函数传递的不同参数，返回不同装饰器函数。

```js
const MusicDecorator = (type: string): ClassDecorator => {
    switch (type) {
        case 'player':
            return (constructor: Function) => {
                constructor.prototype.playMusic = (): void => {
                    console.log(`播放【海阔天空】音乐`);
                }
            }
            break;
        default:
            return (constructor: Function) => {
                constructor.prototype.playMusic = (): void => {
                    console.log(`播放【喜洋洋】音乐`);
                }
            }

    }
}

@MusicDecorator('tank')
class Tank {
    constructor() {
    }
}
const tank = new Tank();
(<any>tank).playMusic();

@MusicDecorator('player')
class Player {
}

const player: Player = new Player();
(player as any).playMusic()
```

## 11. 命名空间

我们可以使用 `TypeScript `可以进行多文件的合并，不过这不推荐。

命名空间

- 数据需要使用 export 导出才可以使用
- 子命名空间也需要 export 后才可以使用

```js
namespace User {
    export let name: string = '123'
}
namespace Member {
    let name: string = '123'
}

console.log(User.name); // 123

console.log(Member.name); // 报错，因为没有使用 export 将变量导出
```

## 12. webpack

使用 `webpack `打包 TS 项目是推荐做法，`webpack `可以将多个模块文件打包到一个文件中。当然不只处理 `TS`、也可以处理` sass、less、vue、react` 等文件。

相比较于命名空间, 更推荐使用 `webpack`

### 12.1 初始化

```bash
# 创建 package.json用于管理项目及扩展包
$ yarn init -y
# 下面安装安装打包需要的软件
$ yarn add -D typescript webpack webpack-cli ts-loader webpack-dev-server
# 创建 typescript 的配置文件 tsconfig.js
$ tsc --init
```

- `webpack`核心文件、`webpack-cl`i 命令行工具，用于实现`webpack`核心功能
- `ts-loader` 用于处理 `typescript `的`ts-loader` 软件
- `webpack-dev-server` 在开发阶段启动访问地址为`localhost:3000`服务，修改时网页自动刷新的热更新效果

> 最后的目录结构

```js
├── public
│   ├── dist
│   │   └── index.js   
│   └── index.html		
├── package.json			
├── src							
│   └── index.ts		
├── tsconfig.json		
├── webpack.config.js	
└── yarn.lock		
```

### 12.2 配置

> webpack.config.js

```js
const path = require('path')

module.exports = {
    //程序打包的起点即入口文件
    entry: './src/index.ts',

    //配置 webpack 如何去输出,webpack 会将打包到一个文件中，从而减少网络请求
    output: {
        //最终编译文件与目录
        filename: 'app.js',
        path: path.resolve(__dirname, 'public/dist'),
        // 使用webpack-dev-server运行编译时，即热更新时的静态文件前缀
        // 因为编译内容是存在内存中的，不会真正创建文件，设置publicPath值决定以什么路径引用文件
        // 值是相对于 public/index.html 的路径，需要以 / 结尾
        // 需要安装 webpack-dev-server
        publicPath: '/dist/',
    },

    //项目中的不同类型模块的处理规则
    module: {
        rules: [
            {
                //test定义文件检测，满足后才处理，下面定义文件是否为 ts 或tsx
                test: /\.tsx?$/,
                //use定义处理器，下面是使用 ts-loader 将 ts或 tsx 文件编译成 javascript
                use: 'ts-loader',
                //exclude排除node_modules 目录中的文件处理
                exclude: /node_modules/,
            },
        ],
    },

    //配置模块如何解析
    resolve: {
        //在使用 import 等代码时，如果不添加扩展名，webpack 按以下扩展名顺序匹配文件
        extensions: ['.tsx', '.ts', '.js'],
    },
}
```

> package.json

```json
{
    "name": "houdunren.com",
    "version": "1.0.0",
    "main": "index.js",
    "license": "MIT",
    "scripts": {
        "dev": "webpack-dev-server --mode=development",
        "build": "webpack --mode=production"
    },
    "devDependencies": {
        "ts-loader": "^9.2.6",
        "typescript": "^4.4.3",
        "webpack": "^5.56.0",
        "webpack-cli": "^4.8.0",
        "webpack-dev-server": "^4.3.0"
    }
}
```

- development是开发阶段
- production是生产环境使用，会对代码进行更好的压缩与优化

> tsconfig.js

```js
"target": "ES6",
"module": "ES6"
```
















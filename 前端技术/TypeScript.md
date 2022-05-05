# TypeScript

在平常我们使用 ES6/7/8/9 语法用于开发中, 要想让具有新特性的代码顺利运行在非现代浏览器，需要借助Babel这种编译工具，将代码转为ES5版本。

而 TypeScript，可以完全不用 Babel，就能将你的代码编译为指定版本标准的代码。

TypeScript 作为 JavaScript 的超集，但是始终紧跟 ECMAScript 标准，所以 ES6/7/8/9 等新语法标准都是支持的，而且我还在语言层面上，对一些语法进行拓展。

- typescript 会在编译时对代码进行严格的静态类型检查，可以在编码阶段就发现问题，而不是在上线运行时才发现
- typeScript语法遵循ES规范，更细速度快，不断支持最新的ECMAScript新特性，如装饰器、public/private修饰符
- typescript 支持 OOP（面向对象）的接口，抽象类，多态特性
- typescript可以为 IDE 提供更好的代码补全、接口提示、跳转到定义
- 还有重要一点是众多科技公司已经采用 typeScript 进行开发，也是前端工程师需要掌握的就业技能
- typescript 是 javascript 的一个超集，typescript 可以运行于任何系统，并且是开源免费的。

## 1. 编译环境

> 安装 typescript

```bash
# 全局安装
$ npm install typescript -g
$ yarn add typescript -g
#  mac 系统
$ brew install typescript	
# 项目中独立安装
$ yarn init -y
$ yarn add typescript -D

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
```

## 2. 类型注解

TypeScript 里的类型注解是一种轻量级的为函数或变量添加约束的方式。 

TypeScript 提供了静态的代码分析，它可以分析代码结构和提供的类型注解。

但要注意的是, 就算你的代码里有错误，你仍然可以使用TypeScript。但在这种情况下，TypeScript会警告你代码可能不会按预期执行。

举例: 

下面没有使用类型限制时，函数参数传入字符串也是可以执行的，显示这个结果是不对的

```js
function sum(a,b){
	return a+b;
}

console.log(sum('a',3)); //结果为 a3
```

加上严格类型后，在编译环节就会提示错误

```js
function sum(a:number,b:number){
	return a+b;
}

console.log(sum('a',3)) 
//报错 Argument of type 'string' is not assignable to parameter of type 'number'.
```

**值得注意的是, 当没有明确设置类型时，系统会根据值推断变量的类型**

> 布尔值

最基本的数据类型就是简单的true/false值

```js
let isDone: boolean = false;
```

> 数值

和JavaScript一样，TypeScript 里的所有数字都是浮点数, 这些浮点数的类型是 number。 

除了支持十进制和十六进制字面量，TypeScript 还支持 ECMAScript 2015中引入的二进制和八进制字面量。

```js
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

> 字符串

JavaScript程序的另一项基本操作是处理网页或服务器端的文本数据。 像其它语言里一样，我们使用 `string`表示文本数据类型。 和JavaScript一样，可以使用双引号（ `"`）或单引号（`'`）表示字符串。

```js
let name: string = "bob";
name = "smith";
```

你还可以使用*模版字符串*，它可以定义多行文本和内嵌表达式。 这种字符串是被反引号包围（ ```），并且以`${ expr }`这种形式嵌入表达式

```js
let name: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ name }. I'll be ${ age + 1 } years old next month.`;
```

> 数组

TypeScript像JavaScript一样可以操作数组元素。 有两种方式可以定义数组。 第一种，可以在元素类型后面接上 `[]`，表示由此类型元素组成的一个数组：

```js
let list: number[] = [1, 2, 3];
```

第二种方式是使用数组泛型，`Array<元素类型>`：

```js
let list: Array<number> = [1, 2, 3];
```

> 元组 Tuple

**元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。** 比如，你可以定义一对值分别为 `string`和`number`类型的元组。

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

`enum`类型是对JavaScript标准数据类型的一个补充。 

像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

```js
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下，从`0`开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从 `1`开始编号：

```js
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```

枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：

```js
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
```

> any

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 

**这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。** 那么我们可以使用 `any`类型来标记这些变量：

```js
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; 

let list: any[] = [1, true, "free"];

list[1] = 100;
```

**一个类型如果为 any, 和直接写 js 没有区别, 麻烦少用, 好去装B**

**any 为顶级类型, 失去了 ts 的严格类型保护**

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

```js
// 对象的操作
let obj: object = [1, 2, 3];
obj = {};
// 限制 ? 表示可选择
let obj: {name: string; age: number; url?: string};
obj = {
  name: 'John',
  age: 30
}
```

> unknown

`unknown` 不知道什么类型, 但是有一个类型, 不可以随意的赋值

- 与 any 的区别是 any 不进行 TS 校验，unknown 类型要安全得多，会进行 TS 的类型检查
- 使用 unknown 类型时一般需要 as **类型断言**来转换类型

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
```

> 类型断言

有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。

类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。 TypeScript会假设你，程序员，已经进行了必须的检查。

```js
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

## 3. 配置文件

在 TypeScript 开发中，``tsconfig.json` 是个不可或缺的配置文件，它是我们在 TS 项目中最常见的配置文件

TypeScript 使用 ``tsconfig.json` 文件作为其配置文件，当一个目录中存在  `tsconfig.json` 文件，则认为该目录为 TypeScript 项目的根目录。
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

## 4. 声明变量

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














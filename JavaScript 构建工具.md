# JavaScript构建工具

- Babel：JS编译工具，主要用于浏览器不支持的ES新特性，比如用于编译TypeScript
- WebPack：模块打包器，主要作用就是打包、压缩、合并及按序加载



## WebPack

​	本质上， webpack是一个现代JavaScript应用程序的静态模块打包器(module bundler) 。当webpack处理应用程序时， 它会递归地构建一个依赖关系图(dependency graph) ， 其中包含应用程序需要的每个模块， 然后将所有这些模块打包成一个或多个bundle.

  **Webpack是当下最热门的前端资源模块化管理和打包工具， 它可以将许多松散耦合的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分离，等到实际需要时再异步加载。通过loader转换， 任何形式的资源都可以当做模块， 比如Commons JS、AMD、ES 6、CSS、JSON、Coffee Script、LESS等；**

  伴随着移动互联网的大潮， 当今越来越多的网站已经从网页模式进化到了WebApp模式。它们运行在现代浏览器里， 使用HTML 5、CSS 3、ES 6等新的技术来开发丰富的功能， 网页已经不仅仅是完成浏览器的基本需求； WebApp通常是一个SPA(单页面应用) ， 每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的JS代码，这给前端的开发流程和资源组织带来了巨大挑战。

  前端开发和其他开发工作的主要区别，首先是前端基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器的，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的模块化系统是前端工程师多年来一直探索的难题。


```bash
npm install webpack -g
npm install webpack-cli -g

webpack -v
webpack-cli -v
```

### 配置

创建 webpack.config.js配置文件

- entry：入口文件， 指定Web Pack用哪个文件作为项目的入口
- output：输出， 指定WebPack把处理完成的文件放置到指定路径
- module：模块， 用于处理各种类型的文件
- plugins：插件， 如：热更新、代码重用等
- resolve：设置路径指向
- watch：监听， 用于设置文件改动后直接打包

```js
module.exports = {
	entry:"",
	output:{
		path:"",
		filename:""
	},
	module:{
		loaders:[
			{test:/\.js$/,;\loade:""}
		]
	},
	plugins:{},
	resolve:{},
	watch:true
}

```

### 使用webpack

创建项目

1. 创建一个名为modules的目录，用于放置JS模块等资源文件

在modules下创建模块文件，如hello.js，用于编写JS模块相关代码

```js
//暴露一个方法：sayHi
exports.sayHi = function(){
	document.write("<div>Hello Webpack</div>");
}
```

2. 在modules下创建一个名为main.js的入口文件，用于打包时设置entry属性

```js
//require 导入一个模块，就可以调用这个模块中的方法了
var hello = require("./hello");
hello.sayHi();
```

3. 在项目目录下创建webpack.config.js配置文件，使用webpack命令打包

```js
module.exports = {
	entry:"./modules/main.js",
	output:{
		filename:"./js/bundle.js"
	}
}
```

4. 在项目目录下创建HTML页面，如index.html，导入webpack打包后的JS文件

```html
<!doctype html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
	</head>
	<body>
		<script src="dist/js/bundle.js"></script>
	</body>
</html>
```





## ES6 模块化的基本语法

ES6 的模块化主要包含如下 3 种用法：

1. 默认导出与默认导入
2. 按需导出与按需导入
3. 直接导入并执行模块中的代码

---

默认导出的语法：**export default 默认导出的成员**

```js
// log.js
let name = "ximingx"
function log () {
    console.log("export default 默认导出成员")
}
export default {
    name,
    log
}
```

默认导出的注意事项：每个模块中，只允许使用唯一的一次 export default，否则会报错！

默认导入的语法：**import 接收名称 from ‘模块标识符’**

默认导入时的接收名称可以任意名称，只要是合法的成员名称即可；

```js
// main.js
import m1 from "./log.js"

console.log(m1.name)
m1.log()
```

---

按需导出的语法：**export 按需导出的成员**

```js
// log.js
export let name = "ximingx"
export function get() {
    
}
```

按需导入的语法：**import { s1 } from ‘模块标识符’**

```js
x // main.js
import { name,get } from "./log.js"
```

1. 每个模块中可以使用多次按需导出；
2. **按需导入的成员名称必须和按需导出的名称保持一致；**
3. **按需导入时，可以使用 as 关键字进行重命名；**
4. 按需导入可以和默认导入一起使用；

---

如果只想单纯地执行某个模块中的代码，并不需要得到模块中向外共享的成员。此时，可以直接导入并执行模块代码

```js
import "./module."
```








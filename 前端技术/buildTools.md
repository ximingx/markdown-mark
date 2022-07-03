# JavaScript构建工具

- Babel：JS编译工具，主要用于浏览器不支持的ES新特性，比如用于编译TypeScript
- WebPack：模块打包器，主要作用就是打包、压缩、合并及按序加载

## 1. WebPack

![image-20220428155849963](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204281558046.png)

​	 	本质上， webpack是一个现代JavaScript应用程序的静态模块打包器(module bundler) 。当webpack处理应用程序时， 它会递归地构建一个依赖关系图(dependency graph) ， 其中包含应用程序需要的每个模块， 然后将所有这些模块打包成一个或多个bundle.

  **Webpack是当下最热门的前端资源模块化管理和打包工具， 它可以将许多松散耦合的模块按照依赖和规则打包成符合生产环境部署的前端资源。**

​		**还可以将按需加载的模块进行代码分离，等到实际需要时再异步加载。**

​		**通过loader转换， 任何形式的资源都可以当做模块， 比如Commons JS、AMD、ES 6、CSS、JSON、Coffee Script、LESS等；**

  伴随着移动互联网的大潮， 当今越来越多的网站已经从网页模式进化到了WebApp模式。它们运行在现代浏览器里， 使用HTML 5、CSS 3、ES 6等新的技术来开发丰富的功能， 网页已经不仅仅是完成浏览器的基本需求； 

​		 WebApp通常是一个SPA(单页面应用) ， 每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的JS代码，这给前端的开发流程和资源组织带来了巨大挑战。

  前端开发和其他开发工作的主要区别，首先是前端基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器的，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的模块化系统是前端工程师多年来一直探索的难题。

> 和gulp的有什么区别？

1. gulp叫做前端自动化任务管理工具；
2. gulp会定义一系列的task，处理各种事务（ES6、ts转化、图片压缩、scss转成css）
3. 通过gulp依次执行这些task，并且让整个流程自动化；

**而 webpack 是功能更加强大的 gulp** 

> 特别强调

- entry：入口文件， 指定Web Pack用哪个文件作为项目的入口, 即入口文件
- output：输出， 指定WebPack把处理完成的文件放置到指定路径, 主要输出文件的默认值是 `./dist/main.js`，其他生成文件默认放置在 `./dist` 文件夹中。
- module：模块， 用于处理各种类型的文件
- plugins：插件， 如：热更新、代码重用等
- resolve：设置路径指向
- watch：监听， 用于设置文件改动后直接打包
- mode: 构建模式

### 1.1 安装


```bash
# 初始化package.json
npm init -y
# 下载
npm install webpack -g
npm install webpack-cli -g
# 显示版本
webpack -v
webpack-cli -v
```

### 1.2 配置

**创建 webpack.config.js 配置文件**

- entry：入口文件， **指定Web Pack用哪个文件作为项目的入口, 即入口文件**
- output：输出， 指定WebPack把处理完成的文件放置到指定路径, 主要输出文件的默认值是 `./dist/main.js`，其他生成文件默认放置在 `./dist` 文件夹中。
- module：模块， 用于处理各种类型的文件
- plugins：插件， 如：热更新、代码重用等
- resolve：设置路径指向
- watch：监听， 用于设置文件改动后直接打包
- mode: 构建模式

```js
module.exports = {
    mode: "production" // "develpoment"
	entry:"", 
	output:{
		path:"", // 存放路径
		filename:"" // 文件名称
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

### 1.3 简单的使用

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

3. 在项目目录下创建webpack.config.js配置文件，使用 webpack 命令打包

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

> 自动打包功能

```bash
> yarn add webpack-dev-server -D
# 使用打包命令 webpack-dev-server
```

### 1.4 entry

简写用法：`entry: string | [string]`

```js
module.exports = {
  entry: './path/to/my/entry/file.js',
};

// 也可以将一个文件路径数组传递给 entry 属性
module.exports = {
  entry: ['./src/file_1.js', './src/file_2.js'],
};
```

### 1.5 output

可以通过配置 `output` 选项，告知 webpack 如何向硬盘写入编译文件。注意，即使可以存在多个 `entry` 起点，但只能指定一个 `output` 配置。

```js
module.exports = {
  output: {
    filename: 'bundle.js',
  },
};
```

### 1.6 loader

**webpack 只能理解 JavaScript 和 JSON 文件，这是 webpack 开箱可用的自带能力。**

loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。

loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。

loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

你可以使用 loader 告诉 webpack 加载 CSS 文件，或者将 TypeScript 转为 JavaScript。为此，首先安装相对应的 loader：

```bash
npm install --save-dev css-loader
npm install --save-dev ts-loader
```

在更高层面，在 webpack 的配置中，**loader** 有两个属性：

1. `test` 属性，识别出哪些文件会被转换。
2. `use` 属性，定义出在进行转换时，应该使用哪个 loader。
3. **使用正则表达式匹配文件时，不要为它添加引号。**也就是说，`/\.txt$/` 与 `'/\.txt$/'` 或 `"/\.txt$/"` 不一样。

**webpack.config.js**

```js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```

> url-loader

**url-loader 功能类似于 file-loader，但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。**

```bash
npm install --save-dev url-loader
```

webpack.config.js

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
}
```

当图片大小大于limit中限制时，需要使用file-loader进行图片加载，再转为base64字符串。 

> es6

```bash
npm install --save-dev babel-loader@7 babel-core babel-preset-es2015
```

```js
module: {
  rules: [
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['es2015']
        }
      }
    }
  ]
}
```

bundle.js从ES6语法编译为ES5语法了。

> 常用

```js
module.exports = {
    ......
    plugins:[ htmlPlugin ],
    module : {
        rules:[
            {
                //test设置需要匹配的文件类型，支持正则
                test:/\.css$/,
                //use表示该文件类型需要调用的loader
                use:['style-loader','css-loader']
            },
            {
                test:/\.less$/,
                use:['style-loader','css-loader','less-loader']
            },
            {
                test:/\.scss$/,
                use:['style-loader','css-loader','sass-loader']
            },{
                test:/\.jpg|png|gif|bmp|ttf|eot|svg|woff|woff2$/,
                //limit用来设置字节数，只有小于limit值的图片，才会转换
                //为base64图片
                use:"url-loader?limit=16940"
            }
        ]
    }
}
```



### 1.5 plugin

loader主要用于转换某些类型的模板，它是一个转换器。

**plugin是插件的意思，通常适用于对某个现有的框架的扩展。**

**而插件则可以用于执行范围更广的任务。包括：打包优化，资源管理，注入环境变量。**

>  使用
>
> 1. 通过npm安装需要使用的plugins
> 2. 在webpack.config.js中的plugins中配置插件

想要使用一个插件，你只需要 `require()` 它，然后把它添加到 `plugins` 数组中。多数插件可以通过选项(option)自定义。









## 2. Babel

> 掌握 `ES6 `之后，如果你的业务需要考虑 `ES5 `的兼容性，则可以这样做：写 `ES6` 语法的 `js `代码，然后通过 `Babel`将 ES6 `转换`为 `ES5`。
>
> 如果没有这样的需要，那么下面的内容，了解即可。

`Babel `是一个工具链，主要用于将采用 `ECMAScript 2015+` 语法编写的代码转换为向后兼容的 `JavaScript` 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。

```js
// Babel 输入： ES2015 箭头函数
[1, 2, 3].map(n => n + 1);

// Babel 输出： ES5 语法实现的同等功能
[1, 2, 3].map(function(n) {
  return n + 1;
});
```

> 降级处理 `babel `的使用步骤 

1. 安装` Node.js`

2. `npm `初始化项目

3. 命令行中安装 `babel`

4. 配置文件 `.babelrc`

5. 运行

> 以一个简单的案例说明

### 2.1 先创建一个项目的目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/bdd90d76902b4db0afddebd454609192.png)

在 `index.js` 写入

```js
let a = item => item + 2
console.log(a(4))
```

这个文件是一个 `ES6 `语法 的 `js` 文件，稍后，我们尝试把这个 `ES6 `语法的` js` 文件转化为 `ES5` 的` js` 文件。

### 2.2 安装 Babel-cli

初始化项目：

在安装 `Babel `之前，需要先用 `npm init` 先初始化我们的项目。打开终端或者通过 `cmd `打开命令行工具，进入项目目录，输入如下命令：

```bash
$ npm init -y
```

上方代码中，`-y` 代表全部默认同意，就不用一次次按回车了（稍后再根据需要，在文件中手动修改）。命令执行完成后，会在项目的根目录下生成 `package.json` 文件：

```json
{
  "name": "babel",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```

### 2.3 本地安装

```bash
npm install --save-dev babel-preset-es2015 babel-cli
```

### 2.4 新建.babelrc：

在根目录下新建文件`.babelrc`，输入如下内容：

```js
{
    "presets":[
        "es2015"
    ],
    "plugins":[]
}
```

### 2.5 开始转换：

现在，我们应该可以将 `ES6 `的文件转化为 `ES5 `的文件了，命令如下：（此命令略显复杂）

```bash
$ babel src/index.js -o dist/index.js
```

我们可以将上面这个命令进行简化一下。操作如下：

在文件 `package.json` 中修改键 `scripts`中的内容：

```json
  "scripts": {
    "build": "babel src/index.js -o dist/index.js"
  },
```

目前为止，环境配置好了。以后，我们执行如下命令，即可将`src/index.js`这个 `ES6 `文件转化为 `dist/index.js`这个 `ES5 `文件：

```bash
npm run build
```

我们执行上面的命令之后，会发现， `dist `目录下会生成 `ES5 `的 `js` 文件：

之后我们就可以在 `index.html` 中使用 `es5`的语法了

```js
"use strict";

var a = function a(item) {
  return item + 2;
};
console.log(a(4));
```

> 补充

```bash
# 把转换的结果输出到指定的文件
$ npx babel index.js -o test.js
# 把转换的结果输出到指定的目录
$ npx babel src -d lib
```



## 3. npm

嗷呜, 以后记录, 现在比较喜欢用 yarn

[npm install 流程1]:(https://godrry.com/archives/in-short-the-overall-process-of-npm-install.html)

[npm install 流程2]:(https://cloud.tencent.com/developer/article/1555982)

## 4. yarn

 yarn是facebook发布的一款取代npm的包管理工具。

特点:

- 速度超快。
- Yarn 缓存了每个下载过的包，所以再次使用时无需重复下载。 同时利用并行下载以最大化资源利用率，因此安装速度更快。
- 超级安全。
  在执行代码之前，Yarn 会通过算法校验每个安装包的完整性。
- 超级可靠。
  使用详细、简洁的锁文件格式和明确的安装算法，Yarn 能够保证在不同系统上无差异的工作。

> 安装

```bash
# 需要有 node 的环境, 使用 npm 安装
$ npm i -g yarn
# macos下安装
$ brew install yarn
# Yarn 淘宝源安装，分别复制粘贴以下代码行到黑窗口运行即可
$ yarn config set registry https://registry.npm.taobao.org -g
$ yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g
```

> 检查安装

```bash
# 查看版本
$ yarn --version
$ yarn -V
```

> 初始化项目

```bash
# 与 npm init 一样通过交互式会话创建一个 package.json
$ yarn init 
$ yarn init --yes 
# 简写 -y
$ yarn init -y
```

> 安装依赖

```bash
# 等同于 npm install  包名 
$ yarn add 包名

# npm i 包名 -D  会记录在 package.json 的 devDependencies开发环境中
$ yarn add 包名 -D  
 
 # npm i 包名 -g 全局安装
$ yarn global add 包名   
```

> 更新依赖

```bash
# 升级所有依赖项，不记录在 package.json 中
# npm update 
$ yarn upgrade 

# npm update 包名 
$ yarn upgrade 包名 # 升级指定包

# 忽略版本规则，升级到最新版本，并且更新 package.json
$ yarn upgrade --latest    
```

> 删除依赖

```bash
$ yarn remove 包名
```

> **安装 package.json 中的所有文件**

```bash
# 在 node_modules 目录安装 package.json 中列出的所又依赖
$ yarn   
# 强制下载安装
$ yarn install --force   
```

> **运行脚本**

```bash
# yarn run 用来执行在 package.json 中 scripts 属性下定义的脚本
# package.json
    {
        "scripts": {
            "dev": "node app.js",
            "start": "node app.js"
        }
    }
# 运行
$ yarn run dev
```

> 显示依赖包的信息

```bash
# 普通输出
$ yarn info 包名
# 输出 json 格式
$ yarn info 包名 --json 
# 输出 README 部分
$ yarn info 包名 readme 
```

> **列出项目的所有依赖**

```bash
$ yarn list 
# 列出全局安装的模
$ yarn global list
```

> 缓存

```bash
# 列出已缓存的每个包
$ yarn cache list
# 返回 全局缓存位置
$ yarn cache dir 
# 清除缓存
$ yarn cache clean 
```




















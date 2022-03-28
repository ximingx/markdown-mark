> 总算是复习到 node.js 了, 顺便做一下总结

## 1. 什么是 Node.js

[Node.js官网](https://nodejs.org/zh-cn/)

Node.js是一个基于 **Chrome V8 引擎**的 JavaScript 运行环境。Node.js 使用了一个**事件驱动**、**非阻塞式 I/O**的模型，使其轻量又高效。Node.js 的包管理工具 npm 是全球最大的开源库生态系统。

Node.js 不是一门语言，也不是 JavaScript 的框架，也不是像Nginx一样的Web服务器 ，**Node.js 是 JavaScript 在服务器端的运行环境（平台）**。


---

### node.js的组成

我们知道，JavaScript 的组成分为三个部分：

-   ECMAScript

-   DOM：标签元素相关的API

-   BOM：浏览器相关的API

ECMAScript 是 JS 的语法；DOM 和 BOM 浏览器端为 JS 提供的 API。

而 Node.js 的组成分为：

-   **ECMAScript**。ECMAScript 的所有语法在 Node 环境中都可以使用。

-   **Node 环境**提供的一些**附加 API**(包括文件、网络等相关的 API)。

在 Node.js 里运行 JavaScript，跟在 Chrome 里运行 JavaScript 有什么不同？

二者采用的是同样的 JS 引擎。在 Node.js 里写 JS，和在浏览器部分的 JS 文件，几乎没有不同。在写法上的区别在于：Node.js 没有浏览器、页面标签相关的 API，但是新增了一些 Node.js 相关的 API。**通俗来说，对于开发者而言，在前端写 JS 是用于控制浏览器；而 Node.js 环境写 JS 可以控制整个计算机。**

---

### Node.js 的架构和依赖

Node.js 内部采用 Google Chrome 的 V8 引擎，作为 JavaScript 语言解释器；同时结合自行开发的 libuv 库，**扩展了 JS 在后端的能力（比如 I/O 操作、文件读写、数据库操作等）**。使得 JS 既可以在前端进行 DOM 操作（浏览器前端），又可以在后端调用操作系统资源，是目前最简单的全栈式语言。

其次，Node 生态系统活跃，提供了大量的开源库，使得 JavaScript 语言能与操作系统进行更多的交互。

Node.js 是 JavaScript 在服务器端的运行环境，在这个意义上，Node.js 的地位其实就是 JavaScript 在服务器端的虚拟机，类似于 Java 语言中的 Java 虚拟机。

-   [V8 引擎](https://v8.dev/) ：编译和执行 JS 代码、管理内存、垃圾回收。V8 给 JS 提供了运行环境，可以说是 JS 的虚拟机。V8 引擎本身是用 C++ 写的。

-   [libuv](https://zh.wikipedia.org/wiki/Libuv)： libuv 是一个专注于异步 I/O 的跨平台类库，目前主要在 Node.js 上使用。它是 Node.js 最初的作者 Ryan Dahl 为 Node.js 写的底层类库，也可以称之为虚拟机。libuv 本身是用 C 写的。

---

### V8 的内存限制

在一般的后端开发语言中，在基本的内存使用上没有什么限制，然而在 Node 中通过 JavaScript 使用内存时就会发现只能使用部分内存（64 位系统下约为 1.4GB，32 位系统下约为 0.7GB）。在这样的限制下，将会导致 Node 无法直接操作大内存对象。

造成这个问题的主要原因在于 Node 基于 V8 构建，所以在 Node 中使用的 JavaScript 对象基本上都是通过 V8 自己的方式来进行分配和管理的。V8 的这套内存管理机制在浏览器的应用场景下使用起来绰绰有余，足以胜任前端页面中的所有需求。但在 Node 中，这却限制了开发者随心所欲使用大内存的想法。

---

### C/S架构

是Client/Server这两个单词的首字母，指的是客户端，服务器。

优点:

- 性能较高：可以将一部分的计算工作放在客户端上,这样服务器只需要处理数据即可。

- 界面酷炫:客户端可以使用更多系统提供的效果,做出更为炫目的效果。

缺点:

- 更新软件：如果有新的功能，就要推出新的版本。

- 不同设备访问：如果使用其他的电脑，没有安装客户端的话就无法登陆软件。

---


### B/S架构

是Browser/Server的这两个单词的首字母。指的是浏览器、服务器，是WEB兴起之后的一种架构。

现在所有的网站都是B/S架构，较为常见的例子有百度、知乎、网易云音乐Web等等，只需要通过浏览器即可使用.

优点：

- 更新简洁：如果需要更新内容了,对开发人员而言需要更改服务器的内容，对用户而言只需要刷新浏览器即可。

- 多设备同步：所有数据都在网上,只要能够使用浏览器即可登录使用。

缺点:

- 性能较低：相比于客户端应用性能较低,但是随着硬件性能的提升,这个差距在缩小。

- 浏览器兼容：处理低版本的浏览器显示问题一直是前端开发人员头痛的问题之一。移动设备兼容性较好，ie6已经越来越少人用了。

---

### 进程（进行中的程序）

- 每一个 **正在运行** 的应用程序都称之为进程。

- 每一个应用程序运行都至少有一个进程。

- 进程是用来给应用程序提供一个运行的环境。

- 进程是操作系统为应用程序分配资源的一个单位。

---

### 线程

- 用来执行应用程序中的代码

- 在一个进程内部，可以有很多的线程

- 在一个线程内部，同时只可以干一件事

- 传统的开发方式大部分都是 I/O 阻塞的，所以需要多线程来更好的利用硬件资源。

线程并不是越多越好。

### 多线程的弊端

缺点一：

- 创建线程耗费。
- 线程数量有限。
- CPU 在不同线程之间转换，有个上下文转换，这个转换非常耗时。

所谓的多线程其实都是假的，对于单核CPU而言，它们无非是在抢占 CPU 资源。线程和线程之间需要**切换和调度**，这是很耗费资源的。

缺点二：

- 线程之间共享某些数据，同步某个状态都很麻烦。

## 2. Node.js 的特点

-   异步、非阻塞 IO 模型

-   事件循环

-   单线程

Node.js 的性能和效率非常高。

传统的 Java 语言是一个请求开启一个线程，当请求处理完毕后就关闭这个线程。而 Node.js 则完全没有采用这种模型，它本质上就是一个单线程。

你可能会疑问：一个线程如何服务于大量的请求、如何处理高并发的呢？这是因为，Node.js 采用的是异步的、非阻塞的模型。

**这里所谓的“单线程”，指的是 Node 的主线程只有一个。为了确保主线程不被阻塞，主线程是用于接收客户端请求。但不会处理具体的任务。而 Node 的背后还有一个线程池，线程池会处理长时间运行的任务（比如 IO 操作、网络操作）。线程池里的任务是通过队列和事件循环的机制来执行。**

## 3. Node.js 安装

实在是懒得写, 下次自己安装再改, 照 ta 的来就可以

[Node.js 安装](https://blog.csdn.net/Yang_yangyang/article/details/121907688)

后面的各种包版本兼容问题很是麻烦

Node.js 版本常识
偶数版本为稳定版（0.6.x ，0.8.x ，8.10.x）
奇数版本为非稳定版（0.7.x ，0.9.x ，9.11.x）

## 4. 包和 NPM

由于 Node 是一套轻内核的平台，虽然提供了一系列的内置模块，但是不足以满足开发者的需求，于是乎出现了包（package）的概念：
与核心模块类似，就是将一些预先设计好的功能或者说 API 封装到一个文件夹，提供给开发者使用。

Node 本身并没有太多的功能性 API，所以市面上涌现出大量的第三方人员开发出来的 Package。

---

### 包的加载机制

如果 Node 中自带的包和第三方的包名冲突了，该怎么处理呢？原则是：

-   先在系统核心（优先级最高）的模块中找；

-   然后到当前项目中 node_modules 目录中找。

比如说：

```javascript
requiere(`fs`);
```

那加载的肯定是核心模块的包。所以，我们尽量不要创建一些和现有的包重名的包。


---

### NPM 的概念

**NPM**：Node Package Manager。官方链接： <https://www.npmjs.com/

Node.js 发展到现在，已经形成了一个非常庞大的生态圈。包的生态圈一旦繁荣起来，就必须有工具去来管理这些包。NPM 应运而生。

举个例子，当我们在使用 Java 语言做开发时，需要用到 JDK 提供的内置库，以及第三方库。同样，在使用 JS 做开发时，我们可以使用 NPM 包管理器，方便地使用成熟的、优秀的第三方框架，融合到我们自己的项目中，极大地加速日常开发的构建过程。

随着时间的发展，NPM 出现了两层概念：

-   一层含义是 Node 的开放式模块登记和管理系统，亦可以说是一个生态圈，一个社区。

-   另一层含义是 Node 默认的模块管理器，是一个命令行下的软件，用来安装和管理 Node 模块。

NPM 不需要单独安装。默认在安装 Node 的时候，会连带一起安装 NPM

## 6. 模块化


**概念**：将一个复杂的程序依据一定的规则（规范）封装成几个块（文件），并组合在一起。

**模块的内部数据、实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信。**

最早的时候，我们会把所有的代码都写在一个js文件里，那么，**耦合性会很高（关联性强），不利于维护；而且会造成全局污染，很容易命名冲突。**


---

### 模块化的好处

- 避免命名冲突，减少命名空间污染

- 降低耦合性；更好地分离、按需加载

- **高复用性**：代码方便重用，别人开发的模块直接拿过来就可以使用，不需要重复开发类似的功能。

- **高可维护性**：软件的声明周期中最长的阶段其实并不是开发阶段，而是维护阶段，需求变更比较频繁。使用模块化的开发，方式更容易维护。

- 部署方便

---

###  模块化的概念解读

模块化起源于 Node.js。Node.js 中把很多 js 打包成 package，需要的时候直接通过 require 的方式进行调用（CommonJS），这就是模块化的方式。


---

### 模块化规范

服务器端规范：

- [**CommonJS规范**](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。

CommonJS 就是一套约定标准，不是技术。用于约定我们的代码应该是怎样的一种结构。


浏览器端规范：

- [**AMD规范**](https://github.com/amdjs/amdjs-api)：是 **[RequireJS](http://requirejs.org/)** 在推广过程中对模块化定义的规范化产出。



- **[CMD规范]()**：是 **[SeaJS](http://seajs.org/)** 在推广过程中对模块化定义的规范化产出。淘宝团队开发。


-  另外，还有ES6规范：import & export。


## 7. CommonJS (重点)


[CommonJS](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。也就是说，**Node.js 就是基于 CommonJS 这种模块化规范来编写的。**

CommonJS 规范规定：每个模块内部，module 变量代表当前模块。这个变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口对象。**加载某个模块，其实是加载该模块的 module.exports 对象。**

**在 CommonJS 中，每个文件都可以当作一个模块：**

- 在服务器端：模块的加载是运行时同步加载的。

- 在浏览器端: 模块需要提前编译打包处理。首先，既然同步的，很容易引起阻塞；其次，浏览器不认识`require`语法，因此，需要提前编译打包。

---

### 模块的暴露和引入

Node.js 中只有模块级作用域，两个模块之间的变量、方法，默认是互不冲突，互不影响，这样就导致一个问题：模块 A 要怎样使用模块B中的变量&方法呢？这就需要通过 `exports` 关键字来实现。

Node.js中，每个模块都有一个 exports 接口对象，我们可以把公共的变量、方法挂载到这个接口对象中，其他的模块才可以使用。

接下来详细讲一讲模块的暴露、模块的引入。

---

### 暴露模块的方式一： exports

`exports`对象用来导出当前模块的公共方法或属性。别的模块通过 require 函数调用当前模块时，得到的就是当前模块的 exports 对象。

**语法格式**：

```js
// 相当于是：给 exports 对象添加属性
exports.xxx = value
```

这个 value 可以是任意的数据类型。

**注意**：暴露的关键词是`exports`，不是`export`。其实，这里的 exports 类似于 ES6 中的 export 的用法，都是用来导出一个指定名字的对象。



**代码举例**：

```js
const name = 'ximingx';

const foo = function (value) {
	return value * 2;
};

exports.name = name;
exports.foo = foo;
```

---

### 暴露模块的方式二： module.exports

- Node中每个模块的最后，都会执行 `return: module.exports`。
- Node中每个模块都会把 `module.exports`指向的对象赋值给一个变量 `exports`，也就是说 `exports = module.exports`。

`module.exports`用来导出一个默认对象，没有指定对象名。

语法格式：

```javascript
// 方式一：导出整个 exports 对象
module.exports = value;

// 方式二：给 exports 对象添加属性
module.exports.xxx = value;
```

这个 value 可以是任意的数据类型。

代码举例：

```js
// 方式1
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}

// 我们不能再继续写 module.exports = value2。因为重新赋值，会把 exports 对象 之前的赋值覆盖掉。

// 方式2
const age = 28;
module.exports.age = age;

```

`module.exports` 还可以修改模块的原始导出对象。比如当前模块原本导出的是一个对象，我们可以通过 module.exports 修改为导出一个函数。如下：

```js
module.exports = function () {
    console.log('hello world')
}
```


---

### exports 和 module.exports 的区别



最重要的区别：

- 使用exports时，只能单个设置属性 `exports.a = a;`

- 使用module.exports时，既单个设置属性 `module.exports.a`，也可以整个赋值 `module.exports = obj`。

其他要点：

- Node中每个模块的最后，都会执行 `return module.exports`。

- Node中每个模块都会把 `module.exports`指向的对象赋值给一个变量 `exports`，也就是说 `exports = module.exports`。

- `module.exports = XXX`，表示当前模块导出一个单一成员，结果就是XXX。

- 如果需要导出多个成员，则必须使用 `exports.add = XXX; exports.foo = XXX`。或者使用 `module.exports.add = XXX; module.export.foo = XXX`。


---

### 引入模块的方式：require

require函数用来在一个模块中引入另外一个模块。传入模块名，返回模块导出对象。

**语法格式**：

```js
const module1 = require('模块名');
```

解释：

- 内置模块：require的是**包名**。

- 下载的第三方模块：require的是**包名**。

- 自定义模块：require的是**文件路径**。文件路径既可以用绝对路径，也可以用相对路径。后缀名`.js`可以省略。


**代码举例**：

```js
const module1 = require('./main.js');

const module2 = require('./main');

const module3 = require('Demo/src/main.js');
```

**require()函数的两个作用**：

- **执行导入的模块中的代码。(别忽略这一条)**

- 返回导入模块中的接口对象。

---

### 主模块

主模块是整个程序执行的入口，可以调度其他模块。

```bash
# 运行main.js启动程序。此时，main.js就是主模块
$ node main.js
```

---

### 模块的初始化

一个模块中的 JS 代码仅在模块**第一次被使用时**执行一次，并且在使用的过程中进行初始化，然后会被缓存起来，便于后续继续使用。

仅在模块**第一次被使用时**执行一次

仅在模块**第一次被使用时**执行一次

仅在模块**第一次被使用时**执行一次

代码举例：

（1）calModule.js:

```js
var a = 1;

function add () {
  return ++a;
}

exports.add = add;

```

（2）main.js：（在 main.js 中引入 hello.js 模块）

```js
var addModule1 = require('./calModule')
var addModule2 = require('./calModule')

console.log(addModule1.add());
console.log(addModule2.add());
```

在命令行执行 `node main.js` 运行程序，打印结果：

```bash
2
3
```

从打印结果中可以看出，`calModule.js`这个模块虽然被引用了两次，但只初始化了一次。

---

## 8. Node.js 三大模块

- Node.js 的API文档（英文）： <https://nodejs.org/docs/latest-v8.x/api/index.html

- Node.js 的API文档（中文）：<http://nodejs.cn/api/

关于 Node.js 的内置模块和常见API，可以看官方文档。


查阅文档时，稳定指数如下：

- 红色：废弃。

- 橙色：实验。表示当前版本可用，其他版本不确定。也许不向下兼容，建议不要在生产环境中使用该特性。

- **绿色：稳定。与 npm 生态系统的兼容性是最高的优先级。**

---

### Node.js 中模块的分类


Node.js 应用由模块组成，采用 CommonJS 模块规范。Node.js中的模块分为三种：

- 内置模块 (核心模块)

- 第三方模块

- 自定义模块


---

### 内置模块

```js
// path 是 node.js 自带的内置模块
const path = require("path");
```

require方法用于加载模块。

常见的内置模块包括：

- FS：文件系统模块

- path：路径模块

- OS：操作系统相关

- net：网络相关

**但其实JS本身是没有能力获取底层系统资源的，这一切都是 JS虚拟机在和底层做交互，然后通过 JS 的表现形式，暴露给应用层。**

**有很多库，是直接使用C/++编写的，通过编译之后，再提供给 JS 应用层调用，或者直接提供给 Node.js层使用。**

---

### 第三方包

### 

```js
// 需要提前通过 npm 下载以后才可以使用
const mysql= require('mysql');
```

require 加载第三方包的机制：

（1）**第三方包安装好后，这个包一般会存放在当前项目的 node_modules 文件夹中。**我们找到这个包的 package.json 文件，并且找到里面的main属性对应的入口模块，这个入口模块就是这个包的入口文件。

（2）如果第三方包中没有找到package.json文件，或者package.json文件中没有main属性，则**默认加载第三方包中的index.js文件。**

（3）如果在 node_modules 文件夹中没有找到这个包，或者**以上所有情况都没有找到，则会向上一级父级目录下查找node_modules文件夹，查找规则如上一致。**

（4）**如果一直找到该模块的磁盘根路径都没有找到，则会报错：can not find module xxx。**

### 自定义模块

每个文件就是一个模块，有自己的作用域。在一个文件里面定义的变量、函数、类，都是私有的，对其他文件不可见。

举例：

```js
var example = require('./example.js');
```

这里需要用到 `./` 来表示当前文件所在的目录
除此之外, `../` 表示上一级, 而`/`表示下一级

## 9. fs 模块 (主要是对目录下文件的操作)

在使用模块之前要先进行导入核心模块

```js
const fs = require("fs");
```

---

### Node.js 中的同步和异步的区别

fs模块对文件的几乎所有操作都有同步和异步两种形式。例如：readFile() 和 readFileSync()。

区别：

- **同步调用会阻塞代码的执行，异步则不会。**

- 异步调用会将 读取任务 下达到任务队列，直到任务执行完成才会回调。

- 异常处理方面：**同步必须使用 try catch 方式，异步可以通过回调函数的第一个参数。**

---

### fs.readFile() 异步读取文件 

语法格式：

```js
fs.readFile(file[, options], callback(error, data))
```

代码举例：

```javascript
const fs = require('fs');

fs.readFile('hello.txt', 'utf8', (err, data) ={
    if (err) {
        // 失败
        console.log(err)
    } else {
        // 成功
        console.log('异步读取数据：' + data2)
    }
});
```


对这一模块的封装

```js
var fs = require('fs');

function fsRead(path) {
    return new Promise((resolve, reject) ={
        fs.readFile(path, { flag: 'r', encoding: "utf-8" }, (err, data) ={
            if (err) {
                //失败执行的内容
                reject(err)
            } else {
                //成功执行的内容
                resolve(data)
            }
        })
    })
}
```

---

### fs.readFileSync() 同步读取文件 

语法格式：

```js
fs.readFileSync(file[, options])
```

代码举例：

```javascript
const fs = require('fs');

try {
  const data = fs.readFileSync('hello.txt', 'utf8');
  console.log(data);
} catch(e) {
  // 文件不存在，或者权限错误
  throw e;
}
```

---

### fs.write() 写入文件

语法格式：

```js
fs.write(path, "要写入的文本内容"[, position[, encoding]], callback)
```

封装：

```js
let fs = require('fs')

function writeFs(path, content) {
    return new Promise(function (resolve, reject) {
        fs.writeFile(path, content, { flag: "a", encoding: "utf-8" }, function (err) {
            if (err) {
                //console.log("写入内容出错")
                reject(err)
            } else {
                resolve(err)
                //console.log("写入内容成功")
            }
        })
    })
}
```

---

### fs.unlink() 删除文件

语法格式：

```js
fs.unlink(path, callback)
```

参数说明：

- path：文件路径。
- callback：回调函数。


代码举例：

```js
const fs =require("fs");
fs.unlink('./a.js', (err) ={
    if (err) throw err;
    console.log('文件删除成功');
});
```

备注：`fs.unlink()` 不能用于删除目录。 如果要删除目录，可以使用 `fs.rmdir()`。

---

### fs.readdir() 读取目录下的文件


语法格式：

```js
fs.readdir(path[, options], callback)
```

代码举例：

```js
var fs = require("fs");

fs.readdir("../dist",function(err, files){
    if (err) {
        return console.error(err);
    }
    files.forEach( function (file){
        console.log( file );
    });
});
```


## 10. path 模块 （路径以及文件后缀等）

### path.extname() 获取文件/路径的扩展名

语法格式：

```js
 path.extname(myPath);
```

代码解释：

- 获取 `myPath` 这个文件或者路径的扩展名。

- `myPath` 这个参数要求是字符串。如果 `myPath` 不是字符串，则抛出 TypeError。

代码举例：

```js
const path = require('path');

path.extname('hello.txt'); // 返回 '.txt'

path.extname('www.qianguyihao.com'); // 返回 '.com'

path.extname('index.coffee.md');  // 返回 '.md'

path.extname('index.');  // 返回 '.'

path.extname('index');  // 返回 ''

path.extname('.index');  // 返回 ''

path.extname('.index.md');  // 返回 '.md'

```

---

### path.resolve() 生成完成的绝对路径

语法格式：

```js
path.resolve([...myPaths])
```

解释：

- 将路径或路径片段的序列解析为绝对路径。

- 返回的路径是**从右往左**处理，后面的每个 myPath 被依次解析，直到构造出一个完整的绝对路径。

代码举例：

```js
const path = require('path');
let paths = ["ximingx","luoyue","none"]
let allpath = path.resolve(...paths)
console.log(allpath) 
```

执行结果：

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/dd418074c31344f395b225cb838c59d8.png)

---

### 几个常见路径

- `__dirname`：这是一个常量，表示：当前执行文件所在**完整目录**。

- `__filename`：这是一个常量。表示：当前执行文件的**完整目录 + 文件名**。

- `process.cwd`：获取当前执行 Node命令 时的目录名。


代码举例：

```js
const path = require('path');
console.log(__dirname)
console.log(__filename)
console.log(process.cwd())
```

运行结果：

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220326115533395.png)

---

### path.join() 将多个路径进行拼接

如果是我们手动拼接路径，容易出错。这个时候，可以利用 path.join() 方法将路径进行拼接。

语法格式：

```js
path.join([...paths]);
```

解释：使用平台特定的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。

代码举例：

```js
const path = require('path');

const result1 = path.join(__dirname, './app.js');
console.log(result1); 

const result2 = path.join('/foo1', 'foo2', './foo3');
console.log(result2); 

const result3 = path.join('/foo1', 'foo2', '/foo3');
console.log(result3);
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220326115529960.png)

## express 框架操作 mysql 数据库


（1）安装 mysql 包：

```bash
npm install mysql
```

（2）引入 mysql 包：

```js
const mysql = require("mysql");
```

（3）建立连接：

```js
let mysql = require("mysql");
let options = {
  host: "localhost",
  port:"3306", 
  user: "root",
  password: 'root', // 这里改成你自己的数据库连接密码
  database: "test",
};
//创建与数据库进行连接的连接对象
let connection = mysql.createConnection(options);

//建立连接
connection.connect((err) ={
  if (err) {
      // 数据库连接失败
    console.log(err);
  } else {
      // 数据库连接成功
    console.log("数据库连接成功");
  }
});
```

---

 对数据库的操作, 执行sql操作

```js
connection.query(sql,function (err, results) {
  if (err) {
    console.log("操作失败");
  } else {
    console.log("操作成功");
  }
})
```

---

### 增删改查操作

```js
/**
 * 引入包
 * */
const express = require('express')
let app = express()
const mysql = require('mysql');

/**
 * 连接数据库
 * */
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '123456',
  database: '2011'
});
connection.connect(function (err) {
  if (err) {
    console.error('error connecting: ' + err.stack);
    return;
  }
  console.log('mysql connect successful');
});


/**
 * 数据库查询
 * */
// 定义参数
let params = [];
let sql = "";

// 查询数据
sql = "select * from user";
connection.query(sql,function (err, results) {
  if (err) {
    console.log("查询失败");
  } else {
    console.log(results)
    console.log("查询成功");
  }
})

// 增加数据
sql = "insert into user (`index`, `id`, `name`, `password`) value ('100', '202016131000', 'test', '202016131000')";
connection.query(sql,function (err, results) {
  if (err) {
    console.log("增加失败");
  } else {
    console.log("增加成功");
  }
})

// 修改数据
sql = "update user set name = ?, age = ?,sex = ? where id = ?";
params = ['ximingx','18','男','202016131000']
connection.query(sql, params, function (err, results) {
  if (err) {
    console.log("修改失败");
  } else {
    console.log("修改成功")
  }
})

// 删除数据
sql = "delete from `user` where `index` = 100";
connection.query(sql,function (err, results) {
  if (err) {
    console.log("删除失败");
  } else {
    console.log("删除成功")
  }
})

/**
 * 开放端口
 * */
let port = 3000
app.listen(port,() ={
  console.log(
    `   ◢＼　 ☆　　 ／◣
　  　∕　　﹨　╰╮∕　　﹨
　  　▏　　～～′′～～ 　｜
　　  ﹨／　　　　　　 　＼∕
　 　 ∕ 　　●　　　 ●　＼
  ＝＝　○　∴·╰╯　∴　○　＝＝
　    ╭──╮　　　　　╭──╮
  ╔═ ∪∪∪═ running ${port} port ═∪∪∪═╗`)
})
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_19,color_FFFFFF,t_70,g_se,x_16.png)

## node express解决跨域

```js
const express = require('express')
// import router from './routes/index.js';
const app = express();

// 设置允许跨域访问该服务
app.all('*', function (req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header('Access-Control-Allow-Methods', 'PUT, GET, POST, DELETE, OPTIONS');
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  res.header('Access-Control-Allow-Headers', 'mytoken');
  next();
});
```

## 内网穿透

### 首先强调几个遇到的问题

1. 直接打开 `vue` 打包后的 `dist` 文件夹里的 `index.html` 是无法正常访问的,因为资源的路径会发生问题
2. 跨域问题
3. 使用 `node` 开放资源目录
4. `natapp` 连接隧道失败
5. 以下步骤要配置`node`环境
![在这里插入图片描述](https://img-blog.csdnimg.cn/19445681fe224eeb97aeab96c2e54a7c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_11,color_FFFFFF,t_70,g_se,x_16)
### 过程

首先将 `vue` 项目打包, 生成dist文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/10659e5de6754b51b42eb205a94e596a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
直接把 `dist` 文件夹放到 node 服务器与 app.js 同级目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/b14438cfe24642dc821d26321c38681d.png)
此时我们进入 `app.js` 

```js
const express = require('express')
const app = express();

// 设置允许跨域访问该服务
app.all("*",function(req,res,next){
  //设置允许跨域的域名，*代表允许任意域名跨域
  res.header("Access-Control-Allow-Origin","*");
  //允许的header类型
  res.header("Access-Control-Allow-Headers","content-type");
  //跨域允许的请求方式
  res.header("Access-Control-Allow-Methods","DELETE,PUT,POST,GET,OPTIONS");
  if (req.method.toLowerCase() == 'options') {
    res.send(200);
  }  //让options尝试请求快速结束
  else {
    next();
  }
})

// 开放服务器 dist 目录,访问时会自动寻找index.html文件
app.use(express.static('dist'))

// 端口
app.listen(3000,function () {
  console.log("// -----------------------------------------------------------------------")
  console.log("port 3000 is listening")
});
```
在当前项目的server目录, 命令行运行
```bash
node app.js
```
<font color="red">此时的网页仅仅是可以在本地访问, 但是使用了内网穿透技术, 我们可以使得别人直接访问到我们本地的项目, 不需要部署服务器, 对于用于测试和买不起服务器的我表示很香</font>

好的,下面演示

首先需要进入 `natapp` 的官网 [官网链接](https://natapp.cn/)

然后选择注册或者登录, 需要实名认证
![在这里插入图片描述](https://img-blog.csdnimg.cn/7351fd56b83f44d3be30f983a593c6e0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
注册完毕后 看那个免费隧道, 真的不错
![在这里插入图片描述](https://img-blog.csdnimg.cn/3b2aa17c2c4345f199e809c6190c9e67.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
在配置隧道的时候, 需要注意的是, 我node服务器使用的端口号是 3000
这里也需要填写 3000
![在这里插入图片描述](https://img-blog.csdnimg.cn/bbc6fb5be12d4dd5a626d422ecbfba10.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
and, 写到这里的时候, 我突然想起来还要安装下载 natapp, 但是很简单, 不要慌
![在这里插入图片描述](https://img-blog.csdnimg.cn/0ce788c6a35a46c1a3341e5df14ad1ca.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
然后直接安装就可以了

![在这里插入图片描述](https://img-blog.csdnimg.cn/a091f76615154f66b11ca5ca9ed7c639.png)
在 config.ini 需要配置一下
```bash
#将本文件放置于natapp同级目录 程序将读取 [default] 段
#在命令行参数模式如 natapp -authtoken=xxx 等相同参数将会覆盖掉此配置
#命令行参数 -config= 可以指定任意config.ini文件
[default]
authtoken=你自己的隧道authtoken,可以在natapp官网里的我的隧道查看               #对应一条隧道的authtoken
clienttoken=                    #对应客户端的clienttoken,将会忽略authtoken,若无请留空,
log=none                        #log 日志文件,可指定本地文件, none=不做记录,stdout=直接屏幕输出 ,默认为none
loglevel=ERROR                  #日志等级 DEBUG, INFO, WARNING, ERROR 默认为 DEBUG
http_proxy=                     #代理设置 如 http://10.123.10.10:3128 非代理上网用户请务必留空
```
配置完成后, 点击 `natapp,exe `, 如果显示的是下面的页面, 表示成功了
![在这里插入图片描述](https://img-blog.csdnimg.cn/6b97a502fcd24335a8d6503bf774730b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
然后搜索你下面红框中的 http地址, 即可成功实现![在这里插入图片描述](https://img-blog.csdnimg.cn/f044573ddbe04c8c9b1b9dc3ac267f7a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
最后演示一下成果, 已经可以在手机访问了
![在这里插入图片描述](https://img-blog.csdnimg.cn/6644e0f26716451f93169c0df32ed659.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
<font color="red">当然在最后一步连接隧道时, 可能会遇到问题, 报错的评论区扣,或者私信截图</font>

### 连接隧道报错解决方法

显示如下图: 
![在这里插入图片描述](https://img-blog.csdnimg.cn/5e1cbec2c889441da405e5ed96bff812.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
[更换阿里公共DNS](https://natapp.cn/article/alidns)
[连不上网络错误调试排查详解](https://natapp.cn/article/networkerrors)

## 网易云接口

**目的功能:**
1. axios 请求获取歌曲的 url 以及 封面照片
2. 切换歌曲
3. 显示当前歌曲的时间,剩余时间
4. 进度条颜色改变
5. 刷新重置进度
6. 歌单的展示

![在这里插入图片描述](https://img-blog.csdnimg.cn/816f80d586a049f9b304019b8ea10376.png#pic_center)


**先展示一波:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/0f4704dd57d1447fa72c1fd3252da280.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
**and**
![在这里插入图片描述](https://img-blog.csdnimg.cn/793be68e640c4405a1ee71cdd7b33b3e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
**首先声明一点: 这里引用的不是官方的网易云接口**
**网易云音乐接口  github地址**  
```bash
https://github.com/Binaryify/NeteaseCloudMusicApi
```
**安装**
```bash
git clone git@github.com:Binaryify/NeteaseCloudMusicApi.git
```
**在他的目录下**
```bash
npm install
```
运行
```bash
node app.js
```
运行后我么可以在
```bash
http://localhost:3000/
```
打开文档
![在这里插入图片描述](https://img-blog.csdnimg.cn/374ae94668b147bca1dac96acd2b9127.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
借此我们可以请求歌单和歌曲的 url 地址 ,  歌曲照片地址等等,详细功能可以自己查看

以上全部借助别人的 api 接口

**这里重点强调一下 获取歌曲 url 的 api**
![在这里插入图片描述](https://img-blog.csdnimg.cn/f0b95cdfb05f460d876e145d367379e9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
需要传入歌曲的 id 返回 url 地址

下面是自己写的样式

```html
<template>
  <div class="music" ref="music">
    <audio :src="audioSrc" ref="audio" autoplay="autoplay"></audio>
    <div class="left">
      <img :src="picUrl" alt="" ref="img">
    </div>
    <div class="right">
      <div class="top">
        <div class="left_item">
          <div>
            <i class="el-icon-arrow-left" ref="left"></i>
          </div>
          <div @click="playMusic">
            <i v-if="isPlaying" class="el-icon-video-pause" ref="start" key="el-icon-video-pause"></i>
            <i v-else class="el-icon-video-play" ref="end" key="el-icon-video-play"></i>
          </div>
          <div>
            <i class="el-icon-arrow-right" ref="right"></i>
          </div>
        </div>
        <div class="right_item">
          <div>
            <i class="el-icon-s-unfold" ref="list"></i>
          </div>
          <div>
            <i class="el-icon-refresh" ref="refresh"></i>
          </div>
        </div>
      </div>
      <div class="bottom">
        <div class="span">
          <p ref="nowData">{{ nowData }}</p>
          <P id="audioName">{{ audioName }}</P>
          <p ref="totalData">{{ total }}</p>
        </div>
        <div class="progress" ref="progress"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: "NewAudio",
  data:function () {
    return {
      isPlaying: false,
      now: '00:00',
      total: '00:00',
      img: [],
      currentIndex: 0,
      audioId: 0,
      audioName: '未知',
      picUrl: '',
      audioSrc: '',
      timer: null,
      nowData: '00:00'
    }
  },
  computed: {

  },
  methods: {
    playMusic:function () {
      if (this.$refs.audio.paused) {
        this.$refs.audio.play()
        this.isPlaying = !this.isPlaying
        this.judgeTime()
        return true;
      }
      this.$refs.audio.pause()
      this.timer = null
    },
    getId:function () {
      const instance = axios.create({
        baseURL: 'http://localhost:3000/',
        timeout: 10000,
      })
      return instance.get('/personalized/newsong').then((data) => {
        let number = Math.ceil(Math.random() * 30);
        this.img = data.data.result[number]
        console.log(this.img)
        this.audioId = this.img.id
        this.audioName = this.img.name
        this.picUrl = this.img.picUrl
        this.getMusic().catch(() => {
          this.getId()
        })
      })
    },
    getMusic() {
      const instance = axios.create({
        baseURL: 'http://localhost:3000/',
        timeout: 10000,
      });
      return instance.get("song/url?id=" + this.audioId).then((data) => {
        this.audioSrc = data.data.data[0].url
      })
    },
    judgeTime() {
      this.timer = setInterval(()=>{
        this.now = Math.ceil(this.$refs.audio.currentTime)
        let data = Math.floor(this.now / 60)
        let seconds = Math.ceil(this.now % 60)
        if (data === 0) {
          data = "00"
        } else if (data > 0 && data <10) {
          data = "0" + data
        }
        if (seconds === 0) {
          seconds = "00"
        } else if (seconds > 0 && seconds <10) {
          seconds = "0" + seconds
        }
        this.nowData = data + ":" +seconds
      },1000)
    },
  },
  mounted() {
    this.getId().catch(() => {
      this.getId()
    })
  }
}
</script>

<style lang="less" scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.music {
  background-image: url("../../assets/img/2.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  border-radius: 10px;
  min-width: 200px;
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  color: rgb(253, 253, 253);
  .left {
    img {
      padding: 20%;
      min-height: 80px;
      height: 8vw;
      min-width: 80px;
      width: 8vw;
      border-radius: 50%;
      animation: rotate 18s linear;
      animation-iteration-count: infinite;
      -webkit-animation: rotate 18s linear;
      -webkit-animation-iteration-count: infinite;
    }
  }
  .right {
    flex: 1;
    margin: 0 30px 0 0;
    height: 5vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    .top {
      margin-top: 10px;
      width: 100%;
      display: flex;
      justify-content: space-between;
      .left_item,.right_item {
        display: flex;
      }
    }

    .bottom {
      display: flex;
      flex-direction: column;
      justify-content: center;
      width: 100%;
      .span {
        display: flex;
        width: 100%;
        justify-content: space-between;
        p {
          padding: 0;
        }
      }
      .progress {
        height: 3px;
        width: 100%;
        background: rgba(255, 255, 255, 0.68);
        margin-bottom: 10px;
      }
    }
  }
}
#audioName {
  margin: 0 20px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
@-webkit-keyframes rotate {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes rotate {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
```

当然,所有的功能还没有全部实现,未完待续
搞了一天,累了,回家

 **\> _<**



# Node.js

Node.js 的 中文官网地址：**https://nodejs.org/zh-cn/**

## 1. 什么是 Node.js

Node.js 是一个基于 **Chrome V8 引擎的 JavaScript 运行环境** 。Node.js 使用了一个**事件驱动**、**非阻塞式 I/O**的模型，使其轻量又高效。Node.js 的**包管理工具 npm 是全球最大的开源库生态系统。**

V8引擎执行`Javascript`的速度非常快，性能非常好。`Node.js`对一些特殊用例进行了优化，提供了替代的API，使得V8在非浏览器环境下运行得更好；

Node.js 不是一门语言，也不是 JavaScript 的框架，也不是像Nginx一样的Web服务器 ，**Node.js 是 JavaScript 在服务器端的运行环境（平台）**。

使用 node.js 我们可以做什么: 

- 基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用；
- 基于 Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用；
- 基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目；
- 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc；


---

### node.js的组成

我们知道，JavaScript 的组成分为三个部分：

-   ECMAScript

-   DOM：标签元素相关的API (文档对象模型)

-   BOM：浏览器相关的API (浏览器对象模型)

ECMAScript 是 JS 的语法；DOM 和 BOM 浏览器端为 JS 提供的 API。

而 Node.js 的组成分为：

-   **ECMAScript**。ECMAScript 的所有语法在 Node 环境中都可以使用。

-   **Node 环境提供的一些附加 API**(包括文件、网络等相关的 API)。

在 Node.js 里运行 JavaScript，跟在 Chrome 里运行 JavaScript 有什么不同？

二者采用的是同样的 JS 引擎。在 Node.js 里写 JS，和在浏览器部分的 JS 文件，几乎没有不同。在写法上的区别在于：Node.js 没有浏览器、页面标签相关的 API，但是新增了一些 Node.js 相关的 API。**通俗来说，对于开发者而言，在前端写 JS 是用于控制浏览器；而 Node.js 环境写 JS 可以控制整个计算机。**

---

### Node.js 的架构和依赖

Node.js 内部采用 Google Chrome 的 V8 引擎，作为 JavaScript 语言解释器；同时结合自行开发的 libuv 库，**扩展了 JS 在后端的能力（比如 I/O 操作、文件读写、数据库操作等）**。使得 JS 既可以在前端进行 DOM 操作（浏览器前端），又可以在后端调用操作系统资源，是目前最简单的全栈式语言。

其次，Node 生态系统活跃，提供了大量的开源库，使得 JavaScript 语言能与操作系统进行更多的交互。

Node.js 是 JavaScript 在服务器端的运行环境，在这个意义上，Node.js 的地位其实就是 JavaScript 在服务器端的虚拟机，类似于 Java 语言中的 Java 虚拟机。

-   [V8 引擎](https://v8.dev/) ：编译和执行 JS 代码、管理内存、垃圾回收。V8 给 JS 提供了运行环境，可以说是 JS 的虚拟机。V8 引擎本身是用 C++ 写的。
-   [libuv](https://zh.wikipedia.org/wiki/Libuv)： libuv 是一个专注于异步 I/O 的跨平台类库，目前主要在 Node.js 上使用。它是 Node.js 最初的作者 Ryan Dahl 为 Node.js 写的底层类库，也可以称之为虚拟机。libuv 本身是用 C 写的。

**注意:** 

- 浏览器是 JavaScript 的前端运行环境；
- Node.js 是 JavaScript 的后端运行环境；
- Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API；

---

### V8 的内存限制

在一般的后端开发语言中，在基本的内存使用上没有什么限制，然而在 Node 中通过 JavaScript 使用内存时就会发现只能使用部分内存（64 位系统下约为 1.4GB，32 位系统下约为 0.7GB）。在这样的限制下，将会导致 **Node 无法直接操作大内存对象。**

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
- ( 2022年 微软决定停止继续使用ie,  前端狂喜 但还是有必要了解一下 ie6 的坑 )

---

### 进程（进行中的程序）

- 每一个正在运行的应用程序都称之为进程。

- 每一个应用程序运行都至少有一个进程。

- 进程是用来给应用程序提供一个运行的环境。

- 进程是操作系统为应用程序分配资源的一个单位。

---

### 线程

- 用来执行应用程序中的代码

- 在一个进程内部，可以有很多的线程

- 在一个线程内部，同时只可以干一件事

- **传统的开发方式大部分都是 I/O 阻塞的，所以需要多线程来更好的利用硬件资源。**

线程并不是越多越好。

### 多线程的弊端

缺点一：

- 创建线程耗费。
- 线程数量有限。
- CPU 在不同线程之间转换，有个上下文转换，这个转换非常耗时。

**所谓的多线程其实都是假的，对于单核CPU而言，它们无非是在抢占 CPU 资源。线程和线程之间需要切换和调度，这是很耗费资源的。**

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

如果希望通过 `Node.js` 来运行 Javascript 代码，则必须在计算机上安装 `Node.js` 环境才行。

安装包可以从 `Node.js` 的官网首页直接下载，进入到 `Node.js` 的官网首页（[**https://nodejs.org/en/**](https://nodejs.org/en/)），点击绿色的按钮，下载所需的版本后，双击直接安装即可。

![image-20220407144134973](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204071441034.png)

[Node.js 安装可以看这篇博客 https://blog.csdn.net/Yang_yangyang/article/details/121907688](https://blog.csdn.net/Yang_yangyang/article/details/121907688)

`LTS` 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装 LTS 版本的 Node.js；

`Current` 为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装 Current 版本的 Node.js。但是，Current 版本中可能存在隐藏的 Bug 或安全性漏洞，因此不推荐在企业级项目中使用 Current 版本的 Node.js；

后面的各种包版本兼容问题很是麻烦

> Node.js 版本常识
> 偶数版本为稳定版（0.6.x ，0.8.x ，8.10.x）
> 奇数版本为非稳定版（0.7.x ，0.9.x ，9.11.x）

### 安装过程

1. 打开官网下载链接:https://nodejs.org/en/download/ 
2. 选择自己需要的版本， 不建议版本太高

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204150834938.png)

3. 点击安装包

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204150834155.png)

4. 一路 next 下去就可以啦

5. 安装完毕后, 可以打开终端，在终端输入命令 `node –v` 后，按下回车键，即可查看已安装的 Node.js 的版本号；

![image-20220407144331354](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204071443400.png)

**终端中快捷操作**

- **使用 ↑ 键，可以快速定位到上一次执行的命令；**
- **使用 tab 键，能够快速补全路径；**
- 使用 esc 键，能够快速清空当前已输入的命令；
- 输入 cls 命令，可以清空终端；

6. 打开 node 的安装目录

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204150835091.png)

7. 配置： 在我安装的文件夹【D:\Develop\nodejs】下创建两个文件夹【node_global】及【node_cache】如下图：

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204150836653.png)

8. 命令行输入

```bash
npm config set prefix "D:\Develop\nodejs\node_global"
npm config set cache "D:\Develop\nodejs\node_cache"
```

9. 环境配置

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204150837796.png)

进入环境变量对话框，在【系统变量】下新建【NODE_PATH】，输入【D:\Develop\nodejs\node_global\node_modules】，将【用户变量】下的【Path】修改为【D:\Develop\nodejs\node_global】

10. 测试

配置完后，安装个module测试下，我们就安装最常用的express模块，打开cmd窗口，
输入如下命令进行模块的全局安装：

```bash
npm install express -g     # -g是全局安装的意思
```

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

NPM：Node Package Manager。官方链接： <https://www.npmjs.com/

Node.js 发展到现在，已经形成了一个非常庞大的生态圈。包的生态圈一旦繁荣起来，就必须有工具去来管理这些包。NPM 应运而生。

举个例子，当我们在使用 Java 语言做开发时，需要用到 JDK 提供的内置库，以及第三方库。同样，在使用 JS 做开发时，我们可以使用 NPM 包管理器，方便地使用成熟的、优秀的第三方框架，融合到我们自己的项目中，极大地加速日常开发的构建过程。

随着时间的发展，NPM 出现了两层概念：

-   一层含义是 Node 的开放式模块登记和管理系统，亦可以说是一个生态圈，一个社区。

-   另一层含义是 Node 默认的模块管理器，是一个命令行下的软件，用来安装和管理 Node 模块。

NPM 不需要单独安装。默认在安装 Node 的时候，会连带一起安装 NPM

### package.json

在项目根目录中，创建一个叫做 `package.json` 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录之后，在团队成员之间共享项目的源代码。

`package.json` 的包管理配置文件。用来记录与项目有关的一些配置信息。例如：

- 项目的名称、版本号、描述等；
- 项目中都用到了哪些包；
- 哪些包只在开发期间会用到；
- 哪些包在开发和部署时都需要用到；

npm 包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，快速创建 `package.json` 这个包管理配置文件：

```js
npm iniy -y
```

当我们拿到一个剔除了 node_modules 的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。

可以运行 `npm install` 命令（或 `npm i`）一次性安装所有的依赖包：

```bash
npm install
```

可以运行 `npm uninstall` 命令，来卸载指定的包：

```bash
npm uninstall mysql
```

在使用 npm 下包的时候，默认从国外的 https://registry.npmjs.org/ 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢。

淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包**同步**到国内的服务器，然后在国内提供下包的服务。从而极大的提高了下包的速度。

```bash
npm config set registry http://registry.npm.taobao.org/
```

**初次装包完成后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件；**

**node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包；**

**package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等, 以及各个包之间的依赖关系；**

## 6. 模块化


概念：将一个复杂的程序依据一定的规则（规范）封装成几个块（文件），并组合在一起。

**模块的内部数据、实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信。**

最早的时候，我们会把所有的代码都写在一个js文件里，那么，耦合性会很高（关联性强），不利于维护；而且会造成全局污染，很容易命名冲突。

Node.js中根据模块来源的不同，将模块分为了 3 大类，分别是：

- **内置模块**（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）；
- **自定义模块**（用户创建的每个 .js 文件，都是自定义模块）；
- **第三方模块**（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）；


---

### 模块化的好处

- 避免命名冲突，减少命名空间污染
- 降低耦合性；更好地分离、按需加载
- **高复用性**：代码方便重用，别人开发的模块直接拿过来就可以使用，不需要重复开发类似的功能。
- **高可维护性**：软件的声明周期中最长的阶段其实并不是开发阶段，而是维护阶段，需求变更比较频繁。使用模块化的开发，方式更容易维护。
- 部署方便

---

### 模块的加载机制

模块在第一次加载后会被缓存。 这也意味着多次调用 `require()` 不会导致模块的代码被执行多次。

不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。

当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：

- 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口；
- 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件；
- 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'；

---

**当模块拥有路径但没有后缀时**

```js
require('./find');
```

- require方法根据模块路径查找模块，如果是完整路径，直接引入模块。
- 如果模块后缀省略，先找同名JS文件再找同名JS文件夹
- 如果找到了同名文件夹，找文件夹中的index.js
- 如果文件夹中没有index.js就会去当前文件夹中的package.json文件中查找main选项中的入口文件
- 如果找指定的入口文件不存在或者没有指定入口文件就会报错，模块没有被找到

**当模块没有路径且没有后缀时**

- Node.js会假设它是系统模块
- Node.js会去node_modules文件夹中
- 首先看是否有该名字的JS文件
- 再看是否有该名字的文件夹
- 如果是文件夹看里面是否有index.js
- 如果没有index.js查看该文件夹中的package.json中的main选项确定模块入口文件
- 否则找不到报错

---

###  模块化的概念解读

模块化起源于 Node.js。Node.js 中把很多 js 打包成 package，需要的时候直接通过 require 的方式进行调用（CommonJS），这就是模块化的方式。


---

### 模块化规范

- AMD 和 CMD 适用于浏览器端的 Javascript 模块化；
- CommonJS 适用于服务器端的 Javascript 模块化；

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

语法格式：

```js
// 相当于是：给 exports 对象添加属性
exports.xxx = value
```

这个 value 可以是任意的数据类型。

**注意**：暴露的关键词是`exports`，不是`export`。其实，这里的 exports 类似于 ES6 中的 export 的用法，都是用来导出一个指定名字的对象。

代码举例：

```js
const name = 'ximingx';

const foo = function (value) {
	return value * 2;
};

exports.name = name;
exports.foo = foo;
```

---

### **暴露模块的方式二： module.exports**

- **Node中每个模块的最后，都会执行 `return: module.exports`。**
- **Node中每个模块都会把 `module.exports`指向的对象赋值给一个变量 `exports`，也就是说 `exports = module.exports`。**

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

- **Node中每个模块的最后，都会执行 `return module.exports`。**
- **Node中每个模块都会把 `module.exports`指向的对象赋值给一个变量 `exports`，也就是说 `exports = module.exports`。**
- `module.exports = XXX`，表示当前模块导出一个单一成员，结果就是XXX。
- 如果需要导出多个成员，则必须使用 `exports.add = XXX; exports.foo = XXX`。或者使用 `module.exports.add = XXX; module.export.foo = XXX`。

使用 `require()` 方法导入模块时，导入的结果，**永远以 module.exports 指向的对象为准**；

**这里需要注意 exports 与 module.exports 的指向问题**


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

关于 Node.js 的内置模块和常见API，可以看官方文档。（ps： 实话实说， 第一次直接看真的是要了我的老命）

**node.js 内置模块的函数参数错误优先, 当 err 对象没有值时(即函数正常运行), 默认值为 null**


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

常见的内置模块包括：

- FS：文件系统模块
- path：路径模块
- OS：操作系统相关
- net：网络相关
- http： 创建 web 服务器

**但其实JS本身是没有能力获取底层系统资源的，这一切都是 JS虚拟机在和底层做交互，然后通过 JS 的表现形式，暴露给应用层。**

**有很多库，是直接使用C/++编写的，通过编译之后，再提供给 JS 应用层调用，或者直接提供给 Node.js层使用。**

---

### 第三方包

```js
// 需要提前通过 npm 下载以后才可以使用
// npm install mysql
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

## 9. fs 模块

> fs 模块是 `Node.js` 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

在使用模块之前要先进行导入核心模块

```js
const fs = require("fs");
```

---

### Node.js 的同步异步的区别

fs模块对文件的几乎所有操作都有同步和异步两种形式。例如：readFile() 和 readFileSync()。

区别：

- **同步调用会阻塞代码的执行，异步则不会。**

- 异步调用会将 读取任务 下达到任务队列，直到任务执行完成才会回调。

- 异常处理方面：**同步必须使用 try catch 方式（捕获异常， 放置程序中断），异步可以通过回调函数的第一个参数。**

---

### fs.readFile() 

语法格式：

```js
fs.readFile(file[, options], callback(error, data))
```

> - **参数1：必选参数，字符串，表示文件的路径。**
> - 参数2：可选参数，表示以什么编码格式来读取文件。
> - **参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。**

第二个参数是对象`options`，有`encoding`(编码，默认值为null)和`flag`(标识位，默认值为 r )。也可以直接传入`encoding`，通常为求简便，都是直接传入encoding。

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
    // 返回一个 Promise 对象, 对其执行 .then 操作来进行获取之以后的过程
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

### fs.readFileSync() 

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

### fs.writeFile()

可以用来记录报错日志

写入文件

语法格式：

```js
fs.writeFile(path, "要写入的文本内容"[, position[, encoding]], callback)
```

> - 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
> - 参数2：必选参数，表示要写入的内容。
> - 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
> - 参数4：必选参数，文件写入完成后的回调函数。

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

### writeFileSync
writeFileSync 有3个参数：

- 第一个参数是文件路径或者文件描述符
- 第二个参数是写入的数据，类型可以是String或者Buffer
- 第三个参数是对象options，其中有 encoding(编码，默认值为utf8)、flag(标识位，默认值为w) 和 mode(权限位，默认值为0o666)。也可以直接传入enconding，为了方便，通常只传encoding即可。

---

### appendFileSync

**writeFileSync 和 writeFile 实现了文件的同步写入和异步写入，但是会直接覆盖原来的文件内容**
appendFileSync 有3个参数，和同步同步写入方法writeFileSync参数一致

---

### fs.unlink() 

删除文件

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

### fs.readdir()

读取目录下的文件


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

---

### fs.mkdirSync()

`mkdirSync` 方法参数为一个目录的路径，没有返回值，在创建目录的过程中，**必须保证传入的路径前面的文件目录都存在，否则会抛出异常。**

```js
const fs = require('fs')
fs.mkdirSync('D:/node')
```

---

### Fs.mkdir()

```js
const fs = require('fs')
fs.mkdir('D:/node',err=>{
    if(!err){
        console.log('文件夹创建成功！')
    }
})
```

---

### fs.rmdirSync()

```js
const fs = require('fs')
fs.rmdirSync('D:/node')
```

---

### fs.rmdir

```js
const fs = require('fs')
fs.rmdir('D:/node',err=>{
    if(!err){
        console.log('删除文件成功！')
    }
})
```

---

### fs.stat

判断是 目录 还是 文件

```js
function isFile(path) {
  return new Promise((resolve, reject) => {
    fs.stat(path,function(err,stat){
      if (err) {
       reject(err);
      } else {
        resolve(stat.isFile()); // 如果是文件， 返回 true
        // resolve(stat.isDirectory());  如果是目录， 返回 true
      }
    })
  })
}
```



## 10. path 模块

> 在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 …/ 开头的相对路径时，很容易出现路径动态拼接错误的问题；
>
> **解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，不要提供 ./ 或 …/ 开头的相对路径，从而防止路径动态拼接的问题**
>
> 这就需要使用到了 path 模块

path 模块是 `Node.js` 官方提供的、用来**处理路径**的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

- `path.join()`方法，用来将多个路径片段拼接成一个完整的路径字符串；
- `path.basename()` 方法，用来从路径字符串中，将文件名解析出来；

### path.extname() 

获取文件/路径的扩展名

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

### path.resolve() 

生成完成的绝对路径

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

### path.join() 

将多个路径进行拼接

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

## 11. http 模块

**http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。**

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```js
const http = require('http')
```

服务器和普通电脑的区别在于，服务器上安装了 web 服务器软件，例如：IIS、Apache 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器；

 在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务；

### 创建 web 服务器的基本步骤

1. 导入 http 模块；
2. 创建 web 服务器实例；
3. 为服务器实例绑定 **request** 事件，监听客户端的请求；
4. 启动服务器；

```js
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
// 调用 http.createServer() 方法，即可快速创建一个 web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
    console.log('server.')
})
// 4. 启动服务器
// 调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例
// 也可以不带函数启动， 只需要端口号
server.listen(3000, function () {
    console.log('server running at http://127.0.0.1:3000')
})
```

### require

只要服务器接收到了客户端的请求，就会调用通过 `server.on()` 为服务器绑定的 `request` 事件处理函数。

如果想在事件处理函数中，**访问与客户端相关的数据或属性**，可以使用如下的方式：

```js
const server = http.createServer()
// req 是请求对象，包含了与客户端相关的数据和属性
server.on('request', (req, res) => {
    // req.url 是客户端请求的 URL 地址
    const url = req.url
    // req.method 是客户端请求的 method 类型
    const method = req.method
    // 获取请求报文
    const headers = req.headers
    const str = `Your request url is ${url}, and request method is ${method}`
    // 调用 res.end() 方法，向客户端响应一些内容
    res.end(str)
})
server.listen(3000, () => {
    console.log('server running at http://127.0.0.1')
})
```

**get 请求**

```js
const http = require('http');
// url 是内置模块, 用于处理 url 地址
const url = require('url');
const app = http.createServer();
app.on('request', (req, res) => {
     // 将url路径的各个部分解析出来并返回对象
     // true 代表将参数解析为对象格式
     // 参数: 查询的地址, query 是否返回对象的形式
     let { query,pathname } = url.parse(req.url, true);
     console.log(query);
    
    // 解决路径判断问题
    if (pathname == "") {
        res.send()
    }
    
});
app.listen(3000);
```

**post 请求**

```js
const http = require('http');
const server = http.createServer();
const queryString = require("queryString");
server.on('request', function (req, res) {
    
   let postParams = ""
   
   req.on("data", (params) => {
       postParams += params
   })
    
   req.on("end", () => {
       // 将处理结果对象化
      console.log(queryString.parse(postParams))
   })
    
   res.send()
})
server.listen(3000, function () {
    console.log('server running at http://127.0.0.1:8080')
})
```

### response

在服务器的 `request` 事件处理函数中，如果想**访问与服务器相关的数据或属性**，可以使用如下的方式：

```js
server.on("request",(require, response) => {
    console.log(response);
})
```

- 200 请求成功
- 404 请求资源错误
- 500 服务器端

```js
server.on('request', (req, res) => {
    // 设置状态码
    res.writeHead(500, {
        // 默认值
        "content-type": "text/plain"
    });
})
```

类型
- **text/html**
- text/css
- application/javascript
- image/jpeg
- application/json

```js
server.on('request', (req, res) => {
    // 设置状态码
    res.writeHead(200, {
        // 默认值
        "content-type": "text/plain;charset=utf8"
    });
})
```

### 解决中文乱码问题

当调用 `res.end()` 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要**手动设置内容的编码格式**：

完整代码演示如下：

```js
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => {
    // 定义一个字符串，包含中文的内容
    const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
    // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
    // res.end() 将内容响应给客户端
    res.end(str)
})

server.listen(80, () => {
    console.log('server running at http://127.0.0.1')
})
```

### 根据 url  响应 内容

核心实现步骤：

- 获取请求的 url 地址；
- 设置默认的响应内容为 404 Not found；
- 判断用户请求的是否为 / 或 /index.html 首页；
- 判断用户请求的是否为 /about.html 关于页面；
- 设置 Content-Type 响应头，防止中文乱码；
- 使用 res.end() 把内容响应给客户端；

```js
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => {
    // 1. 获取请求的 url 地址
    const url = req.url
    // 2. 设置默认的响应内容为 404 Not found
    let content = '<h1>404 Not found!</h1>'
    // 3. 判断用户请求的是否为 / 或 /index.html 首页
    // 4. 判断用户请求的是否为 /about.html 关于页面
    if (url === '/' || url === '/index.html') {
        content = '<h1>首页</h1>'
    } else if (url === '/about.html') {
        content = '<h1>关于页面</h1>'
    }
    // 5. 设置 Content-Type 响应头，防止中文乱码
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
    // 6. 使用 res.end() 把内容响应给客户端
    res.end(content)
})

server.listen(80, () => {
    console.log('server running at http://127.0.0.1')
})
```

路由

```js
const http = require('http');
const app = http.createServer();
const url = require('url');
app.on('request', (req, res) => {
    let method = req.method.toLowerCase();
    let { pathname } = url.parse(req.url);
    res.setHeader(200, {
        'Content-Type': 'text/html; charset=utf-8'
    })
    
    if (method == "get") {
        
        if (pathname == "" || pathname == "index") {
            res.send()
        } 
        
    } else if (method == "post") {
        
    }
    
});
app.listen(3000);
```

## 12. 全局变量与对象

Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性, global 可以省略

### global

1. setTimeout() / clearTimeout
2. setInterval() / clearInterval
3. console 
4. process
5. __filename 当前执行脚本的文件名（全名称），即文件所在位置的绝对路径
6. __dirname 表示当前执行脚本所在的目录。

### process

**它用来描述当前Node.js进程状态的对象**，提供了一个与操作系统的简单接口，通常写`本地命令行`的程序的时候都会用到它。

- process.argv：返回一个数组，成员是当前进程的所有命令行参数。
- **process.env：返回一个对象，成员为当前Shell的环境变量，比如process.env.HOME。**
- process.installPrefix：返回一个字符串，表示 Node 安装路径的前缀，比如/usr/local。相应地，Node 的执行文件目录为/usr/local/bin/node。
- process.pid：返回一个数字，表示当前进程的进程号。
- process.platform：返回一个字符串，表示当前的操作系统，比如Linux。
- process.title：返回一个字符串，默认值为node，可以自定义该值。
- process.version：返回一个字符串，表示当前使用的 Node 版本，比如v7.10.0。
- process.cwd():表示当前文件的绝对路径
- process.on(‘exit’,function(){})表示当程序退出的时候会触发	\

![image-20220418151256489](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204181512557.png)

```JS
console.log(process.env.Lover)
// 电脑中环境变量中的 Lover 的值
// 可以用去区分开发环境与生产环境
```

![image-20220418151403391](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204181514442.png)

## 13. 静态资源

```js
const http = require('http');
const app = http.createServer();
const url = require('url');
app.on('request', (req, res) => {
    let method = req.method.toLowerCase();
    let { query, pathname } = url.parse(req.url);
    pathname = "/" ? "/default.html" : pathname
    let reqPath = path.join(__dirname, "public" + pathname)
    
    fs.readFile(reqPath, (err, data) => {
        if (err) {
            res.write(400, {
            'contentType': 'text/html;charset=utf8'
        })
            return;
        }
        res.write(200, {
            'contentType': 'text/html;charset=utf8'
        })
        res.end(data)
    })
    

});
app.listen(3000);
```

## 14. 异步编程

```js
const fs = require("fs");
// node 内置模块 promisify, 可以返回包裹一个方法的 promise 对象
const promisify = require("util").promisify;
const readFile = promisify(fs.readFile);

async function run () {
    let r1 = await readFile("./1.js","ttf8")
    let r2 = await readFile("./2.js","ttf8")
    let r3 = await readFile("./3.js","ttf8")
    return {
        r1,
        r2,
        r3
    }
}

let result = run()
```









# express

官方给出的概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架；

呜呜呜, node 原生写 web 服务器真的是开发很慢  ~ ~ ~

**通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的；**

**Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法；**

router 是从 express 框架抽离出来的

可以使用它来做: 

- Web 网站服务器：专门对外提供 Web 网页资源的服务器。
- API 接口服务器：专门对外提供 API 接口的服务器。

## 1. 安装和导入

```bash
npm install express
```

```js
// 导入
const express = require("epress");
// 创建 web 服务器
const app = express(); 

// 设置监听端口号
app.listen(3000) 
```

> 对于端口的补充: 
>
> 1. 在网络技术中，端口（Port）大致有两种意思：一是物理意义上的端口，比如，ADSL Modem、集线器、交换机、路由器用于连接其他网络设备的接口，如RJ-45端口、SC端口等等。
> 2. 二是逻辑意义上的端口，一般是指 TCP/IP 协议中的端口，端口号的范围从0到65535，比如用于浏览网页服务的80端口，用于FTP服务的21端口等等。
>
> 
>
> - 21端口：21端口主要用于FTP（File Transfer Protocol，文件传输协议）服务。
> - 23端口：23端口主要用于Telnet（远程登录）服务，是Internet上普遍采用的登录和仿真程序。
> - 25端口：25端口为SMTP（Simple Mail Transfer Protocol，简单邮件传输协议）服务器所开放，主要用于发送邮件，如今绝大多数邮件服务器都使用该协议。
> - 53端口：53端口为DNS（Domain Name Server，域名服务器）服务器所开放，主要用于域名解析，DNS服务在NT系统中使用的最为广泛。
>   67、68端口：67、68端口分别是为Bootp服务的Bootstrap Protocol Server（引导程序协议服务端）和Bootstrap Protocol Client（引导程序协议客户端）开放的端口。
> - 69端口：TFTP是Cisco公司开发的一个简单文件传输协议，类似于FTP。
> - 79端口：79端口是为Finger服务开放的，主要用于查询远程主机在线用户、操作系统类型以及是否缓冲区溢出等用户的详细信息。
> - **80端口：80端口是为HTTP（HyperText Transport Protocol，超文本传输协议）开放的，这是上网冲浪使用最多的协议，主要用于在WWW（World Wide Web，万维网）服务上传输信息的协议。**
> - 99端口：99端口是用于一个名为“Metagram Relay”（亚对策延时）的服务，该服务比较少见，一般是用不到的。
> - 109、110端口：109端口是为POP2（Post Office Protocol Version 2，邮局协议2）服务开放的，110端口是为POP3（邮件协议3）服务开放的，POP2、POP3都是主要用于接收邮件的。
> - 111端口：111端口是SUN公司的RPC（Remote Procedure Call，远程过程调用）服务所开放的端口，主要用于分布式系统中不同计算机的内部进程通信，RPC在多种网络服务中都是很重要的组件。
> - 113端口：113端口主要用于Windows的“Authentication Service”（验证服务）。
> - 119端口：119端口是为“Network News Transfer Protocol”（网络新闻组传输协议，简称NNTP）开放的。
> - 135端口：135端口主要用于使用RPC（Remote Procedure Call，远程过程调用）协议并提供DCOM（分布式组件对象模型）服务。
> - 137端口：137端口主要用于“NetBIOS Name Service”（NetBIOS名称服务）。
> - 139端口：139端口是为“NetBIOS Session Service”提供的，主要用于提供Windows文件和打印机共享以及Unix中的Samba服务。
> - 143端口：143端口主要是用于“Internet Message Access Protocol”v2（Internet消息访问协议，简称IMAP）。
> - 161端口：161端口是用于“Simple Network Management Protocol”（简单网络管理协议，简称SNMP）。
> - **443端口：443端口即网页浏览端口，主要是用于HTTPS服务，是提供加密和通过安全端口传输的另一种HTTP。**
> - 554端口：554端口默认情况下用于“Real Time Streaming Protocol”（实时流协议，简称RTSP）。
> - 1024端口：1024端口一般不固定分配给某个服务，在英文中的解释是“Reserved”（保留）。
> - 1080端口：1080端口是Socks代理服务使用的端口，大家平时上网使用的WWW服务使用的是HTTP协议的代理服务。
> - 1755端口：1755端口默认情况下用于“Microsoft Media Server”（微软媒体服务器，简称MMS）。
> - **4000端口：4000端口是用于大家经常使用的QQ聊天工具的，再细说就是为QQ客户端开放的端口，QQ服务端使用的端口是8000。**
> - **8080端口：8080端口同80端口，是被用于WWW代理服务的，可以实现网页。**

## 2. 监听

通过 `app.get()` 方法，可以监听客户端的 `GET` 请求，具体的语法格式如下：

```js
app.get(" 路径 ",function(require, response) {
    // 处理函数
})
```

在 get 方法中 通过 `req.query` 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

```js
app.get('/', (require, response) => {
    // 通过 req.query 可以获取到客户端发送过来的 查询参数
    // 注意：默认情况下，require.query 是一个空对象
    console.log(require.query)
})

```

通过 `app.post()` 方法，可以监听客户端的 `POST` 请求，具体的语法格式如下：

需要使用第三方包: body-parser 解析传递的参数

```js
app.post(" 路径 ",function(require, response) {
	// 处理函数
})
```

## 3. 响应给客户端消息

通过 `res.send()` 方法，可以把处理好的内容，发送给客户端, 不再使用 end() 的方式

**send 会自动检测响应类型, 自动设置到响应头当中, 设置相应内容编码以及类型**

```js
const express = require('express');
const app = express();
app.get("/", (req, res) => {
  // 会自动设置编码格式为 Content-Type: text/html;charset=utf-8;
  res.send("<h1>Hello World!</h1>");
});
app.get("/list", (req, res) => {
  // 可以直接响应 json 对象
  res.send({
    name: "John",
    age: 30
  });
});
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});
```

```js
// 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (require, response) => {
    // 调用 express 提供的 res.send() 方法，向客户端响应一个 JSON 对象
    res.send({ name: 'ximingx', age: 20, gender: '男' })
})
app.post('/user', (require, response) => {
    // 调用 express 提供的 res.send() 方法，向客户端响应一个 文本字符串
    res.send('请求成功')
})
```

## 4. 开放资源

express.static()

**推荐, 使用绝对路径**

express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器；

例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```js
app.use(express.static("public"));
```

`Express` 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，**存放静态文件的目录名不会出现在 URL 中。**

如果要托管多个静态资源目录，请多次调用 `express.static()` 函数：

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

```js
app.use("public", express.static("public"));
```

## 5. 路由

在 `Express` 中，路由指的是客户端的请求与服务器处理函数之间的映射关系；

**Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数**

**每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。**

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204160849891.png)

在 `Express` 中使用路由最简单的方式，就是把路由挂载到 app 上

```js
const express = require('express')
// 创建 Web 服务器, 命名为 app
const app = express()

// 挂载路由
app.get('/', (req, res) => {
  res.send('Get Request.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})

app.listen(3000)
```

> 模块化路由
>
> 为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。
> 将路由抽离为单独模块的步骤如下：

- 创建路由模块对应的 .js 文件；
- 调用 express.Router() 函数创建路由对象；
- 向路由对象上挂载具体的路由；
- 使用 module.exports 向外共享路由对象；
- 使用 app.use() 函数注册路由模块；

```js
// 1. 导入 express
const express = require('express')
const { userLogin } = require('../db/user')
// 2. 创建路由对象
const router = express.Router()
// 3. 挂载路由

router.post('/api/user/login', (req, res) => {
  const { username, password } = req.query;
  userLogin(username, password).then(data => {
    if (data.length === 0) {
      res.status(500).end({
        message: 'Login Error',
        data: data
      })
    } else {
      res.status(200).send({
        message: 'Login Success',
        data: data
      })
    }
  }).catch(err => {
    res.send({
      message: 'Login Error',
    })
  })
});

// 4. 向外导出路由对象
module.exports = router
```

使用

```js
// 1. 导入路由模块
const router = require('./03.router')
// 2. 使用 app.use() 注册路由模块
app.use(router)
```

>  为路由模块添加前缀
>
> 类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单

```js
// 1. 导入路由模块
const router = require('./03.router')
// 2. 使用 app.use() 注册路由模块
app.use("/spi", router)
```

### 二级路由

```js
const express = require('express');
const app = express();
const home = express.Router();
// 一级路由
app.use("/home", home);
// 二级路由, 需要请求 http://localhost:3000/home/index
home.get("/index", (req, res) => {
    res.send("Hello World!");
});
```

### 构建模块化

为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。
将路由抽离为单独模块的步骤如下：

- 创建路由模块对应的 .js 文件；
- 调用 express.Router() 函数创建路由对象；
- 向路由对象上挂载具体的路由；
- 使用 module.exports 向外共享路由对象；
- 使用 app.use() 函数注册路由模块；

```js
// admin.js
const express = require('express');
const admin = express.Router();
admin.get('/', (req, res) => {
    res.send('admin');
});
admin.get('/index', (req, res) => {
  res.send('admin index');
});
module.exports = admin;



// home.js
const express = require('express');
const home = express.Router();
home.get('/index', (req, res) => {
    res.send('home index');
});
module.exports = home;



// app.js
const express = require('express');
const app = express();
const home = require('./home');
const admin = require('./admin');
app.use('/home', home);
app.use('/admin', admin);
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});
```

### 请求参数

```js
// 请求: localhost:3000/find/123/ximingx
app.get('/find/:id/:name', (req, res) => {
     // 获取参数对象 req.params
    res.send(req.params);
});
```

### 全局数据

```js
req.app.locals
```

### 重定向

express 框架提供的

```js
res.redirect('/admin')
```

 



## 6. 中间件

> 中间件（Middleware ），特指业务流程的中间处理环节业。

当一个请求到达 `Express` 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理；

**相当于中间件就是一堆方法, 可以接收请求, 对请求做出响应, 也可以将请求传递得下一个中间件**

app.get() 实际上也是一个中间件，但是他没事使用 next() ，而是将它作为最后的处理函数

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204070910605.png)

`Express` 的中间件，本质上就是一个 **`function` 处理函数**，`Express` 中间件的格式如下：

```js
app.use(fn())

function fn() {
  return function (req, res, next) {
    console.log('request received');
    next();
  }
}
```

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204070911536.png)

- 中间件函数的形参列表中，**必须包含 next 参数**。而路由处理函数中只包含 req 和 res；
- `next 函数`是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由；
- 默认情况下, 请求从上到下依次匹配中间件, 一旦匹配成功, 终止匹配, 但是可以调用 next() 方法将控制权交给下一个中间件

中间件的定义

```js
// 常量 mw 所指向的，就是一个中间件函数
const mw = function (req, res, next) {
    console.log('这是中间件函数')
    // 注意: 在当前中间件的业务处理完毕后，必须调用 next( )函数, 表示把流转关系，转交给下一个中间件或路由
    next()
}
```

### app.use()

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做**全局生效的中间件**。

通过调用 `app.use(中间件函数)`，即可定义一个全局生效的中间件，示例代码如下：

```JS
const mw = function (req, res, next) {
    console.log('这是最简单的中间件函数')
    // 表示把流转关系，转交给下一个中间件或路由
    next()
}
// 全局生效的中间件
app.use(mw)
```

**简化形式**

```js
app.use((req, res, next) => {
    console.log('这是最简单的中间件函数')
    next()
})
```

**多个中间件之间，共享同一份 `req` 和 `res`。**基于这样的特性，我们可以在上游的中间件中，统一为 `req` 或 `res` 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

```js
const express = require('express')
const app = express()

// 这是定义全局中间件的简化形式
app.use((req, res, next) => {
    // 获取到请求到达服务器的时间
    const time = Date.now()
    // 为 req 对象，挂载自定义属性，从而把时间共享给后面的所有路由
    req.startTime = time
    next()
})

app.get('/', (req, res) => {
    res.send('Home page.' + req.startTime)
})
app.get('/user', (req, res) => {
    res.send('User page.' + req.startTime)
})

app.listen(80, () => {
    console.log('http://127.0.0.1')
})
```

可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用，示例代码如下：

```js
const express = require('express')
const app = express()

// 定义第一个全局中间件
app.use((req, res, next) => {
    console.log('调用了第1个全局中间件')
    next()
})
// 定义第二个全局中间件
app.use((req, res, next) => {
    console.log('调用了第2个全局中间件')
    next()
})

// 定义一个路由
app.get('/user', (req, res) => {
    res.send('User page.')
})

app.listen(80, () => {
    console.log('http://127.0.0.1')
})
```

不使用 `app.use()` 定义的中间件，叫做局部生效的中间件，示例代码如下：

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 定义中间件函数
const mw1 = (req, res, next) => {
    console.log('调用了局部生效的中间件')
    next()
}

// 2. 创建路由
app.get('/', mw1, (req, res) => {
    res.send('Home page.')
})
app.get('/user', (req, res) => {
    res.send('User page.')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
    console.log('Express server running at http://127.0.0.1')
})
```

可以在路由中，通过如下 [] 方式，使用多个局部中间件：

```js
app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home page.')
})
```

> 了解中间件的5个使用注意事项

- 一定要在路由之前注册中间件；
- 客户端发送过来的请求，可以连续调用多个中间件进行处理；
- 执行完中间件的业务代码之后，不要忘记调用 next() 函数；
- 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码；
- 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象；

`Express` 官方把常见的中间件用法，分成了 5 大类，分别是：

1. 应用级别的中间件
2. 路由级别的中间件
3. 错误级别的中间件
4. Express 内置的中间件
5. 第三方的中间件

**应用级别的中间件**

通过 `app.use()` 或 `app.get()` 或 `app.post()` ，**绑定到 app 实例上的中间件，叫做应用级别的中间件**，代码示例如下：

```js
// 应用级别的中间件(全局中间件)
app.use((req, res, next) => {
    next()
})

// 应用级别的中间件(局部中间件)
app.get('/', mw1, (req, res) => {
    res.send('Home page.')
})
```

**路由级别的中间件**

**绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。**它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上，代码示例如下：

```js
const app = express();
const router = express.Router()

router.use(function(require, response, next) {
    // 处理函数
    next()
})
```

### **错误级别的中间件**

错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

**next() 只接收一个参数, 且只能为字符串**

格式：错误级别中间件的 `function` 处理函数中，**必须有 4 个形参**，形参顺序从前到后，分别是 (**err**, req, res, next)。

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 定义路由
app.get('/', (req, res) => {
    // 1.1 人为的制造错误
    throw new Error('服务器内部发生了错误！')
    res.send('Home page.')
})

// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => {
    res.status(500).send('Error：' + err.message)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
    console.log('Express server running at http://127.0.0.1')
})
```

**错误级别的中间件，必须注册在所有路由之后；**

**但是他只能处理同步代码**

```js
// try catch 会捕获代码执行错误, 但不不能捕获回调函数异步任务的错误
app.get('/', async (req, res, next) => {
  try {
    await User.find({name: "张三"})
  } catch (error) {
    next(error)
  }
})


app.get('/admin', (req, res,next) => {
  fs.readFile("./yarn.lock", "utf8",(err, data) => {
    if (err) {
       // 处理异步代码的方式
       next(err);
    } else {
      res.send(data);
    }
  })
});
app.use((req, res, next) => {
  res.status(400).send('页面不存在');
})
```

### 案例

网站维护, 登录, 请求路径不存在

```js
const express = require('express');
const app = express();
app.use((req, res, next) => {
  res.send('维护中...');
})
app.use("/admin",((req, res, next) => {
  let isLogin = true;
  if (isLogin) {
    next();
  } else {
    res.send("You are not login");
  }
}));
app.get('/admin', (req, res) => {
  res.send('Hello root!');
});
app.use((req, res, next) => {
  res.status(400).send('页面不存在');
})
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});
```

## 7. 接口

首先要创建基本的服务器

```js
// 导入 express
const express = require('express')
// 创建 express 的服务器实例
const app = express()

 // write your code here...

// 调用 app.listen 方法，指定端口号并启动Web服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

创建 API 路由模块

```js
// 1. 导入路由模块
const router = require('./03.router')
// 2. 使用 app.use() 注册路由模块
app.use(router)
```

## 8. 操作 mysql 数据库


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

## 9. express解决跨域

解决接口跨域问题的方案主要有两种：

1. `CORS`（主流的解决方案，**推荐使用**）

> `CORS` （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。
>
> 浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。
>
> - CORS 主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口；
> - CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）；

```js
// import router from './routes/index.js';
const app = express();

// 设置允许跨域访问该服务
app.all('*', function (req, res, next) {
  // origin 参数的值指定了允许访问该资源的外域 URL。
  // 如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *，表示允许来自任何域的请求
  res.header("Access-Control-Allow-Origin", "origin");
  // CORS 仅支持客户端向服务器发送如下的 9 个请求头：Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）
  //  如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！
  res.header('Access-Control-Allow-Methods', 'PUT, GET, POST, DELETE, OPTIONS');
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  res.header('Access-Control-Allow-Headers', 'mytoken');
  next();
});
```

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

2. `JSONP`（有缺陷的解决方案：只支持 GET 请求）

> 浏览器端通过 `<script>` 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 `JSONP`。

- JSONP 不属于真正的 Ajax 请求，因为它没有使用 `XMLHttpRequest` 这个对象。
- JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。

实现 JSONP 接口的步骤

1. 获取客户端发送过来的回调函数的名字；
2. 得到要通过 JSONP 形式发送给客户端的数据；
3. 根据前两步得到的数据，拼接出一个函数调用的字符串；
4. 把上一步拼接得到的字符串，响应给客户端的 `<script>` 标签进行解析执行；

```js
app.get("/api/jsonp", require, response) {
    data = {
        name: "ximingx",
        age: 20
    }
    res.sned(`${requ.query.callback (${JSON.strify(data)})}`);
}

// ------------------------------

$("#btn").on("click", function() {
    $.ajax({
        method: "GET",
        url: "http://localhost:3000/api/jsonp",
        dataType: "jsonp",
        success(res) {
            console.log(res);
        }
    })
})
```



3. 使用 cors 中间件解决跨域问题

> cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤分为如下 3 步：

- 运行 npm install cors 安装中间件；
- 使用 const cors = require('cors') 导入中间件；
- 在路由之前调用 app.use(cors()) 配置中间件；

## 10. express-generator

您可以使用 `npx` 命令（在 Node.js 8.2.0 中可用）运行应用程序生成器。

```bash
npx express-generator
```

![image-20220407225823471](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204072258530.png)

生成的项目目录

```bash
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

7 directories, 9 files
```



![image-20220407225734975](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204072257042.png)

然后安装依赖项：

```bash
$ cd myapp
$ npm install
```

```bash
# 启动服务
$ node ./bin/www
```

![image-20220407230029657](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204072300762.png)

## 11. express-art-template

> **模板文件中的请求路径是相对于当前浏览器请求路径的基础上的相对路径**
>
> **要使用绝对路径 /**

```bash
> yarn add art-template express-art-template
```

```js
const express = require('express');
const app = express();
// 设置默认的模板要求
app.engine('html', require('express-art-template'));
// 设置模板的存放路径
app.set('views', __dirname + '/views');
// 设置模板的默认后缀
app.set('view engine', 'html');
app.get("/",(req, res) => {
    // res.render('页面的名字',  {数据});
    res.render('index', {
        title: 'Hello World',
        list: [
            {name: 'tom', age: 18},
            {name: 'jerry', age: 20},
            {name: 'jack', age: 22}
        ]
    });
})
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});
```

```js
const express = require('express');
const app = express();
app.engine('html', require('express-art-template'));
app.set('views', __dirname + '/views');
app.set('view engine', 'html');
// 为 app.locals 添加 index 属性, 为所有的页面提供
app.locals.index = {
  title: 'Hello World',
  list: [
    {name: 'tom', age: 18},
    {name: 'jerry', age: 20},
    {name: 'jack', age: 22}
  ]
}
app.get("/",(req, res) => {
    res.render('index');
})
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});


// index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>{{ index.title }}</h1>
    <ul>
        {{ each index.list }}
            <li>{{ $value.name }}</li>
            <li>{{ $value.age }}</li>
        {{ /each }}
    </ul>
</body>
</html>
```

![image-20220414100732152](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204141007241.png)

# 案例

## 1. 内网穿透

[博客原地址，里面有具体的展示过程， 很详细](https://blog.csdn.net/ximing020714/article/details/122077265?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522164933400216782248544817%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=164933400216782248544817&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-122077265.142^v7^control,157^v4^control&utm_term=node+ximingx&spm=1018.2226.3001.4187)

### 首先强调几个遇到的问题

1. 直接打开 `vue` 打包后的 `dist` 文件夹里的 `index.html` 是无法正常访问的,因为资源的路径会发生问题
2. 跨域问题
3. 使用 `node` 开放资源目录
4. `natapp` 连接隧道失败
5. 以下步骤要配置`node`环境

### 过程

首先将 `vue` 项目打包, 生成dist文件夹

直接把 `dist` 文件夹放到 node 服务器与 app.js 同级目录

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

注册完毕后 看那个免费隧道, 真的不错

在配置隧道的时候, 需要注意的是, 我node服务器使用的端口号是 3000
这里也需要填写 3000

and, 写到这里的时候, 我突然想起来还要安装下载 natapp, 但是很简单, 不要慌

然后直接安装就可以了

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

然后搜索你下面红框中的 http地址, 即可成功实现
<font color="red">当然在最后一步连接隧道时, 可能会遇到问题, 报错的评论区扣,或者私信截图</font>

### 连接隧道报错解决方法


[更换阿里公共DNS](https://natapp.cn/article/alidns)
[连不上网络错误调试排查详解](https://natapp.cn/article/networkerrors)

## 2. 网易云接口

[博客原地址](https://blog.csdn.net/ximing020714/article/details/121366965?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522164933409016780366535612%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=164933409016780366535612&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-121366965.142^v7^control,157^v4^control&utm_term=ximingx+%E7%BD%91%E6%98%93%E4%BA%91&spm=1018.2226.3001.4187)

**目的功能:**
1. axios 请求获取歌曲的 url 以及 封面照片
2. 切换歌曲
3. 显示当前歌曲的时间,剩余时间
4. 进度条颜色改变
5. 刷新重置进度
6. 歌单的展示

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

借此我们可以请求歌单和歌曲的 url 地址 ,  歌曲照片地址等等,详细功能可以自己查看

以上全部借助别人的 api 接口

**这里重点强调一下 获取歌曲 url 的 api**

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

## 3. 简单的登录

```js
const express = require('express');
const app = express();
const BodyParser = require('body-parser');
app.use(BodyParser.json());
app.use(BodyParser.urlencoded({ extended: false }));
const User = require('./db/user');
app.post("/login", async (req, res) => {
    const { username, password } = req.body;
    if (username.trim().length == 0 || password.trim().length == 0) {
        return res.status(400).send("Invalid username or password");
    }
    else {
        let user = await User.findOne({ username });
        if (user) {
            if (user.password == password) {
                return res.status(200).send("Login success");
            }
            else {
                return res.status(400).send("Invalid username or password");
            }
        }
        else {
            return res.status(400).send("Invalid username or password");
        }
    }
});
```

4. 数据fye

```js

```



# npm -g

## nodemon

```bash
npm install nodemon -g
```

```bash
nodemon app.js
```

## nrm

```bash
> npm install nrm -g
```

```bash
// 查看下载地址列表
nrm ls

  npm ---------- https://registry.npmjs.org/
  yarn --------- https://registry.yarnpkg.com/
  tencent ------ https://mirrors.cloud.tencent.com/npm/
  cnpm --------- https://r.cnpmjs.org/
  taobao ------- https://registry.npmmirror.com/
  npmMirror ---- https://skimdb.npmjs.com/registry/
```

```bash
// 切换默认下载地址
> nrm use taobao

   Registry has been set to: https://registry.npmmirror.com/
```

## Gulp

基于node平台开发的前端构建工具
将机械化操作编写成任务, 想要执行机械化操作时执行一个命令行命令任务就能自动执行了, 用机器代替手工，提高开发效率。

- 项目上线，HTML、CSS、JS文件压缩合并
- 语法转换（es6、less ...）
- 公共文件抽离
- 修改文件浏览器自动刷新

```bash
npm install gulp
npm install gulp-cli -g
```

1. 使用npm install gulp下载gulp库文件
2. 在项目根目录下建立gulpfile.js文件
3. 重构项目的文件夹结构 src目录放置源代码文件 dist目录放置构建后文件
4. 在gulpfile.js文件中编写任务.
5. 在命令行工具中执行gulp任务

```js
// gulp 提供的方法
gulp.src()：获取任务要处理的文件
gulp.dest()：输出文件
gulp.task()：建立gulp任务
gulp.watch()：监控文件的变化
```

```js
// gulpfile.js

const gulp = require('gulp');

// 使用gulp.task()方法建立任务
// 参数: 任务名称,回调函数
gulp.task('first', () => {
    // 获取要处理的文件
    gulp.src('./src/css/base.css') 
    
    
    // 操作 ~ ~ ~ 
    
    
    // 将处理后的文件输出到dist/css目录
    .pipe(gulp.dest('./dist/css'));
});
```

```bash
> cd ~ ~ ~ 当前项目目录
# 执行 first 任务
> gulp first
```

### gulp 插件

- gulp-htmlmin ：html文件压缩
- gulp-csso ：压缩css
- gulp-babel ：JavaScript语法转化
- gulp-less: less语法转化
- gulp-uglify ：压缩混淆JavaScript
- gulp-file-include 公共文件包含
- browsersync 浏览器实时同步

使用需要先安装模块

```bash
npm install gulp-htmlmin 
```

```js
// gulpfile.js
const gulp = require('gulp');
const htmlmin = require('gulp-htmlmin');
gulp.task('html', () => {
    gulp.src('./src/*.html') 
    .pipe(htmlmin({ collapseWhitespace: true }))
    .pipe(gulp.dest('dist'));
});

// bash
> gulp html
```

其他同理, 看 npm



# 项目配置

## node_modules

- **文件夹以及文件过多过碎，当我们将项目整体拷贝给别人的时候，传输速度会很慢很慢. (所以一般不传输这个文件)**
- 复杂的模块依赖关系需要被记录，确保模块的版本和当前保持一致，否则会导致当前项目运行报错

> 所以, 在别人拿到项目后首先要
>
> ```bash
> > npm install
> # 看情况
> # 生产环境
> > npm install --production 
> ```

## package.json文件

项目描述文件，记录了当前项目信息，例如项目名称、版本、作者、github地址、当前项目依赖了哪些第三方模块等。

```bash 
// 初始化 package.josn
> npm init -y 
```

script 是调用的简写 

```bash
> npm run （script中的简写）
```

## 项目依赖

在现在下载的较高版本的 node 安装项目依赖的时候，已经不需要我们使用 --save 来保存依赖了

在项目的开发阶段和线上运营阶段，都需要依赖的第三方包，称为项目依赖
**使用npm install 包名命令下载的文件会默认被添加到 package.json 文件的 dependencies 字段中**

```js
{
    "dependencies": {
        "jquery": "^3.3.1“
    }
} 
```

## 开发依赖

在项目的开发阶段需要依赖，线上运营阶段不需要依赖的第三方包，称为开发依赖

**使用npm install 包名 --save-dev命令将包添加到package.json文件的devDependencies字段中**

## package-lock.json

锁定包的版本，确保再次下载时不会因为包版本不同而产生问题

加快下载速度，因为该文件中已经记录了项目所依赖第三方包的树状结构和包的下载地址，重新安装时只需下载即可，不需要做额外的工作

# 模板引擎

## art-template

```bash
npm install art-template
```

- 在命令行工具中使用 npm install art-template 命令进行下载
- 使用const template = require('art-template')引入模板引擎
- 告诉模板引擎要拼接的数据和模板在哪 const html = template(‘模板路径’, 数据);
- 使用模板语法告诉模板引擎，模板与数据应该如何进行拼接 

```js
// 导入模板引擎模块
 const template = require('art-template');
 // 将特定模板与特定数据进行拼接
 const html = template('./views/index.art',{
    data: {
        name: '张三',
        age: 20
    }
 });


// /index.art
 <div>
    <span>{{data.name}}</span>
    <span>{{data.age}}</span>
 </div>
```

art-template同时支持两种模板语法：标准语法和原始语法。

标准语法可以让模板更容易读写，原始语法具有强大的逻辑处理能力。

- 标准语法： {{ 数据 }}
- 原始语法：<%=数据  %>

### 解析标签

```js
 <!-- 标准语法 -->
 <h2>{{@ value }}</h2>
 <!-- 原始语法 -->
 <h2><%- value %></h2>
```

### 条件判断

```js
 <!-- 标准语法 --> 
 {{if 条件}} ... {{/if}}
 {{if v1}} ... {{else if v2}} ... {{/if}}
 <!-- 原始语法 -->
 <% if (value) { %> ... <% } %>
 <% if (v1) { %> ... <% } else if (v2) { %> ... <% } %>
```

### 循环

```js
<!-- 标准语法 -->
 {{each target}}
     {{$index}} {{$value}}
 {{/each}}
  <!-- 原始语法 -->
 <% for(var i = 0; i < target.length; i++){ %>
     <%= i %> <%= target[i] %>
 <% } %>
```

### 子模版

使用子模板可以将网站公共区块(头部、底部)抽离到单独的文件中。

```js
<!-- 标准语法 -->
 {{include './header.art'}}
  <!-- 原始语法 -->
 <% include('./header.art') %>
```

### 模板继承

![image-20220413092928612](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204130929698.png)

```html
 <!doctype html>
 <html>
     <head>
         <meta charset="utf-8">
         <title>HTML骨架模板</title>
         {{block 'head'}}{{/block}}
     </head>
     <body>
         {{block 'content'}}{{/block}}
     </body>
 </html>


<!-- 填充 -->
{{extend './layout.art'}}
 {{block 'head'}} <link rel="stylesheet" href="custom.css"> {{/block}}
 {{block 'content'}} <p>This is just an awesome page.</p> {{/block}}
```

### 模板配置

- 向模板中导入变量 template.defaults.imports.变量名 = 变量值;
- 设置模板根目录 template.defaults.root = 模板目录
- 设置模板默认后缀 template.defaults.extname = '.art'





# 加密 身份验证

## jwt

```js
/*
 * Start at 2022.
 * Author: ximingx.
 * Github: https://github.com/ximingx
 * Csdn: https://ximingx.blog.csdn.net/
 */

// 导入 express 模块
// 创建 express 的服务器实例
const express = require('express')
const app = express()
const port = process.env.PORT || 2022;
// 跨域设置
const cors = require('cors')
app.use(cors())
// req.body 解析
app.use(express.json());
app.use(express.urlencoded({extended: false}));
// 1. 安装并导入 JWT 相关的两个包, express-jwt版本推荐6.1.1, 最近他更新了, 可能会出现一些意外的问题
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')
// 2. 定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'ximingx' + Math.floor(Math.random() * 10);
// 5. JWT字符串解析
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 `req.user` 属性上
app.use(expressJWT({secret: secretKey, algorithms: ['HS256']}).unless({path: ['/login', '/register']}))
// 登录的路由, 在这里登录成功后, 返回 token 字符串
app.post('/login', (req, res) => {
    if (!(req.body.username == 'admin' && req.body.password == "root")) {
        return res.json({
            code: 1,
            msg: '用户名或密码错误'
        })
    }
    // 3. 用户登陆成功后, 需要生成token
    // 参数1：用户的信息对象
    // 参数2：加密的秘钥
    // 参数3：配置对象，可以配置当前 token 的有效期
    const tokenStr = jwt.sign({
        username: req.body.username
    }, secretKey, {expiresIn: '1h'})
    // 返回登陆成功后返回数据
    res.json({
        status: 200,
        message: '登录成功！',
        // 4. 并通过 token 属性发送给客户端
        token: tokenStr,
    })
})

// 这里需要这样请求, 否则 token 会无效报错
// axios({
//     method: 'post',
//     url: 'http://localhost:2022/adimin',
//     headers: {
//         'Authorization': 'Bearer ' + token
//     }
// })
// 这是一个有权限的 API 接口
app.get('/admin', function (req, res) {
    // 6. 使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
    console.log(req.user)
    // {
    //     "status": 200,
    //     "message": "获取用户信息成功！",
    //     "data": {
    //         "username": "admin",
    //         "iat": 1651242605, // 创建时间
    //         "exp": 1651246205 // token 有效期
    //     }
    // }
    res.send({
        status: 200,
        message: '获取用户信息成功！',
        data: req.user, // 要发送给客户端的用户信息
    })
})
// 7：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
    // 这次错误是由 token 解析失败导致的
    if (err.name === 'UnauthorizedError') {
        return res.send({
            status: 401,
            message: '无效的token',
        })
    }
    res.send({
        status: 500,
        message: '未知的错误',
    })
})
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});

```

## bcrypt

**使用 hash 算法实现, 只能加密, 不能解密**

在数据库中使用明文很不安全， 为了防止被不法分子 （对， 说不定就是某一天学成归来的你）

```js
> python2.x
> yarn add node-gyp -g
> yarn add windows-build-tools --global --production
# 依赖的三个环境
> yarn add bcrypt
```

```js
const bcrypt = require('bcrypt');

async function encrypt(message) {
    // 生成随机字符串 参数: 复杂度的难度(默认: 10)
    // 返回生成的随机字符串
    const salt = await bcrypt.genSalt(10);
    // salt: $2b$10$eNXayg7qjbZccgDIB1AKlu

    // 对密码进行加密
    // 对密码进行加密 参数: 密码, 加密的难度
    // 对密码进行加密
    // 参数1: 要进行加密的明文密码
    // 参数2: 加密的随机字符串
    // 返回的是加密后的密码
    const result = await bcrypt.hash(message, salt);
    console.log(`salt: ${salt}`);
    console.log(`result: ${result}`);
    // salt: $2b$10$IwMRYn2.sQ3thmksLnekWe
    // result: $2b$10$IwMRYn2.sQ3thmksLnekWeJDxm6yn32xi/INBSW/plvorEfNAujti
    return result;
}

async function verify(message, hash) {
    // 密码的验证
    return !!(await bcrypt.compareSync(message, hash));
}

module.exports = {
    encrypt,
    verify
};
```

## cookie session

cookie：浏览器在电脑硬盘中开辟的一块空间，主要供服务器端存储数据。

- cookie中的数据是以域名的形式进行区分的。
- cookie中的数据是有过期时间的，超过时间数据会被浏览器自动删除。
- **cookie中的数据会随着请求被自动发送到服务器端。**\
- 4KB限制



![image-20220416101248018](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204161012101.png)

session：实际上就是一个对象，存储在服务器端的内存中，**在session对象中也可以存储多条数据，每一条数据都有一个sessionid做为唯一标识。**

当浏览器访问服务器并发送第一次请求时，服务器端会创建一个session对象，生成一个类似于key,value的键值对，然后将key(cookie)返回到浏览器(客户)端，浏览器下次再访问时，携带key(cookie)，找到对应的session(value)。 客户的信息都保存在session中

Session的用途：

- **session运行在服务器端，当客户端第一次访问服务器时，可以将客户的登录信息保存。**
- **当客户访问其他页面时，可以判断客户的登录状态，做出提示，相当于登录拦截。**
- **session可以和Redis或者数据库等结合做持久化操作，当服务器挂掉时也不会导致某些客户信息（购物车）**
  **丢失。**

![image-20220416102220168](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204161022250.png)

## express-session

在express项目中，只需要安装express-session中间件，即可在项目中使用 Session：

```bash
> npm install express-session
> yarn add express-session
```

```js
// 设置官方文档提供的中间件
var session=require('express-session')
app.use(session({
  secret: 'sercet key',//签名，与 cookie 设置的签名字符串一致
  resave: false,// 一个请求在另一个请求结束时对 session 进行修改覆盖并保存，默认值为true。建议设为false
  saveUninitialized: true,//无论是否使用 session ,默认只要对页面发起请求，都会给客户端一个cookie  
  name: 'connect.sid', // // 在浏览器中生成 cookie 的名称 key ，默认是connect.sid
  cookie:{
   maxAge:1000*60 // session 的有效时长
  }
}))
// 这段代码放在路由前面
```

`secret`:一个`String`类型的字符串，作为服务器端生成`session`的签名。
`name`:返回客户端的key的名称，默认为`connect.sid`,也可以自己设置。
`resave`:(是否允许)当客户端并行发送多个请求时，其中一个请求在另一个请求结束时对`session`进行修改覆盖并保存。
默认为`true`。但是(后续版本)有可能默认失效，所以最好手动添加。
`saveUninitialized`:初始化session时是否保存到存储。默认为`true`， 但是(后续版本)有可能默认失效，所以最好手动添加。
`cookie`:设置返回到前端key的属性，默认值为`{ path: ‘/', httpOnly: true, secure: false, maxAge: null }` 。

- `express-session`的一些方法:
- `Session.destroy()` :删除`session`，当检测到客户端关闭时调用。
- `Session.reload()` :当`session`有修改时，刷新`session`。
- `Session.regenerate()` ：将已有`session`初始化。
- `Session.save()` ：保存`session`。

使用

```js
req.session.username
```

示例 demo1

```js
    var express = require("express");
    var app = express();
    var session = require("express-session");
    //配置中间件
    app.use(session({
        secret: 'keyboard cat',
        resave: false,
        saveUninitialized: true
        //cookie: { secure: true }   /*secure https这样的情况才可以访问cookie*/
    }))
    app.get("/",function(req,res){
        //获取sesssion
        if(req.session.userinfo){  /*获取*/
            res.send('你好'+req.session.userinfo+'欢迎回来');
        }else{
            res.send('未登录');
        }
    });

    app.get("/login",function(req,res){
        req.session.userinfo="zhangsan111"; /*设置session*/
        res.send('登录成功');
    });

    app.get("/news",function(req,res){
        //获取sesssion
        if(req.session.userinfo){  /*获取*/
            res.send('你好'+req.session.userinfo+'欢迎回来 news');
        }else{
            res.send('未登录 news');
        }
    });

    app.listen(3000);
```

示例demo 2

```js
//app.js中添加如下代码(已有的不用添加)
var express = require('express');
var cookieParser = require('cookie-parser');
var session = require('express-session');
 
app.use(cookieParser('sessiontest'));
app.use(session({
 secret: 'sessiontest',//与cookieParser中的一致
 resave: true,
 saveUninitialized:true
}));
```

```js
//修改router/index.js,第一次请求时我们保存一条用户信息。
router.get('/', function(req, res, next) {
 var user={
  name:"Chen-xy",
  age:"22",
  address:"bj"
 }
 req.session.user=user;
 res.render('index', {
  title: 'the test for nodejs session' ,
  name:'sessiontest'
 });
});
```

```js
//修改router/users.js，判断用户是否登陆。
router.get('/', function(req, res, next) {
 if(req.session.user){
  var user=req.session.user;
  var name=user.name;
  res.send('你好'+name+'，欢迎来到我的家园。');
 }else{
  res.send('你还没有登录，先登录下再试试！');
 }
});
```

## cookie-parser

express直接提供了api,只需要在需要使用的地方调用如下api即可

```js
// 一: 没有使用签名
var express = require('express');
var router = express.Router();
 
/* GET users listing. */
router.get('/', function(req, res, next) {
  res.send('respond with a resource');
  console.log(req.cookies)
  console.log(req.cookies.username)
});
router.get('/a', function(req, res, next) {
  
  res.cookie('username','张三',{maxAge:1000*10})
  res.cookie('password','123',{maxAge:1000*10})
 
  res.redirect('/users')
});
module.exports = router;


// 二: 使用签名
var express = require('express');
var router = express.Router();
 
/* GET users listing. */
router.get('/', function(req, res, next) {
  res.send('respond with a resource');
 
  console.log(req.signedCookies)
  console.log(req.signedCookies.username)
});
router.get('/a', function(req, res, next) {
 
  res.cookie('username','张三',{maxAge:1000*10,signed:true})
  res.cookie('password','123',{maxAge:1000*10,signed:true})
 
  res.redirect('/users')
});
module.exports = router;

// s
 res.clearCookie('age')
```

**express就会将其填入 Response Header 中的Set-Cookie，达到在浏览器中设置cookie的作用。**

- name: 类型为String
- value: 类型为String和Object，**如果是Object会在cookie.serialize()之前自动调用JSON.stringify对其进行处理**
- Option: 类型为对象，可使用的属性如下

```js
-   domain：cookie在什么域名下有效，类型为String,。默认为网站域名
-   expires: cookie过期时间，类型为Date。如果没有设置或者设置为0，那么该cookie只在这个这个session有效，即关闭浏览器后，这个cookie会被浏览器删除。
-   httpOnly: 只能被web server访问，类型Boolean。
-   maxAge: 实现expires的功能，设置cookie过期的时间，类型为String，指明从现在开始，多少毫秒以后，cookie到期。
-   path: cookie在什么路径下有效，默认为'/'，类型为String
-   secure：只能被HTTPS使用，类型Boolean，默认为false
-   signed:使用签名，类型Boolean，默认为false。`express会使用req.secret来完成签名，需要cookie-parser配合使用`
```

```js
res.cookie('name', 'koby', { domain: '.example.com', path: '/admin', secure: true });
//cookie的有效期为900000ms
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true });
//cookie的有效期为900000ms
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true });
 
//cookie的value为对象
res.cookie('cart', { items: [1,2,3] });
res.cookie('cart', { items: [1,2,3] }, { maxAge: 900000 });
 
res.cookie('name', 'tobi', { signed: true });
```

**cookie的删除**
express直接提供了api删除浏览器中的cookie,只需要在需要使用的地方调用如下api即可

```javascript
    function(req, res, next){
        res.clearCookie(name [, options]);
    }
```

npm 安装 `cookie-parser` 命令

```ruby
$ npm install cookie-parser --save
```

使用方式

```js
var express = require('express');
var cookieParser = require('cookie-parser');
 
var app = express();
//不使用签名
app.use(cookiePareser());
 
//若需要使用签名，需要指定一个secret,字符串,否者会报错
app.use(cookiePareser('Simon'));
```

#

### 登录拦截

```js
app.use('/admin', (req, res, next) => {
  if (req.url != '/login' && !req.session.user) {
    res.redirect('/admin/login');
  } else {
    next();
  }
})
```

## joi 格式验证

```js
const Joi = require('joi');

const schema = Joi.object({
    username: Joi.string() // 必须是字符串
        .alphanum()
        .min(3)  // 最小长度
        .max(30) // 最大长度
        .required(), // 必填
    	.valid('0', '1') // 只能选择 0 或者 1

    password: Joi.string()
        .pattern(new RegExp('^[a-zA-Z0-9]{3,30}$')), // 正则表达式

    repeat_password: Joi.ref('password'),

    // [] 里面的都是可选项
    access_token: [
        Joi.string(),
        Joi.number()
    ],

    birth_year: Joi.number()
        .integer()
        .min(1900)
        .max(2013),

    email: Joi.string()
        .email({ minDomainSegments: 2, tlds: { allow: ['com', 'net'] } }) // 邮箱验证
})
    .with('username', 'birth_year')
    .xor('password', 'access_token')
    .with('password', 'repeat_password');






// 方式一: 
schema.validate({ username: 'abc', birth_year: 1994 });
// -> { value: { username: 'abc', birth_year: 1994 } }

schema.validate({});
// -> { value: {}, error: '"username" is required' }


// 方式二:
try {
    const value = await schema.validateAsync({ username: 'abc', birth_year: 1994 });
}
catch (err) { 

}
```

# 解析请求

## body-parser

**在处理程序之前在中间件中解析传入的请求主体，在`req.bod`**

**``body-parser`是非常常用的一个`express`中间件，作用是对post请求的请求体进行解析。使用非常简单，以下两行代码已经覆盖了大部分的使用场景。y`属性下可用。**

`body-parser`实现的要点如下：

1. 处理不同类型的请求体：比如`text`、`json`、`urlencoded`等，对应的报文主体的格式不同。
2. 处理不同的编码：比如`utf8`、`gbk`等。
3. 处理不同的压缩类型：比如`gzip`、`deflare`等。
4. 其他边界、异常的处理。

```js
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```

安装

```bash
npm install body-parser
```

使用

```js
var bodyParser = require('body-parser')
```

```js
const express = require('express');
const app = express();
const bodyParser = require('body-parser');
app.use(bodyParser.json());
// false 使用 querystring 模块 处理请求参数
// true 使用 第三方模块 qs 处理请求参数
app.use(bodyParser.urlencoded({ extended: false }));
app.post('/add', (req, res) => {
    console.log(req.body);
    res.send(req.body);
});
app.listen(3000, () => {
  console.log('Server running on port http://localhost:3000')
});
```

## formidable

```bash
> yarn add formidable
```

作用：解析表单，支持get请求参数，post请求参数、文件上传,  文件上传

```js
// 引入formidable模块
 const formidable = require('formidable');
 // 创建表单解析对象
 const form = new formidable.IncomingForm();
 // 设置文件上传路径
 form.uploadDir = "";
 // 是否保留表单上传文件的扩展名
 form.keepExtensions = true;
 // 对表单进行解析
 form.parse(req, async (err, fields, files) => {
     // fields 存储普通请求参数
     // files 存储上传的文件信息
     // 保存的路径
     await Article.create({
         title: fields.title,
         author: fields.author,
         img: siles.cover.path.split('public')[1],
         conteng: fields.conteng,
     })
     res.redirect("/index")
 });
```

## file-reader

文件读取

在 js 中 文件上传的按钮添加事件

```bash
>  yarn add file-reader
```

异步方法

```js
var reader = new FileReader();
 reader.readAsDataURL('文件');
 reader.onload = function () {
     console.log(reader.result); 
 }
```

```js
let file = document.querySelector("#file")
let img = document.querySelector("#img")
file.onchange = function() {
    let reader = new FileReader();
    reader.readsDataURL(this.files[0]);
	   reader.onload = function () {
       	img.src = reader.result
    }
}
```







# 通用第三方模块

## dateformat

```js
import dateFormat, { masks } from "dateformat";
const now = new Date();

// Basic usage
dateFormat(now, "dddd, mmmm dS, yyyy, h:MM:ss TT");
// Saturday, June 9th, 2007, 5:46:21 PM

// You can use one of several named masks
dateFormat(now, "isoDateTime");
// 2007-06-09T17:46:21

// ...Or add your own
masks.hammerTime = 'HH:MM! "Can\'t touch this!"';
dateFormat(now, "hammerTime");
// 17:46! Can't touch this!

// You can also provide the date as a string
dateFormat("Jun 9 2007", "fullDate");
// Saturday, June 9, 2007

// Note that if you don't include the mask argument,
// dateFormat.masks.default is used
dateFormat(now);
// Sat Jun 09 2007 17:46:21

// And if you don't include the date argument,
// the current date and time is used
dateFormat();
// Sat Jun 09 2007 17:46:22

// You can also skip the date argument (as long as your mask doesn't
// contain any numbers), in which case the current date/time is used
dateFormat("longTime");
// 5:46:22 PM EST

// And finally, you can convert local time to UTC time. Simply pass in
// true as an additional argument (no argument skipping allowed in this case):
dateFormat(now, "longTime", true);
// 10:46:21 PM UTC

// ...Or add the prefix "UTC:" or "GMT:" to your mask.
dateFormat(now, "UTC:h:MM:ss TT Z");
// 10:46:21 PM UTC

// You can also get the ISO 8601 week of the year:
dateFormat(now, "W");
// 42

// and also get the ISO 8601 numeric representation of the day of the week:
dateFormat(now, "N");
// 6
```

## router

使用步骤：

- 获取路由对象
- 调用路由对象提供的方法创建路由
- 启用路由，使路由生效

```js
const getRouter = require('router')
const router = getRouter();
router.get('/add', (req, res) => {
    res.end('Hello World!')
}) 
server.on('request', (req, res) => {
    router(req, res)
})
```

## serve-static

功能：实现静态资源访问服务
步骤：

- 引入serve-static模块获取创建静态资源服务功能的方法
- 调用方法创建静态资源服务并指定静态资源服务目录
- 启用静态资源服务功能

```js
const serveStatic = require('serve-static')
const serve = serveStatic('public')
server.on('request', () => { 
    serve(req, res)
})
server.listen(3000)
```

```js
 // 引入formidable模块
 const formida ble = require('formidable');
 // 创建表单解析对象
 const form = new formidable.IncomingForm();
 // 设置文件上传路径
 form.uploadDir = "/my/dir";
 // 是否保留表单上传文件的扩展名
 form.keepExtensions = false;
 // 对表单进行解析
 form.parse(req, (err, fields, files) => {
     // fields 存储普通请求参数
         // files 存储上传的文件信息
 });
```

## mongoose-sex-page

分页功能

```js
const pagination = require('mongoose-sex-page');
pagination(集合构造函数).page(1) .size(20) .display(8) .exec();
```

## config

可以自动判断当前的运行环境, 获取配置信息

```bash
# 安装
yarn add config
# 在项目的根目录创建 config 文件夹
# config 里面新建 default.json development.json production.json

# require
const config = require('config');
# 获取信息
config.get()将为未定义的键抛出异常，以帮助捕获拼写错误和缺失值。
config.has()测试是否定义了配置值。
```

### production.json

```json
{
  "dbConfig": {
    "host": "localhost",
    "port": 27017,
    "dbName": "customers"
  }
}
```

#### 

敏感信息



# 测试

## Debug

Express 在内部使用[调试](https://www.npmjs.com/package/debug)模块来**记录关于路由匹配、使用的中间件函数、应用程序模式以及请求/响应循环流程的信息。**

要查看 Express 中使用的所有内部日志，在启动应用程序时，请将 `DEBUG` 环境变量设置为 `express:*`。

```bash
$ DEBUG=express:* node index.js
```

在 Windows 上，使用对应的命令。

```bash
> set DEBUG=express:* & node index.js
```



# 开发环境生产环境

## morgan

  ```js
  // 将访问请求打印到控制台
  const morgan = require("margan")
  app.use(morgan('dev'))
  // 使用场景
  // 不同的开发环境做不同的事情
  const morgan = require('morgan');
  if (process.env.NODE_ENV === 'production') {
      // app.use(morgan('dev'));
    	module.exports = require('./prod');
  } else {
    	module.exports = require('./dev');
  }
  ```

# 部署优化

## gzip

> Node+Express部署前端 gzip资源压缩

```js
const express = require('express');
const proxy = require('http-proxy-middleware');
// 服务端压缩gzip
var compression = require('compression');
const app = express();
// 启用服务端压缩gzip
app.use(compression());

app.use(express.static('../deploy'));

app.listen(3000, (req, res) => {
  console.log(req, res);
  console.log('启动成功，请通过localhost:9900访问');
});
```


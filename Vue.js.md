> 我记得 B站 是有尤雨溪关于 vue.js 的纪录片的, 感兴趣的可以去看看
>
> 本文主要是学习 vue3 
>
> 选择 **Options API** 代码风格编写案例

# Vue.js

## 1. 初步了解 vue.js

官方定义： Vue（读作 /vjuː/，类似视图）是一个帮助用户制造界面的 JavaScript 框架。它在标准 HTML、CSS 和 JavaScript 中创建，并提供了一个声明性和基于组件的编程模型，可有效开发地简单或复杂的用户界面。

```html
// .vue 文件
<template>
<!-- 类似于 html 的模版 -->
</template>

<script>
 // 进行 js 操作
</script>

<style>
// css 样式
</style>
```

 在Vue中，一个核心的概念就是：**数据驱动，避免手动操作DOM元素**。这样的话，可以更多的时间去关注数据的业务逻辑，而不是关心 DOM 是如何渲染的了。

```html
<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      // 我们可以通过 data 中的数据来动态修改页面的数据显示
      show: false
    }
  },
}
</script>
```

**解释一下， 就是修改在 vue 实例对象里的 data 数据时，页面会自动更新显示的数据**

 **Vue通过MVVM模式,能够实现视图与模型的双向绑定。**

 **简单来说，就是数据变化的时候, 页面会自动刷新, 页面变化的时候，数据也会自动变化.**

---

### 提高开发效率的发展历程

原生JS -> Jquery之类的类库 -> 前端模板引擎 -> Angular.js / Vue.js（能够帮助我们减少不必要的DOM操作；提高渲染效率；双向数据绑定的概念）

Vue.js 中我们有自己操作 DOM 的方式， 可以不再使用原生方法

---

### 什么是虚拟 DOM

传统的web开发，是利用 jQuery操作DOM，这是非常耗资源的。

**我们可以在 JS 的内存里构建类似于DOM的对象，去拼装数据，拼装完整后，把数据整体解析，一次性插入到html里去。这就形成了虚拟 DOM。**

Vue1.0没有虚拟DOM，直到Vue2.0改成了基于虚拟DOM， 现在常用的版本是 vue3， 本文重点讲解 vue3

---

### Vue框架的特点

与 jquery 的区别：vue数据驱动，通过数据来显示视图层而不是节点操作。

vue 一般使用场景：数据操作比较多、频繁的场景，更加便捷。


- 模板渲染：基于 html 的模板语法，学习成本低。

- **响应式的更新机制：数据改变之后，视图会自动刷新。**

- 渐进式框架 （在任何页面上嵌入为 Web 组件）

- 组件化/模块化 （确实使代码结构页面看起来清楚）

- 轻量：开启 gzip压缩后，可以达到 20kb 大小。（React 达到 35kb，AngularJS 达到60kb）。

---

### MVVM 模式

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16%20%E4%B8%8B%E5%8D%884.18.55.png)

**ViewModel是 Vue.js 的核心，它是一个Vue实例。**

Vue实例是作用于某一个HTML元素上的，这个元素可以是HTML的 body 元素，也可以是指定了id的某个元素。（一般以 #app 指定，当然也可以自己指定，我们会把 vue 实例挂载到该 DOM 元素）

**当创建了ViewModel后，双向绑定是如何达成的呢？**

首先，我们将上图中的DOM Listeners和Data Bindings看作两个工具，它们是实现双向绑定的关键。 

从View侧看，ViewModel中的**DOM Listeners工具会帮我们监测页面上DOM元素的变化**，如果有变化，则更改Model中的数据； 

从Model侧看，当我们更新Model中的数据时，**Data Bindings工具会帮我们更新页面中的DOM元素。**

MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

mvc和mvvm其实区别并不大，都是一种设计思想。主要就是mvc中Controller演变成mvvm中的viewModel。mvvm主要解决了mvc中大量的DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。

---

### 单文件组件

在大多数支持构建工具的 Vue 项目中，我们使用类似于 HTML 的文件格式创建 Vue 组件，称为单文件组件（也称为*.vue文件，缩写为SFC）。

顾名思义，Vue SFC 将组件的逻辑 (JavaScript)、模板 (HTML) 和样式 (CSS) 封装在一个文件中。这是前面的示例，以 SFC 格式编写：

```html
<script>
export default {
  data() {
    return {
      键值对的形式保存数据
    }
  }
}
</script>

<template>
  <p>类似于 html 的标签语法展示组件内容</p>
</template>

<style scoped>
// 样式的设计
</style>
```

**通常一个 .vue 文件就是一个组件， 用于实现页面某一个部分**

---

## 2. Vue 的应用方式

> 推荐： 我们首先要安装好 Node.js环境，然后再来做下面的操作。

---

### 引用 Vue.js 文件

**首先介绍的方式都是直接在 `html` 文件中使用**

1、**方式一**：（CDN的方式进行引用）

```html
<head>
    <script src="https://unpkg.com/vue@3"></script>
</head>
```

2、方式二：（下载 vue.js 文件）

去网站下载 vue.js 文件，直接放到工程文件里，然后引用。

3、方式三：（NPM的方式安装vue）

```bash
# 最新稳定版
$ npm install vue
```

然后在代码中通过下面这种方式进行引用：

```javascript
  import Vue from 'vue'
```

首先我们需要通过 createApp 创建一个应用程序实例

```html
<script src="https://unpkg.com/vue@3"></script>

<div id="app">
  
</div>

<script>
  Vue.createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

.mount()在调用方法中，应用程序实例不会出现其之前的任何内容。它需要一个“容器”，它可以是实际的 DOM 元素或选择参数字符串：

```html
<div id="app"></div>
```

```js
*.mount('#app')
```

**上面的示例使用了 Vue 的全局构建，其中所有 API 都暴露在全局`Vue`变量下。**

---

### 利用 vue-cli 新建项目

Vue 提供一个命令行工具，可用于快速搭建大型单页应用。该工具为现代化的前端开发工作流提供了开箱即用的构建配置。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目。

> 推荐使用 vue3, vue3 已经成为了 vue 的默认版本

```bash
// 全局安装, 可以在任何位置安装脚手架
  npm install -g @vue/cli
```

```bash
// vue3 创建项目的写法 
  vue create project
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/fa43f9cbf6ed4b09887936606b1e8e88.png)
这里的上半部分是提醒我要升级， 下半部分是正常显示

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220325094417451%20%E4%B8%8B%E5%8D%884.18.55.png)

这里有三个选项 （空格是选中， 回车是确定)

1. 使用 vue3 （默认版本） ， babel（为了打包后使es6语法降级兼容低版本浏览器），eslint（语法规范）
2. 同上， 只有 vue 版本不一样
3. 自定义


选择完成以后， 会自动搭建项目， 这里我们稍等一会

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220325094418524%20%E4%B8%8B%E5%8D%884.18.55.png)

```bash
// 进入项目目录
  cd project
// 运行项目
  npm run serve
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220325094417522%20%E4%B8%8B%E5%8D%884.18.55.png)
点击显示的链接就可以进入创建项目所显示的页面了

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220325094418699%20%E4%B8%8B%E5%8D%884.18.55.png)

---

### 使用 vite （官方推荐）

官方的 Vue 构建设置基于[Vite](https://vitejs.dev/)，这是一个现代、轻量级且速度极快的前端构建工具。

创建启用构建工具的 Vue 项目，请在命令行中运行以下命令（不带`>`符号）：

```
> npm init vue@latest
```

选择配置

```vite
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add Cypress for both Unit and End-to-End testing? … No / Yes
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formating? … No / Yes
```

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220325103100559%20%E4%B8%8B%E5%8D%884.18.55.png)

然后进入项目， 运行项目

```
> cd <your-project-name>
> npm install
> npm run dev
```

![image-20220325103159428](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220325103159428%20%E4%B8%8B%E5%8D%884.18.55.png)

---

### vue 实例的解释

每个 Vue 应用程序首先使用以下函数创建一个新的**应用程序实例**[`createApp`](https://vuejs.org/api/application.html#createapp)：

```js
// 从 vue 中导入 creatApp 这个方法（看不懂可以忽视或者去看一下模块化的介绍， 并不重要）
import { createApp } from 'vue'

const app = createApp({
  /* root component options */
})
```

---

### 根组件

我们传入的对象`createApp`实际上是一个组件。每个应用程序都需要一个“根组件”，它可以包含其他组件作为其子组件。

如果您使用的是单文件组件，我们通常会从另一个文件中导入根组件：

```js
import { createApp } from 'vue'
// import the root component App from a single-file component.
import App from './App.vue'

const app = createApp(App)
```

---

### 挂载

`.mount()`在调用其方法之前，应用程序实例不会呈现任何内容。它需要一个“容器”参数，它可以是实际的 DOM 元素或选择器字符串：

```html
<div id="app"></div>

app.mount('#app')
```

应用程序根组件的内容将在容器元素内呈现。容器元素本身不被视为应用程序的一部分。

在完成应用程序注册后，应调用该`.mount()`方法。另请注意，与注册方法不同，它的返回值是根组件实例而不是应用程序实例。

---

### 应用程序配置

应用程序实例公开了一个`.config`对象，允许我们配置一些应用程序级选项

---

## 3. vue 系统指令

Vue 使用基于 HTML 的模板语法，允许您以声明方式将渲染的 DOM 绑定到底层组件实例的数据。所有 Vue 模板都是语法上有效的 HTML，可以被符合规范的浏览器和 HTML 解析器解析。

指令是带有`v-`前缀的特殊属性。Vue 提供了许多内置指令`v-html`

**指令的工作是在其表达式的值发生变化时对 DOM 进行响应式更新。**

###  插值表达式 {{ }}

数据绑定最常见的形式就是使用 “**Mustache**” 语法（双大括号）的文本插值，在标签中使用。例如：

```html
<span>Message: {{ msg }}</span>
```

Mustache 标签将会被替代为对应数据对象上 msg 属性（msg定义在data对象中）的值。

无论何时，绑定的数据对象上 msg 属性发生了改变，插值处的内容都会**自动更新**。

`{{  }}`对JavaScript 表达式支持，例如：

```javascript
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ name == 'x' ? 'true' : 'false' }}

{{ message.split('').reverse().join('') }}
```


但是有个限制就是，每个绑定都**只能包含单个表达式**，如下表达式无效：

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (true) { return message } }}
```

---

### v-cloak

`v-cloak`：保持和元素实例的关联，直到结束编译后自动消失。

v-cloak指令和CSS 规则一起用的时候，能够**解决差值表达式闪烁的问题**（即：可以隐藏未编译的标签直到实例准备完毕）。

**在网速很慢的情况下，一开始会直接显示`{{name}}`这个内容** ，等网络加载完成了，才会显示`name` 属性的值。

```html
<html lang="en">
<head>
  <style>
    /*2、在样式表里设置：只要是有 v-cloak 属性的标签，我都让它隐藏。
    直到 Vue实例化完毕以后，v-cloak 会自动消失，那么对应的css样式就会失去作用，最终将span中的内容呈现给用户 */
    [v-cloak] {
      display: none;
    }
  </style>
</head>

<body>
  <div id="app">
    <!-- 1、给 span 标签添加 v-cloak 属性 -->
    <span v-cloak>{{name}}</span>
  </div>
</body>

<script src="vue2.5.16.js"></script>
<script>
  new Vue({
    el: '#app',
    data: {
      name: 'ximingx'
    }
  });
</script>
</html>
```

---

### v-text

v-text可以将一个变量的值渲染到指定的元素中。

与插值表达式的区别: 插值表达式只会**替换自己的这个占位符**，并不会把整个元素的内容清空。v-text 会**覆盖**元素中原本的内容。

---

### v-html


`v-text`是纯文本，而`v-html`会被解析成html元素。

注意：使用v-html渲染数据可能会非常危险，因为它很容易导致 XSS（跨站脚本） 攻击，使用的时候请谨慎，能够使用{{}}或者v-text实现的不要使用v-html。

v-text和v-html专门用来展示数据, 其作用和插值表达式类似。**v-text和v-html可以避免插值闪烁问题.**

当网速比较慢时, 使用 {{ }} 来展示数据, **有可能会产生插值闪烁问题。**

插值闪烁: 在数据未加载完成时，页面会显示出原始的{undefined{}}, 过一会才会展示正常数据.

---

### v-on: 事件绑定

![指令语法图](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/directive.69c37117%20%E4%B8%8B%E5%8D%884.18.55.png)

例如：

```html
    <button v-on:click="change">改变name的值</button>
```

可以简写成：

```html
	// change 是写在下面的方法
    <button @click="change">改变name的值</button>
```

这里的 change 是写在 vue是 实例对象里的 methods 里的方法

```js
<script>
  var myVue = new Vue({
    el: '#div1',
    data: { 
      name: 'ximingx'
    },
    //注意，下方这个 `methods` 是Vue中定义方法的关键字，不能改
    //这个 methods 属性中定义了当前Vue实例所有可用的方法
    methods: {
      change: function() { //上面的button按钮的点击事件
        this.name += '1';
      }
    }
  });
</script>
```

v-on的常用事件

v-on 提供了click 事件，也提供了一些其他的事件。


- v-on:click

- v-on:keydown

- v-on:keyup

- v-on:mousedown

- v-on:mouseover

- v-on:submit

v-on的常见事件修饰符

vue为v-on提供了事件修饰符，通过点(.)表示的指令后缀来调用修饰符。

注：使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。

`v-on` 提供了很多事件修饰符来辅助实现一些功能。事件修饰符有如下：

- `.stop`  阻止冒泡。本质是调用 event.stopPropagation()。阻止点击事件冒泡。等同于JavaScript中的event.stopPropagation(). 使用了.stop后，点击子节点不会捕获到父节点的事件


- `.prevent`  阻止默认事件（默认行为）。本质是调用 event.preventDefault()。
- `.capture`  添加事件监听器时，使用捕获的方式（也就是说，事件采用捕获的方式，而不是采用冒泡的方式）。
- `.self`  只有当事件在该元素本身（比如不是子元素）触发时，才会触发回调。
- `.once`  事件只触发一次。
- `.{keyCode | keyAlias}`   只当事件是从侦听器绑定的元素本身触发时，才触发回调。
- `.native` 监听组件根元素的原生事件。

关键修饰符

在监听键盘事件时，我们经常需要检查特定的键。Vue 允许为`v-on`或`@`在监听键事件时添加键修饰符：

```
<!-- only call `vm.submit()` when the `key` is `Enter` -->
<input @keyup.enter="submit" />
```

您可以直接使用通过`KeyboardEvent.key` 修饰符公开的任何有效键名，方法是将它们转换为 kebab-case。

```
<input @keyup.page-down="onPageDown" />
```

Vue 为最常用的键提供别名：

- `.enter`
- `.tab`
- `.delete`（捕获“删除”和“退格”键）
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

---


### v-bind：属性绑定机制

不能在 HTML 属性中使用胡须。相反， `v-bind`：用于绑定**属性**。动态的获取属性的值， 不再是一个固定的值

>  他绑定的是属性 要和 {{ }} 语法区分开

**如果绑定值为null或undefined，则该属性将从呈现的元素中删除。**

比如说：

```html
    <img v-bind:src="imageSrc +'string'">

    <div v-bind:style="{ fontSize: size + 'px' }">{{ msg }}</div>
```


上方代码中，给属性加了 v-bind 之后，属性值里的整体内容是**表达式**，属性值里的`imageSrc`和`size`是Vue实例里面的**变量**。

也就是说， v-bind的属性值里，可以写合法的 js 表达式。

上面两行代码也可以简写成：

```html
    <img :src="imageSrc +'string'">

    <div :style="{ fontSize: size + 'px' }"></div>
```

Vue中通过属性绑定为元素设置class 类样式

下面这是一般的写法

```html
    <style>
        .red {
            color: red;
        }

        .thin {
            font-weight: thin;
        }
    </style>

    <h1 class="red thin"></h1>
```

而在 vue 中， 我们可以使用多种方式传递值

**方式一： 数组**

```html
    <h1 :class="['red', 'thin']"></h1>
```

上方代码中，注意，数组里写的是字符串；如果不加单引号，就不是字符串了，而是变量，我们一般可以用这种方式来搞事情

**方式二： 三元表达式**

外层也是通过数组的形式

```html
<div id="app">
        <!-- 通过data中布尔值 flag 来判断：如果 flag 为 true，就给 h1 标签添加`red`样式；否则，就不设置样式。 -->
        <h1 :class="[flag ? 'red' : '']"></h1>
    </div>

    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                flag: false
            }
        });
    </script>
```

**写法三：在数组中使用 对象 来代替 三元表达式**

```html
    <div id="app">
        <!-- vue的写法3：在数组中使用对象来代替三元表达式。-->
        <h1 :class="[ {'thin': flag} ]"></h1>
    </div>

    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                flag: true
            }
        });
    </script>
```

**写法四：直接使用对象**


```html
<!-- 在为 class 使用 v-bind 绑定 对象的时候，对象的属性是类名。由于 对象的属性名可带引号，也可不带引号，所以 这里我没写引号；  属性的值 是一个标识符 -->
 <h1 :class="{style1: true, style2: false}"></h1>
```

上方代码的意思是，给`<h1>`标签使用样式`style1`，不使用样式`style2`。

除此之外， 还可以这样绑定多个属性

```js
<div v-bind="objectOfAttrs"></div>

data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```

除此之外还可以绑定函数

```html
<span :class="choice(data)">
  {{ formatDate(date) }}
</span>
```

> 每次组件更新时都会调用内部绑定表达式的函数，因此它们没有任何副作用，例如更改数据或触发异步操作。

---

### v-model：双向数据绑定


> 重点：**双向数据绑定，只能用于表单元素，或者用于自定义组件**。
> 而 v-bind 所有元素都可以， 但他是单向绑定的

之前的文章里，我们通过v-bind，给`<input>`标签绑定了`data`对象里的`name`属性。当`data`里的`name`的值发生改变时，`<input>`标签里的内容会自动更新。但是修改 `<input>`标签里的内容 不会引起`data`里的`name`的值发生改变

可我现在要做的是：我在`<input>`标签里修改内容，要求`data`里的`name`的值自动更新。从而实现双向数据绑定。该怎么做呢？这就可以利用`v-model`这个属性。

**区别**：

- v-bind：只能实现数据的**单向**绑定，从 M 自动绑定到 V。

- v-model：只有`v-model`才能实现**双向**数据绑定。注意，v-model 后面不需要跟冒号，

**注意**：v-model 只能运用在**表单元素中，或者用于自定义组件**。常见的表单元素包括：input(radio, text, address, email....) 、select、checkbox 、textarea。

我们还可以将多个复选框绑定到同一个数组或[Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)值：

```html
<script>
export default {
  data() {
    return {
      checkedNames: []
    }
  }
}
</script>
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
```

### .lazy

默认情况下，`v-model`在每个事件之后将输入与数据同步（[上述](https://vuejs.org/guide/essentials/forms.html#vmodel-ime-tip)`input`IME 组合除外）。您可以添加修饰符以改为在事件后同步：`lazy``change`

```html
<!-- synced after "change" instead of "input" -->
<input v-model.lazy="msg" />
```

### .number

如果您希望用户输入自动转换为数字，您可以将`number`修饰符添加到`v-model`托管输入：

```html
<input v-model.number="age" />
```

如果无法用 解析该值`parseFloat()`，则使用原始值代替。

如果输入有，`number`则自动应用修饰符`type="number"`。

### .trim

如果您希望自动修剪用户输入中的空白，您可以将`trim`修饰符添加到您的`v-model`-managed 输入中：

```html
<input v-model.trim="msg" />
```

---

### v-for 循环遍历

我们可以使用该v-for指令基于数组呈现项目列表。该v-for指令需要格式为 的特殊语法`item in items`，其中`items`是源数据数组，`item`是被迭代的数组元素的别名：

```js
<li v-for="item in items">
  {{ item.message }}
</li>

data() {
  return {
    items: [{ message: 'mes1' }, { message: 'mes2' }]
  }
}
```


```html
<!-- 不是每一个都需要全写， 看需求 -->
<li v-for="(value, key, index) in obj1" :key="index">值：{{value}} --- 键：{{key}} --- index：{{index}} </li>
<script>
    new Vue({
      el: '#app',
      data: {
        obj1: {
          name: 'ximingx',
          age: '20',
          gender: '男'
        }
      }
    });
</script>
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/3d4cfb9d1026470cbf4961f96d8db39a%20%E4%B8%8B%E5%8D%884.18.54.png)

与 template 类似`v-if`，您也可以使用`<template>`标签 with`v-for`来渲染一个包含多个元素的块。例如：

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

您也可以使用`of`作为分隔符而不是`in`，以便它更接近 JavaScript 的迭代器语法：

```html
<div v-for="item of items"></div>
```

**注意**：在 Vue 2.2.0+ 版本里，当在**组件中**使用 v-for 时，key 属性是必须要加上的。

这样做是因为：每次 for 循环的时候，通过指定 key 来标示当前循环这一项的**唯一身份**。

> 当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引下显示已被渲染过的每个元素。

> 为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 key 属性。

key的类型只能是：string/number，而且要通过 v-bind 来指定。

---

### v-if：设置元素的显示和隐藏

**作用**：根据表达式的值的真假条件，来决定是否渲染元素，如果为false则不渲染（达到隐藏元素的目的），如果为true则渲染。

在切换时，元素和它的数据绑定会被销毁并重建。

**`v-if`在`<template>`**

因为`v-if`是一个指令，所以它必须附加到单个元素。但是如果我们想要切换多个元素怎么办？在这种情况下，我们可以`v-if`在一个`<template>`元素上使用，它作为一个不可见的包装器。最终渲染结果将不包括该`<template>`元素。

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

`v-else`也`v-else-if`可以用在`<template>`.

---

### v-show：元素的显示和隐藏

**作用**：根据表达式的真假条件，来切换元素的 display 属性。如果为false，则在元素上添加 `display:none`属性；否则移除`display:none`属性。

`v-show`不支持该`<template>`元素


---

### v-if和v-show的区别

`v-if`和`v-show`都能够实现对一个元素的隐藏和显示操作。

区别：

- v-if：每次都会重新添加/删除DOM元素

- v-show：每次不会重新进行DOM的添加/删除操作，只是在这个元素上添加/移除`style="display:none"`属性，表示节点的显示和隐藏。

优缺点：

- v-if：有较高的切换性能消耗。这个很好理解，毕竟每次都要进行dom的添加／删除操作。

- v-show：**有较高的初始渲染消耗**。也就是说，即使一开始`v-show="false"`，该节点也会被创建，只是隐藏起来了。而`v-if="false"`的节点，根本就不会被创建。

**总结**：

- 如果元素涉及到频繁的切换，最好不要使用 v-if, 而是推荐使用 v-show
- 如果元素可能永远也不会被显示出来被用户看到，则推荐使用 v-if
- 由于隐含优先级，不建议在同一元素上**使用**and `v-if`。当`v-if`和`v-for`都用于同一个元素时，`v-if`将首先评估。

---

## 4. vue Reactivity

### data

我们使用`data`选项来声明组件的反应状态。选项值应该是一个返回对象的函数。Vue 会在创建新组件实例时调用该函数，并将返回的对象包装在其响应系统中。此对象的任何顶级属性都代理在组件实例上（`this`在方法和生命周期挂钩中）：

```js
data() {
    return {
      
    }
  }
```

这些实例属性仅在首次创建实例时添加，因此您需要确保它们都存在于函数返回的对象中`data`。如有必要，使用`null`或`undefined`其他一些占位符值来表示所需值尚不可用的属性。

### methods

Vue 自动绑定`this`值，`methods`以便它始终引用组件实例。这可确保方法在`this`用作事件侦听器或回调时保留正确的值。定义 时应避免使用箭头函数`methods`，因为这会阻止 Vue 绑定适当的`this`值：

```js
export default {
  methods: {
    increment: () => {
      
    }
  }
}
```

---

### computed

计算属性就是一个提前定义好的方法, 该方法可以看作是一个特殊的值, 可以在插值表达式中使用.

```js
 var app = new Vue({
     el:"#app",
     // 计算属性必须放在Vue的computed中
     computed:{
         // 定义计算属性
         // 有方法的皮， 但是却是当作属性使用
         属性名() {
             return "返回值";
         }
     }
});

```

---

### watch

计算属性允许我们以声明方式计算派生值。但是，在某些情况下，我们需要执行“副作用”以响应状态更改——例如，改变 DOM，或根据异步操作的结果更改另一部分状态。

使用 Options API，我们可以使用`watch`选项在反应属性发生变化时触发函数：

 watch可以监听简单属性值及其对象中属性值的变化.

 **watch类似于onchange事件,可以在属性值修改的时候,执行某些操作.**

```js
var app = new Vue({
    el:"#app",
    data:{
        message:"白大锅",
        person:{"name":"heima", "age":13}
    },
    //watch监听
    watch:{
        //监听message属性值,newValue代表新值,oldValue代表旧值
        message(newValue, oldValue){
        	console.log("新值：" + newValue + "；旧值：" + oldValue);
        },
        //监控person对象的值,对象的监控只能获取新值
        person: {
            //开启深度监控；监控对象中的属性值变化
            deep: true,
            //获取到对象的最新属性数据(obj代表新对象)
            handler(obj){
                console.log("name = " + obj.name + "; age=" + obj.age);
            }
        }
    }
});
```

---

## 5. Vue.js 生命周期

从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期。

Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。

生命周期钩子 = 生命周期函数 = 生命周期事件。

生命周期中里有一个很重要的概念： **钩子函数**, 其实就是Vue提前定义好的事件, 其作用类似于Servlet的init方法和distory方法


### 创建期间的生命周期函数

- beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性

- created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板。我们可以在这里进行Ajax请求。

- beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中

- mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示。（mounted之后，表示**真实DOM渲染完了，可以操作DOM了**）

---

### 运行期间的生命周期函数

- beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点

- updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了。

PS：数据发生变化时，会触发这两个方法。不过，我们一般用watch来做。

---

### 销毁期间的生命周期函数

- beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。

- destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

PS：可以在beforeDestroy里**清除定时器、或清除事件绑定**。

---

第一次页面加载时会触发 beforeCreate, created, beforeMount, mounted 这几个钩子

DOM 渲染在 mounted 中就已经完成了。

生命周期钩子的一些使用方法：

- beforecreate : 可以在此阶段加loading事件，在加载实例时触发；

- created : 初始化完成时的事件写在这里，如在这结束loading事件，异步请求也适宜在这里调用；

- mounted : 挂载元素，获取到DOM节点；

- updated : 如果对数据统一处理，在这里写上相应函数；

- beforeDestroy : 可以做一个确认停止事件的确认框；

---

![组件生命周期图](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/lifecycle.16e4c08e%20%E4%B8%8B%E5%8D%884.18.55.png)

---

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/480a7cdefd3a9a2a01a4289c8d3d038e%20%E4%B8%8B%E5%8D%884.18.55.png)

## 6. Vue 动画

Vue 提供了两个内置组件，可以帮助处理过渡和动画以响应不断变化的状态：

- `<Transition>`用于在元素或组件进入和离开 DOM 时应用动画。本页对此进行了介绍。

- `<TransitionGroup>`用于在将元素或组件插入列表、从中删除或在v-for列表中移动时应用动画。

### 6.1 Transition

`<Transition>`是一个内置组件：这意味着它可以在任何组件的模板中使用，而无需注册它。它可用于在通过其默认插槽传递给它的元素或组件上应用进入和离开动画。进入或离开可以由以下之一触发：

- 通过条件渲染v-if
- 通过条件显示v-show
- <component>通过特殊元素切换动态组件

> <Transition>仅支持单个元素或组件作为其插槽内容。如果内容是一个组件，则该组件也必须只有一个根元素。

### 6.2 动画状态


| .              | 状态                                                         |
| -------------- | ------------------------------------------------------------ |
| v-enter-from   | 进入的起始状态。在元素插入之前添加，在元素插入后立马（一帧）移除。 |
| v-enter-active | 进入的活动状态。在整个进入阶段应用。在插入元素之前添加，在过渡/动画完成时移除。此类可用于定义进入过渡的持续时间、延迟和缓动曲线。 |
| v-enter-to     | 进入的结束状态。在元素插入后添加一帧（同时v-enter-from被移除），在过渡/动画完成时移除。 |
| v-leave-from   | 离开的开始状态。触发离开过渡时立即添加，一帧后删除。         |
| v-leave-active | 离开的活动状态。在整个离开阶段应用。在触发离开过渡时立即添加，在过渡/动画完成时删除。此类可用于定义离开过渡的持续时间、延迟和缓动曲线。 |
| v-leave-to     | 休假的结束状态。在触发离开过渡后添加一帧（同时v-leave-from删除），在过渡/动画完成时删除。 |

### 6.3 transition 命名

```html
<Transition name="fade">

</Transition>
```

对于命名转换，其转换类将以其名称而不是 `v` . 例如，上述转换的应用类将fade-enter-active代替v-enter-active. 淡入淡出过渡的 CSS 应如下所示：

```css
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```

## 7. 组件

组件的出现，就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可。

在 vue 项目中， 我们将 ui 作为单独的一部分，嵌套应用程序 ， 每一个组件负责自己的页面内容， 最重要的是， 减少了造轮子

![image-20220325201424552](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220325201424552.png)

---

### 7.1 模块化和组件化的区别

- 模块化：是从代码逻辑的角度进行划分的；方便代码分层开发，保证每个功能模块的职能单一
- 组件化：是从UI界面的角度进行划分的；前端的组件化，方便UI组件的重用

### 7.2 组件的注册

我们可以使用以下方法使组件在当前[Vue 应用程序](https://vuejs.org/guide/essentials/application.html)`app.component()`中全局可用：

```js
import { createApp } from 'vue'

const app = createApp({})

app.component(
  // the registered name
  'MyComponent',
  // the implementation
  {
    /* ... */
  }
)
```

如果使用 SFC，您将注册导入的`.vue`文件：

```js
import MyComponent from './App.vue'

app.component('MyComponent', MyComponent)
```

全局注册的组件可以在此应用程序中的任何组件的模板中使

局部注册的组件只能在当前组件使用

```html
<script>
import ComponentA from './ComponentA.vue'

export default {
  // 局部注册的组件
  components: {
    ComponentA
  }
}
</script>

<template>
  <ComponentA />
</template>
```

### 7.3 组件的使用

```html
<script>
import ButtonCounter from './ButtonCounter.vue'

export default {
  components: {
    ButtonCounter
  }
}
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

使用 切换多个组件一个组件在切换离开时将被卸载。我们可以通过内置组件`KeepAlive` 强制非活动组件保持

### 7.4 组件之间值的传递

`Vue` 组件作用域是孤立的，不允许在子组件模板内直接引用父组件的数据。必须使用特定的方法才能实现组件之间的数据传递。

- 父组件通过标签上`:data=data`方式定义传值， 子组件通过`props`方法接受数据
- 子组件通过`$emit`方法传递参数， 父组件通过定义的函数接收数据

```html
<!-- BlogPost.vue -->
<script>
export default {
  props: ['title']
}
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```

当一个值被传递给一个 prop 属性时，它就成为该组件实例上的一个属性。该属性的值可以在模板中和组件的`this`上下文中访问，就像任何其他组件属性一样。

一个组件可以拥有任意数量的 props，默认情况下，任何值都可以传递给任何 props。

注册后，您可以将数据作为自定义属性传递给它，如下所示：

```html
<!-- App.vue -->
import BlogPost.vue from " ~ ~ ~ 路径"

<!-- 组件的调用， 在父组件之中给子组件传递值 -->
<!-- 在这个案例中App.vue是父组件，BlogPost.vue是子组件 -->
<BlogPost title="My journey with Vue" />
<BlogPost title="Blogging with Vue" />
<BlogPost title="Why Vue is so fun" />
```

### 7.5 props

**1.数组形式**

```c
props: [data1, data2]
1
```

数组形式相当于直接接收消息，不做任何校验，一般来说，不建议使用数组形式。

**2.简单对象形式**

除了使用字符串数组声明 props 之外，我们还可以使用对象语法：

```js
export default {
  props: {
    title: String,
    likes: Number
  }
}
```

组件可以为其 props 指定要求，例如您已经看到的类型。如果不满足要求，Vue 将在浏览器的 JavaScript 控制台中警告

**3.复杂对象形式**

要指定 prop 验证，您可以向option提供具有验证要求的对象，而不是字符串数组。例如：`props`

- type: 设定参数类型，当传入参数类型与type不相符时，控制台会报错；

- > - `String`
  > - `Number`
  > - `Boolean`
  > - `Array`
  > - `Object`
  > - `Date`
  > - `Function`
  > - `Symbol`

- required：设定参数是否是必传，当设为true时，不传该参数会报错；

- default：设定默认值，当参数类型为复杂类型时，需使用工厂模式生成默认值，否则Vue会在控制台抛出警告。

- validator：校验器，是一个函数，拥有一个代表传入值的形参，可以自定义各种校验，当返回false时，会报错，表示没通过校验。

**`props` 会在一个组件实例创建之前进行验证，所以实例的属性 (如 `data`、`computed` 等) 在 `default` 或 `validator` 函数中是不可用的。**

```js
export default {
  props: {
    // Basic type check
    //  (`null` and `undefined` values will allow any type)
    propA: Number,
    // Multiple possible types
    propB: [String, Number],
    // Required string
    propC: {
      type: String,
      required: true
    },
    // Number with a default value
    propD: {
      type: Number,
      default: 100
    },
    // Object with a default value
    propE: {
      type: Object,
      // Object or array defaults must be returned from
      // a factory function. The function receives the raw
      // props received by the component as the argument.
      default(rawProps) {
        // default function receives the raw props object as argument
        return { message: 'hello' }
      }
    },
    // Custom validator function
    propF: {
      validator(value) {
        // The value must match one of these strings
        return ['success', 'warning', 'danger'].includes(value)
      }
    },
    // Function with a default value
    propG: {
      type: Function,
      // Unlike object or array default, this is not a factory function - this is a function to serve as a default value
      default() {
        return 'Default function'
      }
    }
  }
}
```

### 7.6 slot 插槽



## 8. Vue-router

### 后端路由

对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源。

当前端输入url请求资源时，服务器会监听到是什么url地址，那后端会返回什么样的资源呢？后端这个处理的过程就是通过**路由**来**分发**的。

**总结**：后端路由，就是把所有url地址都对应到服务器的资源，这个**对应关系**就是路由。

---

### 前端路由

对于单页面应用程序来说，主要通过URL中的`hash`（url地址中的#号）来实现不同页面之间的切换。

同时，hash有一个特点：HTTP请求中不会包含hash相关的内容。所以，单页面程序中的页面跳转主要用hash实现。

**总结**：在**单页应用**程序中，这种通过`hash`改变来**切换页面**的方式，称作前端路由（区别于后端路由）。

---

### Vue页面跳转

方式一：

```html
<router-link :to="{name: 'bookshelf', params: { entityId: this.entityId } }"></router-link>
<router-view></router-view>
```

方式二：

```js
// 基础
// 想要导航到不同的 URL，使用 router.push 方法。这个方法会向 history 栈添加一个新记录，所以，当用户点击浏览器后退按钮时，可以返回到之前的 URL。
this.$router.push({path: '/index'})

// 通过 this.$route.params.id 接收参数
this.$router.push({
        name: 'particulars',
        params: {
          id: id
        }
      })

// 通过 this.$route.query.id 接收参数
// 通过query来传递参数，这种情况下 query传递的参数会显示在url后面以?id=？形式展示。
this.$router.push({
      path: '/particulars',
      query: {
        id: id
      }
   })

// query要用path来引入，params要用name来引入，接收参数都是类似的，分别是this.$route.query.name和this.$route.params.name。

this.$router.replace({})
// 设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，于是导航后不会留下 history 记录。点击返回按钮时，不会返回到这个页面。
```



## 9. axios

### 1. axios 的基本了解
1. **官方定义**: Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。
2. 它可以在具有相同代码库的浏览器和 nodejs 中运行
3. 在服务器端它使用本机 node.js 的 http模块，而在客户端（浏览器）它使用 XMLHttpRequests。
4. axios必须先导入才可以使用
5. 使用get或者post方法即可发送请求，
6. then方法的回调函数会在请求成功或者失败时触发
7. 通过回调函数形参可以获取响应内容或者错误信息
8. **简单的理解就是ajax的封装**

### 2. 通过 npm 下载
首先得需要 node 环境
使用 npm：
```bash
npm install axios
```
### 3. 应用场景
CommonJS 用法
```js
const axios = require('axios');
```
### 4. 支持多种请求方法

- axios(config)
- axios.request(config)
- axios.get(url,[,config])
- axios.delete(url,[,config])
- axios.head(url,[,config])
- axios.post(url,[,data[, config]])
- axios.put(url,[,data[, config]])
- axios.patch(url,[,data[, config]])

 > 可以任意选择需要的方式， 灵活的使用

### 5. get set 请求示例

最基础的两种请求方式
> axios(config)
```js
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user'
});
```
> axios(url[, config])

```js
// 发送 GET 请求（默认的方法）
axios('http://ximingx.com',{
      method:"GET",
    })
```
> axios.get(url[, config])
```js
axios.get('/user', {
  params: {
    ID: 123456
  }
})
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  }
```
上面的配置中的 params 用于传递参数

和 async await 的使用

```js
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```
async/await是 ECMAScript 2017 的一部分，在 Internet Explorer 和旧版浏览器中不受支持，因此请谨慎使用。
> 请求默认配置

```js
// 在全局声明之后， 每次的 axios 请求路径前都会拼接上全局声明的路径
axios.defaults.baseURL = 'https://api.example.com';
```

### 6.  并发发送请求

使用axios.all，可以放入多个请求的数组。

axios.all([])返回的是一个数组，使用axios.spread可以将数组[res1,res2]展开为res1和res2。

```js
import axios from 'axios'

export default {
	name: 'app',
	created(){
		// 数组里存放两个 axios 请求，用 `，` 隔开
		axios.all([axios.get('http://127.0.0.1:8080/getAll'),
				   axios.get('http://1ximingx.com/getUserPage',{
						params: {pageNum: 1, pageSize: 10}
					})
		]).then(axios.spread((res1,res2) => {
			console.log(res1)
			console.log(res2)
		}))
	}
}
```

### 7. config 配置总结
**只有 url 是必需的。如果没有指定 method，请求将默认使用 get 方法。**

```js
//config
 
{
  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://ximingx.com/api/',


  // `url` 是用于请求的服务器 URL
  url: '/user',
  // 实际上请求的 url 路径为 https://ximingx.com/api/user/
 
  // `method` 是创建请求时使用的方法
  method: 'post', // 默认是 get

 
  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data) {
    // 对 data 进行任意转换处理
 
    return data;
  }],
 
  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理
 
    return data;
  }],
 
  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},
 
  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 20201613118,
    name: "ximingx"
  },
 
  // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },
 
  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },
 
  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 5000,
 
  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // 默认的
 
  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },
 
  // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },
 
  // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // 默认的
 
  // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default
 
  // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认的
 
  // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },
 
  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },
 
  // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,
 
  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认的
  },
 
  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // 默认的
 
  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),
 
  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: : {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },
 
  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```
### 8. 实例化
> axios.create()
```js
var instance = axios.create({
  baseURL: 'https://ximingx.com',
  timeout: 1000
});
 
// 在实例已创建后修改默认值
instance.defaults.timeout = 2500;

instance({
  url: '/home/getAll'
}).then(res => {
  console.log(res);
})
```
### 9. 请求的响应
```js
{
  // `data` 由服务器提供的响应
  data: {},
 
  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,
 
  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',
 
  // `headers` 服务器响应的头
  headers: {},
 
  // `config` 是为请求提供的配置信息
  config: {}
}
```
### 10. 拦截器

请求拦截的作用是什么？

- 比如config中的一些信息不符合服务器的要求
- 比如每次发送网络请求时, 都希望在界面中显示一个请求的图标
- 某些网络请求(比如登录(token)), 必须携带一些特殊的信息

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });
 
// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```
当然也可以实例化之后使用

```js
import axios from 'axios'

export function request(config) {
  // 1.创建axios的实例
  const instance = axios.create({
    baseURL: 'http://127.0.0.1:8080',
    timeout: 5000
  })

  // 2.axios的拦截器
  // 2.1.请求拦截的作用
  instance.interceptors.request.use(config => {
    // console.log(config);
    return config
  }, err => {
    // console.log(err);
  })

  // 2.2.响应拦截
  instance.interceptors.response.use(res => {
    // console.log(res);
    return res.data
  }, err => {
    console.log(err);
  })

  // 3.发送真正的网络请求
  return instance(config)
}
```


### 11. axios的封装

```js
import axios from 'axios'

export default function axios(option){
	return new Promise((resolve,reject) => {
		//1.创建sxios实例
		const instance = axios.create({
			url: 'api',
			timeout: 5000,
			headers: ''
		})

		//2.传入对象进行网络请求
		// option 处将参数传递过来进行请求
		instance(option).then(res => {
			resolve(res)
		}).catch(err => {
			reject(err)
		})
	})
}
```

或者使用 Promise 的方式

```js
// 封装 request 方法 (request.js 文件)
const axios = require('axios')

module.exports = function request(config) {
  return new Promise((resolve, reject) => {
    // 1.创建axios的实例
    const instance = axios.create({
      baseURL: 'http://localhost:3000/',
      timeout: 5000
    })

    // 发送真正的网络请求
    return instance(config)
  })
}

// 在当前目录另一个文件中调用
const request = require("./request.js")

request("/").then(res => {
  console.log(res);
}).catch(err => {
  console.log(err);
})
```
### 12 封装

```js
import axios from 'axios'

export function request(config) {
  const instance = axios.create({
    baseURL: "http://localhost:3000",
    timeout: 5000,
  })

  instance.interceptors.request.use(config => {
    return config
  },err => {
    console.log(err)
  })

  instance.interceptors.response.use(res => {
    return res.data
  },err => {
    console.log(err)
  })

  return instance(config)
}
```

调用

```js
import {request} from "network/request";
export function que(name) {
  return request({
    url: '/que',
    params: {
      name: name
    }
  })
}
```

### 使用示例

[axios 网络请求获取音乐信息](https://ximingx.blog.csdn.net/article/details/121899533?spm=1001.2014.3001.5502)

### 13. 补充

> 为什么不适用jQuery的Ajax？

在vue开发中不需要使用jQuery，因为jQuery很重量级。使用 jquery 比 vue 体积还大， 得不偿失

> vue官方在Vue1.x的时候，推出了Vue-resource。

Vue-resource角jQuery轻便很多，但在vue2.x之后，尤雨溪对Vue-resource不维护了，简言之，就是弃用了。

> 尤雨溪推荐使用axios。

## 10. Vuex

vuex 是 `vue`框架中**状态管理**工具。

```bahs
npm install vuex
```

需要在在`main.js`引入`store`

```js
// 引入vuex-store
import store from './store/index';
 
createApp(App).use(store)
```

新建一个目录`store` , 新建个index.js文件

```js
import { createStore } from 'vuex'
 
export default createStore({
    state:{
        pathName: "",
        currDbSource: {},
        currJobData: {},
        DbSource: []
    },
    mutations:{
        // 保存当前菜单栏的路径
        savePath(state,pathName){
            state.pathName = pathName;
        },
        // 保存当前点击的数据源
        saveCurrDbSource(state,currDbSource){
            state.currDbSource = currDbSource;
        },
        // 保存当前点击的元数据
        saveCurrJobData(state,currJobData){
            state.currJobData = currJobData;
        },
        // 保存所有数据源
        saveDbSource(state,DbSource){
            state.DbSource = DbSource;
        }
    }
})
```

state是自定义的一些变量，需要用来保存数据，mutations是用来触发事件，相当于方法，用户需要通过触发这个方法，借此来保存数据，参数的话，第二个参数就是用户传入的值，然后在方法中赋值给state中的变量

场景举例：当我点击按钮后，我需要把当前的数据保存到vuex中，然后跳转到别的路由，然后使用这些数据

```js
methods:{
    click(){
        // 点击按钮进行一些操作，然后保存数据
        this.$store.commit('saveCurrDbSource',this.db)
    }
}
```

这里的第一个参数是要触发的方法，也就是上面mutations中的方法，第二个参数是你要传递的数据

**获取数据**

```js
this.$store.state.变量名
 
// 例如
this.$store.state.currDbSource
```

场景有：单页应用中，组件之间的状态，音乐播放、登录状态、加入购物车等。

### vuex 属性

有五种，分别是 `State`、 `Getter`、`Mutation` 、`Action`、 `Module`。

Vuex就是一个仓库，仓库里面放了很多对象。

一般情况下，如果需要访问`vuex.store`中`state`存放的数据，需要使用`this.$store.state.属性名`方式。显然，采取这样的数据访问方式，代码略显繁杂，**辅助函数**为了解决繁杂行问题应运而生。

**State**

- 其中state就是数据源存放地，对应于一般Vue对象里面的data。

- state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新。

**Getter**

- `getters` 可以对`State`进行计算操作，它就是`Store`的计算属性。
- 虽然在组件内也可以做计算属性，但是`getters` 可以在多组件之间复用。
- 如果一个状态只在一个组件内使用，可以不用`getters`。

**Mutation Action**

- `Action` 类似于 `mutation`，不同在于：`Action` 提交的是 `mutation`，而不是直接变更状态；`Action` 可以包含任意异步操作。

### 辅助函数

**通过辅助函数mapGetters、mapState、mapActions、mapMutations，把vuex.store中的属性映射到vue实例身上，这样在vue实例中就能访问vuex.store中的属性了，对于操作vuex.store就变得非常方便。**

state辅助函数为mapState，actions辅助函数为mapActions，mutations辅助函数为mapMutations。（Vuex实例身上有mapState、mapActions、mapMutations属性，属性值都是函数）

1. 需要在当前组件中引入`Vuex`。
2. 通过`Vuex`来调用辅助函数。

## 11. Pinia

Pinia 是 Vue 的存储库，它允许您跨组件/页面共享状态。

Pinia 最初是为了探索 Vuex 的下一次迭代可能会是什么样子，结合了 Vuex 5 核心团队讨论中的许多想法。最终，我们意识到 Pinia 已经实现了我们在 Vuex 5 中想要的大部分内容，并决定实现它取而代之的是新的建议。

**与 Vuex 相比，Pinia 提供了一个更简单的 API，具有更少的仪式，提供了 Composition-API 风格的 API，最重要的是，在与 TypeScript 一起使用时具有可靠的类型推断支持。**

简单的使用案例

```js
// stores/counter.js
import { defineStore } from 'pinia'
export const useCounterStore = defineStore('counter', {
  state: () => {
    return {
      count: 0
    }
  },
  actions: {
    increment() {
      this.count++
    },
  },
})

// 组件中使用
import { useCounterStore } from '@/stores/counter'
export default {
  setup() {
    const counter = useCounterStore()

    counter.count++
    // with autocompletion ✨
    counter.$patch({ count: counter.count + 1 })
    // or using an action instead
    counter.increment()
  },
}
```

### 安装使用

```bash
yarn add pinia
# or with npm
npm install pinia
```

使用

```js
import { createPinia } from 'pinia'

app.use(createPinia())
```

### defineStore（）

存储是使用定义的`defineStore()`，并且它需要一个**唯一的**名称，作为第一个参数传递：

```js
import { defineStore } from 'pinia'

// main 这个名称，也称为id，是必要的，是唯一的
export const useStore = defineStore('main', {
 
})
```

我们正在*定义*`useStore()`一个 store ，因为商店在被调用之前不会被创建`setup()`：

```js
import { useStore } from '@/stores/counter'

export default {
  setup() {
    const store = useStore()

    return {
      store,
    }
  },
}
```



## @补充

### 动态添加对象的属性

Vue中，动态新增对象的属性时，不能直接添加。正确的做法是：Vue.set(obj,key,value)。

### normalize.css

安装

```bash
npm install --save normalize.css 
```

main.js 引入

```js
import 'normalize.css/normalize.css'
```

### keep-alive 

包裹动态组件时，会缓存不活动的组件实例，主要用于**保留组件状态**或**避免重新渲染**。


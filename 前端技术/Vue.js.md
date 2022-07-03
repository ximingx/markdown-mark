# Vue.js

![image-20220529224028541](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205292240654.png)

[TOC]

> 参考文章

| 文章 | 地址 |
|---|---|
| `官网` |https://vuejs.org/ |
| `中文官网` |https://cn.vuejs.org/ |
| `中文官网vue3` |https://v3.cn.vuejs.org/ |
| `通俗易懂中文版翻译` |[staging-cn.vuejs.org](https://link.juejin.cn/?target=https%3A%2F%2Fstaging-cn.vuejs.org%2F) |
| `菜鸟教程` |https://www.runoob.com/vue3/vue3-tutorial.html |
| `W3CSchool` | https://www.w3cschool.cn/vuejs3 |

## 1. 基础理论认识

首先普及一个知识, 近年来比较受欢迎的前端框架有 `Google `的` AngularJS` , `Facebook` 的 `ReactJs`, 以及 `尤雨溪`的 `Vue.js`

### 1. vue 初步了解

> `vue` 的定义

官方定义： `Vue`（读作` /vjuː/`，类似 `ivew` ）是一个帮助用户制造界面的 `JavaScript `框架。

传统的网站开发一般采用`HTML+CSS+JS`作为技术架构，而`vue`立足于其上，以模板语法为基础，以数据绑定和组件化开发为核心

```js
// 从 vue 的包中解构出 createApp 方法, 用来创建一个实例
import { createApp } from 'vue'

createApp({
  data() {
    return {
      count: 0
    }
  }
// 链式调用, mount('#app'), 绑定到 #app 元素上
}).mount('#app')
```

```html
<div id="app">
  <button @click="count++">
    {{ count }}
  </button>
</div>
```

---

### 2. 渐进式前端框架

> 官方给 `vue `的定位是前端框架
>
> 因为它提供了构建用户界面的一整套解决方案（俗称 **`vue 全家桶`**）

- `vue`（核心库）
- `vue-router`（路由方案）
- `vuex`（状态管理方案）
- `vue 组件库`（快速搭建页面`UI `效果的方案）

> 以及辅助 `vue `项目开发的一系列工具：

- `vue-cli`（`npm `全局包：一键生成工程化的 `vue `项目 -` `基于 `webpack`、大而全）
- `vite`（`npm `全局包：一键生成工程化的 `vue `项目 - 小而巧）
- `vue-devtools`（浏览器插件：辅助调试的工具）
- `vetur`（`vscode `插件：提供语法高亮和智能提示）
- `axios`: `ajax`请求
- `vue-router`: 路由
- `vuex`: 状态管理
- `vue-lazyload`: 图片懒加载
- `vue-scroller`: 页面滑动相关
- `mint-ui`: 基于`vue`的组件库(移动端)
- `element-plus`: 基于`vue`的组件库(PC端)

> 与其它框架的关联

- 借鉴`angular`的模板和`数据绑定技术`
- 借鉴`react`的组件化和`虚拟DOM技术`

> `vue` 是渐进化框架, 应用于

- 增强静态的 `HTML `而无需构建步骤
- 在任何页面中作为` Web Components `嵌入
- 单页应用 (`SPA`)
- 全栈 / 服务端渲染 (`SSR`)
- `Jamstack `/ 静态站点生成 (`SSG`)
- 目标为桌面端、移动端、`WebGL`，甚至是命令行终端

---

### 3. 提高效率的发展历程

大概了解一下前端的库和框架的发展

特殊强调一下: `jQuery2.0`的原始大小为`235KB`，优化后为`81KB`, 唔, 后面会有和其他框架文件大小的对比

`原生JS` -> `Jquery之类的类库` -> `前端模板引擎` -> `Angular.js / Vue.js`

---

### 4. 虚拟 DOM

传统的`web`开发，是利用 `jQuery`操作`DOM`，这是非常耗资源的

而且 `jquery` 的包比 `vue` 大很多, 加载更慢

> `Vue1.0`没有`虚拟DOM`，直到`Vue2.0`改成了基于`虚拟DOM`

虚拟 `DOM` 使得我们可以在 `JS `的内存里构建类似于`DOM`的对象，去拼装数据，拼装完整后，把数据整体解析，一次性插入到`html`里去。

---

### 5. Vue框架的特点

与 `jquery `的区别：`vue`是数据驱动，通过数据来显示视图层而不是通过繁杂的节点操作。

> `vue `一般使用场景：数据操作比较多、频繁的场景


- 模板渲染：基于 `html `的模板语法，学习成本低。

- 响应式的更新机制：数据改变之后，视图会自动刷新。

- 渐进式框架 （在任何页面上嵌入为 `Web `组件） , `vue `的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合, 减少造轮子, 嗷呜, 不是我懒的原因

- 组件化/模块化 （确实使代码结构页面看起来清楚）

- 轻量：开启 `gzip`压缩后，可以达到 `20kb` 大小。（`React `达到 `35kb`，`AngularJS `达到`60kb`）。(当然你学习的时候可能是看不出来差别的, 但是一个项目上线的时候, 加载资源是很耗时的任务, 呜呜呜)

---

### 6. MVVM 模式

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16%20%E4%B8%8B%E5%8D%884.18.55.png)

**`ViewModel`是` Vue.js` 的核心，它是一个`Vue实例`。**

首先，我们将上图中的**`DOM Listeners`和`Data Bindings`**看作两个工具，它们是实现双向绑定的关键。 

> `View`

从`View`侧看，`ViewModel`中的**`DOM Listeners`工具会帮我们监测 `view` 页面上`DOM`元素的变化**，如果有变化，则更改`Model`中的数据； 

> `Model`

从`Model`侧看，当我们更新`Model`中的数据时，**`Data Bindings`工具会帮我们更新页面中的`DOM`元素。**

> `MVVM`

`MVVM`是`Model-View-ViewModel`的缩写。

`MVVM`是一种设计思想。`Model `层代表数据模型，也可以在`Model`中定义数据修改和操作的业务逻辑；`View `代表`UI 组件`，它负责将数据模型转化成`UI `展现出来，`ViewModel `是一个同步`View `和 `Model`的对象。

在`MVVM`架构下，`View `和 `Model `之间并没有直接的联系，而是通过`ViewModel`进行交互，`Model `和 `View ` 与 `ViewModel`之间的交互都是双向的， 因此`View `数据的变化会同步到`Model`中，而`Model `数据的变化也会立即反应到`View `上。

`ViewModel `通过双向数据绑定把 `View `层和 `Model `层连接起来，而`View `和 `Model `之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作`DOM`, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 `MVVM `来统一管理。

> `mvc `和 `mvvm`

`mvc`和`mvvm`其实区别并不大，都是一种设计思想。

主要就是`mvc`中`Controller`演变成`mvvm`中的`viewModel`。`mvvm`主要解决了`mvc`中大量的`DOM `操作使页面渲染性能降低，加载速度变慢，影响用户体验。

---

### 7. 单文件组件

嗷呜, 前提是支持构建工具的项目中, 别问我为什么要强调这个, 必不可能是因为我犯过错, 嗷呜

> **在大多数支持构建vue工具的 `Vue `项目中**，我们使用类似于 `HTML `的文件格式创建 `Vue `组件，称为单文件组件（也称为`*.vue`文件，缩写为`SFC`）。

顾名思义，`Vue SFC` 将组件的逻辑 (`JavaScript`)、模板 (`HTML`) 和样式 (`CSS`) 封装在一个文件中。

```html
<script>
export default {
  data() {
    return {
      // 键值对的形式保存数据
    }
  }
}
</script>

<template>
  <p>类似于 html 的标签语法展示组件内容</p>
</template>

<style scoped>
/* 样式的设计 */
</style>
```

---

### 8. 单页面

> 多页面
>
> 即服务端渲染

多页面跳转刷新所有资源，每个公共资源`(js、css等)`需选择性重新加载

页面跳转是所有的资源都要重新加载，页面之间的切换会出现卡顿空白的问题，不容易实现切换动画等。这种类型的网站也就是多页网站，也叫做多页应用

> 单页面
>
> 可以做到前后端分离

一个项目中只有一个完整的`html`主页面，其他都是`html`片段组成的分页面，浏览器一开始会在主页面加载所有必须的 `html, js, css`。

当用户向服务器发送请求的时候, 只需要访问一次就可以, 服务器返回一个`web`页面, 当页面跳转的时候只需要做到局部刷新, 由路由程序将分页面动态载入主页面，跳转只是局部刷新，不会重新加载全部资源。

原理：在`js`会感知到`url`的变化后动态地将当前页面的内容清除，然后将下一个页面的内容挂载到当前页面上。这个时候的路由不再是后端来做了，而是前端来做，判断页面显示相应的组件，清除不需要的。

### 9. API 风格

> `选项式 API`

使用`选项式 API`，我们可以用包含多个选项的对象来描述组件的逻辑，例如 `data`、`methods` 和 `mounted`。

选项所定义的属性都会暴露在函数内部的 `this` 上，它会指向当前的组件实例。

实际上，`选项式 API `也是用`组合式 API` 实现的

```js
<script>
export default {
  // data() 返回的属性将会成为响应式的状态
  // 并且暴露在 `this` 上
  data() {
    return {
      count: 0
    }
  },

  // methods 是一些用来更改状态与触发更新的函数
  // 它们可以在模板中作为事件监听器绑定
  methods: {
    increment() {
      this.count++
    }
  },

  // 生命周期钩子会在组件生命周期的各个不同阶段被调用
  // 例如这个函数就会在组件挂载完成后被调用
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>
```

> `组合式 API`

通过`组合式 API`，我们可以使用导入的 `API 函数`来描述组件逻辑。

在单文件组件中，`组合式 API` 通常会与 `<script setup>` 搭配使用

告诉 `Vue `需要在编译时进行转换，来减少使用`组合式 API `时的样板代码。

`vue3` 向下兼容了 `vue2` 的语法, 在简单的业务中任然可以使用 `vue2 `的 `选项式 API`

这种形式更加自由，也需要你对 `Vue `的响应式系统有更深的理解才能高效使用。相应的，它的灵活性也使得组织和重用逻辑的模式变得更加强大。

```html
<!-- setup 是进一步的简化 -->
<script setup>
import { ref, onMounted } from 'vue'

// 响应式状态
const count = ref(0)

// 用来修改状态、触发更新的函数
function increment() {
  count.value++
}

// 生命周期钩子
onMounted(() => {
  // 响应式的数据需要通过 .value 的方式获取他的值
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

### 10. 与jQuery的对比

在开始学习`Vue.js`之前我们先回顾下过去是如何开发前端页面的

在过去开发前端页面我们经常会选择使用`jQuery`库，使用`jQuery`库开发的好处是屏蔽了不同浏览器操作`DOM`的兼容性问题，相对于使用原生`JavaScript`开发，`jQuery`实现相同的功能使用的代码更少，`jQuery`的开发原则就是写更少的代码完成更多的功能。

使用`jQuery`仅仅是减少了操作`DOM`的代码，实际在开发项目的过程中你需要考虑你的业务如何实现同时又要考虑如果操作`DOM`。

随着这几年前端的快速发展，前端页面中需要实现的功能越来越复杂，`jQuery`已经不能满足时代的需求。

这个时候应运而生了很多前端开发框架，例如：`Vue、React、Angular`前端大三框架。

使用这些框架开发前端页面我们不需要再手动操作`DOM`，它们已经把`DOM`操作封装起来了，我们只需要考虑项目中的业务功能如何实现即可。

相比于其他库，`Vue.js` 提供了更加简洁、更易于理解的 `API`，使得我们能够快速上手。

也就是使用`Vue.js`开发前端项目会比过去的`jQuery`库开发更简单方便，`jQuery`的核心只是简化了`DOM`操作，使用`Vue.js`开发我们不需要操作`DOM`

### 11. vue 核心思想

`Vue.js` 是为了克服 `HTML` 在构建应用上的不足而设计的。`Vue.js` 有着诸多特性，最为核心的是数据驱动和组件化

> 数据驱动

- `DOM `是数据的一种自然映射
- 数据改变自动驱动视图更新(响应式数据)

> 组件化

- 扩展 `HTML `元素，封装可重用代码

## 2. Vue 的应用方式

> 根据你的使用场景和个人偏好，在使用 `Vue `时，你可以选择是否采用构建流程(`vite` 或者是 `webpack`)。
>
> 使用构建工具的时候, 我们才可以使用 `SFC` 
>
> 推荐： 我们首先要安装好` Node.js`环境，然后再来做下面的操作。
>
> 可以使用 `nvm `也可以直接使用 `node`, 新手学习可以使用 `node`, 开发中可以替换 `nvm` 环境

---

### 1. 不使用构建工具

> 可以直接引入线上的`Vue.js`

```vue
<script src="https://unpkg.com/vue@next"></script>
```

> 可以把`vue.js`下载到本地，然后引入本地的`vue.js`

```html
<script src="./vue.js"></script>
```

---

### 2. 利用 vue-cli

`Vue `提供一个命令行工具，可用于快速搭建大型单页应用。

只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目。

需要有 `node` 的环境, 利用 `npm `或 `yarn` 进行安装

关于 `yarn `和 `npm `的命令可以网上去参考

```bash
# 全局安装, 可以在任何位置安装脚手架
$ npm install -g @vue/cli
# h或者
$ yarn add global @vue/cli
```

```bash
# vue3 创建项目的写法 
$ vue create project
```

> 依赖的选项 

```bash
? Please pick a preset: 
❯ Default ([Vue 2] babel, eslint) 
  Default (Vue 3 Preview) ([Vue 3] babel, eslint) 
  Manually select features 
```

1. 使用 `vue2 `（默认版本） ， `babel`（为了打包后使`es6`语法降级兼容低版本浏览器），`eslint`（语法规范）
2. 同上， 但是版本选择 `vue3`
3. 自定义选择添加的依赖

> 空格是选中， 回车是确定


选择完成以后， 会自动搭建项目， 这里我们稍等一会

```bash
# 进入项目目录
$ cd project
# 运行项目
$ npm run serve
```

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16-20220325094418699%20%E4%B8%8B%E5%8D%884.18.55.png)

---

### 3. 使用 vite

`Vite`这是一个现代、轻量级且速度极快的前端构建工具。

这一指令将会安装并执行` create-vue`，它是 Vue 官方的项目脚手架工具。

```bash
$ npm install -g @vue/cli
$ npm init vue@latest
# 或者使用 yarn
$ yarn global add @vue/cli
$ yarn create vite
```

选择配置

```bash
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

然后进入项目， 运行项目

```bash
$ cd <your-project-name>
$ npm install
$ npm run dev
# 或者 yarn
$ cd <your-project-name>
$ yarn
$ yarn dev
```

![image-20220325103159428](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220325103159428%20%E4%B8%8B%E5%8D%884.18.55.png)

---

### 4. 实例的解释

每个 `Vue `应用都是通过 [`createApp`](https://staging-cn.vuejs.org/api/application.html#createapp) 函数创建一个新的 应用实例

我们可以在原来的没有使用 `vue` 框架的项目中局部使用 `vue`, 通过绑定某一个具体的元素

```js
// 从 vue 中导入 creatApp 这个方法
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})
```

---

###  5. 根组件

我们传入的对象`createApp`实际上是一个组件。

每个应用程序都需要一个根组件，它可以包含其他组件作为其子组件。

```js
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})
```

如果您使用的是单文件组件，我们通常会从另一个文件中导入根组件

在使用脚手架 ( 构建工具 ) 的时候常用

```js
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)
```

应用根组件的内容将会被渲染在容器元素里面。

需要注意的是容器元素自己将不会被视为应用的一部分。

---

### 6. 挂载

`.mount()`在调用其方法之前，应用程序实例不会呈现任何内容。

它需要一个“容器”参数，它可以是实际的 `DOM `元素或选择器字符串

```html
<div id="app"></div>
```

```js
const app = createApp(App)
app.mount('#app')
```

在完成应用程序注册后，应调用该`.mount()`方法。

同时请注意，不同于其他资源注册方法，它的返回值是根组件实例

当在未采用构建流程的情况下使用 `Vue `时，我们可以在挂载容器中直接书写根组件模板

```html
<div id="app">
  <button @click="count++">{{ count }}</button>
</div>
```

```js
import { createApp } from 'vue'

const app = createApp({
  data() {
    return {
      count: 0
    }
  }
})

app.mount('#app')
```

当根组件没有设置 `template` 选项时，`Vue `将自动使用容器的 `innerHTML` 作为模板。

---

### 7. 应用程序配置

应用程序实例公开了一个`.config`对象，允许我们配置一些应用程序级选项

```js
app.config.errorHandler = (err) => {
  /* 处理错误 */
}
```

---

### 8. 多个应用实例

`createApp` `API `允许多个 `Vue `应用共存于同一个页面上，而且每个应用都拥有自己的用于配置和全局资源的作用域。

我们可以把渐进式理解为, 在原有的基础上, 使用 `vue` 框架补充页面

```js
const app1 = createApp({
  /* ... */
})
app1.mount('#container-1')

const app2 = createApp({
  /* ... */
})
app2.mount('#container-2')
```

## 3. 响应式

### 1. reactive

`reactive()` 仅适用于对象（包括数组和内置类型，如 `Map `和 `Set`）。

我们可以使用 [`reactive()`](https://staging-cn.vuejs.org/api/reactivity-core.html#reactive) 函数创建一个响应式对象或数组

```js
import { reactive } from 'vue'

const state = reactive({ count: 0 })
```

要在组件模板中使用响应式状态，需要在 `setup()` 函数中定义并返回。

```js
import { reactive } from 'vue'

export default {
  setup() {
    const state = reactive({ count: 0 })

    function increment() {
      state.count++
    }
      
    // 一定更要返回
    return {
      state,
      increment
    }
  }
}
```

在 `setup()` 函数中手动暴露状态和方法可能非常繁琐。

也可以通过使用构建工具来简化该操作。

当使用单文件组件（`SFC`）时，我们可以使用 `<script setup>` 来简化大量样板代码。

```html
<script setup>
import { reactive } from 'vue'

const state = reactive({ count: 0 })

function increment() {
  state.count++
}
</script>

<template>
  <button @click="increment">
    {{ state.count }}
  </button>
</template>
```

`<script setup>`  中的顶层的导入和变量声明可在同一组件的模板中自动使用, 不需要 `return `返回

### 2. DOM 更新时机

当你更改响应式数据后，`DOM `也会自动更新

对 `Vue `组件数据的更改不会立即反映在 `DOM `中。相反，`Vue `异步更新 `DOM`。

```html
<template>
  <div>
    <button @click="handleClick">Insert/Remove</button>
    <div v-if="show" ref="content">I am an element</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      show: true,
    };
  },
  methods: {
    handleClick() {
      this.show = !this.show;
      console.log(this.show, this.$refs.content);
    },
  },
};
</script>

<!-- 
点击的时候会有这么两组结果, 

false <div> I am an element </div>

true null
-->
```

我们可以发现, 在 `v-if='true'`的时候, 并没有存在当前的 `DOM `

若要等待一个状态改变后的 `DOM `更新完成，你可以使用 `nextTick` 这个全局 `API`

Vue 允许`this.$nextTick(callback)`在组件实例上使用权限。`callback`在新数据更新到达 `DOM `后立即执行。

```html
<template>
  <div>
    <button @click="handleClick">Insert/Remove</button>
    <div v-if="show" ref="content">I am an element</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      show: true,
    };
  },
  methods: {
    handleClick() {
      this.show = !this.show;
      this.$nextTick(() => {
        console.log(this.show, this.$refs.content);
      });
    },
  },
};
</script>

<!-- 
点击的时候会有这么两组结果, 

false null
true <div>I am an element</div>
-->
```

在 `this.$nextTick` 函数中我们可以获取到发送改变后的 `DOM`

如果在没有参数的情况下调用 `this.$nextTick()`，则函数返回一个 `promise`，当组件数据更改到达 `DOM `时该 `promise `会被解析。

```js
<template>
  <div>
    <button @click="handleClick">Insert/Remove</button>
    <div v-if="show" ref="content">I am an element</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      show: true,
    };
  },
  methods: {
    async handleClick() {
      this.show = !this.show;
      await this.$nextTick();
      console.log(this.show, this.$refs.content);
    },
  },
};
</script>
```

### 3. 深层响应性

在 `Vue `中，状态都是默认深层响应式的。

这意味着即使在更改深层次的对象或数组，你的改动也能被检测到。

```js
import { reactive } from 'vue'

const obj = reactive({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})

function mutateDeeply() {
  // 以下都会按照期望工作
  obj.nested.count++
  obj.arr.push('baz')
}
```

### 4. 响应式代理

值得注意的是，`reactive()` 返回的是一个原始对象的 `Proxy`，它和原始对象是不相等的

关于 `proxy `是 `es6 `的知识点

```js
const raw = {}
const proxy = reactive(raw)

// 代理和原始对象不是全等的
console.log(proxy === raw) // false
```

只有代理是响应式的，更改原始对象不会触发更新。因此，使用 `Vue `的响应式系统的最佳实践是 仅使用你声明对象的代理版本。

为保证访问代理的一致性，对同一个对象调用 `reactive()` 会总是返回同样的代理，而对一个已存在代理调用 `reactive()` 也是返回同样的代理：

```js
// 在同一个对象上调用 reactive() 会返回相同的代理
console.log(reactive(raw) === proxy) // true

// 在一个代理上调用 reactive() 会返回它自己
console.log(reactive(proxy) === proxy) // true
```

这个规则对嵌套对象也适用。依靠深层响应性，响应式对象内的嵌套对象依然是代理

```js
const proxy = reactive({})

const raw = {}
proxy.nested = raw

console.log(proxy.nested === raw) // false
```

### 5. reactive 局限性

> 1 仅对对象类型有效（对象、数组和 `Map`、`Set` 这样的数据类型有效，而对 `string`、`number` 和 `boolean` 这样的无效。

```js

```

> 2 因为 `Vue `的响应式系统是通过 `property `访问进行追踪的，因此我们必须始终保持对该响应式对象的相同引用。

这意味着我们不可以随意地替换一个响应式对象，因为这将导致对初始引用的响应性连接丢失

```js
let state = reactive({ count: 0 })

// 上面的引用 ({ count: 0 }) 将不再被追踪（响应性连接已丢失！）
state = reactive({ count: 1 })
```

同时这也意味着当我们将响应式对象的 `property `赋值或解构至本地变量时，或是将该 `property `传入一个函数时，我们会失去响应性

```js
const state = reactive({ count: 0 })

// n 是一个局部变量，同 state.count
// 失去响应性连接
let n = state.count
// 不影响原始的 state
n++

// count 也和 state.count 失去了响应性连接
let { count } = state
// 不会影响原始的 state
count++
```

### 6. ref

为了解决 `reactive()` 带来的限制, ` ref() `可以采用任何值类型并创建一个对象，该对象在` .value` 属性下公开内部值

和响应式对象的 `property `类似，ref 的 `.value` `property `也是响应式的。

```js
import { ref } from 'vue'

const message = ref('Hello World!')

console.log(message.value) // "Hello World!"
message.value = 'Changed'
console.log(message.value) // "Changed"
```

在模板中使用时我们不需要再使用 `.value` 的形式, 直接使用该对象就可以

```html
<h1>{{ message }}</h1>
```

`ref `被传递给函数或是从一般对象上被解构时，不会丢失响应性

```js
const obj = {
  foo: ref(1),
  bar: ref(2)
}

// 该函数接收一个 ref
// 需要通过 .value 取值
// 但它会保持响应性
callSomeFunction(obj.foo)

// 仍然是响应式的
const { foo, bar } = obj
```

一言以蔽之，`ref()` 使我们能创造一种任意值的引用并能够不丢失响应性地随意传递。



## 4. vue 系统指令

指令（`Directives`）是 `vue `为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。

`vue `中的指令按照不同的用途可以分为如下 6 大类：

- 内容渲染指令
- 属性绑定指令
- 事件绑定指令
- 双向绑定指令
- 条件渲染指令
- 列表渲染指令

指令是带有`v-`前缀的特殊属性。`Vue `提供了许多内置指令`v-html`

指令的工作是在其表达式的值发生变化时对 `DOM `进行`响应式更新`。

### 1. 模板语法

`Vue `使用一种基于 `HTML `的模板语法，使我们能够声明式地将其组件实例的数据绑定到呈现的 `DOM `上。所有的 `Vue 模板`都是语法上合法的 `HTML`，可以被符合规范的浏览器和 `HTML `解析器解析。

在底层机制中，`Vue `会将模板编译成高度优化的 `JavaScript `代码。结合响应式系统，当应用状态变更时，`Vue `能够智能地推导出需要重新渲染的组件的最少数量，并应用最少的 `DOM `操作。

###  2. {{ }}

数据绑定最常见的形式就是使用 “`Mustache`” 语法（双大括号）的文本插值，在标签中使用。

```html
<span>Message: {{ msg }}</span>
```

`Mustache `标签将会被替代为对应数据对象上 `msg `属性（`msg`定义在`data`对象中）的值

但是需要注意的是, 在页面最初的时候, 页面上显示的内容是 `{{msg}}` `msg` 的内容未来得及被替换

无论何时，绑定的数据对象上 `msg `属性发生了改变，插值处的内容都会自动更新。

`{{  }}`对JavaScript 表达式支持，例如：

```javascript
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ name == 'x' ? 'true' : 'false' }}

{{ message.split('').reverse().join('') }}
```


但是有个限制就是，每个绑定都只能包含单个表达式，如下表达式无效：

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (true) { return message } }}
```

---

### 3. v-cloak

`v-cloak`会保持和元素实例的关联，直到结束编译后自动消失。

`v-cloak`指令和`CSS `规则一起用的时候，能够解决差值表达式闪烁的问题（即：可以隐藏未编译的标签直到实例准备完毕）。

在网速很慢的情况下，一开始会直接显示`{{name}}`这个内容 ，等网络加载完成了，才会显示`name` 属性的值。

原理: 先通过样式隐藏内容, 然后在内存中进行值的替换, 替换好之后再显示最后的结果

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

###  4. v-text

`v-text`可以将一个变量的值渲染到指定的元素中。

与插值表达式的区别: 插值表达式只会替换自己的这个占位符，并不会把整个元素的内容清空。`v-text` 会覆盖元素中原本的内容。

没有闪动问题

- `v-text`指令用于将数据填充到标签中，作用于插值表达式类似，但是没有闪动问题
- 如果数据中有`HTML`标签会将`html`标签一并输出
- 注意：此处为单向绑定，数据对象上的值改变，插值会发生变化；但是当插值发生变化并不会影响数据对象的值

```html
<div id="app">
    <!--  
		注意:在指令中不要写插值语法  直接写对应的变量名称 
         在 v-text 中 赋值的时候不要在写 插值语法
		一般属性中不加 {{}}  直接写 对应 的数据名 
	-->
    <p v-text="msg"></p>
    <p>
        <!-- Vue  中只有在标签的 内容中 才用插值语法 -->
        {{msg}}
    </p>
</div>

<script>
    new Vue({
        el: '#app',
        data: {
            msg: 'Hello Vue.js'
        }
    });

</script>
```

---

### 5. v-html

`v-text`是纯文本，而`v-html`会被解析成`html`元素。

注意：使用`v-html`渲染数据可能会非常危险，因为它很容易导致 `XSS`（跨站脚本） 攻击，使用的时候请谨慎，能够使用`{{}}`或者v-text实现的不要使用`v-html`。

`v-text`和`v-html`专门用来展示数据, 其作用和插值表达式类似。`v-text`和`v-html`可以避免插值闪烁问题.

当网速比较慢时, 使用 `{{ }} `来展示数据, 有可能会产生插值闪烁问题。

```js
<div id="app">
　　<p v-html="html"></p> <!-- 输出：html标签在渲染的时候被解析 -->
    
    <p>{{message}}</p> <!-- 输出：<span>通过双括号绑定</span> -->
    
　　<p v-text="text"></p> <!-- 输出：<span>html标签在渲染的时候被源码输出</span> -->
</div>
<script>
　　let app = new Vue({
　　el: "#app",
　　data: {
　　　　message: "<span>通过双括号绑定</span>",
　　　　html: "<span>html标签在渲染的时候被解析</span>",
　　　　text: "<span>html标签在渲染的时候被源码输出</span>",
　　}
 });
</script>
```

---

###  6. v-pre

- 显示原始信息跳过编译过程
- 跳过这个元素和它的子元素的编译过程。
- 一些静态的内容不需要编译加这个指令可以加快渲染

```html
    <span v-pre>{{ this will not be compiled }}</span>    
	<!--  显示的是{{ this will not be compiled }}  -->
	<span v-pre>{{msg}}</span>  
     <!--   即使data里面定义了msg这里仍然是显示的 {{msg}}  -->
<script>
    new Vue({
        el: '#app',
        data: {
            msg: 'Hello Vue.js'
        }
    });

</script>
```

### 7. v-once

- 执行一次性的插值【当数据改变时，插值处的内容不会继续更新】
- 可以提高性能

```html
  <!-- 即使data里面定义了msg 后期我们修改了 仍然显示的是第一次data里面存储的数据即 Hello Vue.js  -->
     <span v-once>{{ msg}}</span>    
<script>
    new Vue({
        el: '#app',
        data: {
            msg: 'Hello Vue.js'
        }
    });
</script>
```

---

### 8. v-on

![指令语法图](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/directive.69c37117%20%E4%B8%8B%E5%8D%884.18.55.png)

> 你可以使用 `v-on` 指令 (简写为 `@`) 来监听 `DOM `事件和运行 `JavaScript `代码。

```html
<button v-on:click="num++">{{ num }}</button>
```

可以简写成：

```html
<button @click="num++">{{ num }}</button>
```

> 方法事件处理器会自动接收原生 `DOM `事件并触发执行, 事件对象的名称必须是` $event `

```vue
<script setup>
const name = ref('Vue.js')

function greet(event) {
  alert(`Hello ${name.value}!`)
  // `event` 是 DOM 原生事件
  if (event) {
    alert(event.target.tagName)
  }
}
</script>

<template>
	<!-- `greet` 是上面定义过的方法名 -->
	<button @click="greet">Greet</button>
</template>
```

`$event` 是 `vue `提供的特殊变量，用来表示原生的事件参数对象`event`。`$event` 可以解决事件参数对象`event`被覆盖的问题。

> `v-on` 提供了一些事件


- `v-on:click`

- `v-on:keydown`

- `v-on:keyup`

- `v-on:mousedown`

- `v-on:mouseover`

- `v-on:submit`

> `v-on`的常见事件修饰符

在处理事件时调用 `event.preventDefault()` 或 `event.stopPropagation()` 是很常见的。

`Vue `不推荐我们操作`DOM    `, 为了解决这个问题，`Vue.js` 为 `v-on` 提供了事件修饰符

- `.stop`  阻止冒泡。本质是调用 `event.stopPropagation()`。阻止点击事件冒泡。等同于`JavaScript`中的`event.stopPropagation()`. 使用了.`stop`后，点击子节点不会捕获到父节点的事件

```vue
<!-- 单击事件将停止传递 -->
<a @click.stop="doThis"></a>
```


- `.prevent`  阻止默认事件（默认行为）。本质是调用 `event.preventDefault()`。

```vue
<!-- 提交事件将不再重新加载页面 -->
<form @submit.prevent="onSubmit"></form>

<!-- 修饰语可以使用链式书写 -->
<a @click.stop.prevent="doThat"></a>

<!-- 也可以只有修饰符 -->
<form @submit.prevent></form>
```


- `.capture`  添加事件监听器时，使用捕获的方式（也就是说，事件采用捕获的方式，而不是采用冒泡的方式）。

```vue
<!-- 添加事件监听器时，使用 `capture` 捕获模式 -->
<!-- 例如：指向内部元素的事件，在被内部元素处理前，先被外部处理 -->
<div @click.capture="doThis">...</div>
```


- `.self`  只有当事件在该元素本身（比如不是子元素）触发时，才会触发回调。

```vue
<!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
<div @click.self="doThat">...</div>
```


- `.once`  事件只触发一次。

```vue
<!-- 点击事件最多被触发一次 -->
<a @click.once="doThis"></a>
```

- `.passive` 修饰符一般用于触摸事件的监听器

```vue
<!-- 滚动事件的默认行为 (scrolling) 将立即发生而非等待 `onScroll` 完成 -->
<!-- 以防其中包含 `event.preventDefault()` -->
<div @scroll.passive="onScroll">...</div>
```

> 按键修饰符

在监听键盘事件时，我们经常需要检查特定的键。`Vue `允许为`v-on`或`@`在监听键事件时添加键修饰符：

```html
<input @keyup.enter="submit" />
```

您可以直接使用通过`KeyboardEvent.key` 修饰符公开的任何有效键名，但需要转为 `kebab-case` 形式。

```html
<input @keyup.page-down="onPageDown" />
```

`Vue `为最常用的键提供别名：

- `.enter`
- `.tab`
- `.delete`
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`
- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

> `.exact` 修饰符

`.exact` 修饰符允许控制触发一个事件所需的确定组合的系统按键修饰符。

```vue
<!-- 当按下 Ctrl 时，即使同时按下 Alt 或 Shift 也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 仅当按下 Ctrl 且未按任何其他键时才会触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 仅当没有按下任何系统按键时触发 -->
<button @click.exact="onClick">A</button>
```

---

### 9. v-bind

数据绑定的一个常见需求场景是操纵元素的` CSS class` 列表和内联样式。因为它们都是 `attribute`，我们可以使用 `v-bind` 来做这件事

>  他绑定的是属性 要和 `{{ }}` 语法区分开

- 不能在 `HTML属性 ` 中使用 `{{ }}`。 `v-bind`用于绑定属性

- 如果绑定的值是 `null` 或者 `undefined`，那么该 `attribute `将会从渲染的元素上移除。
- 凡是`有-的style属性名`都要变成驼峰式，比如`font-size`要变成`fontSize`
- 值要用引号括起来

```html
<img v-bind:src="imageSrc +'string'">
<div v-bind:style="{ fontSize: size + 'px' }">{{ msg }}</div>
```


上方代码中，给属性加了 `v-bind` 之后，`:`之后的是属性的名字, 属性值里的整体内容是表达式

> 我们可以给 `:class` (`v-bind:class` 的缩写) 传递一个对象来动态切换 `class`：

```vue
<div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>
```

你可以在对象中写多个字段来操作多个 `class`。

此外，`:class` 指令也可以和一般的 `class` `attribute `共存。

> 数组

我们可以给 `:class` 绑定一个数组以应用一系列 `CSS class`

```html
<!-- 直接传递类名 -->   
<h1 :class="['red', 'thin']"></h1>

<h1 :style="[
    {display: (activeName=='first'?'flex':'none')},
    {fontSize: '20px'}
]"></h1>
```

> 三元表达式

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

> 在数组中使用 对象 来代替 三元表达式

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

> 直接使用对象


```html
<!-- 
	 在为 class 使用 v-bind 绑定 对象的时候，对象的属性是类名。
  	 由于 对象的属性名可带引号，也可不带引号，所以 这里我没写引号；  属性的值 是一个标识符 
-->

<!-- { 类名: Boolean } -->
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

每次组件更新时都会调用内部绑定表达式的函数，因此它们没有任何副作用，例如更改数据或触发异步操作。

> 动态参数

同样在指令参数上也可以使用一个 `JavaScript `表达式，需要包含在一对方括号内

```js
<a v-bind:[attributeName]="url"> ... </a>

<!-- 简写 -->
<a :[attributeName]="url"> ... </a>
```

这里的 `attributeName` 会作为一个 `JavaScript `表达式被动态执行，计算得到的值会被用作最终的参数。

动态参数期望结果为一个字符串，或者是 `null`。特殊值 `null` 意为显式移除该绑定。

---

### 10. v-model

在前端处理表单时，我们常常需要将表单输入框的内容同步给 `JavaScript `中相应的变量。

```vue
<input v-model="text">
```

注意插值表达式在 `<textarea>` 中将不会工作。请使用 `v-model` 来替代。

> 表单修饰符

- `.lazy`

默认情况下，`v-model` 会在每次 `input` 事件后更新数据, 你可以添加 `lazy` 修饰符来改为在每次 `change` 事件后更新数据

```html
<input v-model.lazy="msg" />
```

- `.number`

如果您希望用户输入自动转换为数字，您可以将`number`修饰符添加到`v-model`托管输入：

```html
<input v-model.number="age" />
```

如果无法用 解析该值`parseFloat()`，则使用原始值代替。

如果输入有，`number`则自动应用修饰符`type="number"`。

- `.trim`

如果您希望自动修剪用户输入中的空白，您可以将`trim`修饰符添加到您的`v-model`-managed 输入中：

只能去掉首尾的 不能去除中间的空格

```html
<input v-model.trim="msg" />
```

> `v-model` 的实现原理

```html
<input :value="msg" @input="msg = @event.target.value">{{ msg }}</input>
```

---

### 11. v-for

我们可以使用 `v-for` 指令基于一个数组来渲染一个列表。

> 使用注意点

- 不推荐同时使用 `v-if` 和 `v-for`
- 当 `v-if` 与 `v-for` 一起使用时，`v-if` 具有比` v-for `更高的优先级。

> 我们可以使用该`v-for`指令基于数组呈现项目列表。

在 `v-for` 块中可以完整地访问父作用域内的 `property`。`v-for` 也支持使用可选的第二个参数表示当前项的位置索引。

```vue
<li v-for="item in items">
  {{ item.message }}
</li>

data() {
  return {
    items: [{ message: 'mes1' }, { message: 'mes2' }]
  }
}
```

> 您也可以使用`<template>`标签 `v-for`来渲染一个包含多个元素的块

```vue
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

> 你也可以使用 `of` 作为分隔符来替代 `in`，这也和 `JavaScript` 的迭代器语法非常相似

```html
<div v-for="item of items"></div>
```

> 你也可以使用 `v-for` 来遍历一个对象的所有属性 

第一个参数表示属性值

第二个参数表示属性名

第三个参数表示位置索引

```vue
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

> key 管理状态

用 `v-for` 正在更新已渲染过的元素列表时，它默认用就地复用策略。如果数据项的顺序被改变，`Vue`将不是移动 `DOM `元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。

为了给 `Vue `一个提示，以便它可以跟踪每个节点的标识，从而重用和重新排序现有的元素，你需要为每个项目提供一个唯一的 `key`  `attribute`

```vue
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

- `key `的值只能是字符串或数字类型
- `key `的值必须具有唯一性, 建议把数据项 `id `属性的值作为 `key `的值
- 使用 `index `的值当作 `key `的值没有任何意义（因为`index `的值不具有唯一性）
- 建议使用 `v-for` 指令时一定要指定 `key `的值, 既提升性能、又防止列表状态紊乱, 最主要的是， 他不会给你警告， 看的心烦哎

> 组件上使用 `v-for`

可以直接在组件上使用 `v-for`，和其他任何一般的元素没有区别 (别忘记提供一个 `key`)：

```vue
<my-component v-for="item in items" :key="item.id"></my-component>
```

但是，这不会自动将任何数据传递给组件，因为组件有自己独立的作用域。

为了将迭代后的数据传递到组件中，我们还是应该使用 `prop`：



---

### 12. v-if

`v-if` 会根据表达式的值的真假条件，来决定是否渲染元素，如果为`false`则不渲染，如果为`true`则渲染。

在切换时，元素和它的数据绑定会被销毁并重建

因为`v-if`是一个指令，所以它必须附加到单个元素。

我们可以`v-if`在一个`<template>`元素上使用，它作为一个不可见的包装器。最终渲染结果将不包括该`<template>`元素。

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

和 `v-else` 相似，一个使用 `v-else-if` 的元素必须紧跟在一个 `v-if` 或一个 `v-else-if` 元素后面。

```js
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

`v-else`也`v-else-if`可以用在`<template>`.

---

### 13. v-show

`v-show`用于控制元素的显示和隐藏

根据表达式的真假条件，来切换元素的 `display `属性。如果为`false`，则在元素上添加 `display:none`属性；否则移除`display:none`属性。

`v-show`不支持该`<template>`元素


---

### 14. v-if v-show

`v-if`和`v-show`都能够实现对一个元素的隐藏和显示操作。

> 区别

- `v-if`：每次都会重新添加/删除`DOM`元素

- `v-show`：每次不会重新进行`DOM`的添加/删除操作，只是在这个元素上添加/移除`style="display:none"`属性，表示节点的显示和隐藏。

> 优缺点

- `v-if`：有较高的切换性能消耗。这个很好理解，毕竟每次都要进行`dom`的添加／删除操作。

- `v-show`：有较高的初始渲染消耗。也就是说，即使一开始`v-show="false"`，该节点也会被创建，只是隐藏起来了。而`v-if="false"`的节点，根本就不会被创建。

> 总结

- 如果元素涉及到频繁的切换，最好不要使用 `v-if`, 而是推荐使用 `v-show`
- 如果元素可能永远也不会被显示出来被用户看到，则推荐使用` v-if`
- 当 `v-if` 和 `v-for` 同时存在于一个元素上的时候，`v-if` 会首先被执行。

---

###  15. 自定义指令

- 内置指令不能满足我们特殊的需求
- Vue允许我们自定义指令

```html
<div id="app">
    <p>页面载入时，input 元素自动获取焦点：</p>
<!-- 
使用自定义的指令，只需在对用的元素中，加上'v-'的前缀形成类似于内部指令'v-if'，'v-text'的形式。 
-->
    <input v-focus>
</div>
 
<script>
const app = Vue.createApp({})
// 注册一个全局自定义指令 `v-focus`
app.directive('focus', {
  // 当被绑定的元素挂载到 DOM 中时……
  mounted(el) {
    // 聚焦元素
    el.focus()
  }
})
app.mount('#app')
</script>
```

```html
<div id="app">
    <p>页面载入时，input 元素自动获取焦点：</p>
    <input v-focus>
</div>
 
<script>
const app = {
   data() {
      return {
          
      }
   },
   directives: {
      focus: {
         // 指令的定义
         mounted(el) {
            el.focus()
         }
      }
   }
}
</script>
```

```html
<input type="text" v-color='msg'>
 <input type="text" v-focus>
 <script type="text/javascript">
    /*
      自定义指令-局部指令
    */
    var vm = new Vue({
      el: '#app',
      data: {
        msg: {
          color: 'red'
        }
      },
   	  // 局部指令，需要定义在  directives 的选项
      directives: {
        color: {
          // binding 为自定义的函数形参   通过自定义属性传递过来的值 存在 binding.value 里面
          bind: function(el, binding){
            el.style.backgroundColor = binding.value.color;
          }
        },
        focus: {
          inserted: function(el) {
            el.focus();
          }
        }
      }
    });
  </script>
```

指令定义函数提供了几个钩子函数（可选）：

- `created `: 在绑定元素的属性或事件监听器被应用之前调用。
- `beforeMount `: 指令第一次绑定到元素并且在挂载父组件之前调用。。
- `mounted `: 在绑定元素的父组件被挂载后调用。。
- `beforeUpdate`: 在更新包含组件的 VNode 之前调用。。
- `updated`: 在包含组件的 VNode 及其子组件的 VNode 更新后调用。
- `beforeUnmount`: 当指令与在绑定元素父组件卸载之前时，只调用一次。
- `unmounted`: 当指令与元素解除绑定且父组件已卸载时，只调用一次。

钩子函数的参数有：

> `el`

- `el `指令绑定到的元素。这可用于直接操作 `DOM`。

> `binding`

`binding `是一个对象，包含以下属性：

- `instance`：使用指令的组件实例。
- `value`：传递给指令的值。例如，在 `v-my-directive="1 + 1"` 中，该值为 `2`。
- `oldValue`：先前的值，仅在 `beforeUpdate` 和 `updated` 中可用。值是否已更改都可用。
- `arg`：参数传递给指令 (如果有)。例如在 `v-my-directive:foo` 中，arg 为 `"foo"`。
- `modifiers`：包含修饰符 (如果有) 的对象。例如在 `v-my-directive.foo.bar` 中，修饰符对象为 `{foo: true，bar: true}`。
- `dir`：一个对象，在注册指令时作为参数传递



## 5. vue options

### 1. data

我们使用`data`选项来声明组件的反应状态。选项值应该是一个返回对象的函数。`Vue `会在创建新组件实例时调用该函数，并将返回的对象包装在其响应系统中。此对象的任何顶级属性都代理在组件实例上（`this`在方法和生命周期挂钩中）：

```js
data() {
    return {
      
    }
  }
```

这些实例属性仅在首次创建实例时添加，因此您需要确保它们都存在于函数返回的对象中`data`。如有必要，使用`null`或`undefined`其他一些占位符值来表示所需值尚不可用的属性。

在 `vue3` 中, 我们使用 `ref` 来替换掉 `data `的使用

```js
export default {
  setup() {
    let num = ref(2)
    let add = () => {
      // 使用时需要用 .value 的形式
      num.value ++
    }
    // 如果不返回的话, 在模板中是无法使用的
    return {
      num,
      add
    }
  }
}
</script>
```

### 2. methods

Vue 自动绑定`this`值，`methods`以便它始终引用组件实例。这可确保方法在`this`用作事件侦听器或回调时保留正确的值。定义 时应避免使用箭头函数`methods`，因为这会阻止 Vue 绑定适当的`this`值：

```js
export default {
  methods: {
    increment: () => {
      
    }
  }
}
```

在 `vue3` 中, 我们在 `setup` 中写

```js
export default {
  setup() {
    let num = ref(2)
    let add = () => {
      // 使用时需要用 .value 的形式
      num.value ++
    }
    // 如果不返回的话, 在模板中是无法使用的
    return {
      num,
      add
    }
  }
}
</script>
```

---

### 3. computed

模板中的表达式虽然方便，但也只能用来做简单的操作。如果在模板中写太多逻辑，会让使其变得臃肿，难以维护。

计算属性就是一个提前定义好的方法, 该方法可以看作是一个特殊的值, 可以在插值表达式中使用.

> `computed` 比较适合对多个变量或者对象进行处理后返回一个结果值，也就是数多个变量中的某一个值发生了变化则我们监控的这个值也就会发生变化

`computed()` 方法期望接收一个 `getter `函数，返回值为一个`计算属性 ref`。

```vue
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  age: 20,
  firstName: '',
  lastName: ''
})

// 一个计算属性 ref
const fullName = computed(() => {
    return author.firstName + author.lastName
})

</script>

<template>
  <span>{{ fullName }}</span>
</template>
```

> 缓存特性

而且它可以将计算结果缓存起来的属性, 将行为转化成了静态的属性, 计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销

这意味着只要 `author.firstName` 或者  `author.lastName` 不改变，无论多少次访问 `fullName` 都会立即返回先前的计算结果，而不用重复执行 `getter `函数。

> 每个计算属性都包含有一个 `getter `和 `setter`, 当没有明确指明使用方法时, 默认采取的是 `getter `方法

```vue
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('123')
const lastName = ref('456')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // 注意：我们这里使用的是解构赋值语法
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
</script>
```

现在当你再运行 `fullName.value = '1 2'` 时，`setter `会被调用而 `firstName` 和 `lastName` 会随之更新。

> 不要在计算函数中做`异步请求`或者更改 `DOM`

---

### 4. watch

在`组合式 API` 中，我们可以使用`watch`在每次响应式状态发生变化时触发回调函数

> `watch`类似于`onchange`事件,可以在属性值修改的时候,执行某些操作.

```vue
<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')

// 可以直接侦听一个 ref
watch(question, async (newQuestion, oldQuestion) => {
  if (newQuestion.indexOf('?') > -1) {
    answer.value = 'Thinking...'
    try {
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).answer
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error
    }
  }
})
</script>

<template>
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</template>
```

> `watch` 的第一个参数可以是不同形式的
>
> 它可以是一个 `ref `(包括计算属性)、一个响应式对象、一个 `getter` 函数、或多个来源组成的数组

```js
const x = ref(0)
const y = ref(0)

// 单个 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

// getter 函数
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// 多个来源组成的数组
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})
```

> 直接给 `watch()` 传入一个响应式对象，会隐式地创建一个深层侦听器
>
> 该回调函数在所有嵌套的变更时都会被触发

```js
const obj = reactive({ count: 0 })

watch(obj, (newValue, oldValue) => {
  // 在嵌套的 property 变更时触发
  // 注意：`newValue` 此处和 `oldValue` 是相等的
  // 因为它们是同一个对象！
})

obj.count++
```

这不同于返回响应式对象的 `getter `函数：只有在 `getter `函数返回不同的对象时，才会触发回调

```js
watch(
  () => state.someObject,
  () => {
    // 仅当 state.someObject 被替换时触发
  }
)
```

然而，在上面的例子里，你可以显式地加上 `deep` 选项，强制转成深层侦听器：

```js
watch(
  () => state.someObject,
  (newValue, oldValue) => {
    // 注意：`newValue` 此处和 `oldValue` 是相等的
  },
  { deep: true }
)
```

深度侦听需要遍历被侦听对象中的所有嵌套的 property，当用于大型数据结构时，开销很大。因此请只在必要时才使用它，并且要留意性能。

> 常见场景

```js
// 情况一：监视 ref 定义的响应式数据
watch(sum, (newValue, oldValue) => {
	console.log('sum变化了', newValue, oldValue)
}, {immediate:true})

// 情况二：监视多个 ref 定义的响应式数据
watch([sum, msg], (newValue,oldValue) => {
	console.log('sum或msg变化了', newValue,oldValue)
}) 

// 情况三：监视 reactive 定义的响应式数据
// 若 watch 监视的是 reactive 定义的响应式数据，则无法正确获得 oldValue , 而且强制开启了深度监视
watch(person, (newValue, oldValue) => {
	console.log('person变化了', newValue, oldValue)
}, { immediate:true, deep:false }) // 此处的deep配置不再奏效

// 情况四：监视 reactive 定义的响应式数据中的某个属性
watch(() => person.job, (newValue, oldValue) => {
	console.log('person的job变化了', newValue, oldValue)
}, { immediate:true, deep:true }) 

// 情况五：监视reactive定义的响应式数据中的某些属性
watch([() => person.job, () => person.name], (newValue, oldValue) => {
	console.log('person的job变化了', newValue, oldValue)
}, { immediate:true, deep:true })

// 特殊情况：此处由于监视的是reactive定义的对象中的某个属性，所以deep配置有效
watch(() => person.job, (newValue, oldValue) => {
    console.log('person的job变化了', newValue, oldValue)
}, { deep:true })
```

### 5. watchEffect

和`watch`的区别是，`watch`既要指明监视的属性，也要指明监视的回调。

而`watchEffect`，不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性，不用写返回值。

`watch()` 是懒执行的：仅在侦听源变化时，才会执行回调。`watchEffect` 在创建侦听器时，立即执行一遍回调。

```js
// 回调中用到的数据只要发生变化，则直接重新执行回调
watchEffect(() => {
    const x1 = sum.value
    const x2 = person.age
    console.log('watchEffect配置的回调执行了')
})
```

> `watchEffect()` 会立即执行一遍回调函数
>
> 如果这时函数产生了副作用，`Vue `会自动追踪副作用的依赖关系，自动分析出响应源。

```js
const url = ref('https://...')
const data = ref(null)

async function fetchData() {
  const response = await fetch(url.value)
  data.value = await response.json()
}

// 立即获取
fetchData()
// ...再侦听 url 变化
watch(url, fetchData)

// 也可以这样子

watchEffect(async () => {
  const response = await fetch(url.value)
  data.value = await response.json()
})
```

> 回调的刷新时机

默认情况下，用户创建的侦听器回调，都会在 `Vue `**组件更新****之前**被调用。这意味着你在侦听器回调中访问的 `DOM` 将是被 `Vue `更新之前的状态。

如果想在侦听器回调中能访问被 `Vue `更新之后的`DOM`，你需要指明 `flush: 'post'` 选项

```js
watch(source, callback, {
  flush: 'post'
})

watchEffect(callback, {
  flush: 'post'
})
```

后置刷新的 `watchEffect()` 有个更方便的别名 `watchPostEffect()`：

```js
import { watchPostEffect } from 'vue'

watchPostEffect(() => {
  /* 在 Vue 更新后执行 */
})
```

---

## 6. Vue.js 生命周期

每个 `Vue `组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM 以及数据改变时更新 `DOM`。

### 1. vue2 生命周期

> 创建期间生命周期函数

- `beforeCreate`：实例刚在内存中被创建出来，此时，还没有初始化好 `data `和 `methods` 属性

- `created`：实例已经在内存中创建OK，此时 `data `和 `methods `已经创建，此时还没有开始 编译模板。我们可以在这里进行`Ajax`请求。

- `beforeMount`：此时已经完成了模板的编译，但是还没有挂载到页面中

- `mounted`：此时，已经将编译好的模板，挂载到了页面指定的容器中显示。（`mounted`之后，表示真实DOM渲染完了，可以操作`DOM`了）

> 运行期间生命周期函数

- `beforeUpdate`：状态更新之前执行此函数， 此时 `data `中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染`DOM`节点

- `updated`：实例更新完毕之后调用此函数，此时 `data `中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了。

数据发生变化时，会触发这两个方法。不过，我们一般用`watch`来做。

> 销毁期间生命周期函数

- `beforeDestroy`：实例销毁之前调用。在这一步，实例仍然完全可用。

- `destroyed：Vue `实例销毁后调用。调用后，`Vue `实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

可以在`beforeDestroy`里清除定时器、或清除事件绑定。

> 第一次页面加载时会触发 `beforeCreate, created, beforeMount, mounted` 这几个钩子

`DOM `渲染在 `mounted `中就已经完成了。

生命周期钩子的一些使用方法：

- `beforecreate `: 可以在此阶段加`loading`事件，在加载实例时触发；
- `created` : 初始化完成时的事件写在这里，如在这结束`loading`事件，异步请求也适宜在这里调用；
- `mounted` : 挂载元素，获取到`DOM`节点；
- `updated `: 如果对数据统一处理，在这里写上相应函数；
- `beforeDestroy `: 可以做一个确认停止事件的确认框；

> 图解

![](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/480a7cdefd3a9a2a01a4289c8d3d038e%20%E4%B8%8B%E5%8D%884.18.55.png)

### 2. vue3 生命周期

> 注册周期钩子

```vue
<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  console.log(`the component is now mounted.`)
})
</script>
```

> 生命周期

![img](https://staging-cn.vuejs.org/assets/lifecycle.16e4c08e.png)



## 6. Vue 动画

Vue 提供了两个内置组件，可以帮助处理过渡和动画以响应不断变化的状态：

- `<transition>`用于在元素或组件进入和离开 `DOM `时应用动画。

- `<transitionGroup>`用于在将元素或组件插入列表、从中删除或在`v-for`列表中移动时应用动画。

### 6.1 Transition

`<transition>`是一个内置组件：这意味着它可以在任何组件的模板中使用，而无需注册它。它可用于在通过其默认插槽传递给它的元素或组件上应用进入和离开动画。进入或离开可以由以下之一触发：

- 通过条件渲染`v-if`
- 通过条件显示`v-show`
- `<component>` 通过特殊元素切换动态组件

> `<transition>` 仅支持单个元素或组件作为其插槽内容。**如果内容是一个组件，则该组件也必须只有一个根元素。**

### 6.2 动画状态


| .                | 状态                                                         |
| ---------------- | ------------------------------------------------------------ |
| `v-enter-from`   | 进入的起始状态。在元素插入之前添加，在元素插入后立马（一帧）移除。 |
| `v-enter-active` | 进入的活动状态。在整个进入阶段应用。在插入元素之前添加，在过渡/动画完成时移除。此类可用于定义进入过渡的持续时间、延迟和缓动曲线。 |
| `v-enter-to`     | 进入的结束状态。在元素插入后添加一帧（同时`v-enter-from`被移除），在过渡/动画完成时移除。 |
| `v-leave-from`   | 离开的开始状态。触发离开过渡时立即添加，一帧后删除。         |
| `v-leave-active` | 离开的活动状态。在整个离开阶段应用。在触发离开过渡时立即添加，在过渡/动画完成时删除。此类可用于定义离开过渡的持续时间、延迟和缓动曲线。 |
| `v-leave-to`     | 休假的结束状态。在触发离开过渡后添加一帧（同时`v-leave-from`删除），在过渡/动画完成时删除。 |

```html
<template>
  <transition>
    <template v-if="show">
      <div class="btn">123</div>
    </template>
  </transition>
  <button @click="show = !show">button</button>
</template>

<script setup>
import {ref} from 'vue'
let show = ref(false)
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}

.v-enter-from, .v-leave-to {
  opacity: 0;
}

.v-enter-active, .v-leave-active {
  transition: 2s linear;
}

.v-enter-to, .v-leave-from {
  opacity: 1;
}
</style>
```

> v-move 



### 6.3 transition 命名

```html
<transition name="fade">

</transition>
```

对于命名转换，其转换类将以其名称而不是 `v` . 例如，上述转换的应用类将`fade-enter-active`代替`v-enter-active` 淡入淡出过渡的 `CSS `应如下所示：

```scss
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```

### 6.4 keyframes

```js
<template>
  <transition name="show">
    <template v-if="show">
      <div class="btn">123</div>
    </template>
  </transition>
  <button @click="show = !show">button</button>
</template>

<script setup>
import {ref} from 'vue'

let show = ref(false)
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}
.show-enter-active  {
  animation: fade 2s ease;
}
.show-leave-active {
  animation: fade 2s ease reverse;
}
@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>

```

### 6.5 appear

> 使得页面一开始就加载动画, 很有用

```js
<template>
  <transition
      appear
      enter-active-class="animate__animated animate__bounce"
  >
    <div class="btn">123</div>
  </transition>
</template>

<script setup>
import 'animate.css';
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}
</style>
```

### 6.6 动画钩子函数

> `beforeEnter ` `enter ` `afterEnter`  `beforeLeave  ` `leave` `fterLeave`

```html
<template>
  <transition appear @before-enter="beforeEnter" @enter="enter" @leave="leave"
  >
    <template v-if="show">
      <div class="btn">123</div>
    </template>
  </transition>
  <button @click="show = !show">btn</button>
</template>

<script setup>
import {ref} from 'vue'
import gsap from 'gsap'
let show = ref(false);
const beforeEnter = (el) => {
  console.log('beforeEnter')
  gsap.set(el, {
    opacity: 0,
    y: 100
  })
};
const enter = (el, done) => {
  console.log('enter')
  gsap.to(el, {
    opacity: 1,
    y: 0,
    duration: 0.5,
    onComplete: done
  })
};
const leave = (el, done) => {
  console.log('leave')
  gsap.to(el, {
    opacity: 0,
    y: 100,
    duration: 0.5,
    onComplete: done
  })
}
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}
</style>

```

### 6.7 transitionGroup

 



### @补充

> 一个很无聊的补充, 可以自定义类名, 貌似对我好像没什么用

```js
<template>
  <transition leave-active-class="ximingx-leave" enter-active-class="ximingx-enter">
    <template v-if="show">
      <div class="btn">123</div>
    </template>
  </transition>
  <button @click="show = !show">button</button>
</template>

<script setup>
import {ref} from 'vue'

let show = ref(false)
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}
.ximingx-enter  {
  animation: fade 2s ease;
}
.ximingx-leave {
  animation: fade 2s ease reverse;
}
@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
```







## 7. Components

组件的出现，就是为了拆分 `Vue `实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可。

在 `vue `项目中， 我们将 `ui `作为单独的一部分，嵌套应用程序 ， 每一个组件负责自己的页面内容， 最重要的是， 减少了造轮子

- 组件 (`Component`) 是 `Vue.js` 最强大的功能之一
- 组件可以扩展 `HTML `元素，封装可重用的代码

![image-20220325201424552](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220325201424552.png)

---

### 1. 模块化和组件化的区别

- 模块化：是从`代码逻辑`的角度进行划分的；方便代码分层开发，保证每个功能模块的职能单一
- 组件化：是从`UI界面`的角度进行划分的；前端的组件化，方便`UI组件`的重用

### 2. 组件的定义

当使用构建步骤时，我们一般会将 `Vue `组件定义在一个单独的 `.vue` 文件中，这被叫做 `SFC`

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```

当不使用构建步骤时，一个 `Vue `组件以一个包含 `Vue `特定选项的 `JavaScript `对象来定义：

```js
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
  // 或者 `template: '#my-template-element'`
}
```

这里的模板是一个内联的 `JavaScript `字符串，`Vue `将会在运行时编译它。你也可以使用 ID 选择器来指向一个元素 (通常是原生的 `<template>` 元素)，`Vue `将会使用其内容作为模板来源。

上面的例子中定义了一个组件，并在一个 `.js` 文件里默认导出了它自己，但你也可以通过具名导出在一个文件中导出多个组件。

### 3. 组件的注册

一个 `Vue 组件`需要被注册使得 `Vue `在渲染模板时能找到其实现。有两种方式来注册组件：全局注册和局部注册。

> 全局注册

我们可以使用 `app.component()` 方法，让组件在全局可用。

```js
import MyComponent from './App.vue'

app.component('MyComponent', MyComponent)
```

但全局组件，只要声明，即使不使用也会被初始化，影响性能。如果你全局注册了一个组件，却一次都没有使用，它仍然会出现在最终的构建产物中。

`app.component()` 方法可以被链式调用

```js
app
  .component('ComponentA', ComponentA)
  .component('ComponentB', ComponentB)
  .component('ComponentC', ComponentC)
```

全局注册的组件可以在此应用的任意组件的模板中使用：

```vue
<!-- 这在当前应用的任意组件中都可用 -->
<ComponentA/>
<ComponentB/>
<ComponentC/>
```

所有的子组件也可以使用全局注册的组件，这意味着这三个组件也都可以在彼此内部使用。

> 局部注册

`局部注册的组件`只能在当前组件使用

```js
import ComponentA from './ComponentA.vue'

export default {
  // 局部注册的组件
  components: {
    ComponentA
  },
  setup() {
    // ...
  }
}
```

局部组件，如果不使用，就不会初始化，因此对性能有好处。

当你在单文件组件中使用了 `<script setup>`，导入的组件可以在本地使用而无需注册：

```vue
<script setup>
import ComponentA from './ComponentA.vue'
</script>

<template>
  <ComponentA />
</template>
```

局部注册组件在后代组件中并不可用, 只可以在当前组件中使用

> 组件名格式

推荐使用 `PascalCase `作为组件名的注册格式，这是因为：

1. `PascalCase `是合法的 `JavaScript `标识符。这使得在 `JavaScript` 中导入和注册组件都很容易，同时 IDE 也能提供较好的自动补全。
2. `<PascalCase />` 在模板中更明显地表明了这是一个 `Vue `组件，而不是原生 `HTML `元素。同时也能够将 `Vue `组件和自定义元素区分开来。

但是，`PascalCase `的标签名在 `DOM 模板`中是不可用的

`Vue `支持将使用 `kebab-case` 的标签解析为使用 `PascalCase `注册的组件。这意味着一个以 `MyComponent` 为名注册的组件，在模板中可以通过 `<MyComponent>` 或 `<my-component>` 引用。

### 4. 组件的使用

```vue
<script setup>
import ButtonCounter from './ButtonCounter.vue'
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

通过 `<script setup>`，导入的组件都在模板中直接可用。

使用 切换多个组件一个组件在切换离开时将被卸载。我们可以通过内置组件`KeepAlive` 强制非活动组件保持

### 5. 组件之间值的传递

`Vue` 组件作用域是孤立的，不允许在子组件模板内直接引用父组件的数据。必须使用特定的方法才能实现组件之间的数据传递。

组件需要显式声明 `prop`，这样 `Vue `才能知道外部传入的哪些是 `prop`，哪些是透传 `attribute`

- 父组件通过标签上`:data=data`方式定义传值， 子组件通过`props`方法接受数据
- 子组件通过`$emit`方法传递参数， 父组件通过定义的函数接收数据

当一个值被传递给一个 `prop `属性时，它就成为该组件实例上的一个属性。

### 6. props

组件需要显式声明 `prop`，这样 `Vue `才能知道外部传入的哪些是 `prop`

声明的 `props `会自动暴露给模板。

`defineProps` 会返回一个对象，其中包含了可以传递给组件的所有 `props`，因此我们在 `JavaScript `中使用

> `defineProps` 是一个仅 `<script setup>` 中可用的编译宏命令，并不需要显式地导入。

```vue
<!-- BlogPost.vue -->
<script setup>
defineProps(['title'])
    
const props = defineProps(['title'])
console.log(props.title)
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```

如果你没有使用 `<script setup>`，`props `必须以 `props` 选项的方式声明，`props` 对象会作为 `setup()` 函数的第一个参数

```js
export default {
  props: ['title'],
  setup(props) {
    console.log(props.title)
  }
}
```

一个组件可以有任意多的 `props`，默认情况下，任何值都可以传递给任何 `prop`。

> 1.数组形式

```js
props: [data1, data2]
```

数组形式相当于直接接收消息，不做任何校验，一般来说，不建议使用数组形式。

> 2.简单对象形式

除了使用字符串数组声明 `props `之外，我们还可以使用对象语法

```js
// 使用 <script setup>
defineProps({
  title: String,
  likes: Number
})
```

对于以对象形式声明中的每个属性，key 是 prop 的名称，而值应该是预期类型的构造函数。

组件可以为其 `props `指定要求，例如您已经看到的类型。如果不满足要求，`Vue `将在浏览器的 `JavaScript `控制台中警告

如果你正在搭配 `TypeScript `使用 `<script setup>`，也可以使用类型标注来声明 prop

```vue
<script setup lang="ts">
defineProps<{
  title?: string
  likes?: number
}>()
</script>
```

> 3.复杂对象形式

要指定 `prop `验证，您可以向`option`提供具有验证要求的对象，而不是字符串数组。例如：`props`

- `type`: 设定参数类型，当传入参数类型与type不相符时，控制台会报错；

- > - `String`
  > - `Number`
  > - `Boolean`
  > - `Array`
  > - `Object`
  > - `Date`
  > - `Function`
  > - `Symbol`

- `required`：设定参数是否是必传，当设为`true`时，不传该参数会报错；

- `default`：设定默认值，当参数类型为复杂类型时，需使用工厂模式生成默认值，否则`Vue`会在控制台抛出警告。

- `validator`：校验器，是一个函数，拥有一个代表传入值的形参，可以自定义各种校验，当返回`false`时，会报错，表示没通过校验。

`props` 会在一个组件实例创建之前进行验证，所以实例的属性 (如 `data`、`computed` 等) 在 `default` 或 `validator` 函数中是不可用的。

```js
export default {
  props: {
    propA: Number,

    propB: [String, Number],

    propC: {
      type: String,
      required: true
    },

    propD: {
      type: Number,
      default: 100
    },

    // 对象和数组需要使用函数返回, 否则所有组件将共用一个对象, 会发生一些问题
    propE: {
      type: Object,
      default(rawProps) {
        return { message: 'hello' }
      }
    },

    propF: {
      validator(value) {
        return ['success', 'warning', 'danger'].includes(value)
      }
    },

    // 方法也是可以进行传递的 
    propG: {
      type: Function,
      default() {
        return 'Default function'
      }
    }
  }
}
```

### 7.6 $emit

除了上面的父组件传值给子组件, 子组件也可以传值给子组件, 这就需要用到 `$emit`

组件要触发的事件可以显式地通过 [`defineEmits()`](https://staging-cn.vuejs.org/api/sfc-script-setup.html#defineprops-defineemits) 宏来声明。

```vue
<script setup>
const emit = defineEmits(['inFocus', 'submit'])
</script>
```

- 参数
  - `{string} eventName 触发的事件名`
  - `[...args] 传递给事件的参数`
- **作用**： 触发当前实例上的事件。附加参数都会传给监听器回调。

> 子组件

```vue
<template>
  <div>
    <h1>{{ message }}</h1>
	// 1. 我们需要在子组件中触发事件去给父组件传递值
    <button @click="changeFatherData">son button</button>
  </div>
</template>

<script>
export default {
  name: "SonComponents",
  data() {
    return {
      message: "I am son"
    }
  },
  methods: {
    changeFatherData() {
      // 2. 通过 $emit 给组件绑定一个 changeData 的点击方法, 第二个参数是传递的数据
      this.$emit('changeData', "my father data changed")
    }
  }
}
</script>

<style scoped>

</style>
```

> 父组件

```js
<template>
  <div id="app">
    <h1>{{ message }}</h1>
	// 使用$emit触发父组件中写好的方法。
	// 第一个 changeData 是子组件中的的定义的方法名字
	// 第二个 changeData 是当前组件定义的 changeData 方法
    <SonComponents @changeData="changeData"></SonComponents>
  </div>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  data() {
    return {
      message: 'I am father'
    }
  },
  components: {
    SonComponents
  },
  methods: {
    // 参数为子组件传递的值
    changeData(message) {
      this.message = message
    }
  }
}
</script>
```

> 我们也可以对 $emit 的传递的参数进行验证

```js
<template>
  <button @click="sonClick">son button</button>
</template>

<script>
export default {
  name: "SonComponents",
  emits: {
    commit(v) {
      return /^\d$/.test(v);
    }
  },
  methods: {
    sonClick() {
      this.$emit("commit", 1);
    }
  }
}
</script>

<style scoped>

</style>
```

我们通过 `emits` 来对自定义事件传递的参数进行验证

```js
<template>
  <div id="app">
    <h1>{{ number }}</h1>
    <SonComponents @commit="change"></SonComponents>
  </div>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  components: {
    SonComponents
  },
  data() {
    return {
      number: 0
    }
  },
  methods: {
    change(data) {
      this.number = data
    }
  }
}
</script>
```

### 7.7 $parent

`$parent` 指向调用该组件的直接组件（父组件）实例

可以通过` $parent  `直接获取到父组件 中的 `props 、 data或者方法`, 并且可以进行修改

然后通过 `$parent` 层叠可以一层一层地往上追溯各级父组件，比如 `this.$parent.$patent.message`

> 子组件

```js
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  name: "SonComponents",
  data() {
    return {
      message: "I am son"
    }
  },
  mounted() {
    console.log(`这是子组件中使用$parents获得父组件中的data中的message: ${this.$parent.$data.message}`)
  }
}
</script>
```

> 父组件

```js
<template>
  <div id="app">
    <h1>{{ message }}</h1>
    <SonComponents></SonComponents>
  </div>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  data() {
    return {
      message: 'I am father'
    }
  },
  components: {
    SonComponents
  }
}
</script>
```

![image-20220517204206464](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205172042539.png)

### 7.8 $children

> <font color="red" weidth="bolder">在 `Vue 3.x` 中，将移除且不再支持 `$children` 。不推荐使用</font>

需要注意 `$children` 并不保证顺序，也不是响应式的。

借助`$children`，可以获取到当前组件的所有子组件的全部实例。所以，借助`$children`可以访问子组件的data、方法等。一种常用的用法就是用于父子组件间的通讯途径。

### 7.9 ref

使用原生的 `js `操作 `ref` 绑定的元素

因为` Vue 3.x` 中，`$children`被移除了。如果我们要想访问子组件实例，可以通过`$refs`来实现。

```js
<template>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="btnClick">father</button>
    <SonComponents ref="son"></SonComponents>
  </div>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  data() {
    return {
      message: 'I am father'
    }
  },
  components: {
    SonComponents
  },
  methods: {
    btnClick() {
      console.log(this.$refs.son.message)
    }
  }
}
</script>
```

![image-20220517214648991](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205172146060.png)

两者获取到的数据基本没有什么差别。所以，`$refs`替代`$children`完成没问题。

### 7.10 provide / inject

`provide`和`inject`可以实现嵌套组件之间进行传递数据。这两个函数都是在`setup`函数中使用的。

在使用`provide`和`inject`的时候需从`vue`中引入

> `provide`

父组件/祖先组件向子组件/子孙组件传递数据时，写在父级组件里，接收两个参数  

第一个参数是 `key`，即数据的名称；第二个参数为 `value`，即数据的值

> `inject`

子组件/子孙组件接收从父级/祖先组件传递过来的数据，写在子组件里，接收一个参数 `key`，即父组件或祖先组件传递的数据名称

> 父组件

```js
<template>
  <div id="app">
    <SonComponents></SonComponents>
  </div>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  components: {
    SonComponents
  },
  provide: {
    test: 'test'
  }
}
</script>
```

> 子组件

```vue
<template>
    <p>{{test}}</p>
</template>

<script>
export default {
  name: "SonComponents",
  inject: ['test']
}
</script>
```

### 7.11 $listeners

<font color="red" weidth="bolder">Vue 3.x 已经弃用`$listeners` 对象。`vue3`把把`$attrs`和`$listeners`统一合并到`$attrs`中</font>

`vue2`中使用`$attrs`从父组件传递数据给子组件嵌套组件，父组件通过通过`$listeners`监听子组件的事件

`$listeners`属性，它是一个对象，里面包含了作用在这个组件上的所有监听器，你就可以配合 v-on="$listeners" 将所有的事件监听器指向这个组件的某个特定的子元素。

```html
<label>
    <input type="text" v-bind="$attrs" v-on="$listeners" />
</label>
```

上面代码为 `input` 元素绑定父组件传递过来的属性和监听器。

### 7.12 $attrs

- `$attrs`是在`vue的2.40版本以上`添加的。
- 项目中**有多层组件传参**可以使用`$attrs`，可以使代码更加美观，更加简洁，维护代码的时候更方便。
- 如果使用普通的父子组件传参`prop和$emit，$on`会很繁琐；如果使用`vuex`会大材小用，只是在这几个组件中使用，没必要使用`vuex`；使用事件总线`eventBus`，使用不恰当的话，有可能会出现事件多次执行。

```js
<template>
    <input type="text" v-bind="$attrs" />
</template>
<script>
export default {
  inheritAttrs: false,
  props:{
    attrA: String
  }
}
</script>

```

> 可能会看不懂上面的解释
>
> **举一个例子来说明: **
>
> ​		当我们的一个子组件想要使用他父级的父级的数据, 在简单无脑的使用中我们需要一次次在组件中使用 `props` 进行数据的传递, 但是这样子是很麻烦的, 下面演示一下

```js
// 目录结构
- App.vue
+ components
--  Index0Components.vue
++  Index1Componenes
---   Index1Componenes.vue
+++   Index2Componenes
----    Index2Componenes.vue
```

> `App.vue`

```js
<template>
  <h1> 1:{{ message }}</h1>
  <Index0Components :message="message"></Index0Components>
</template>

<script>
import Index0Components from "@/components/Index0Components";
export default {
  name: 'App',
  data() {
    return {
      message: 'Hello ximingx!'
    }
  },
  components: {
    Index0Components
  }
}
</script>
```

> `Index0Components.vue`

```js
<template>
  <h2> 2:{{ message }}</h2>
  <Index1Components :message="message"></Index1Components>
</template>

<script>
import Index1Components from "@/components/Index1Components/Index1Components";
export default {
  name: "Index0Components",
  props: ["message"],
  components: {
    Index1Components
  }
}
</script>
```

> `Index1Components.vue`

```js
<template>
  <h3> 3:{{ message }}</h3>
  <Index2Components :message="message"></Index2Components>
</template>

<script>
import Index2Components from "@/components/Index1Components/Index2Components/Index2Components";
export default {
  name: "Index1Components",
  props: ["message"],
  components: {
    Index2Components
  }
}
</script>
```

> `Index2Components.vue`

```js
<template>
  <h4> 4:{{ message }}</h4>
</template>

<script>
export default {
  name: "Index2Components",
  props: ["message"],
}
</script>
```

![image-20220517103612768](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205171036834.png)

确实, 最后的数据是传递过来了, 但是不得不承认他的写法很麻烦, 所以我们放弃了通过 `props `传值, 而是选择使用 `$attrs`

**上面的代码可以写为**

> `App.vue` 不需要改变

```html
<template>
  <h1> 1:{{ message }}</h1>
  <Index0Components :message="message" data="123" style="color: red"></Index0Components>
</template>
```

> `Index0Components.vue`
>
> ​		我们可以看到, 这里减少了 `props `属性的传值, 使用 `v-bind="$attrs"`

```js
<template>
  <Index1Components v-bind="$attrs"></Index1Components>
</template>

<script>
import Index1Components from "@/components/Index1Components/Index1Components";
export default {
  name: "Index0Components",
  components: {
    Index1Components
  }
}
</script>
```

> `Index1Components.vue`
>
> ​		我们可以看到, 这里减少了 `props `属性的传值, 使用 `v-bind="$attrs"`

```js
<template>
  <Index2Components v-bind="$attrs"></Index2Components>
</template>

<script>
import Index2Components from "@/components/Index1Components/Index2Components/Index2Components";
export default {
  name: "Index1Components",
  components: {
    Index2Components
  }
}
</script>
```

> `Index2Components.vue`

```js
<template>
  <h4> message:{{ message }}</h4>
  <h4> data:{{data}}</h4>
  <h4> style:{{style}}</h4>
</template>

<script>
export default {
  name: "Index2Components",
  props: ["message","data","style"],
}
</script>
```

![image-20220517105803049](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205171058112.png)

多级组件传值时，调用目标组件绑定`$attrs`，**可直接获取根组件所传递参数，而不用每一级组件逐层传递。** 中间的组间不再需要获取多余的数据

当然如果传递过程中也需要使用的话, 也可以在标签上添加 `v-bind="$attrs"`

```js
<template>
  <Index2Components v-bind="$attrs"></Index2Components>
  <p v-bind="$attrs">123456</p>
</template>

<script>
import Index2Components from "@/components/Index1Components/Index2Components/Index2Components";
export default {
  name: "Index1Components",
  components: {
    Index2Components
  }
}
</script>
```

![image-20220517114620301](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205171146369.png)

也可以只获取一个数据

```js
<template>
  <h2 v-bind:style="$attrs.style">123</h2>
</template>

<script>
export default {
  name: "Index0Components",
  inheritAttrs: false,
}
</script>
```

- 父组件调用子组件时，给子组件标签添加的属性中，除了在子组件的`props`中声明的属性，其他属性会自动添加到子组件根元素上。
- `Vue 3.x` 中， `$attrs`将包含传递给组件的所有属性，包括`class`和`style`

> 需要注意的是
>
> ​		`inheritAttrs: false`的含义是不希望本组件的根元素继承父组件的`attribute`，同时父组件传过来的属性（没有被子组件的`props`接收的属性），也不会显示在子组件的`dom`元素上，但是在组件里可以通过其`$attrs`可以获取到没有使用的注册属性, ``inheritAttrs: false`是不会影响 `style `和 `class `的绑定

> 在上面例子的基础上修改一下

```js
<template>
  <div>
    <h4> message:{{ message }}</h4>
    <h4> data:{{data}}</h4>
  </div>
</template>

<script>
export default {
  name: "Index2Components",
  inheritAttrs: true,
  props: ["message","data"],
}
</script>
```

我们没有使用 `props `接收 `style`, 他将添加到我们组建的根元素上 

![image-20220517110406453](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205171104521.png)

但是在我们修改为 `inheritAttrs: false` 之后

![image-20220517110602746](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205171106811.png)

即使 `props` 没有接收 `style` , 也不会添加到根组件上

**如果你不希望组件的根元素继承特性，你可以在组件的选项中设置` inheritAttrs: false`**

### 7.13 Bus

在使用`vue3.0`做后台管理系统的过程中，需要实现兄弟组件间的通信，一个组件触发事件，另一个组件接收到事件后执行某操作

### 7.14 vuex

`vuex `在下面会单独介绍, 作为 `vue` 全家桶的一部分还是很重要的

### 7.15 slot 

> `<slot>< /slot> `一般被写在子组件里,可以被父组件内写的东西"插"满

```vue
<template>
  <SonComponents>
    <h1>ximingx</h1>
  </SonComponents>
</template>
```

```vue
<template>
  <button>son button</button>
  <slot></slot>
  <slot></slot>
  <slot></slot>
</template>

<script>
export default {
  name: "SonComponents",
}
</script>
```

![image-20220519092618947](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205190926021.png)

> 插槽在哪一个组件中使用, 使用的就是哪一个组件的数据

```vue
<template>
    <h1>{{ number }}</h1>
    <SonComponents @commit="change">
      template: <span>{{ number }}</span>
    </SonComponents>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
export default {
  name: 'App',
  components: {
    SonComponents
  },
  data() {
    return {
      number: 0
    }
  },
  methods: {
    change(data) {
      this.number = data
    }
  }
}
</script>
```

这里的 `template: <span>{{ number }}</span>` number 的值是当前组件中的值

> `Vue3`（其实从`2.6`开始）中引入了一个新的指令`v-slot`，用来表示具名插槽和默认插槽

大多数使用默认插槽

```vue
<template>
  <slot>
    <button>ximingx</button>
  </slot>
</template>
```

默认显示 `<button>ximingx</button>`

除此之外, 我们可以在`slot`容器`<template>`上使用`v-slot`来表示一个传入组件的插槽，通过**指令参数**来表示插槽的名称。

```vue
<template>
  <header>
    <slot name="header"></slot>
    <slot name="main"></slot>
    <slot name="footer"></slot>
  </header>
</template>



<foo>
    <template v-slot:header>
        <div class="header"></div>
    </template>
    <template v-slot:body>
        <div class="body"></div>
    </template>
    <template v-slot:footer>
        <div class="footer"></div>
    </template>
</foo>
```

> 组件传值是单向数据流

一般情况下, 父组件的值发生改变会影响子组件中的数据, 而子组件中的值发生改变不会影响父组件, 是单向数据流的

但是特殊情况除外, 如果数据是`引用类型`, 例如对象或者数组, 在子组件中修改值, 可能会影响父组件中的数据

> 默认插槽的名字是 `default`

```html
<slot>
    <button>ximingx</button>
</slot>
<!-- 等价于 -->
<slot  name="default">
    <button>ximingx</button>
</slot>
```

> 插槽的简写是 `#`

```html
<template>
  <SonComponents>
    <template #main></template>
  </SonComponents>
</template>
```



### 7.16 is

有的需求会想要在两个组件间来回切换

> `<component :is="current"></component>` 的使用可以动态的渲染组件

```vue
<template>
  <component :is="current"></component>
  <button @click="current = 'XimingTest'"></button>
</template>

<script>
import SonComponents from './components/SonComponents.vue'
import XimingTest from "@/components/XimingTest";
export default {
  name: 'App',
  components: {
    SonComponents,
    XimingTest
  },
  data() {
    return {
      current: 'SonComponents'
    }
  }
}
</script>
```

组件会在被切换掉后卸载。我们可以通过 `keepAlive` 组件强制不活跃的组件仍然保持“存活”的状态。

## 8. Vue-router

`vue-router` 它是一个`Vue.js`官方提供的路由管理器。

`Vue Router`和`Vue.js`非常契合，可以一起方便的实现`SPA(single page web application`,单页应用程序)应用程序的开发。
`Vue Router`依赖于`Vue`，所以需要先引入`Vue`，再引入`Vue Router`

### 2. 路由案例

看完这个`vue-router` 的简单实现, 就可以对  `vue-router` 有大概的了解

> 实现效果
>
>     		1. 页面没有刷新
>     		2. 完成路由的切换

![img](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205240800649.gif)

> 目录结构

![image-20220524074840383](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205240748443.png)

> 首先我们进入到 `router` 中的 `inde.js`

```js
import {ref} from 'vue'
import Home from '../views/Home.vue'
import About from '../views/About.vue'
// 动态获取当前的 url 地址
const path = ref(window.location.pathname)
const router = [
    {
    path: '/',
    name: 'home',
    component: Home
  },
  {
    path: '/about',
    name: 'about',
    component: About
  }
];

export {
  path,
  router
}
```

> `RouterLink.vue`

```html
<template>
  <!--阻止点击事件的默认跳转行为, 防止每一次的页面刷新都会向服务器请求-->
  <a href="#" @click.prevent="push">
    <slot></slot>
  </a>
</template>

<script setup>
import {path} from '../router/index'

const prop = defineProps({
  to: {
    type: String,
    required: true
  },
})
const push = (e) => {
  path.value = prop.to
}
</script>

<style>
a {
  text-decoration: none;
  padding: 5px 10px;
  color: black;
  font-weight: bold;
}
a:hover {
  background-color: #eee;
}
</style>
```

> `RouterView.vue`

```html
<template>
    // 动态渲染组件
	<component :is="view"></component>
</template>

<script setup>
import {computed} from 'vue';
import {router, path} from '../router';
const view = computed(() => {
  const route = router.find(r => r.path === path.value);
  return route.component ;
});
</script>
```

> `App.vue`

```html
<template>
  <router-link to="/">home</router-link>
  <router-link to="/about">about</router-link>
  <hr>
  <router-view></router-view>
</template>

<script>
import RouterView from './components/RouterView.vue'
import RouterLink from './components/RouterLink.vue'
export default {
  name: 'App',
  components: {
    RouterView,
    RouterLink
  }
}
</script>
```

> `Home.vue` `About.vue`

```html
<template>
  <div>
    <h1>Home</h1>
    <p>This is the home page</p>
  </div>
</template>

<script>
export default {
  name: "Home"
}
</script>
```

 ```html
 <template>
   <div>
     <h1>About</h1>
     <p>This is the about page</p>
   </div>
 </template>
 
 <script>
 export default {
   name: "About"
 }
 </script>
 ```







### 8.1 前后端路由

> 前端路由

对于普通的网站，所有的超链接都是`URL`地址，所有的`URL`地址都对应服务器上对应的资源。

当前端输入`url`请求资源时，服务器会监听到是什么`url`地址，那后端会返回什么样的资源呢？后端这个处理的过程就是通过**路由**来**分发**的。

**总结**：后端路由，就是把所有`url`地址都对应到服务器的资源，这个**对应关系**就是路由。

> 后端路由

对于单页面应用程序来说，主要通过`URL`中的`hash`（`url`地址中的`#`号）来实现不同页面之间的切换。

同时，`hash`有一个特点：`HTTP`请求中不会包含`hash`相关的内容。所以，单页面程序中的页面跳转主要用`hash`实现。

**总结**：在**单页应用**程序中，这种通过`hash`改变来**切换页面**的方式，称作前端路由（区别于后端路由）。

核心实现依靠一个事件，即监听`hash`值变化的事件

```js
window.onhashchange = function(){
    //location.hash可以获取到最新的hash值
    location.hash
}
```

---

### 8.2 使用路由

> 安装引入

```bash
# 安装
$ npm i vue-router -S
```

在 `src `目录下新建文件夹 `router`, 然后再在里面新建文件 `index.js`

```js
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router'
import HomeView from '../views/HomeView.vue'

const routes: Array<RouteRecordRaw> = [
  {
    path: '/about',
    name: 'about',
    component: () => import('../views/AboutView.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
```

然后在 `main.js` 中引入 `import router;` 并使用插件  `Vue.use(router);`

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

createApp(App).use(router).mount('#app')
```

需要注意的是, 默认情况下，进入网站的首页，我们希望渲染首页的内容。

我们需要多配置一个映射就可以了

```js
{
  path: '/',
  redirect: '/home'
}
```

解释上面的代码

- 我们在`routes`中又配置一个映射
- `path`配置的是根路径：`/`
- `redirect`是重定向，也就是我们将根路径重定向到`/home`的路径下，这样就可以得到我们想要的结果了。

### 路由名称

网页具体路径显示是由`vue-router`配置中 `path`决定的，`path`设置的是什么就显示什么，和`name`无关。

```js
export default new VueRouter({
 routes: [
     { path:"/",redirect:"/user"},
     { path: "/user", component: User , name: "users"}
]

<router-link to={name: 'users'}></router-link>
```

其实`name`就相当于给你的`path`取个别名，方便使用，路由并不是一定要设置`name`值。（如果不设置`name`，`vue-router`默认`name`值为 `default`）





### 8.3 页面跳转

> 方式一：

```html
<router-link :to="{name: 'bookshelf', params: { entityId: this.entityId } }"></router-link>
<router-view></router-view>
```

> 方式二：

```js
// 基础
// 想要导航到不同的 URL，使用 router.push 方法。这个方法会向 history 栈添加一个新记录，所以，当用户点击浏览器后退按钮时，可以返回到之前的 URL。
this.$router.push({path: '/index'})

// 通过 this.$route.params.id 接收参数
// name 对应 router 中 index,js 里的 name
this.$router.push({
        name: 'particulars',
        params: {
          id: id
        }
      })

// 通过 this.$route.query.id 接收参数
// 通过query来传递参数，这种情况下 query 传递的参数会显示在url后面以?id=？形式展示。
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

> and 直接修改地址栏, 但愿你不需要以后这样做

### 8.4 路由嵌套

```js
export default new VueRouter({
 routes: [
            { path:"/",redirect:"/user"},
            { path: "/user", component: User , name: "users"},
            { 
                path: "/login", 
                component: Login,
                //通过children属性为/login添加子路由规则
                children:[
                    { path: "/login/account", component: account },
                    { path: "/login/phone", component: phone },
                ]
            }
        ]
})
```

### 8.5 传递参数

```js
{
    // path 属性中增加了 :id 这样的占位符
	path: '/user/profile/:id', 
	name:'UserProfile', 
	component: UserProfile
}


// 注意 router-link 中的 name 属性名称 一定要和 路由中的 name 属性名称 匹配
<router-link :to="{name:'UserProfile',params:{id:1}}">个人信息</router-link>


// 使用 {{$route.params.id}} 


// router.push() query params
```

### 8.6 路由模式与 404

`SPA(single page application)`: 单一页面应用程序，只有一个完整的页面；它在加载页面时，不会加载整个页面，而是只更新某个指定的容器中内容。**单页面应用(`SPA`)的核心之一是: 更新视图而不重新请求页面**;

`vue-router`在实现单页面前端路由时，提供了两种方式：`Hash`模式和`History`模式；

```js
// createWebHistory history模式
// createWebHashHistory hash模式
const router = createRouter({
  // process.env.BASE_URL 这里是路由前缀
  history: createWebHistory(process.env.BASE_URL),
  routes
})
```

路由模式有两种

>  `hash`：路径带 `#` 符号，如 `http://localhost/#/login`

**`vue-router` 默认 `hash `模式 —— 使用 `URL `的 `hash `来模拟一个完整的 `URL`，于是当 `URL `改变时，页面不会重新加载。**

` hash（#）`是`URL `的锚点，代表的是网页中的一个位置，单单改变`#`后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说 `#`是用来指导浏览器动作的，对服务器端完全无用，`HTTP`请求中也不会不包括`#`；

同时每一次改变`#`后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说**`Hash`模式通过锚点值的改变，根据不同的值，渲染指定`DOM`位置的不同数据**

> `history`：路径不带 `#` 符号，如 `http://localhost/login`

由于`hash`模式会在`url`中自带`#`，如果不想要很丑的 `hash`，我们可以用路由的 `history` 模式，只需要在配置路由规则时修改

这种模式充分利用 `history.pushState API` 来完成 `URL `跳转而无须重新加载页面。

```js
// createWebHistory history模式
// createWebHashHistory hash模式
const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})
```

但是这种情况也有弊端, 会访问到未知路径, 因为我们的应用是个单页客户端应用，如果后台没有正确的配置，会返回 `404 `

用户会经常输错页面，当用户输错页面时，我们希望给他一个友好的提示页面，这个页面就是我们常说的`404`页面。`vue-router`也为我们提供了这样的机制。

```js
{
   path:'*',
   component:Error
}
```

这里的`path:'*'`就是输入地址不匹配时，自动显示出`Error.vue`的文件内容

### 8.7 导航守卫

> 全局首守卫

当从一个路由跳转到另一个路由的时候触发此守卫，这个守卫也叫全局**前置**守卫，所以它是跳转前触发的。任何路由跳转都会触发。

三个参数

- to：这是你要跳去的路由对象。
- from：这是你要离开的路由对象。
- next：是一个方法，它接受参数。如过没有调用 next 方法, 路由不会向下传递

```js
const router = new VueRouter({ ... })
 
router.beforeEach((to, from, next) => {
  // ...
})
```

> 全局后置钩子, 钩子不会接受 next 函数也不会改变导航本身, 只有 to, from 两个参数

> 路由独享守卫

这个守卫是写在路由里面的，只有当进入这个路由时才会调用的，这些守卫与全局前置守卫的方法参数是一样的。

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

### 8.8 补充

> router-link 的 tag 属性

router-link 的 tag 属性可以指定`<router-link>`之后渲染成什么组件，比如我们下面的代码会被渲染成一个`<li>`元素，而不是`<a>` 。 如：`<router-link to='/home' tag='li'>`

> 路由懒加载的方式

```js
 {
    path: '/about',
    name: 'about',
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
```



## 9. axios

> 学习之前希望先去看一下 promise 好方便理解

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
$ npm install axios
$ bower install axios
```
### 3. 简单的引入

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

**其中即使请求地址相同, 方式的不同也会导致结果的不同** 

- get：获取数据，请求指定的信息，返回实体对象
- post：向指定资源提交数据（例如表单提交或文件上传）
- put：更新数据，从客户端向服务器传送的数据取代指定的文档的内容
- patch：更新数据，是对put方法的补充，用来对已知资源进行局部更新
- delete：请求服务器删除指定的数据

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

> async await 的使用

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
async/await是 ECMAScript 2017 的一部分，在 Internet Explorer 和旧版浏览器中不受支持，因此请谨慎使用。嗷呜。
> 请求默认配置

```js
// 在全局声明之后， 每次的 axios 请求路径前都会拼接上全局声明的路径
axios.defaults.baseURL = 'https://api.example.com';
```

### 6.  并发发送请求

使用axios.all，可以放入多个请求的数组。

axios.all([])返回的是一个数组，使用axios.spread可以将数组[res1,res2]展开为res1和res2。

等到最后都返回结果的时候才会调用 then 方法

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

通过 axios 发送请求返回的数据都会被处理, 最后返回的数据在data 中

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

### 11 封装

> 封装形式一

```js
import axios from 'axios'
const TIMEOUT = 5000
const BASEURL = 'http://localhost:3000/api/ximingx/v1'

export function request(config) {
  const instance = axios.create({
    baseURL: BASEURL,
    timeout: TIMEOUT,
    headers: {
        'Content-Type': 'application/json'
    }
  })

  // 请求拦截器
  instance.interceptors.request.use(config => {
    // 设置 token 
	config.headers.Authorization = `Bearer ${localStorage.getItem('token')}`;
    return config
  },err => {
    console.log(err)
  })

    // 响应拦截器
  instance.interceptors.response.use(res => {
    // 直接返回数据
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

  return request({
    url: '/api/user',
    params: {
      name: "ximingx"
    }
  })
```

> 封装形式二

```js
import axios from 'axios'

export default {
  // app Vue 的应用实例
  // options 可选项，插件所需选项
  install (app) {
    // axios.defaults.baseURL = 'http://127.0.0.1:3000'
    // axios.defaults.timeout = 30000

    const instance = axios.create({
      baseURL: 'http://127.0.0.1:3000',
      timeout: 30000
    })

    // Add a request interceptor
    instance.interceptors.request.use(function (config) {
      // Do something before request is sent
      return config
    }, function (error) {
      // Do something with request error
      return Promise.reject(error)
    })

    // Add a response interceptor
    instance.interceptors.response.use(function (response) {
      // Any status code that lie within the range of 2xx cause this function to trigger
      // Do something with response data
      console.log(response)
      if (response.status !== 200 && response.status !== 201) {
        return Promise.reject(new Error('网络请求出现错误'))
      }
      return response.data
    }, function (error) {
      // Any status codes that falls outside the range of 2xx cause this function to trigger
      // Do something with response error
      return Promise.reject(error)
    })

    app.config.globalProperties.$http = instance
  }
}
```

调用

```js
async loadData () {
  const data = await this.$http.get('/heroes')
  this.heroes = data
}
```

### 12. 补充

> 为什么不使用`jQuery`的`Ajax`？

在`vue`开发中不需要使用`jQuery`，因为`jQuery`很重量级。

使用 `jquery `比 vue体积还大， 得不偿失

> `vue`官方在`Vue1.x`的时候，推出了`Vue-resource`

`Vue-resource` 比 `jQuery` 轻便很多，但在`vue2.x`之后，尤雨溪对`Vue-resource`不维护了，简言之，就是弃用了。

> 尤雨溪推荐使用`axios`。 

## 10. Vuex

`vuex `是 `vue`框架中**状态管理**工具。

`vue `脚手架创建项目时勾选 `vuex`，会自动生成一个`store`文件夹自带一个 `index.js`

```bash
$ yarn add vuex

$ yarn add vuex@next --save
```

### 10.1 vuex 属性

有五种，分别是 `State`、 `Getter`、`Mutation` 、`Action`、 `Module`。

Vuex就是一个仓库，仓库里面放了很多对象。

- $store.state 或 context.state，访问state。
- $store.getters 或者 context.state，访问getters。
- $store.dispatch() 或 context.dispatch()，将触发 action函数。
- $store.commit() 或 context.commit()，将触发mutation函数。

**State**

- 其中state就是数据源存放地，对应于一般Vue对象里面的data。

- **state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新。**

**Getter**

- **`getters` 可以对`State`进行计算操作，它就是`Store`的计算属性。**
- 虽然在组件内也可以做计算属性，但是`getters` 可以在多组件之间复用。
- 如果一个状态只在一个组件内使用，可以不用`getters`。
- 它只会包装Store中保存的数据，并不会修改Store中保存的数据，当Store中的数据发生变化时，Getter生成的内容也会随之变化

````html
// this.$store.getters.方法名h
<h1>{{$store.getters.showNum}}</h1>
````

**Mutation Action**

- Mutation用于修改变更$store中的数据

- `Action` 类似于 `mutation`，不同在于：`Action` 提交的是 `mutation`，而不是直接变更状态；`Action` 可以包含任意异步操作。`actions `通过`dispach `-> `mutations`中的方法来实现的
- 可以使用Action来执行异步操作。

### 10.2 案例引入

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
    // 声明变量
    // 在全局通过 this.$store.state.变量名 使用
    state:{
        pathName: "",
        currDbSource: {},
        currJobData: {},
        DbSource: []
    },
    // 修改变量（state不能直接赋值修改，只能通过mutations）
    mutations:{
        // 第一个形参永远都是 state 也就是 $state 对象
        // 第二个形参是调用add时传递的参数
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
    },
    action: {
        // 通过dispach -> mutations中的方法来实现
        // actions的第一个参数是固定的，是 context，是不需要你进行传递的，第二个参数是将要进行操作的数据
        asyncSave(context, payload) {
            setTimeout(() => {
        		context.commit('saveDbSource', payload)
     		 }, 2000)
        }
    }
})
```

**state 提供唯一的公共数据源，所有共享的数据都要统一放到Store中的State中存储**

mutations是用来触发事件，相当于方法，用户需要通过触发这个方法，借此来保存数据，参数的话，第二个参数就是用户传入的值，然后在方法中赋值给state中的变量

场景举例：当我点击按钮后，我需要把当前的数据保存到vuex中，然后跳转到别的路由，然后使用这些数据

```js
methods:{
    // 在一个组件中
    click(){
        // 点击按钮进行一些操作，然后保存数据
        this.$store.commit('saveCurrDbSource',"db")
    }
}
```

这里的第一个参数是要触发的方法，也就是上面`mutations`中的方法，第二个参数是你要传递的数据

**获取数据**

```js
this.$store.state.变量名
 
// 例如
this.$store.state.currDbSource
```

场景有：单页应用中，组件之间的状态，音乐播放、登录状态、加入购物车等。

### 10. 3辅助函数

一般情况下，如果需要访问`vuex.store`中`state`存放的数据，需要使用`this.$store.state.属性名`方式。显然，采取这样的数据访问方式，代码略显繁杂，**辅助函数**为了解决繁杂行问题应运而生。

通过辅助函数 mapGetters、mapState、mapActions、mapMutations，把vuex.store中的属性映射到 vue 实例身上，这样在vue实例中就能访问vuex.store中的属性了，对于操作vuex.store就变得非常方便。

**实际就是把state、getters、mutations、actions整合成一个数组，一次性返回,**

state辅助函数为mapState，actions辅助函数为mapActions，mutations辅助函数为mapMutations。（Vuex实例身上有mapState、mapActions、mapMutations属性，属性值都是函数）

使用辅助函数是把vuex中的getters等函数映射到vue中，调用时使用 this.user 即可调用 this.$store.getters.user 函数

1. 需要在当前组件中引入`Vuex`。
2. 通过`Vuex`来调用辅助函数。

```js
import { mapState, mapGetters, mapActions, mapMutations } from "vuex";
export default {
  computed: {
    ...mapGetters({
      "": "vuex仓库定义的方法",
    }),
    ...mapState({}),
  },
  methods: {
    ...mapMutations({}),
    ...mapActions({}),
      ...mapActions([
      'increment' // 映射 this.increment() 为 this.$store.dispatch('increment')
    ]),
    ...mapActions({
      add: 'increment' // 映射 this.add() 为 this.$store.dispatch('increment')
    })
  },
};
</script>
```



## 11. Pinia

Pinia 是 Vue 的存储库，它允许您跨组件/页面共享状态。

Pinia 最初是为了探索 Vuex 的下一次迭代可能会是什么样子，结合了 Vuex 5 核心团队讨论中的许多想法。

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
    const store = useCounterStore()

    store.count++
    // with autocompletion ✨
    store.$patch({ count: counter.count + 1 })
    // or using an action instead
    store.increment()
  },
}
```

### 安装使用

```bash
yarn add pinia@next
# or with npm
npm install pinia@next
```

在 main.js 中引入 pinia 并创建容器挂载到根实例上

```js
import { createApp } from 'vue'
import App from './App.vue'

import { createPinia } from "pinia";

createApp(App).use(pinia()).mount('#app');
```

在上面的片段中，你将Pinia添加到Vue.js项目中，这样你就可以在你的代码中使用Pinia的全局对象。

## 12. vue.config.js

`vue.config.js` 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载。

这个文件应该导出一个包含了选项的对象：

### 常用配置

```js
const { defineConfig } = require('@vue/cli-service')
// alias 中使用
const path = require('path');
function resolve (dir) {
  return path.join(__dirname, dir)
}
module.exports = defineConfig({
  // 部署应用包时的基本 URL。
  publicPath: "/",
  // 当运行 vue-cli-service build 时生成的生产环境构建文件的目录。注意目标目录的内容在构建之前会被清除
  outputDir: "dist",
  // 放置生成的静态资源 (js、css、img、fonts) 的 (相对于 outputDir 的) 目录。
  assetsDir: "",
  // 指定生成的 index.html 的输出路径 (相对于 outputDir)。
  indexPath: 'index.html',
  // 设置为 true 或 'warning' 时，eslint-loader 会将 lint 错误输出为编译警告。默认情况下，警告仅仅会被输出到命令行，且不会使得编译失败。
  lintOnSave: 'default',
  // 如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。
  productionSourceMap: "false",
  // 文件hash
  filenameHashing: true,
  //  ( 注意看清楚这里 ) 如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。 使用proxy
  devServer: {
    port: 8080, // 端口
    host: "localhost", // 域名
    https: false, // 是否开启https
    open: true,	// 是否在开启服务器后自动打开浏览器访问该服务器
    // 这会告诉开发服务器将任何未知请求 (没有匹配到静态文件的请求)
    proxy: {
      // 只要请求中带有/api的url,就会经过这里请求
      '/api': {
        // //目标请求地址
        target: 'http://ximingx.com',
        ws: true,
        // true为可以跨域  
        changeOrigin: true
      }
    }
  },
  // 在这里对 webpack 进行设置
  configureWebpack: {
    resolve: {
      alias: {
         // 配置别名
        '@': resolve('src'),
        'components': resolve('@/components'),
        'views': resolve('@/views'),
        'assets': resolve('@/assets'),
      }
    }
  },
})
```

> vue 中的代理 proxy

由于大多情况下由前端像后端服务器发起的请求都会存在跨域，由于跨域，会导致请求不通，因此需要进行代理

跨域：协议、域名、端口只要有一个不同，就会存在跨域

如前端网站为：http://101.42.249.175:80

后端服务器接口地址为：http://101.42.249.175:3000

这样前端要请求接口时就会存在跨域问题，这个时候就需要使用代码来进行请求

配置`vue.config.js`：这里的配置只对本地有效，测试环境或正式环境的需要通过`nginx`进行代理配置

```js
module.exports = {
    devServer: {
        port: 8080,
        // vue.config.js 中配置的代理，打包到服务器之后这里的配置是无效的，实际代理到 nginx 去了，因此这里的代理只对本地运行有效
        proxy: {
            '/api': { 
                // 将请求中路径x http://192.168.1.xxx:8001/api
                target: 'http://192.168.1.xxx:8001', // 测试服务器
                ws: false,
                changeOrigin: true,
            },
            '/orderApi': {
                target: 'http://192.168.1.xxx:8889/', // 测试服务器
                ws: false,
                changeOrigin: true,
                pathRewrite:{  // 路径重写，
                    '^/orderApi': '/order' // 这里相对上面的不同就是在将 /orderApi 替换为 target+/order，也就是：http://192.168.1.xxx:8889/order
                }
            },
        }
    },
}
```

###  cdn加载资源

Vue项目打包的时候，默认会把所有代码合并生产新文件,其中包括各种库导致打包出来很大。如果使用cdn的话,会更利于程序的加载速度。

**在`Vue`项目中，引入到工程中的所有js、css文件，编译时都会被打包进`vendor.js`，浏览器在加载该文件之后才能开始显示首屏。**若是引入的库众多，那么`vendor.js`文件体积将会相当的大，影响首开的体验。

将引用的外部js、css文件剥离开来，不编译到`vendor.js`中，而是用资源的形式引用，这样浏览器可以使用多个线程异步将`vendor.js`、外部的js等加载下来，达到加速首开的目的。

外部的库文件，可以使用`CDN资源`，或者别的服务器资源等。

> 1. index.html

在项目根目录index.html使用cdn节点导入

```html
<head>
    <% for (var i in htmlWebpackPlugin.options.cdn && htmlWebpackPlugin.options.cdn.css) { %>
    <link href="<%= htmlWebpackPlugin.options.cdn.css[i] %>" rel="preload" as="style" />
    <link href="<%= htmlWebpackPlugin.options.cdn.css[i] %>" rel="stylesheet" />
  	<% } %>
</head>
<body>
    <div id="app"></div>
    <% for (let i in htmlWebpackPlugin.options.cdn && htmlWebpackPlugin.options.cdn.js) { %>
    <script src="<%= htmlWebpackPlugin.options.cdn.js[i] %>"></script>
  <% } %>
</body>
```

> 2. vue.config.js

```js
const CDN = {
  css: [
    'https://cdn.bootcdn.net/ajax/libs/normalize/8.0.1/normalize.min.css',
    'https://unpkg.com/browse/element-plus@1.2.0-beta.6/theme-chalk/index.css'
  ],
  js: [
    'https://cdn.bootcdn.net/ajax/libs/vue/3.2.6/vue.global.js',
    'https://cdn.bootcdn.net/ajax/libs/vue-router/4.0.11/vue-router.global.js',
    'https://cdn.bootcdn.net/ajax/libs/vuex/4.0.2/vuex.global.js',
    'https://cdn.bootcdn.net/ajax/libs/axios/0.21.4/axios.js',
    'https://unpkg.com/element-plus@1.2.0-beta.6/dist/index.full.js',
    'https://unpkg.com/browse/element-plus@1.2.0-beta.6/lib/locale/lang/zh-cn.js'
  ]
};

let objExternals = {
  vue: 'Vue',
  axios: 'axios',
  vuex: 'Vuex',
  'vue-router': 'VueRouter',
  'element-plus': 'ElementPlus'
}

module.exports = {
  publicPath: '/',
  assetsDir: './assets',
  chainWebpack: config => {
  	// 配置，将当前页定义的cdn值传到主页面（index.html）
    config.plugin('html').tap(args => {
    // 这里我是除本地环境，其余均使用CDN，可自己选择是否配置
      args[0].cdn = process.env.VUE_APP_STAGE === 'LOCAL' ? {} : CDN
      return args;
    });
  },
  configureWebpack: {
    devServer: {
    	//...与本文无关
    },
    resolve: {
    	//...与本文无关
    },
    plugins: [
    	//...与本文无关
    ],
    // 定义webpack打包配置
    externals: process.env.VUE_APP_STAGE === 'LOCAL' ? {} : objExternals 
  }
}
```

这里解释一下`externals `配置选项的作用：

我们想引用一个库，但是又不想让`webpack`打包，并且又不影响我们在程序中以`CMD`、`AMD`或者`window/global`全局等方式进行使用，那就可以通过配置`externals`。





## @ 补充知识

### 1. 动态添加对象的属性

Vue中，动态新增对象的属性时，不能直接添加。正确的做法是：Vue.set(obj,key,value)。

### 2. normalize.css

- 保护有用的浏览器默认样式而不是完全去掉它们
- 一般化的样式, 为大部分HTML元素提供
- 修复浏览器自身的bug并保证各浏览器的一致性
- 优化CSS可用性, 用一些小技巧

安装

```bash
npm install --save normalize.css 
npm install css-loader style-loader
```

main.js 引入

```js
import 'normalize.css'
```

### 3. keep-alive

包裹动态组件时，会缓存不活动的组件实例，主要用于**保留组件状态**或**避免重新渲染**。

### 4. 过滤器

**从 Vue 3.0 开始，过滤器已移除，且不再支持。**

- 可被用于一些常见的文本格式化。
- **过滤器可以用在两个地方：双花括号插值和v-bind表达式。**
- 过滤器应该被添加在JavaScript表达式的尾部，由“管道”符号指示
- 支持级联操作
- **过滤器不改变真正的`data`，而只是改变渲染的结果，并返回过滤后的版本**
- 全局注册时是filter，没有s的。而局部过滤器是filters，是有s的

```html
  <div id="app">
    <input type="text" v-model='msg'>
      <!-- upper 被定义为接收单个参数的过滤器函数，表达式  msg  的值将作为参数传入到函数中 -->
    <div>{{msg | upper}}</div>
    <div>{{msg | upper | lower}}</div>
	<div>{{ message | filterA('arg1', 'arg2') }}</div>  
  </div>
<script type="text/javascript">
   //  lower  为全局过滤器     
   Vue.filter('lower', function(val) {
      return val.charAt(0).toLowerCase() + val.slice(1);
    });
    var vm = new Vue({
      el: '#app',
      data: {
        return {
          	msg: '',
        	message: 'ximingx'
      	}
      },
       //  定义filters 中的过滤器为局部过滤器 
      filters: {
        //    upper 自定义的过滤器名字 
        //    upper 被定义为接收单个参数的过滤器函数，表达式  msg  的值将作为参数传入到函数中
        upper: function(val) {
         //  过滤器中一定要有返回值 这样外界使用过滤器的时候才能拿到结果
          return val.charAt(0).toUpperCase() + val.slice(1);
        }
        // 带有参数
        // 在过滤器中 第一个参数 对应的是  管道符前面的数据  n  此时对应 message
        // 第2个参数  a 对应 实参  arg1 字符串
        // 第3个参数  b 对应 实参  arg2 字符串
        filterAfunction(n,a,b){
            if(n<10){
                return n+a;
            }else{
                return n+b;
            }
        }   
      }
    });
  </script>
```

### 5. 数组变异方法

在 `Vue `中，直接修改对象属性的值无法触发响应式。

变异数组方法即保持数组方法原有功能不变的前提下对其进行功能拓展, 可以触发响应式

> 修改当前的数组

| 方法        | 含义                                                         |
| ----------- | ------------------------------------------------------------ |
| `push()`    | 往数组最后面添加一个元素，成功返回当前数组的长度             |
| `pop()`     | 删除数组的最后一个元素，成功返回删除元素的值                 |
| `shift()`   | 删除数组的第一个元素，成功返回删除元素的值                   |
| `unshift()` | 往数组最前面添加一个元素，成功返回当前数组的长度             |
| `splice()`  | 有三个参数，第一个是想要删除的元素的下标（必选），第二个是想要删除的个数（必选），第三个是删除 后想要在原位置替换的值 |
| `sort()`    | `sort()`  使数组按照字符编码默认从小到大排序,成功返回排序后的数组 |
| `reverse()` | `reverse()`  将数组倒序，成功返回倒序后的数组                |

> 不会改变原始数组，但总是返回一个新数组

| 方法     | 含义                                                         |
| -------- | ------------------------------------------------------------ |
| `filter` | 创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素 |
| `concat` | 用于连接两个或多个数组                                       |
| `slice`  | 可从已有的数组中返回选定的元素                               |

> 通过索引修改数据是不会发生响应式的

一般可以通过` Vue.set(arr,index,value)`   来修改, 让 触发视图重新更新一遍，数据动态起来

```js
var vm = new Vue({
      el: '#app',
      data: {
        return {
          	arr[1,2,3,4,5,6]
      	}
      },
      mounted() {
      	 Vue.set(this.arr, 2, "aw")          
      }
    });
  </script>
```

### 6. 生成二维码

```bash
import QRCode from 'qrcodejs2'
```

```html
<template>
  <div ref="qrCodeUrl" className="cart"></div>
</template>

<script>
import QRCode from 'qrcodejs2'

export default {
  name: "ShowCart",
  methods: {
    creatQrCode(text, color) {
      new QRCode(this.$refs.qrCodeUrl, {
        text: text, // 需要转换为二维码的内容
        width: 400,
        height: 400,
        colorDark: color,
        colorLight: '#ffffff',
        correctLevel: QRCode.CorrectLevel.H
      })
    },
  },
  mounted() {
    // 这里的信息是我自己发送的信息 (b)
    let {name, phone, activity, heath, pass, desc, date} = this.$route.params
    this.creatQrCode(`姓名: ${name}
    电话: ${phone}
    活动区域: ${activity}
    健康码是否是绿色: ${heath}
    行程码是否是绿色: ${pass}
    补充信息: ${desc}
    记录时间: ${date}
    `, (heath && pass)?"#2aad2a":'#ff0000' )
  },
}
</script>

<style scoped>
.cart {
  display: block;
  width: 400px;
  height: 400px;
  margin: 20vh auto;
  position: relative;
  color: cornsilk;
}
</style>
```

### 7. fetch

- Fetch API是新的ajax解决方案 Fetch会返回Promise
- **fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象**。
- fetch(url, options).then(）

```js
  <script type="text/javascript">
    /*
      Fetch API 基本用法
      	fetch(url).then()
     	第一个参数请求的路径   
    */
    fetch('http://localhost:3000/fdata').then(function(data){
      // text()方法属于fetchAPI的一部分，它返回一个Promise实例对象，用于获取后台返回的数据
      return data.text();
    }).then(function(data){
      //   在这个then里面我们能拿到最终的数据  
      console.log(data);
    })
  </script>
```

> http 请求

- fetch(url, options).then(）
- HTTP协议，它给我们提供了很多的方法，如POST，GET，DELETE，UPDATE，PATCH和PUT
  - 默认的是 GET 请求
  - 需要在 options 对象中 指定对应的 method       method:请求使用的方法 
  - post 和 普通 请求的时候 需要在options 中 设置  请求头 headers   和  body

```html
   <script type="text/javascript">
       #1.1 GET参数传递 - 传统URL  通过url  ？ 的形式传参 
        fetch('http://localhost:3000/books?id=123', {
            	# get 请求可以省略不写 默认的是GET 
                method: 'get'
            })
            .then(function(data) {
            	# 它返回一个Promise实例对象，用于获取后台返回的数据
                return data.text();
            }).then(function(data) {
            	# 在这个then里面我们能拿到最终的数据  
                console.log(data)
            });

      #1.2  GET参数传递  restful形式的URL  通过/ 的形式传递参数  即  id = 456 和id后台的配置有关   
        fetch('http://localhost:3000/books/456', {
            	# get 请求可以省略不写 默认的是GET 
                method: 'get'
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       #2.1  DELETE请求方式参数传递      删除id  是  id=789
        fetch('http://localhost:3000/books/789', {
                method: 'delete'
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       #3 POST请求传参
        fetch('http://localhost:3000/books', {
                method: 'post',
            	# 3.1  传递数据 
                body: 'uname=lisi&pwd=123',
            	#  3.2  设置请求头 
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

       # POST请求传参
        fetch('http://localhost:3000/books', {
                method: 'post',
                body: JSON.stringify({
                    uname: '张三',
                    pwd: '456'
                }),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });

        # PUT请求传参     修改id 是 123 的 
        fetch('http://localhost:3000/books/123', {
                method: 'put',
                body: JSON.stringify({
                    uname: '张三',
                    pwd: '789'
                }),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(function(data) {
                return data.text();
            }).then(function(data) {
                console.log(data)
            });
    </script>
```

> 响应格式

用fetch来获取数据，如果响应正常返回，我们首先看到的是一个response对象，其中包括返回的一堆原始字节，这些字节需要在收到后，需要我们通过调用方法将其转换为相应格式的数据，比如`JSON`，`BLOB`或者`TEXT`等等

```js
    fetch('http://localhost:3000/json').then(function(data){
      // return data.json();   //  将获取到的数据使用 json 转换对象
      return data.text(); //  //  将获取到的数据 转换成字符串 
    }).then(function(data){
      // console.log(data.uname)
      // console.log(typeof data)
      var obj = JSON.parse(data);
      console.log(obj.uname,obj.age,obj.gender)
    })

```

### 8. Vue图片路径问题

vue 中我们可以直接使用静态相对路径导入, 也可以直接使用静态绝对导入路径

但是对于的动态相对路径, 可能会发生小问题, 例如

```js
<img :src="../../assets/' + imageUrl" />
    
data() {
   return {
       // 图片路径变量，真实路径为 assets/images/1.png
       imageUrl: 'images/1.png'
   }
}
```

此时我们需要使用 require 的方式

```js
<img :src="require('../../assets/' + imageUrl)" />
```

或者是

```js
<img :src="imageUrl" />
<script>
export default {
	data() {
        return {
            // 图片路径变量，真实路径为 assets/images/1.png
            img: 'images/1.png',
            imageUrl: require('../../assets/' + this.img)
        }
    }
}
</script>
```

>  原因

当你在 JavaScript、CSS 或 `*.vue` 文件中使用相对路径 (必须以 `.` 开头) 引用一个静态资源时，该资源将会被包含进入 webpack 的依赖图中。在其编译过程中，所有诸如 `<img src="...">`、`background: url(...)` 和 CSS `@import` 的资源 URL **都会被解析为一个模块依赖**。

例如，`url(./image.png)` 会被翻译为 `require('./image.png')`，而：

```js
<img src="./image.png">
```

将会被编译到：

```js
h('img', { attrs: { src: require('./image.png') }})
```

### 9. 自定义指令

稍后补充







# Element

## 1. 自动导入

官网对vue3+vuecli4的「自动导入」说的不是很清楚，导致自己踩坑配置了很久，特此写下文章记录

1. 安装unplugin-vue-components

```bash
> yarn add element-plus
> yarn add -D unplugin-vue-components unplugin-auto-import
```

2. 配置config(vuecli配置的是vue.config.js)

```js
// vue.config.js
const Components = require('unplugin-vue-components/webpack')
const { ElementPlusResolver } = require('unplugin-vue-components/resolvers')
module.exports = {
    configureWebpack: {
      plugins: [
        require('unplugin-vue-components/webpack')({ /* options */
        }),
        Components({
            resolvers:[ElementPlusResolver()],
        })
    ],
    },
  }
```

3. main.js

```js
import 'element-plus/dist/index.css'
```

**常用配置**

```js
const { defineConfig } = require('@vue/cli-service')
const path = require('path');
const Components = require('unplugin-vue-components/webpack')
const { ElementPlusResolver } = require('unplugin-vue-components/resolvers')
function resolve (dir) {
  return path.join(__dirname, dir)
}
module.exports = defineConfig({
  publicPath: "/",
  outputDir: "dist",
  assetsDir: "",
  indexPath: 'index.html',
  lintOnSave: 'default',
  productionSourceMap: "false",
  filenameHashing: true,
  devServer: {
    port: 8080,
    host: "localhost",
    https: false, 
    open: true,	
    proxy: {
      '/api': {
        target: 'http://ximingx.com',
        ws: true,
        changeOrigin: true
      }
    }
  },
  configureWebpack: {
    plugins: [
      require('unplugin-vue-components/webpack')(),
      Components({
        resolvers:[ElementPlusResolver()],
      })
    ],
    resolve: {
      alias: {
        '@': resolve('src'),
        'components': resolve('@/components'),
        'views': resolve('@/views'),
        'assets': resolve('@/assets'),
      }
    }
  },
})
```

## 2. 修改默认样式

> 在vue组件中，为了使样式私有化（模块化），不对全局造成污染，可以在style标签上添加scoped属性以表示它的只属于当下的模块。**但是同时，scoped也会阻碍我们修改第三方组件库（element plus）的样式。**
>
> vue-cli生成时，自动给样式加了[data-v-]，所以无法修改样式。如果去掉文件样式中的scoped，会造成全局样式污染。

1. 在公共css中修改全局样式，main.js引入即可；
2. 将 style 中的限定 `scoped` 删除即可,但是不建议  ( 相当于快捷的第一种方式, 但是可能会会造成全局样式污染, 造成最后其他页面莫名其妙的排版 )
3. vue 的深度选择器

```js
>>>
/deep/
::v-deep
```

```css
eg:
<style lang="css" scoped>
.el-table >>> .row-done {
  text-decoration: line-through;
}
</style>

eg:
<style lang="scss" scoped>
.el-table /deep/ .row-done {
  text-decoration: line-through;
}
</style>

eg:
<style lang="scss" scoped>
.a{
   ::v-deep .b { 
      /* ... */ 
   }
} 
</style>
```

**利用深度::v-deep深度修改组建的样式，可以直接写在到scoped作用域的style里面。（推荐）**



# Vue CLI

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统

- 一个丰富的官方插件集合，集成了前端生态中最好的工具。
- 通过 `@vue/cli` 实现的交互式的项目脚手架。
- 通过 `@vue/cli` + `@vue/cli-service-global` 实现的零配置原型开发。
- Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。
- 与此同时，它也为每个工具提供了调整配置的灵活性，无需 eject。

## 1. Vue CLI 系统的组件

> CLI

**CLI (`@vue/cli`) 是一个全局安装的 npm 包，提供了终端里的 `vue` 命令。**

它可以通过 `vue create` 快速搭建一个新项目

```bash
$ vue create 项目名称
```

在创建项目中可以选“手动选择特性”来选取需要的特性。

```bash
# ~/.vuerc

# 被保存的 preset 将会存在用户的 home 目录下一个名为 .vuerc 的 JSON 文件里。如果你想要修改被保存的 preset / 选项，可以编辑这个文件。

# 在项目创建的过程中，你也会被提示选择喜欢的包管理器或使用淘宝 npm 镜像源以更快地安装依赖。这些选择也将会存入 ~/.vuerc。
```

你也可以通过 `vue ui` 通过一套图形化界面管理你的所有项目。

```bash
$ vue ui
```

上述命令会打开一个浏览器窗口，并以图形化界面将你引导至项目创建的流程。

嗷呜, 可是我老是用不习惯, 习惯手敲命令, 但是确实很好用, 打包后的依赖资源, 加载速度看的很方便

> CLI 服务

CLI 服务 (`@vue/cli-service`) 是一个开发环境依赖。**它是一个 npm 包，局部安装在每个 `@vue/cli` 创建的项目中。**

CLI 服务是构建于 [webpack](http://webpack.js.org/) 和 [webpack-dev-server](https://github.com/webpack/webpack-dev-server) 之上的。它包含了：

- 加载其它 CLI 插件的核心服务；
- 一个针对绝大部分应用优化过的内部的 webpack 配置；
- 项目内部的 `vue-cli-service` 命令，提供 `serve`、`build` 和 `inspect` 命令。

> CLI 插件

CLI 插件是向你的 Vue 项目提供可选功能的 npm 包，例如 Babel/TypeScript 转译、ESLint 集成、单元测试和 end-to-end 测试等。

Vue CLI 插件的名字以 `@vue/cli-plugin-` (内建插件) 或 `vue-cli-plugin-` (社区插件) 开头

当你在项目内部运行 `vue-cli-service` 命令时，它会自动解析并加载 `package.json` 中列出的所有 CLI 插件。

## 2. 安装

> Node 版本要求
>
> Vue CLI 4.x 需要 [Node.js](https://nodejs.org/) v8.9 或更高版本 (推荐 v10 以上)。你可以使用 [n](https://github.com/tj/n)，[nvm](https://github.com/creationix/nvm) 或 [nvm-windows](https://github.com/coreybutler/nvm-windows) 在同一台电脑中管理多个 Node 版本。

```bash
$ npm install -g @vue/cli

$ yarn global add @vue/cli
# 你还可以用这个命令来检查其版本是否正确
$ vue --version

# 升级 vue-cli
$ npm update -g @vue/cli
$ yarn global upgrade --latest @vue/cli
```

## 3. 插件

**Vue CLI 使用了一套基于插件的架构。**如果你查阅一个新创建项目的 `package.json`，就会发现依赖都是以 `@vue/cli-plugin-` 开头的。

**插件可以修改 webpack 的内部配置，也可以向 `vue-cli-service` 注入命令。**

在项目创建的过程中，绝大部分列出的特性都是通过插件来实现的。

> 在现有的项目中安装插件
>
> `vue add` 的设计意图是为了安装和调用 Vue CLI 插件。这不意味着替换掉普通的 npm 包。对于这些普通的 npm 包，你仍然需要选用包管理器。

```bash
$ vue add eslint
# 这个和之前的用法等价
$ vue add cli-plugin-eslint
```

这个命令将 `@vue/eslint` 解析为完整的包名 `@vue/cli-plugin-eslint`，然后从 npm 安装它，调用它的生成器。

## 4. Present

一个 Vue CLI preset 是一个包含创建新项目所需预定义选项和插件的 JSON 对象，让用户无需在命令提示中选择它们。

在 `vue create` 过程中保存的 preset 会被放在你的 home 目录下的一个配置文件中 (`~/.vuerc`)。你可以通过直接编辑这个文件来调整、添加、删除保存好的 preset。

这里有一个 preset 的示例：

```js
{
  "useTaobaoRegistry": false,
  // presets
  "presets": {
     // 这里是你的多个配置中的第一个 vue3_bable_router_scs 是名称
    "vue3_bable_router_scss": {
      "useConfigFiles": true,
      "plugins": {
        "@vue/cli-plugin-babel": {},
        "@vue/cli-plugin-router": {
          "historyMode": true
        }
      },
      "vueVersion": "3",
      "cssPreprocessor": "dart-sass"
    }
    // 
  },
   // 看上面的就可
  "latestVersion": "5.0.4",
  "lastChecked": 1648106165203,
  "packageManager": "yarn"
}
```

Preset 的数据会被插件生成器用来生成相应的项目文件。除了上述这些字段，你也可以为集成工具添加配置：

```js
{
  "useConfigFiles": true,
  "plugins": {...},
  "configs": {
    "vue": {...},
    "postcss": {...},
    "eslintConfig": {...},
    "jest": {...}
    // 你可以显式地指定用到的插件的版本, 当被忽略时，CLI 会自动使用 registry 中最新的版本
    "@vue/cli-plugin-eslint": {
      "version": "^3.0.0",
      // ... 该插件的其它选项
    }
  }
}
```

这些额外的配置将会根据 `useConfigFiles` 的值被合并到 `package.json` 或相应的配置文件中。其中当 `"useConfigFiles": true` 时， `configs` 内的配置信息会直接覆盖初始化后项目中的 `vue.config.js`。

所以当你需要给组里定制一份基于 vue-cli 的前端项目初始化模板时, 我们要做的事情很简单，就是当别人使用 `vue create xxx` 命令初始化一个前端项目时，可以从 git repo 去拉取项目初始化信息

> **你可以通过发布 git repo 将一个 preset 分享给其他开发者。这个 repo 应该包含以下文件：**
>
> - **preset.json**: 包含 preset 数据的主要文件（必需）。
> - **generator.js**: 一个可以注入或是修改项目中文件的 Generator。
> - **prompts.js**: 一个可以通过命令行对话为 generator 收集选项的 prompts 文件。

使用`vue create` 创建过项目的小伙伴应该都记得，在创建完成后 CLI 会提示是否保存为一个 preset，这里第一条指的就是要保存的那个对象。如果你保存过，下面的命令就能看到之前保存的 preset。

> **preset.json 文件**

先说一点：当你直接用 `vue create xxx` 初始化项目时，如果你将初始化信息保存成一个本地模板后，会写入到你系统的 `~/.vuerc` 文件中。该文件中的内容其实就是我们接下来需要配置的 `present.json`。

```json
{
  "useConfigFiles": true,
  "plugins": {...},
  "configs": {
    "vue": {...},
    "postcss": {...},
    "eslintConfig": {...},
    "jest": {...}
  }
}
```

> **prompts.js** 

prompts.js 其实就是你在初始化项目时，系统会询问你的配置选项问题，比如你的项目需不需要安装 `vuex`? 需不需要安装 `vue-router`?

你的回答会直接影响后面初始化生成的项目文件。

```js
module.exports = [
{
    type: 'list', // 即类型为 选择项
    name: 'module', // 名称，作为下面 generator 函数 options 的键
    message: '请选择你要生成的模块', // 提示语
    choices: [
      { name: 'Module1', value: 'module1' },
      { name: 'Module2', value: 'module2' },
      { name: 'Module3', value: 'module3' }
    ],
    default: 'module0',
  },
  {
    type: 'input', // 类型为 输入项
    name: 'moduleName',
    message: '请输入模块名称',
    default: 'myModule'
  }
];
```

> **generator.js**

接下来就是 `generator.js`，这个文件负责的就是 **注入或是修改项目中文件**。

```js
module.exports = (api, options, rootOptions) => {
  // 安装一些基础公共库
  api.extendPackage({
    dependencies: {
      "axios"
    }
  });

  // 安装 vuex
  if (options.vuex) {
    api.extendPackage({
      dependencies: {
        vuex
      }
    });

    api.render('./template/vuex');
  }

  // 安装 element-ui 库
  if (options.elementUI) {
    api.extendPackage({
      devDependencies: {
        "element-ui": "^2.4.6"
      }
    });
  }

  // 公共基础目录和文件
  api.render('./template/default');

  // 配置文件
  api.render({
    './.eslintrc.js'     : './template/_eslintrc.js',
    './.gitignore'       : './template/_gitignore',
    './.postcssrc.js'    : './template/_postcssrc.js'
  });
}

```

> 最后的使用
>
> vue create --preset ximingx/vue-preset my-project

## 5.CLI 服务

在一个 Vue CLI 项目中，`@vue/cli-service` 安装了一个名为 `vue-cli-service` 的命令。你可以在 npm scripts 中以 `vue-cli-service`、或者从终端中以 `./node_modules/.bin/vue-cli-service` 访问这个命令。

你可以通过 npm 或 Yarn 调用这些 script：

```bash
$ npm run serve
# OR
$ yarn serve
```

## 6. 资源处理

> 插值

`public/index.html` 文件是一个会被 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) 处理的模板。在构建过程中，资源链接会被自动注入。

因为 index 文件被用作模板，所以你可以使用 [lodash template](https://lodash.com/docs/4.17.10#template) 语法插入内容：

- `<%= VALUE %>` 用来做不转义插值；
- `<%- VALUE %>` 用来做 HTML 转义插值；
- `<% expression %>` 用来描述 JavaScript 流程控制。

> preload

`<link rel="preload">`是一种 resource hint，用来指定页面加载后很快会被用到的资源，所以在页面加载的过程中，我们希望在浏览器开始主体渲染之前尽早 preload。

默认情况下，一个 Vue CLI 应用会为所有初始化渲染需要的文件自动生成 preload 提示。

这些提示会被 [@vue/preload-webpack-plugin](https://github.com/vuejs/preload-webpack-plugin) 注入，并且可以通过 `chainWebpack` 的 `config.plugin('preload')` 进行修改和删除。

> 静态资源

静态资源可以通过两种方式进行处理：

- 在 JavaScript 被导入或在 template/CSS 中通过相对路径被引用。这类引用会被 webpack 处理。
- **放置在 `public` 目录下或通过绝对路径被引用。这类资源将会直接被拷贝，而不会经过 webpack 的处理。**

当你在 JavaScript、CSS 或 `*.vue` 文件中使用相对路径 (必须以 `.` 开头) 引用一个静态资源时，该资源将会被包含进入 webpack 的依赖图中。在其编译过程中，所有诸如 `<img src="...">`、`background: url(...)` 和 CSS `@import` 的资源 URL **都会被解析为一个模块依赖**。

所有编译后的 CSS 都会通过 [css-loader](https://github.com/webpack-contrib/css-loader) 来解析其中的 `url()` 引用，并将这些引用作为模块请求来处理。

## 7.vue.config.js

`vue.config.js` 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载。

调整 webpack 配置最简单的方式就是在 `vue.config.js` 中的 `configureWebpack` 选项提供一个对象：

```js
// vue.config.js
module.exports = {
  configureWebpack: {
    plugins: [
      new MyAwesomeWebpackPlugin()
    ]
  }
}
```

> publicPath

- Type: `string`
- Default: `'/'`

部署应用包时的基本 URL。

> outputDir

- Type: `string`
- Default: `'dist'`

当运行 `vue-cli-service build` 时生成的生产环境构建文件的目录。

> assetsDir

- Type: `string`

- Default: `''`

  放置生成的静态资源 (js、css、img、fonts) 的 (相对于 `outputDir` 的) 目录。

> filenameHashing

- Type: `boolean`

- Default: `true`

  默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。然而，这也要求 index 的 HTML 是被 Vue CLI 自动生成的。如果你无法使用 Vue CLI 生成的 index HTML，你可以通过将这个选项设为 `false` 来关闭文件名哈希。

>  productionSourceMap

- Type: `boolean`

- Default: `true`

  如果你不需要生产环境的 source map，可以将其设置为 `false` 以加速生产环境构建。

> **configureWebpack**

Type: `Object | Function`

如果这个值是一个对象，则会通过 [webpack-merge](https://github.com/survivejs/webpack-merge) 合并到最终的配置中。

```js
configureWebpack:{
  resolve: {
    // 别名配置
    alias: {
      'assets': '@/assets',
      'common': '@/common',
      'components': '@/components',
      'network': '@/network',
      'configs': '@/configs',
      'views': '@/views',
      'plugins': '@/plugins',
    }
  }
},
```

如果这个值是一个函数，则会接收被解析的配置作为参数。该函数既可以修改配置并不返回任何东西，也可以返回一个被克隆或合并过的配置版本。

```js
module.exports = {
  configureWebpack: config => {
    if (isProduction) {
      ...
    } else {
      ...
    }
    // 可以选择返回一个将要合并的对象
    return {
      resolve: {
        alias: {
          '@asset':resolve('src/assets')
        }
      }
    } 
  }
}
```

这个属性特别之处就是，他有两种类型形态，但是又不能重复使用

> **chainWebpack**

Type: `Function`

是一个函数，会接收一个基于 [webpack-chain](https://github.com/mozilla-neutrino/webpack-chain) 的 `ChainableConfig` 实例。允许对内部的 webpack 配置进行更细粒度的修改。

> **devServer**

Type: `Object`

- 有些值像 `host`、`port` 和 `https` 可能会被命令行参数覆写。













# 项目优化

## 1. cdn 引入资源

具体看上面 vue.config.js

## 2. 路由懒加载

```js
component: () => import('views/home/Home.vue'),
```

## 3. express gzip压缩

> 安装

```bash
$ npm install compression
```

> 使用

```js
var compression = require('compression')
// 要在静态资源托管之前使用
app.use(compression())
```

## 4. https

首先需要有证书

```bash
const express = require("express")
const https = require("https");
const fs = require("fs");
const app = express();
const option = {
	cert: fs.readFileSync(''./full_chain.pem'),
	key: fs.readFileSync(''./priveate.key')
}
https.createServer(options, app)
```

## 5. pm2

```bash
$ yarn global add pm2
# 启动项目
$ pm2 start 脚本 --name 自定义名称
# 查看运行任务
$ pm2 ls
# 停止服务
$ pm2 stop 名称 
# 重启服务
$ pm2 restart 名称 
# 删除服务
$ pm2 delete 名称 
```
























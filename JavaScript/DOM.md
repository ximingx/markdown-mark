# DOM

## Node 节点

### 1. 先解释清楚节点与元素

**节点**（Node）：构成 `HTML `网页的最基本单元。网页中的每一个部分都可以称为是一个节点，比如：`html`标签、属性、文本、注释、整个文档等都是一个节点。

虽然都是节点，但是实际上他们的具体类型是不同的。常见节点分为四类：

- 文档节点（文档）：整个 `HTML` 文档。整个 `HTML` 文档就是一个文档节点。

- 元素节点（标签）：`HTML`标签。

- 属性节点（属性）：元素的属性。

- 文本节点（文本）：`HTML`标签中的文本内容（包括标签之间的空格、换行）。

节点的类型不同，属性和方法也都不尽相同。所有的节点都是`Object`。

**总的来说:** 

**元素（element）**：页面中所有的**标签,每个`html`标签都是一个元素**

**节点（node）**：页面中所有的内容，包括标签、属性（标签的属性）、文本(文字,换行,空格,回车)) **即使元素也是节点**

**nodeType**:节点的类型

- **nodeType == 1  表示的是元素节点**（标签） 。记住：在这里，元素就是标签。

- nodeType == 2  表示是属性节点。

- nodeType == 3  是文本节点。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/ad987c77522c40719c1c75ef50392bbf.png)


---

### 2. 什么是`DOM`

**`DOM`**：Document Object Model，文档对象模型。`DOM` 为文档提供了结构化表示，并定义了如何通过脚本来访问文档结构。目的其实就是为了能让js操作html元素而制定的一个规范。

而 `DOM` 就是由节点组成的。

**解析过程**：
HTML加载完毕，渲染引擎会在内存中把HTML文档，生成一个DOM树，getElementById是获取内中DOM上的元素节点。然后操作的时候修改的是该元素的**属性**。


---

### 3. 获取节点

节点的访问关系，是以**属性**的方式存在的。

#### 获取父节点

调用者就是节点。一个节点只有一个父节点，调用方式就是

```js
	node.parentNode
```

#### 获取兄弟节点

| 方法                   | 说明               |
| ---------------------- | ------------------ |
| nextElementSibling     | 获取下一个元素节点 |
| previousElementSibling | 获取上一个元素节点 |

> 获得任意一个兄弟节点：
> **节点自己.parentNode.children[index];**  

####  获取单个的子节点

| 方法              | 说明                   |
| ----------------- | ---------------------- |
| firstElementChild | 获取第一个子元素节点   |
| lastElementChild  | 获取最后一个子元素节点 |


#### 获取所有的子节点

| 方法       | 说明                                                       |
| ---------- | ---------------------------------------------------------- |
| childNodes | 指定元素的子节点的集合（包括元素节点、所有属性、文本节点） |
| children   | 子元素节点的集合, 只返回HTML节点，甚至不返回文本节点。     |


### 4. 节点的操作

#### 创建节点

```javascript
	新的标签(元素节点) = document.createElement("标签名");
```

#### 插入节点

> 父节点的最后插入一个新的子节点。
> 但是需要注意: 一个已经存在的节点插入另一个已经存在的节点, 被插入的原节点的位置会消失

```javascript
	父节点.appendChild(新的子节点);
```

> 在参考节点前插入一个新的节点。
> 如果参考节点为null，那么他将在父节点里面的最后插入一个子节点。

```javascript
	父节点.insertBefore(新的子节点,作为参考的子节点)
```

insertAdjacentHTML

语法：

```js
object.insertAdjacentHTML(where,html)
```

参数说明：

1. where: 包括beforeBegin,beforeEnd,afterBegin,afterEnd

- beforeBegin: 插入到标签开始前
- afterBegin:插入到标签开始标记之后
- beforeEnd:插入到标签结束标记前
- afterEnd:插入到标签结束标记后

2. html:需插入的html内容

需注意的是：

**1.这两个方法必须等文档加载好后才能执行，否则会出错。**

2.insertAdjacentText只能插入普通文本，insertAdjacentHTML插入html代码。

3.使用insertAdjacentHTML方法插入script脚本文件时，必须在script元素上定义defer属性。

4.使用insertAdjacentHTML方法插入html代码后，页面上的元素集合将发生变化。

#### 删除节点

```javascript
	父节点.removeChild(子节点);
```

#### 克隆节点


```javascript
	要复制的节点.cloneNode();       //括号里不带参数和带参数false，效果是一样的。
	要复制的节点.cloneNode(true);
```

- 不带参数/带参数false：只复制节点本身，不复制子节点。

- 带参数true：既复制节点本身，也复制其所有的子节点。


#### 设置节点的属性值

```javascript
	元素节点.setAttribute("属性名", "新的属性值");
```

#### 删除节点的属性

```javascript
	元素节点.removeAttribute(属性名);
```


### 5. 获取 html 文档的方法

获取title、body、head、html标签的方法如下：

- `document.title` 文档标题；

- `document.head`  文档的头标签

- `document.body`  文档的body标签；

- `document.documentElement`  文档的html标签（这个很重要）。

`document.documentElement`表示文档的html标签。也就是说，基本结构当中的 `html 标签`而是通过`document.documentElement`访问的，并不是通过 document.html 去访问的。

## 新增全屏显示

> 》 HTML5规范允许用户自定义网页上**任一元素**全屏显示。

### 开启/关闭全屏显示

方法如下：（注意 screen 是小写）

```javascript
	requestFullscreen()   //让元素开启全屏显示

	cancleFullscreen()    //让元素关闭全屏显示
```

### 检测当前是否处于全屏状态

方法如下：

```js
	document.fullScreen
```


### 全屏的伪类

- :full-screen .box {}

- :-webkit-full-screen {}

- :moz-full-screen {}

比如说，当元素处于全屏状态时，改变它的样式。这时就可以用到伪类。

```js
<script>
    var box = document.querySelector('.box');
    // box.requestFullscreen();   
    //直接这样写是没有效果的。浏览器的机制，必须要点一下才可以实现全屏功能。
    document.querySelector('.box').onclick = function () {
        // 开启全屏显示的兼容写法
        if (box.requestFullscreen) {  
        //如果支持全屏，那就让元素全屏
            box.requestFullscreen();
        } else if (box.webkitRequestFullScreen) {
            box.webkitRequestFullScreen();
        } else if (box.mozRequestFullScreen) {
            box.mozRequestFullScreen();
        }

    }
</script>
```

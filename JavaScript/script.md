# script

![image-20220329084449645](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202203290844743.png)

## script 的常用标签

![image-20220329084545991](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202203290845065.png)

首先我们先来看一下`` <script> `标签 的几个重要特性：

- script标签的会阻止文档渲染。相关脚本会立即下载并执行。（不带defer或async属性的情况下）
- document.currentScript 可以获得当前正在运行的脚本(Chrome 29+, FF4+)。
- 脚本顺序再默认情况下和script标签出现的顺序一致。
- script标签是没有跨域问题，可以加载任何网站的脚本，和img标签非常类似，所以通常也会用来解决跨域问题，就是人们通常所说的JSONP。
- 当 type = “moudle” 的时候， 代码会被识别为ES6模块， 才可以使用 import 和 export
- 同时具有行内代码和src标签的时候， 会忽视行内代码

`<script>` 一般都放在页面的 `<head>` 元素中, 这也意味着必须等到全部的JavaScript代码都被下载解析执行后，才开始呈现页面的内容

如果JavaScript代码太大的话，可能会让浏览器显示页面出现延迟的情况，所以通常可以把``<script>``放在`<body>`的最后位置，这样的话会使在解析JavaScript代码前就已经把页面显示出来，减少用户的等待时间

## async属性

async属性是HTML5的新特性，这意味着其兼容性并不乐观（IE10+）。好在 IE 浏览器将在2022年被微软抛弃了

async表示该script标签并不柱塞，也不同步执行。

浏览器只需要在脚本下载完毕后再执行即可， 即不必柱塞页面渲染等待该脚本的下载和执行。

考究这个属性产生的原有，其实有大量的脚本加载器在做这样的事情：

```js
var script = document.createElement("script");
script.src = "file.js";
document.body.appendChild(script);
// 那么我们不难想象，通过脚本异步插入的script标签达到的效果和带async属性的script标签是一样的。
// 换句话说，由上面这种方式脚本插入的script标签默认是async的。

// 我们可以在上面的基础上把它设置为同步方式
script.async = false;

// 但是通过这种方式获取 script， 会影响资源队列的优先级
```

##  defer属性

带有defer属性的脚本，同样会推迟脚本的执行，并且不会阻止文档解析。

defer属性是会确保脚本在文档解析完毕后执行的。

即使这个脚本在文档解析过程中就已经下载完毕变成可执行的状态，

浏览器也会推迟这个脚本的执行，直到文档解析完毕，并在DOMContentLoaded之前。

同时，带有defer的脚本彼此之间，能保证其执行顺序。

## noscript

`noscript`标签是一个相当古老的标签，其被引入的最初目的是帮助老旧浏览器的平滑升级更替，因为早期的浏览器并不能支持 JavaScript。noscript 标签在不支持JavaScript 的浏览器中显示替代的内容。这个元素可以包含任何 HTML 元素。这个标签的用法也非常简单：

```xml
<noscript>
  <p>本页面需要浏览器支持（启用）JavaScript</p>
</noscript>
```

不过到了现在，浏览器不支持 Javascript 的事情应该已经不会出现了，但是用户也可能因为各种原因而禁用了 Javascript。
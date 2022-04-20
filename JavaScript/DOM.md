# DOM

## 节点操作

### insertAdjacentHTML

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


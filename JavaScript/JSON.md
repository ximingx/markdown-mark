

# JSON

一般我们可以在本地存储使用

1、js对象(数组) --> json对象(数组)：

```javascript
	JSON.stringify(obj/arr)
```

2、json对象(数组) --> js对象(数组)：


```javascript
	JSON.parse(json)
```


上面这两个方法是ES5中提供的。

我们要记住，我们通常说的“json字符串”，只有两种：**json对象、json数组**。

`typeof json字符串`的返回结果是string。


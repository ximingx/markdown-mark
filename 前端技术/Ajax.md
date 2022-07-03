# Ajax

传统网站中存在的问题

- 网速慢的情况下，页面加载时间长，用户只能等待
- 表单提交后，如果一项内容不合格，需要重新填写所有表单内容
- 页面跳转，重新加载页面，造成资源浪费，增加用户等待时间

## 一: Ajax 概述

它是浏览器提供的一套方法，可以实现页面无刷新更新数据，提高用户浏览网站应用的体验。

应用场景

- 页面上拉加载更多数据
- 列表数据无刷新分页
- 表单项离开焦点数据验证
- 搜索框提示文字下拉列表
- 注册时，验证用户名是否存在等。
- 百度地图，可以在页面不刷新的情况下，移动显示不同地点的信息。

### 1. 运行原理

`Ajax `技术需要运行在网站环境中才能生效

`Ajax `相当于浏览器发送请求与接收响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

![image-20220418191914223](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204181919265.png)

### 2. JSON 数据格式

`JSON`不是一种语言,而是一种信息的特定格式,与`XML`类似,主要用于数据的传输与交换.

```js
// 将 json 字符串转换为json对象 
JSON.parse() 
// 将 json 对象 转换为json字符串
JSON.stringify()
```

> `toJSON`

在序列化的时候返回自己希望的数据, 可以为数据对象添加`toJSON`的方法

```js
var person = {
    name: '',
    sex: 0,
    age: 20,
    toJSON: function () {
        return {
            name: this.name||"匿名",
            sex: this.sex===0?"男人":"女人",
            age:this.age>=18?"成年人":"未成年人",
        }
    }
}

console.log(JSON.stringify(person));
// {"name":"匿名","sex":"男人","age":"成年人"}
```

### 3. 响应的数据格式

在真实的项目中，服务器端大多数情况下会以 `JSON `对象作为响应数据的格式。当客户端拿到响应数据时，要将 `JSON `数据和 `HTML `字符串进行拼接，然后将拼接的结果展示在页面中。

在 `http `请求与响应的过程中，无论是请求参数还是响应内容，如果是对象类型，最终都会被转换为对象字符串进行传输。

### 4. XMLHttpRequest

`xhr`对象是基于浏览器自带的`XMLHttpRequest`构造方法创建的, 通过 `xhr` 我们可以进行 `ajax` 请求

这是 `ajax` 请求的第一步

```JS
var xhr = new XMLHttpRequest();
```

早期`IE`创建`Ajax`

```javascript
var xhr =new ActiveXObject(“Microsoft.XMLHTTP”);
```

### 5. 传递请求参数

`xhr.open(method,urL,async)`

`async` `true`代表异步,`false`代表同步 (默认是异步)

>数据格式为字符串

```js
// > get
// 一般可以使用拼接字符串的方式
xhr.open('get', 'http://www.example.com?name=zhangsan&age=20');
// GET 可以不用在 send 中添加信息，在请求的 URL 中写入即可
xhr.send();

// > post 
xhr.open('post', 'http://www.example.com');
// 头信息设置只需要在POST发送的时候设置即可，模拟表单的POST头信息
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded') 
// POST发送需要将信息填入send
xhr.send('name=zhangsan&age=20');
```

>数据格式为`json对象`

```js
// > get
// get 请求是不能提交 json 对象数据格式的

// > post 
// 在请求头中指定 Content-Type 属性的值是 application/json，告诉服务器端当前请求参数的格式是 json。
xhr.open('post', 'http://www.example.com');
xhr.setRequestHeader('Content-Type', 'application/json') 
xhr.send(JSON.stringify({
    name: "ximingx"
}));

// 传统网站的表单提交也是不支持 json 对象数据格式的。
```

### 6. Ajax 状态码

 在创建`ajax`对象，配置`ajax`对象，发送请求，以及接收完服务器端响应数据，这个过程中的每一个步骤都会对应一个数值，这个数值就是`ajax`状态码。

| `ajax`状态码 | 含义 |
| ---- | ---- |
| `0` | 请求未初始化(还没有调用`open()`) |
| `1` | 请求已经建立，但是还没有发送(还没有调用`send()`) |
| `2` | 请求已经发送 |
| `3` | 请求正在处理中，通常响应中已经有部分数据可以用了 |
| `4` | 响应已经完成，可以获取并使用服务器的响应了 |

> 获取`Ajax状态码`

```js
 xhr.readyState // 获取Ajax状态码
```

> 监听事件状态的改变 `onreadystatechange `

当 `Ajax 状态码`发生变化时将自动触发该事件。在事件处理函数中可以获取` Ajax 状态码`并对其进行判断，当状态码为 4 时就可以通过 `xhr.responseText` 获取服务器端的响应数据了。`xhr.status`是服务器返回的状态响应码

```js
 // 当Ajax状态码发生变化时
 xhr.onreadystatechange = function () {
     // 判断当Ajax状态码为4时
     if (xhr.readyState == 4) {
         //检测服务器是否正确响应
         if(xhr.status == 200){
 			// 获取服务器端的响应数据
         	console.log(xhr.responseText); 
        }
     }
 }
```

### 7. Ajax 封装

```js
function ajax (options) {
	// 默认值
	var defaults = {
		type: 'get',
		url: '',
		async: true,
		data: {},
		header: {
			'Content-Type': 'application/x-www-form-urlencoded'
		},
		success: function () {},
		error: function () {}
	}
	// 使用用户传递的参数替换默认值参数
	Object.assign(defaults, options);
	// 创建ajax对象
	var xhr = new XMLHttpRequest();
	// 参数拼接变量
	var params = '';
	// 循环参数
	for (var attr in defaults.data) {
		// 参数拼接
		params += attr + '=' + defaults.data[attr] + '&';
		// 去掉参数中最后一个&
		params = params.substr(0, params.length-1)
	}
	// 如果请求方式为get
	if (defaults.type == 'get') {
		// 将参数拼接在url地址的后面
		defaults.url += '?' + params;
	}

	// 配置ajax请求
	xhr.open(defaults.type, defaults.url, defaults.async);
	// 如果请求方式为post
	if (defaults.type == 'post') {
		// 设置请求头
		xhr.setRequestHeader('Content-Type', defaults.header['Content-Type']);
		// 如果想服务器端传递的参数类型为json
		if (defaults.header['Content-Type'] == 'application/json') {
			// 将json对象转换为json字符串
			xhr.send(JSON.stringify(defaults.data))
		}else {
			// 发送请求
			xhr.send(params);
		}
	} else {
		xhr.send();
	}
	// 请求加载完成
	xhr.onload = function () {
		// 获取服务器端返回数据的类型
		var contentType = xhr.getResponseHeader('content-type');
		// 获取服务器端返回的响应数据
		var responseText = xhr.responseText;
		// 如果服务器端返回的数据是json数据类型
		if (contentType.includes('application/json')) {
			// 将json字符串转换为json对象
			responseText = JSON.parse(responseText);
		}
		// 如果请求成功
		if (xhr.status == 200) {
			// 调用成功回调函数, 并且将服务器端返回的结果传递给成功回调函数
			defaults.success(responseText, xhr);
		} else {
			// 调用失败回调函数并且将xhr对象传递给回调函数
			defaults.error(responseText, xhr);
		} 
	}
	// 当网络中断时
	xhr.onerror = function () {
		// 调用失败回调函数并且将xhr对象传递给回调函数
		defaults.error(xhr);
	}
}
```

```js
  ajax({
        url: 'http://localhost:3000/api/users',
        method: 'GET',
        data: {
            name: '张三',
            age: 18
        },
        header: {
            // 'Content-Type': 'application/json'
            'Content-Type': 'application/x-www-form-urlencoded'
        },
        success: function (data) {
            console.log(data);
        },
        error: function (status,xhr) {
            console.log(status,xhr);
        }
    });
```









## 二: JSONP

### 1. Ajax请求限制

`Ajax `只能向自己的服务器发送请求。

比如现在有一个A网站、有一个B网站，A网站中的 `HTML` 文件只能向A网站服务器中发送 `Ajax `请求，B网站中的 `HTML `文件只能向 B 网站中发送 `Ajax `请求，但是 A 网站是不能向 B 网站发送 `Ajax`请求的，同理，B 网站也不能向 A 网站发送 ``Ajax``请求。

### 2. 什么是同源

如果两个页面拥有相同的协议、域名和端口，那么这两个页面就属于同一个源，其中只要有一个不相同，就是不同源。

- http://www.example.com/dir/page.html 以他为例

- http://www.example.com/dir2/other.html：同源
- http://example.com/dir/other.html：不同源（域名不同）
- http://v2.www.example.com/dir/other.html：不同源（域名不同）
- http://www.example.com:81/dir/other.html：不同源（端口不同）
- https://www.example.com/dir/page.html：不同源（协议不同）

同源政策是为了保证用户信息的安全，防止恶意的网站窃取数据。最初的同源政策是指 A 网站在客户端设置的 `Cookie`，B网站是不能访问的。

随着互联网的发展，同源政策也越来越严格，在不同源的情况下，其中有一项规定就是无法向非同源地址发送`Ajax 请求`，如果请求，浏览器就会报错。

### 3. 解决方案

`JSONP `就是一种跨域的解决方案, 是利用浏览器加载文件的操作实现的

我们在使用浏览器加载文件的时候是不会受到同源限制的

`JSONP`请求数据的时候服务器返回的是一段可以执行的`JS`代码

### 4. JSONP 解决同源限制

> 解决方案

不同源的服务器端请求地址写在 `script `标签的 `src `属性中

```html
 <script src="www.example.com"></script>
 <script src=“https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
```

服务器端响应数据必须是一个函数的调用，真正要发送给客户端的数据需 要作为函数调用的参数。

```js
 const data = 'fn({name: "张三", age: "20"})';
 res.send(data);
```

在客户端全局作用域下定义函数 `fn`

```js
 function fn (data) { }
```

在 `fn `函数内部对服务器端返回的数据进行处理

```js
 function fn (data) { console.log(data); }
```

> 使用示例

```js
// 获取按钮
var btn = document.getElementById('btn');
// 为按钮添加点击事件
btn.onclick = function () {
   // 创建script标签
   var script = document.body.createElement('script');
   // 设置src属性
   script.src = 'http://localhost:3001/better?callback=fn2';
   // 将script标签追加到页面中
   document.body.appendChild(script);
}
```

# Ajax

传统网站中存在的问题

- 网速慢的情况下，页面加载时间长，用户只能等待
- 表单提交后，如果一项内容不合格，需要重新填写所有表单内容
- 页面跳转，重新加载页面，造成资源浪费，增加用户等待时间

## Ajax 概述

它是浏览器提供的一套方法，**可以实现页面无刷新更新数据**，提高用户浏览网站应用的体验。

**应用场景**

- 页面上拉加载更多数据
- 列表数据无刷新分页
- 表单项离开焦点数据验证
- 搜索框提示文字下拉列表

### 运行原理

Ajax 技术需要运行在网站环境中才能生效

**Ajax 相当于浏览器发送请求与接收响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据**，从而提高用户体验。

![image-20220418191914223](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204181919265.png)

### Ajax 的实现步骤

```html
	<script type="text/javascript">
		// 1.创建ajax对象
		var xhr = new XMLHttpRequest();
		// 2.告诉Ajax对象要向哪发送请求，以什么方式发送请求
		// 1)请求方式 2)请求地址
		xhr.open('get', 'http://localhost:3000/first');
		// 3.发送请求
		xhr.send();
		// 4.获取服务器端响应到客户端的数据
		xhr.onload = function (){
			console.log(xhr.responseText)
		}
	</script>
```

### 响应的数据格式

在真实的项目中，服务器端大多数情况下会以 JSON 对象作为响应数据的格式。当客户端拿到响应数据时，要将 JSON 数据和 HTML 字符串进行拼接，然后将拼接的结果展示在页面中。

在 http 请求与响应的过程中，无论是请求参数还是响应内容，如果是对象类型，最终都会被转换为对象字符串进行传输。

```js
// 将 json 字符串转换为json对象 
JSON.parse() 
// 将 json 对象 转换为json字符串
JSON.stringify()
```

### 传递请求参数

方法一:

```js
// get
// 一般可以使用拼接字符串的方式
xhr.open('get', 'http://www.example.com?name=zhangsan&age=20');
xhr.send();

// post 
xhr.open('post', 'http://www.example.com');
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded') 
xhr.send('name=zhangsan&age=20');
```

方法二

```js
// get
// get 请求是不能提交 json 对象数据格式的

// post 
// 在请求头中指定 Content-Type 属性的值是 application/json，告诉服务器端当前请求参数的格式是 json。
xhr.open('post', 'http://www.example.com');
xhr.setRequestHeader('Content-Type', 'application/json') 
xhr.send(JSON.stringify({}));

// 传统网站的表单提交也是不支持 json 对象数据格式的。
```

### Ajax 状态码

 在创建ajax对象，配置ajax对象，发送请求，以及接收完服务器端响应数据，这个过程中的每一个步骤都会对应一个数值，这个数值就是ajax状态码。

- 0: a请求未初始化(还没有调用open()) 
- 1: 请求已经建立，但是还没有发送(还没有调用send())
- 2: 请求已经发送
- 3: 请求正在处理中，通常响应中已经有部分数据可以用了
- 4: 响应已经完成，可以获取并使用服务器的响应了

```js
 xhr.readyState // 获取Ajax状态码
```

onreadystatechange 事件

当 Ajax 状态码发生变化时将自动触发该事件。在事件处理函数中可以获取 Ajax 状态码并对其进行判断，当状态码为 4 时就可以通过 xhr.responseText 获取服务器端的响应数据了。

```js
 // 当Ajax状态码发生变化时
 xhr.onreadystatechange = function () {
     // 判断当Ajax状态码为4时
     if (xhr.readyState == 4) {
         // 获取服务器端的响应数据
         console.log(xhr.responseText); 
     }
 }
xhr.send(JSON.stringify({}));
```

两种获取服务器端响应方式的区别

| **区别描述**           | **onload****事件** | **onreadystatechange****事件** |
| ---------------------- | ------------------ | ------------------------------ |
| 是否兼容IE低版本       | 不兼容             | 兼容                           |
| 是否需要判断Ajax状态码 | 不需要             | 需要                           |
| 被调用次数             | 一次               | 多次                           |

### Ajax 错误处理

- 网络畅通，服务器端能接收到请求，服务器端返回的结果不是预期结果。
  可以判断服务器端返回的状态码，分别进行处理。xhr.status 获取http状态码

- 网络畅通，服务器端没有接收到请求，返回404状态码。
  检查请求地址是否错误。

- 网络畅通，服务器端能接收到请求，服务器端返回500状态码。
  服务器端错误，找后端程序员进行沟通。

- 网络中断，请求无法发送到服务器端。
  会触发xhr对象下面的onerror事件，在onerror事件处理函数中对错误进行处理。

### 低版本 IE 浏览器的缓存问题

问题：在低版本的 IE 浏览器中，Ajax 请求有严重的缓存问题，即在请求地址不发生变化的情况下，只有第一次请求会真正发送到服务器端，后续的请求都会从浏览器的缓存中获取结果。即使服务器端的数据更新了，客户端依然拿到的是缓存中的旧数据。

**解决方案：在请求地址的后面加请求参数，保证每一次请求中的请求参数的值不相同。** 

```js
xhr.open('get', 'http://www.example.com?t=' + Math.random());
```

### Ajax 封装

问题：发送一次请求代码过多，发送多次请求代码冗余且重复。

解决方案：将请求代码封装到函数中，发请求时调用函数即可。

```js
 ajax({ 
     type: 'get',
     url: 'http://www.example.com',
     success: function (data) { 
         console.log(data);
     }
 })
```

## 编程扩展

使用模板引擎提供的模板语法，可以将数据和 HTML 拼接起来。

### 模板引擎

1.   下载 art-template 模板引擎库文件并在 HTML 页面中引入库文件

```html
 <script src="./js/template-web.js"></script>
```

2. 准备 art-template 模板

```html
 <script id="tpl" type="text/html">
     <div class="box"></div>
 </script>
```

3.   告诉模板引擎将哪一个模板和哪个数据进行拼接

```js
 var html = template('tpl', {username: 'zhangsan', age: '20'});
```

4. 将拼接好的html字符串添加到页面中

```js
 document.getElementById('container').innerHTML = html;
```

5. 通过模板语法告诉模板引擎，数据和html字符串要如何拼接

```html
 <script id="tpl" type="text/html">
     <div class="box"> {{ username }} </div>
 </script>
```

### 邮箱验证

- 获取文本框并为其添加离开焦点事件
- 离开焦点时，检测用户输入的邮箱地址是否符合规则
- 如果不符合规则，阻止程序向下执行并给出提示信息
- 向服务器端发送请求，检测邮箱地址是否被别人注册
- 根据服务器端返回值决定客户端显示何种提示信息

```js
/^[A-Za-z\d]+([-_.][A-Za-z\d]+)*@([A-Za-z\d]+[-.])+[A-Za-z\d]{2,4}$/
```

### 搜索框内容自动提示

- 获取搜索框并为其添加用户输入事件
- 获取用户输入的关键字
- 向服务器端发送请求并携带关键字作为请求参数
- 将响应数据显示在搜索框底部

### 省市区三级联动

- 通过接口获取省份信息
- 使用JavaScript获取到省市区下拉框元素
- 将服务器端返回的省份信息显示在下拉框中
- 为下拉框元素添加表单值改变事件（onchange）
- 当用户选择省份时，根据省份id获取城市信息
- 当用户选择城市时，根据城市id获取县城信息

### FormData 

- 模拟HTML表单，相当于将HTML表单映射成表单对象，自动将表单对象中的数据拼接成请求参数的格式。

- 异步上传二进制文件

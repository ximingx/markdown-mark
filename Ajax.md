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

| **区别描述**           | **onload事件** | **onreadystatechange事件** |
| ---------------------- | -------------- | -------------------------- |
| 是否兼容IE低版本       | 不兼容         | 兼容                       |
| 是否需要判断Ajax状态码 | 不需要         | 需要                       |
| 被调用次数             | 一次           | 多次                       |

### Ajax 错误处理

- 网络畅通，服务器端能接收到请求，服务器端返回的结果不是预期结果。
  可以判断服务器端返回的状态码，分别进行处理。****
- 网络畅通，服务器端没有接收到请求，返回404状态码。
  检查请求地址是否错误。
- 网络畅通，服务器端能接收到请求，服务器端返回500状态码。
  服务器端错误，找后端程序员进行沟通。
- 网络中断，请求无法发送到服务器端。
  **会触发xhr对象下面的onerror事件，在onerror事件处理函数中对错误进行处理。**
- **xhr.status 获取http状态码**

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

## 编程扩展

使用模板引擎提供的模板语法，可以将数据和 HTML 拼接起来。

### 客户端模板引擎

[https://aui.github.io/art-template/zh-cn/docs/installation.html](https://aui.github.io/art-template/zh-cn/docs/installation.html)

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

```js
		var emailInp = document.getElementById('email');
		var info = document.getElementById('info');

		// 当文本框离开焦点以后
		emailInp.onblur = function () {
			// 获取用户输入的邮箱地址
			var email = this.value;
			// 验证邮箱地址的正则表达式
			var reg = /^[A-Za-z\d]+([-_.][A-Za-z\d]+)*@([A-Za-z\d]+[-.])+[A-Za-z\d]{2,4}$/;
			// 如果用户输入的邮箱地址不符合规则
			if (!reg.test(email)) {
				// 给出用户提示
				info.innerHTML = '请输入符合规则的邮箱地址';
				// 让提示信息显示为错误提示信息的样式
				info.className = 'bg-danger';
				// 阻止程序向下执行
				return;
			}

			// 向服务器端发送请求
			ajax({
				type: 'get',
				url: 'http://localhost:3000/verifyEmailAdress',
				data: {
					email: email
				},
				success: function (result) {
					console.log(result);
					info.innerHTML = result.message;
					info.className = 'bg-success';
				},
				error: function (result) {
					console.log(result)
					info.innerHTML = result.message;
					info.className = 'bg-danger';
				}
			});

		}
```

```js
// 邮箱地址验证
app.get('/verifyEmailAdress', (req, res) => {
	// 接收客户端传递过来的邮箱地址
	const email = req.query.email;
	// 判断邮箱地址注册过的情况
	if (email == 'itheima@itcast.cn') {
		// 设置http状态码并对客户端做出响应
		res.status(400).send({message: '邮箱地址已经注册过了, 请更换其他邮箱地址'});
	} else {
		// 邮箱地址可用的情况
		// 对客户端做出响应
		res.send({message: '恭喜, 邮箱地址可用'});
	} 
});
```

### 搜索框内容自动提示

- 获取搜索框并为其添加用户输入事件
- 获取用户输入的关键字
- 向服务器端发送请求并携带关键字作为请求参数
- 将响应数据显示在搜索框底部

```js
		// 获取搜索框
		var searchInp = document.getElementById('search');
		// 获取提示文字的存放容器
		var listBox = document.getElementById('list-box');
		// 存储定时器的变量
		var timer = null;
		// 当用户在文本框中输入的时候触发
		searchInp.oninput = function () {
			// 清除上一次开启的定时器
			clearTimeout(timer);
			// 获取用户输入的内容
			var key = this.value;
			// 如果用户没有在搜索框中输入内容
			if (key.trim().length == 0) {
				// 将提示下拉框隐藏掉
				listBox.style.display = 'none';
				// 阻止程序向下执行
				return;
			}

			// 开启定时器 让请求延迟发送
			timer = setTimeout(function () {
				// 向服务器端发送请求
				// 向服务器端索取和用户输入关键字相关的内容
				ajax({
					type: 'get',
					url: 'http://localhost:3000/searchAutoPrompt',
					data: {
						key: key
					},
					success: function (result) {
						// 使用模板引擎拼接字符串
						var html = template('tpl', {result: result});
						// 将拼接好的字符串显示在页面中
						listBox.innerHTML = html;
						// 显示ul容器
						listBox.style.display = 'block';
					}
				})
			}, 1000)
			
		}
```

```js
app.get('/searchAutoPrompt', (req, res) => {
	// 搜索关键字
	const key = req.query.key;
	// 提示文字列表
	const list = [
		'黑马程序员',
		'黑马程序员官网',
		'黑马程序员顺义校区',
		'黑马程序员学院报名系统',
		'传智播客',
		'传智博客前端与移动端开发',
		'传智播客大数据',
		'传智播客python',
		'传智播客java',
		'传智播客c++',
		'传智播客怎么样'
	];
	// 搜索结果
	let result = list.filter(item => item.includes(key));
	// 将查询结果返回给客户端
	res.send(result);
});
```

### 省市区三级联动

- 通过接口获取省份信息
- 使用JavaScript获取到省市区下拉框元素
- 将服务器端返回的省份信息显示在下拉框中
- 为下拉框元素添加表单值改变事件（onchange）
- 当用户选择省份时，根据省份id获取城市信息
- 当用户选择城市时，根据城市id获取县城信息

```js
		// 获取省市区下拉框元素
		var province = document.getElementById('province');
		var city = document.getElementById('city');
		var area = document.getElementById('area');
		// 获取省份信息
		ajax({
			type: 'get',
			url: 'http://localhost:3000/province',
			success: function (data) {
				// 将服务器端返回的数据和html进行拼接
				var html = template('provinceTpl', {province: data});
				// 将拼接好的html字符串显示在页面中
				province.innerHTML = html;
			}
		});

		// 为省份的下拉框添加值改变事件
		province.onchange = function () {
			// 获取省份id
			var pid = this.value;

			// 清空县城下拉框中的数据
			var html = template('areaTpl', {area: []});
			area.innerHTML = html;

			// 根据省份id获取城市信息
			ajax({
				type: 'get',
				url: '/cities',
				data: {
					id: pid
				},
				success: function (data) {
					var html = template('cityTpl', {city: data});
					city.innerHTML = html;
				}
			})
		};

		// 当用户选择城市的时候
		city.onchange = function () {
			// 获取城市id
			var cid = this.value;
			// 根据城市id获取县城信息
			ajax({
				type: 'get',
				url: 'http://localhost:3000/areas',
				data: {
					id: cid
				},
				success: function(data) {
					var html = template('areaTpl', {area: data});
					area.innerHTML = html;
				}
			})
		}

```

### FormData 

- 模拟HTML表单，相当于将HTML表单映射成表单对象，自动将表单对象中的数据拼接成请求参数的格式。
- 异步上传二进制文件

1.   准备 HTML 表单

```html
<form id="form">
     <input type="text" name="username" />
     <input type="password" name="password" />
     <input type="button"/>
</form>
```

2.   将 HTML 表单转化为 formData 对象

```js
var form = document.getElementById('form'); 
var formData = new FormData(form);
```

3. 提交表单对象

```js
  xhr.send(formData);
  xhr.onload
```

注意：

- **Formdata 对象不能用于 get 请求**，因为对象需要被传递到 send 方法中，而 get 请求方式的请求参数只能放在请求地址的后面。
- 服务器端 bodyParser 模块不能解析 formData 对象表单数据，**我们需要使用 formidable 模块进行解析。**

1.   获取表单对象中属性的值

```JS
 formData.get('key');
```

2. 设置表单对象中属性的值

```JS
 formData.set('key', 'value');
```

3. 删除表单对象中属性的值

```JS
 formData.delete('key');
```

4.   向表单对象中追加属性值

```JS
 formData.append('key', 'value');
```

注意：set 方法与 append 方法的区别是，在属性名已存在的情况下，set 会覆盖已有键名的值，append会保留两个值。

二进制文件上传

```html
<input type="file" id="file"/>
```

```js
 var file = document.getElementById('file')
// 当用户选择文件的时候
 file.onchange = function () {
     // 创建空表单对象
     var formData = new FormData();
     // 将用户选择的二进制文件追加到表单对象中
     formData.append('attrName', this.files[0]);
     // 配置ajax对象，请求方式必须为post
     xhr.open('post', 'www.example.com');
     xhr.send(formData);
 }
```

```js
 // 当用户选择文件的时候
 file.onchange = function () {
     // 文件上传过程中持续触发onprogress事件
     xhr.upload.onprogress = function (ev) {
         // 当前上传文件大小/文件总大小 再将结果转换为百分数
         // 将结果赋值给进度条的宽度属性 
         bar.style.width = (ev.loaded / ev.total) * 100 + '%';
     }
 }
```

```js
 xhr.onload = function () {
     var result = JSON.parse(xhr.responseText);
     var img = document.createElement('img');
     img.src = result.src;
     img.onload = function () {
         document.body.appendChild(this);
     }
 }
```

```js
const formidable = require('formidable');

app.post('/formData', (req, res) => {
	// 创建formidable表单解析对象
	const form = new formidable.IncomingForm();
	// 解析客户端传递过来的FormData对象
	form.parse(req, (err, fields, files) => {
		res.send(fields);
	});
});

// 实现文件上传的路由
app.post('/upload', (req, res) => {
	// 创建formidable表单解析对象
	const form = new formidable.IncomingForm();
	// 设置客户端上传文件的存储路径
	form.uploadDir = path.join(__dirname, 'public', 'uploads');
	// 保留上传文件的后缀名字
	form.keepExtensions = true;
	// 解析客户端传递过来的FormData对象
	form.parse(req, (err, fields, files) => {
		// 将客户端传递过来的文件地址响应到客户端
		res.send({
			path: files.attrName.path.split('public')[1]
		});
	});
});
```

### Ajax请求限制

Ajax 只能向自己的服务器发送请求。比如现在有一个A网站、有一个B网站，A网站中的 HTML 文件只能向A网站服务器中发送 Ajax 请求，B网站中的 HTML 文件只能向 B 网站中发送 Ajax 请求，但是 A 网站是不能向 B 网站发送 Ajax请求的，同理，B 网站也不能向 A 网站发送 Ajax请求。

### 什么是同源

如果两个页面拥有相同的协议、域名和端口，那么这两个页面就属于同一个源，其中只要有一个不相同，就是不同源。

- http://www.example.com/dir/page.html

- http://www.example.com/dir2/other.html：同源
- http://example.com/dir/other.html：不同源（域名不同）
- http://v2.www.example.com/dir/other.html：不同源（域名不同）
- http://www.example.com:81/dir/other.html：不同源（端口不同）
- https://www.example.com/dir/page.html：不同源（协议不同）

同源政策是为了保证用户信息的安全，防止恶意的网站窃取数据。最初的同源政策是指 A 网站在客户端设置的 Cookie，B网站是不能访问的。

随着互联网的发展，同源政策也越来越严格，在不同源的情况下，其中有一项规定就是无法向非同源地址发送Ajax 请求，如果请求，浏览器就会报错。

### JSONP 解决同源限制

1.   将不同源的服务器端请求地址写在 script 标签的 src 属性中

```html
 <script src="www.example.com"></script>
 <script src=“https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
```

2.   服务器端响应数据必须是一个函数的调用，真正要发送给客户端的数据需 要作为函数调用的参数。

```js
 const data = 'fn({name: "张三", age: "20"})';
 res.send(data);
```

3.   在客户端全局作用域下定义函数 fn

```js
 function fn (data) { }
```

4.   在 fn 函数内部对服务器端返回的数据进行处理

```js
 function fn (data) { console.log(data); }
```

### 使用示例

```js
// 获取按钮
var btn = document.getElementById('btn');
// 为按钮添加点击事件
btn.onclick = function () {
   // 创建script标签
   var script = document.createElement('script');
   // 设置src属性
   script.src = 'http://localhost:3001/better?callback=fn2';
   // 将script标签追加到页面中
   document.body.appendChild(script);
   // 为script标签添加onload事件
   script.onload = function () {
      // 将body中的script标签删除掉
      document.body.removeChild(script);
   }
}
```

### JSONP 代码优化

- 客户端需要将函数名称传递到服务器端。
- 将 script 请求的发送变成动态请求。
- 封装 jsonp 函数，方便请求发送。
- 服务器端代码优化之 res.jsonp 方法。

```js
		var btn1 = document.getElementById('btn1');
		var btn2 = document.getElementById('btn2');
		// 为按钮添加点击事件
		btn1.onclick = function () {
			jsonp({
				// 请求地址
				url: 'http://localhost:3001/better',
				data: {
					name: 'lisi',
					age: 30
				},
				success: function (data) {
					console.log(123)
					console.log(data)
				}
			})
		}

		btn2.onclick = function () {
			jsonp({
				// 请求地址
				url: 'http://localhost:3001/better',
				success: function (data) {
					console.log(456789)
					console.log(data)
				}
			})
		}

		function jsonp (options) {
			// 动态创建script标签
			var script = document.createElement('script');
			// 拼接字符串的变量
			var params = '';

			for (var attr in options.data) {
				params += '&' + attr + '=' + options.data[attr];
			}
			
			// myJsonp0124741
			var fnName = 'myJsonp' + Math.random().toString().replace('.', '');
			// 它已经不是一个全局函数了
			// 我们要想办法将它变成全局函数
			window[fnName] = options.success;
			// 为script标签添加src属性
			script.src = options.url + '?callback=' + fnName + params;
			// 将script标签追加到页面中
			document.body.appendChild(script);
			// 为script标签添加onload事件
			script.onload = function () {
				document.body.removeChild(script);
			}
		}

```

### CORS 跨域资源共享

CORS：全称为 Cross-origin resource sharing，即跨域资源共享，它允许浏览器向跨域服务器发送 Ajax 请求，克服了 Ajax 只能同源使用的限制。

```js
app.use(function(, req, res, next) {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
  next()
});
```

### $.ajax()

```js
			$.ajax({
				// 请求方式
			    type: 'post',
				// 请求地址
			    url: '/user',
                 data: JSON.striify({
                     
                 }),
                 contenType: "application/json"
				// 在请求发送之前调用
				beforeSend: function () {
					alert('请求不会被发送')
					// 请求不会被发送
					return false;
				},
				// 请求成功以后函数被调用
				success: function (response) {
					// response为服务器端返回的数据
					// 方法内部会自动将json字符串转换为json对象
					console.log(response);
				}
                  error: function (xhr) {
					console.log(xhr);
				}
			})
```


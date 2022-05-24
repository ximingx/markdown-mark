#  Function

函数：就是将一些功能或语句进行**封装**，在需要的时候，通过**调用**的形式，执行这些语句。

- **函数也是一个对象**

- 使用`typeof`检查一个函数对象时，会返回 `function`

**函数的作用**：

- 将大量重复的语句抽取出来，写在函数里，以后需要这些语句的时候，可以直接调用函数，避免重复劳动。

- **简化编程，让编程模块化。高内聚、低耦合。**

来看个例子：

```javascript
console.log("你好");
sayHello();	// 调用函数

// 定义函数
function sayHello(){
	console.log("欢迎");
	console.log("welcome");
}
```

## 函数的定义/声明

### 方式一：利用函数关键字自定义函数（命名函数）

使用`函数声明`来创建一个函数（也就是 function 关键字）。语法：

```javascript
function 函数名([形参1,形参2...形参N]){  // 备注：语法中的中括号，表示“可选”
	语句...
}
```

举例：

```javascript
function fun1(a, b){
	return a+b;
}
```

解释如下：

- function：是一个关键字。中文是“函数”、“功能”。

- 函数名字：命名规定和变量的命名规定一样。只能是字母、数字、下划线、美元符号，不能以数字开头。

- 参数：可选。

- 大括号里面，是这个函数的语句。

PS：在有些编辑器中，方法写完之后，我们在方法的前面输入`/**`，然后回车，会发现，注释的格式会自动补齐。

### 方式二：函数表达式（匿名函数）

使用`函数表达式`来创建一个函数。语法：

```javascript
var 变量名  = function([形参1,形参2...形参N]){
	语句....
}
```

举例：

```javascript
var fun2 = function() {
	console.log("我是匿名函数中封装的代码");
};
```

解释如下：


- **上面的 fun2 是变量名，不是函数名。**

- 函数表达式的声明方式跟声明变量类似，只不过变量里面存的是值，而函数表达式里面存的是函数。

- 函数表达式也可以传递参数。

从方式二的举例中可以看出：所谓的“函数表达式”，其实就是将匿名函数赋值给一个变量。

### 方式三：使用构造函数 new Function()

使用构造函数`new Function()`来创建一个对象。这种方式，用的少。

语法：

```javascript
var 变量名/函数名  = new Function('形参1', '形参2', '函数体');
```

注意，Function 里面的参数都必须是**字符串**格式。也就是说，形参也必须放在**字符串**里；函数体也是放在**字符串**里包裹起来，放在 Function 的最后一个参数的位置。

- **所有函数都是 Function 的实例(对象)  **
- **函数也属于对象**

代码举例：

```javascript
var fun3 = new Function('a', 'b', 'console.log("我是函数内部的内容");  console.log(a + b);');

fun3(1, 2); // 调用函数
```

打印结果：

```js
我是函数内部的内容
3
```

**分析**：

方式3的写法很少用，原因如下：

- 不方便书写：写法过于啰嗦和麻烦。

- 执行效率较低：首先需要把字符串转换为 js 代码，然后再执行。

### 总结

1、**所有的函数，都是 `Fuction` 的“实例”**（或者说是“实例对象”）。函数本质上都是通过 new Function 得到的。

2、函数既然是实例对象，那么，**函数也属于“对象”**。还可以通过如下特征，来佐证函数属于对象：

（1）我们直接打印某一个函数，比如 `console.log(fun2)`，发现它的里面有`__proto__`。

（2）我们还可以打印 `console.log(fun2 instanceof Object)`，发现打印结果为 `true`。这说明 fun2 函数就是属于 Object。

## 函数的调用

### 方式1：普通函数的调用

函数调用的语法：

```javascript
函数名();
```

或者：

```js
函数名.call();
```

代码举例：

```javascript
/* 1. 普通函数 */
function fn1() {
	console.log('我是函数体里面的内容1');
}

function fn2() {
	console.log('我是函数体里面的内容2');
}

fn1(); // 调用函数


// call() 方法调用, 文章下面会讲到
fn2.call(); // 调用函数
```

### 方式2：通过对象的方法来调用

```javascript
/* 2. 对象的方法 */
var obj = {
	a: 'qianguyihao',
	fn2: function() {
		console.log('千古壹号，永不止步!');
	},
};

obj.fn2(); // 调用函数
```

如果一个函数是作为一个对象的属性保存，那么，我们称这个函数是这个对象的**方法**。


### 方式3：立即执行函数

代码举例：

```javascript
(function() {
	console.log('我是立即执行函数');
})();
```

立即执行函数在定义后，会自动调用。

### 方式4：通过构造函数来调用

代码举例：

```javascript
/* 3. 构造函数*/
function Star() {};
new Star();
```

这种方式用得不多。

### 方式5：绑定事件函数

代码举例：


```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <div id="btn">我是按钮，请点击我</div>

        <script>
            var btn = document.getElementById('btn');
            /* 4. 绑定事件函数 */
            btn.onclick = function() {
                console.log('点击按钮后，要做的事情');
            };
        </script>
    </body>
</html>

```

### 方式6：定时器函数

代码举例：（每间隔一秒，将 数字 加1）

```javascript
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
```

这里涉及到定时器的知识点。

## 形参和实参

**形参：**

- 概念：形式上的参数。定义函数时传递的参数，当时并不知道是什么值。

- 定义函数时，可以在函数的`()`中来指定一个或多个形参。

- 多个形参之间使用`,`隔开，声明形参就相当于在函数内部声明了对应的变量，但是并不赋值。

**实参**：

- 概念：实际上的参数。调用函数时传递的参数，实参将会传递给函数中对应的形参。

- 在调用函数时，可以在函数的 `()`中指定实参。

注意：实际参数和形式参数的个数，一般要相同。

举例：

```javascript
// 调用函数
sum(3,4);
sum("3",4);
sum("Hello","World");

// 定义函数：求和
function sum(a, b) {
	console.log(a + b);
}
```

控制台输出结果：

```js
7
34
helloworld
```

### 实参的类型

函数的实参可以是任意的数据类型。

调用函数时，解析器不会检查实参的类型，所以要注意，是否有可能会接收到非法的参数，如果有可能则需要对参数进行类型的检查。

### 实参的数量

调用函数时，解析器也不会检查实参的数量。

- 如果实参的数量多余形参的数量，多余实参不会被赋值。

- **如果实参的数量少于形参的数量，多余的形参会被定义为 undefined。表达式的运行结果为 NaN。**

代码举例：

```javascript
	function sum(a, b) {
		console.log(a + b);
	}

	sum(1, 2);
	sum(1, 2, 3);
	sum(1);
```

打印结果：

```ja
3

3

NaN
```

注意：在 JS 中，形参的默认值是 undefined。

## 函数的返回值

举例：

```javascript
console.log(sum(3, 4)); // 将函数的返回值打印出来

//函数：求和
function sum(a, b) {
	return a + b;
}
```

return 的作用是结束方法（终止函数）。

### 注意：

- return 的值将会作为函数的执行结果返回，可以定义一个变量，来接收该结果。
- **在函数中，return后的语句都不会执行（函数在执行完 return 语句之后停止并立即退出函数）**
- 如果return语句后不跟任何值，就相当于返回一个undefined
- **如果函数中不写return，则也会返回undefined**
- 返回值可以是任意的数据类型，可以是对象，也可以是函数。
- **return 只能返回一个值。如果用逗号隔开多个值，则以最后一个为准。**

### break、continue、return

- break ：结束当前的循环体（如 for、while）

- continue ：跳出本次循环，继续执行下次循环（如 for、while）

- return ：1、退出循环。2、返回 return 语句中的值，同时结束当前的函数体内的代码，退出当前函数。

## 函数名, 函数体, 函数加载问题

### fn()  和 fn 的区别

- `fn()`：调用函数。调用之后，还获取了函数的返回值。

- `fn`：函数对象。相当于直接获取了整个函数对象。

我们要记住：**函数名 == 整个函数**。举例：

```javascript
//定义fn方法
function fn(){
	alert(1)
};

console.log(fn == fn()); // false
```

**我们知道，当我们在调用一个函数时，通常使用`函数()`这种格式；可如果，我们是直接使用`函数`这种格式，它的作用相当于整个函数。**

**函数的加载问题**：JS加载的时候，只加载函数名，不加载函数体。所以如果想使用内部的成员变量，需要调用函数。

## 立即执行函数

现有匿名函数如下：

```javascript
	function(a, b) {
		console.log("a = " + a);
		console.log("b = " + b);
	};
```

立即执行函数如下：

```javascript
	(function(a, b) {
		console.log("a = " + a);
		console.log("b = " + b);
	})(123, 456);
```

立即执行函数：函数定义完，立即被调用，这种函数叫做立即执行函数。

立即执行函数往往只会执行一次。为什么呢？因为没有变量保存它，执行完了之后，就找不到它了。

## 函数与方法

函数也可以成为对象的属性。**如果一个函数是作为一个对象的属性保存，那么，我们称这个函数是这个对象的方法**。

调用这个函数就说调用对象的方法（method）。函数和方法，有什么本质的区别吗？它只是名称上的区别，并没有其他的区别。

函数举例：

```javascript
	// 调用函数
	fn();
```

方法举例：

```javascript
	// 调用方法
	obj.fn();
```

我们可以这样说，如果直接是`fn()`，那就说明是函数调用。如果是`XX.fn()`的这种形式，那就说明是**方法**调用。

## 类数组 arguments

在调用函数时，浏览器每次都会传递进两个隐含的参数：

- 函数的上下文对象 this

- **封装实参的对象** arguments

例如：

```javascript
function foo() {
    console.log(arguments);
    console.log(typeof arguments);
}

foo();
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/0d5383b246ea4dadbd32cec682e59cde.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)



**arguments 是一个类数组对象，它可以通过索引来操作数据，也可以获取长度。**

**arguments 代表的是实参**。在调用函数时，我们所传递的实参都会在arguments 中保存。

有个讲究的地方是：arguments **只在函数中使用**。

### length 属性

`arguments.length` 可以用来获取**实参的长度**。

> **函数名.length 可以获取形参的个数**

举例：

```javascript
fn(2, 4);
fn(2, 4, 6);
fn(2, 4, 6, 8);

function fn(a, b) {
    console.log(arguments);
    console.log(fn.length); // 获取形参的个数
    console.log(arguments.length); // 获取实参的个数

    console.log('----------------');
}
```

打印结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/97e3a8410cd949299e95c47b4429b67c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


我们即使不定义形参，也可以通过 arguments 来使用实参（只不过比较麻烦）：arguments[0] 表示第一个实参、arguments[1] 表示第二个实参...

### arguments.callee

arguments 里边有一个属性叫做 callee，这个属性对应一个函数对象，就是**当前正在指向的函数对象**。

```javascript
function fun() {
    console.log(arguments.callee == fun); //打印结果为true
}

fun('hello');
```

在使用函数**递归**调用时，推荐使用 arguments.callee 代替函数名本身。

### arguments 可以修改元素

之所以说 arguments 是伪数组，是因为：**arguments 可以修改元素，但不能改变数组的长短**。举例：

```javascript
fn(2, 4);
fn(2, 4, 6);
fn(2, 4, 6, 8);

function fn(a, b) {
    arguments[0] = 99; //将实参的第一个数改为99
    arguments.push(8); //此方法不通过，因为无法增加元素
}
```


### arguments 的使用

当我们不确定有多少个参数传递的时候，可以用 **arguments** 来获取。在 JavaScript 中，arguments 实际上是当前函数的一个**内置对象**。所有函数都内置了一个 arguments 对象**（只有函数才有 arguments 对象）**，arguments 对象中存储了**传递的所有实参**.

arguments的展示形式是一个**伪数组**。伪数组具有以下特点：

- 可以进行遍历；具有数组的 length 属性。

- 按索引方式存储数据。

- 不具有数组的 push()、pop() 等方法。

**代码举例**：利用 arguments 求函数实参中的最大值

代码实现：

```javascript
	function getMaxValue() {
		var max = arguments[0];
		// 通过 arguments 遍历实参
		for (var i = 0; i < arguments.length; i++) {
			if (max < arguments[i]) {
				max = arguments[i];
			}
		}
		return max;
	}

	console.log(getMaxValue(1, 3, 7, 5));

```

## 函数参数默认值

**传统写法**：

```javascript
function fn(param) {
    let p = param || 'hello';
    console.log(p);
}
```

上方代码中，函数体内的写法是：如果 param 不存在，就用 `hello`字符串做兜底。这样写比较啰嗦。

**ES6 写法**：（参数默认值的写法，很简洁）

```javascript
function fn(param = 'hello') {
    console.log(param);
}
```

在 ES6 中定义方法时，我们可以给方法里的参数加一个**默认值**（缺省值）：

-   方法被调用时，如果没有给参数赋值，那就是用默认值；

-   方法被调用时，如果给参数赋值了新的值，那就用新的值。

如下：

```javascript
var fn2 = (a, b = 5) => {
    console.log('haha');
    return a + b;
};
console.log(fn2(1)); //第二个参数使用默认值 5。输出结果：6

console.log(fn2(1, 8)); //输出结果：9
```

**提醒 1**：默认值的后面，不能再有**没有默认值的变量**。比如`(a,b,c)`这三个参数，如果我给 b 设置了默认值，那么就一定要给 c 设置默认值。

**提醒 2**：

我们来看下面这段代码：

```javascript
let x = 'smyh';
function fn(x, y = x) {
    console.log(x, y);
}
fn('vae');
```

注意第二行代码，我们给 y 赋值为`x`，这里的`x`是括号里的第一个参数，并不是第一行代码里定义的`x`。打印结果：`vae vae`。

如果我把第一个参数改一下，改成：

```javascript
let x = 'smyh';
function fn(z, y = x) {
    console.log(z, y);
}
fn('vae');
```

此时打印结果是：`vae smyh`。

## 剩余参数 (rest 运算符)

**剩余参数**允许我们将不确定数量的**剩余的元素**放到一个**数组**中。

比如说，当函数的实参个数大于形参个数时，我们可以将剩余的实参放到一个数组中。

**传统写法**：

ES5 中，在定义方法时，参数要确定个数，如下：（程序会报错）

```javascript
function fn(a, b, c) {
    console.log(a);
    console.log(b);
    console.log(c);
    console.log(d);
}

fn(1, 2, 3);
```

上方代码中，因为方法的参数是三个，但使用时是用到了四个参数，所以会报错：

![](https://img-blog.csdnimg.cn/img_convert/706fe8b2403c41e4eac4840b86d13abe.png)

**ES6 写法**：

ES6 中，我们有了剩余参数，就不用担心报错的问题了。代码可以这样写：

```javascript
const fn = (...args) => {
    //当不确定方法的参数时，可以使用剩余参数
    console.log(args[0]);
    console.log(args[1]);
    console.log(args[2]);
    console.log(args[3]);
};

fn(1, 2);
fn(1, 2, 3); //方法的定义中了四个参数，但调用函数时只使用了三个参数，ES6 中并不会报错。
```

打印结果：

```bash
1
2
undefined
undefined


1
2
3
undefined
```

上方代码中注意，args 参数之后，不能再加别的参数，否则编译报错。

下面这段代码，也是利用到了剩余参数：

```js
function fn1(first, ...args) {
    console.log(first); // 10
    console.log(args); // 数组：[20, 30]
}

fn1(10, 20, 30);
```

### 剩余参数的举例：参数求和

代码举例：

```js
const sum = (...args) => {
    let total = 0;
    args.forEach(item => total += item); // 注意 forEach里面的代码，写得 很精简
    return total;
};
console.log(sum(10, 20, 30));
```

打印结果：60

### 剩余参数和解构赋值配合使用

代码举例：

```js
const students = ['张三', '李四', '王五'];
let [s1, ...s2] = students;

console.log(s1); // '张三'
console.log(s2); // ['李四', '王五']
```

## 闭包的引入

我们知道，变量根据作用域的不同分为两种：全局变量和局部变量。

- 函数内部可以访问全局变量和局部变量。

- 函数外部只能访问全局变量，不能访问局部变量。

- 当函数执行完毕，本作用域内的局部变量会销毁。

比如下面这样的代码：

```js
function foo() {
    let a = 1;
}

foo();
console.log(a); // 打印报错：Uncaught ReferenceError: a is not defined
```

上方代码中，由于变量 `a` 是函数内的局部变量，所以外部无法访问。

但是，在有些场景下，我们就是想要在函数外部访问函数内的局部变量，那要怎么办呢？这就需要引入闭包的概念。

### 闭包的概念

**闭包**（closure）：指有权**访问**另一个函数作用域中**变量**的**函数**。

闭包是一种函数；当然，你可以**把闭包理解成是一种现象**。具体解释如下。

简单理解就是：如果**这个作用域可以访问另外一个函数内部的局部变量**，那就产生了闭包（此时，你可以把闭包理解成是一种现象）；而另外那个作用域所在的函数称之为**闭包函数**。注意，这里强调的是访问**局部变量**哦。

### 闭包代码举例

代码举例：

```js
function fn1() {
    let a = 10;

    return function fn2() {
        console.log(a);
    }
   
}

fn1();
```

打印结果：

```js
10
```

上方代码中，函数 fn2 的作用域 访问了 fn1 中的局部变量，那么，此时在 fn1 中就产生了闭包，fn1 称之为闭包函数。

### 闭包的作用

**延伸变量的作用范围**

我们来看看下面这段闭包的代码：

```js
function fn1() {
    let a = 20;

    function fn2() {
        console.log(a);
    }
    return fn2;
}

const foo = fn1(); // 执行 fn1() 之后，会得到一个返回值。foo 代表的就是 fn2 函数
foo();
```

上方代码中，foo 代表的就是整个 fn2 函数。当执行了 `foo()` 语句之后（相当于执行了 ），fn1 函数内就产生了闭包。

一般来说，在 fn1 函数执行完毕后，它里面的变量 a 会立即销毁。但此时由于产生了闭包，所以 **fn1 函数中的变量 a 不会立即销毁，因为 fn2 函数还要继续调用变量 a**。只有等所有函数把变量 a 调用完了，变量 a 才会销毁。

而且，可以看出， 在执行 `foo()`语句之后，竟然能够打印出 `20`，这就完美通过闭包实现了：全局作用域成功访问到了局部作用域中的变量 a。

因此，我们可以看出，闭包的主要作用就是：**延伸了变量的作用范围。**

上面的代码也可以简写成：

```js
function fn1() {
    let a = 20;

    return function () {
        console.log(a);
    };
}

const foo = fn1(); // 执行 fn1() 之后，会得到一个返回值, 这个返回值是函数
foo();
```

## 执行期上下文

当**函数执行**时**（准确来说，是在函数发生预编译的前一刻）**，会创建一个执行期上下文的内部对象。一个执行期上下文定义了一个函数执行时的环境。

每调用一次函数，就会创建一个新的上下文对象，他们之间是相互独立且独一无二的。当函数执行完毕，它所产生的执行期上下文会被销毁。

### this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数，这个隐含的参数就是 this，this 指向的是一个对象，这个对象我们称为函数执行的 上下文对象。

### 普通函数内 this 的指向

根据函数的调用方式的不同，this 会指向不同的对象：

- 1.以函数的形式（**包括普通函数、定时器函数、立即执行函数）**调用时，this 的指向永远都是 window。比如`fun();`相当于`window.fun();`

- 2.以方法的形式调用时，this 指向调用方法的那个对象

- 3.以构造函数的形式调用时，this 指向实例对象

- 4.以事件绑定函数的形式调用时，this 指向**绑定事件的对象**

- 5.使用 call 和 apply 调用时，this 指向指定的那个对象

**针对第 1 条的举例**：

```javascript
function fun() {
    console.log(this);
    console.log(this.name);
}

var obj1 = {
    name: 'ximingx',
    sayName: fun,
};

var obj2 = {
    name: 'luoyue',
    sayName: fun,
};

var name = '全局的name属性';

// 以函数形式调用，this是window
// 可以理解成 window.fun()
fun(); 
```

打印结果：

```js
    Window
    全局的name属性
```

上面的举例可以看出，this 指向的是 window 对象，所以 this.name 指的是全局的 name。

**第 2 条的举例**：

```javascript
function fun() {
    console.log(this);
    console.log(this.name);
}

var obj1 = {
    name: 'ximingx',
    sayName: fun,
};

var obj2 = {
    name: 'luoyue',
    sayName: fun,
};

var name = '全局的name属性';

// 以方法的形式调用，this是调用方法的对象
obj2.sayName();
```

打印结果：

```js
    Object
    luoyue
```

上面的举例可以看出，this 指向的是 对象 obj2 ，所以 this.name 指的是 obj2.name。

### 箭头函数中 this 的指向

ES6 中的箭头函数并不会使用上面的准则，而是会继承外层函数调用的 this 绑定（无论 this 绑定到什么）。


### 改变 this 的指向

JS 专门为我们提供了一些方法来改变函数内部的 this 指向。常见的方法有 call()、apply()、bind() 方法。

### call

#### call() 方法的作用

call() 方法的作用：可以**调用**一个函数，与此同时，它还可以改变这个函数内部的 this 指向。

call() 方法的另一个应用：**可以实现继承**。之所以能实现继承，其实是利用了上面的作用。

语法：

```js
fn1.call(想要将this指向哪里, 函数实参1, 函数实参2);
```

**备注：第一个参数中，如果不需要改变 this 指向，则传 null。**

#### call() 方法举例

**举例 1**、通过 call() 调用函数：

```js
const obj1 = {
    nickName: 'ximingx',
    age: 28,
};
function fn1() {
    console.log(this);
    console.log(this.nickName);
}

fn1.call(this);
// window
// undefined

fn1.call(obj1);
// { nickName: 'ximingx', age: 28 }
// ximingx
```

**举例 2**、通过 call() 改变 this 指向：

```js
var obj1 = {
    nickName: 'ximingx',
    age: 28,
};

function fn1(a, b) {
    console.log(this);
    console.log(this.nickName);
    console.log(a + b);
}

fn1.call(obj1, 2, 4); // 先将 this 指向 obj1，然后执行 fn1() 函数
```

上方代码的打印结果：

```js
// { nickName: 'ximingx', age: 28 }
// ximingx
// 6
```

**举例 3**、通过 call() 实现继承：

```js
// 给 Father 增加 name 和 age 属性
function Father(myName, myAge) {
    this.name = myName;
    this.age = myAge;
}

function Son(myName, myAge) {
    // 通过这一步，将 father 里面的 this 修改为 Son 里面的 this；另外，给 Son 加上相应的参数，让 Son 自动拥有 Father 里的属性。最终实现继承
    Father.call(this, myName, myAge);
}

const son1 = new Son('ximingx', 28);
console.log(son1);
```

上方代码中，通过 call() 方法，让 Son 继承了 Father 里面的 name 和 age 属性。

打印结果：

```js
{"myName":"ximingx","myAge":28}
```

### apply() 方法

#### apply() 方法的作用

apply() 方法的作用：可以**调用**一个函数，与此同时，它还可以改变这个函数内部的 this 指向。这一点，和 call()类似。

apply() 方法的应用： 由于 apply()需要传递数组，所以它有一些巧妙应用，稍后看接下来的应用举例就知道了。

语法：

```js
fn1.apply(想要将this指向哪里, [函数实参1, 函数实参2]);
```

备注：第一个参数中，如果不需要改变 this 指向，则传 null。

到这里可以看出， call() 和 apply() 方法的作用是相同的。唯一的区别在于，apply() 里面传入的**实参，必须是数组（或者维数组）**。

#### apply() 方法举例

**举例**、通过 apply() 改变 this 指向：

```js
var obj1 = {
    nickName: 'ximingx',
    age: 28,
};

function fn1(a) {
    console.log(this);
    console.log(this.nickName);
    console.log(a);
}

fn1.apply(obj1, ['hello']); // 先将 this 指向 obj1，然后执行 fn1() 函数
```

注意，上方代码中，call() 里面传实参时，需要以数组的形式。即便是传一个实参，也需要传数组。

打印结果：

```js
obj1
ximingx
hello
```

#### apply() 方法的巧妙应用：求数组的最大值

我们知道，如果想要求数组中元素的最大值的时候，数组本身是没有自带方法的。那怎么办呢？

虽然数组里没有获取最大值的方法，但是数值里面有 `Math.max(数字1，数字2，数字3)` 方法，可以获取**多个数值中的最大值**。 另外，由于 apply() 方法在传递实参时，必须要以数组的形式，所以我们可以 通过 Math.max() 和 apply() 曲线救国。

**举例**：求数组中多个元素的最大值：

```js
const arr1 = [3, 7, 10, 8];

// 下面这一行代码的目的，无需改变 this 指向，所以：第一个参数填 null，或者填 Math，或者填 this 都可以。严格模式中，不让填null。
const maxValue = Math.max.apply(Math, arr1); // 求数组 arr1 中元素的最大值
console.log(maxValue);

const minValue = Math.min.apply(Math, arr1); // 求数组 arr1 中元素的最小值
console.log(minValue);
```

打印结果：

```js
10

3
```

### bind()

bind() 方法**不会调用函数，但是可以改变函数内部的 this 指向, 返回的是原函数改变this之后产生的新函数**

把call()、apply()、bind()这三个方法做一下对比，你会发现：实际开发中， bind() 方法使用得最为频繁。如果有些函数，我们不需要立即调用，但是又想改变这个函数内部的this指向，此时用 bind() 是最为合适的。


语法：

```js
新函数 = fn1.bind(想要将this指向哪里, 函数实参1, 函数实参2);
```

参数：

- 第一个参数：在 fn1 函数运行时，指定 fn1 函数的this 指向。如果不需要改变 this 指向，则传 null。

- 其他参数：fn1 函数的实参。

解释：它不会调用 fn1 函数，但会返回 由指定this 和指定实参的**原函数拷贝**。可以看出， bind() 方法是有返回值的。

```js
 var o = {
 	name: 'andy'
 };

function fn(a, b) {
	console.log(this);
	console.log(a + b);
};
var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
f(); //调用新函数  this指向的是对象o 参数使用逗号隔开
// {name: 'andy'}
// 3
```

```html
<!-- 使用场景 -->
<button></button>

<script>
    let btn = document.querySelector("button");
    btn.onlick = function() {
        this.disabled = "false";
        setTimeout(function() {
            this.disabled = "true"
        }.bind(this), 3000)
    }
</script>
```

### call、apply、bind三者的异同

- 共同点 : 都可以改变this指向
- 不同点:
  - call 和 apply  会调用函数, 并且改变函数内部this指向.
  - call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
  - bind  不会调用函数, 可以改变函数内部this指向.


- 应用场景
  1. call 经常做继承. 
  2. apply 经常跟数组有关系.  比如借助于数学对象实现数组最大值最小值
  3. bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向. 

## 递归

**递归：**如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。**简单理解:函数内部自己调用自己, 这个函数就是递归函数**

**注意：**递归函数的作用和循环效果一样，由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件return。

### 利用递归求1~n的阶乘

```js
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
 function fn(n) {
     if (n == 1) { //结束条件
       return 1;
     }
     return n * fn(n - 1);
 }
 console.log(fn(3));
```

### 利用递归求斐波那契数列

```js
// 利用递归函数求斐波那契数列(兔子序列)  1、1、2、3、5、8、13、21...
// 用户输入一个数字 n 就可以求出 这个数字对应的兔子序列值
// 我们只需要知道用户输入的n 的前面两项(n-1 n-2)就可以计算出n 对应的序列值
function fb(n) {
  if (n === 1 || n === 2) {
        return 1;
  }
  return fb(n - 1) + fb(n - 2);
}
console.log(fb(3));
```

## 箭头函数

ES6中新增的定义函数的方式。

```javascript
() => {} //()：代表是函数； =>：必须要的符号，指向哪一个代码块；{}：函数体
const fn = () => {}//代表把一个函数赋值给fn
```

函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号

```javascript
 function sum(num1, num2) { 
     return num1 + num2; 
 }
 //es6写法
 const sum = (num1, num2) => num1 + num2; 

```

如果形参只有一个，可以省略小括号

```javascript
 function fn (v) {
     return v;
 } 
//es6写法
 const fn = v => v;

```

箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置的上下文this

```javascript
const obj = { name: '张三'} 
 function fn () { 
     console.log(this);//this 指向 是obj对象
     return () => { 
         console.log(this);//this 指向 的是箭头函数定义的位置，那么这个箭头函数定义在fn里面，而这个fn指向是的obj对象，所以这个this也指向是obj对象
     } 
 } 
 const resFn = fn.call(obj); 
 resFn();

```

#### 小结

- 箭头函数中不绑定this，箭头函数中的this指向是它所定义的位置，可以简单理解成，定义箭头函数中的作用域的this指向谁，它就指向谁
- 箭头函数的优点在于解决了this执行环境所造成的一些问题。比如：解决了匿名函数this指向的问题（匿名函数的执行环境具有全局性），包括setTimeout和setInterval中使用this所造成的问题

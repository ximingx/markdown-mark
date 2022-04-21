#  Object

## 对象的基本操作

### 创建对象

使用 new 关键字调用的函数，是构造函数 constructor。**构造函数是专门用来创建对象的函数**。

例如：

```javascript
var obj = new Object();
```

记住，使用`typeof`检查一个对象时，会返回`object`。

关于常见对象的更多方式，可以看上一篇文章《对象的创建&构造函数》。

### 向对象中添加属性

在对象中保存的值称为属性。

向对象添加属性的语法：

```javascript
对象.属性名 = 属性值;
```

举例：

```javascript
var obj = new Object();

//向obj中添加一个name属性
obj.name = '孙悟空';

//向obj中添加一个gender属性
obj.gender = '男';

//向obj中添加一个age属性
obj.age = 18;

console.log(JSON.stringify(obj)); // 将 obj 以字符串的形式打印出来
```

打印结果：

```jS
	{
		"name":"孙悟空",
		"gender":"男",
		"age":18
	}
```

### 获取对象中的属性

**方式 1**：

语法：

```javascript
对象.属性名;
```

如果获取对象中没有的属性，不会报错而是返回`undefined`。

举例：

```javascript
var obj = new Object();

//向obj中添加一个name属性
obj.name = '孙悟空';

//向obj中添加一个gender属性
obj.gender = '男';

//向obj中添加一个age属性
obj.age = 18;

// 获取对象中的属性，并打印出来
console.log(obj.gender); // 打印结果：男
console.log(obj.color); // 打印结果：undefined
```

**方式 2**：可以使用`[]`这种形式去操作属性

对象的属性名不强制要求遵守标识符的规范，不过我们尽量要按照标识符的规范去做。

但如果确实要使用特殊的属性名，就不能采用`.`的方式来操作对象的属性。比如说，`123`这种属性名，如果我们直接写成`obj.123 = 789`来操作属性，是会报错的。那怎么办呢？办法如下：

语法格式如下：（读取时，也是采用这种方式）

```javascript
// 注意，括号里的属性名，必须要加引号
对象['属性名'] = 属性值;
```

上面这种语法格式，举例如下：

```javascript
obj['123'] = 789;
```

**重要**：使用`[]`这种形式去操作属性，更加的灵活，因为，我们可以在`[]`中直接传递一个**变量**。

**方式三: Object.keys()**

Object.keys(对象) 获取到当前对象中的属性名 ，返回值是一个数组

```js
 var obj = {
     id: 1,
     pname: '小米',
     price: 1999,
     num: 2000
};
var result = Object.keys(obj)
console.log(result) // [id，pname,price,num]
```

### 修改对象的属性值

方法一:

语法：

```javascript
对象.属性名 = 新值;
```

```javascript
obj.name = 'tom';
```

方法二: **defineProperty**

语法

```js
Object.defineProperty(对象，修改或新增的属性名，{})
// 三个参数都是必填
```

```js
Object.defineProperty(对象，修改或新增的属性名，{
		value: 1,// value: 修改或新增的属性的值,
		writable:true/false, // 如果值为false 不允许修改这个属性值
		enumerable: false, // enumerable 如果值为false 则不允许遍历, 默认为false
         configurable: false  // configurable 如果为false 则不允许删除这个属性 属性是否可以被删除或是否可以再次修改特性
})	
```

### 删除对象的属性

语法：

```javascript
delete obj.name;
```

### in 运算符

通过该运算符可以检查一个对象中是否含有指定的属性。如果有则返回 true，没有则返回 false。

语法：

```javascript
'属性名' in 对象;
```

举例：

```javascript
//检查对象 obj 中是否含有name属性
console.log('name' in obj);
```

我们平时使用的对象不一定是自己创建的，可能是从接口获取的，这个时候，in 运算符可以派上用场。

当然，还有一种写法可以达到上述目的：

```js
if (obj.name) {
    // 如果对象 obj 中有name属性，我就继续做某某事情。
}
```

### Object.freeze() 冻结对象

Object.freeze() 方法可以冻结一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改。freeze() 返回和传入的参数相同的对象。

代码举例：

```js
const params = {
    name: 'ximingx';
    port: '8899';
}

Object.freeze(params); // 冻结对象 params

params.port = '8080';// 修改无效

```

上方代码中，把 params 对象冻结后，如果想再改变 params 里面的属性值，是无效的。

## 遍历操作

### for of：遍历数组


ES6 中，如果我们要遍历一个数组，可以这样做：

```js
let arr1 = [2, 6, 8, 5];

for (let value of arr1) {
    console.log(value);
}
```

打印结果：


```js
2
6
8
5
```


for ... of 的循环可以避免我们开拓内存空间，增加代码运行效率，所以建议大家在以后的工作中使用 for…of 遍历数组。

注意，上面的数组中，`for ... of`获取的是数组里的值；如果采用`for ... in`遍历数组，则获取的是 index 索引值。

### Map 对象的遍历

`for ... of`既可以遍历数组，也可以遍历 Map 对象。

### for in：遍历对象的属性

> `for ... in`主要用于遍历对象，不建议用来遍历数组。

语法：

```javascript
for (const 变量 in 对象) {

}
```

解释：对象中有几个属性，循环体就会执行几次。每次执行时，会将对象中的**每个属性的 属性名 赋值给变量**。

语法举例：

```javascript
for (var key in obj) {
    console.log(key); // 这里的 key 是：对象属性的键（也就是属性名）
    console.log(obj[key]); // 这里的 obj[key] 是：对象属性的值（也就是属性值）
}
```

### for in 遍历数组（不建议）

另外，for in 当然也可以用来遍历数组（只是不建议），此时的 key 是数组的索引。举例如下：

```js
const arr = ['hello1', 'hello2', 'hello3'];

for (const key in arr) {
    console.log('属性名：' + key);
    console.log('属性值：' + arr[key]);
}
```

打印结果：

```js
属性名：0
属性值：hello1

属性名：1
属性值：hello2

属性名：2
属性值：hello3
```

## 深拷贝 浅拷贝

-   浅拷贝：只拷贝最外面一层的数据；更深层次的对象，只拷贝引用。

-   深拷贝：拷贝多层数据；每一层级别的数据都会拷贝。

**总结**：

**浅拷贝的时候如果数据是基本数据类型，那么就如同直接赋值那种，会拷贝其本身，如果除了基本数据类型之外还有一层对象，那么对于浅拷贝而言就只能拷贝其引用，对象的改变会反应到拷贝对象上；但是深拷贝就会拷贝多层，即使是嵌套了对象，也会都拷贝出来。**

拷贝引用的时候，是属于**传址**，而非**传值**。

深拷贝会把对象里**所有的数据**重新复制到新的内存空间，是最彻底的拷贝。

### 浅拷贝的实现方式

### 用 for in 实现浅拷贝

```js
const obj1 = {
    name: 'ximingx',
    age: 28,
    info: {
        msg: '~ ~ ~',
    },
};

const obj2 = {};

//  用 for in 将 obj1 的值拷贝给 obj2
for (let key in obj1) {
    obj2[key] = obj1[key];
}

console.log('obj2:' + JSON.stringify(obj2));

obj1.age = 20;

obj1.info.msg = 'aw'; // 当修改 obj1 的第二层数据时，obj2的值也会被改变。所以  for in 是浅拷贝

console.log('obj2:' + JSON.stringify(obj2));
```

上方代码中，用 for in 做拷贝时，只能做到浅拷贝。也就是说，在 obj2 中， name 和 age 这两个属性会单独存放在新的内存地址中，和 obj1 没有关系。但是，`obj2.msg` 属性，跟 `obj1.msg`属性，**它俩指向的是同一个堆内存地址**。所以，当我修改 `obj1.msg` 里的值之后，`obj2.msg`的值也会被修改。

打印结果如下：

```js
obj2:{"name":"ximingx","age":28,"info":{"msg":"~ ~ ~"}}

obj2:{"name":"ximingx","age":28,"info":{"msg":"aw"}}
```

### Object.assgin() 实现浅拷贝

上面的 for in 方法做浅拷贝过于繁琐。ES6 给我们提供了新的语法糖，通过 `Object.assgin()` 可以实现**浅拷贝**。

`Object.assgin()` 在日常开发中，使用得相当频繁，非掌握不可。

**语法**：

```js
// 语法1
obj2 = Object.assgin(obj2, obj1);

// 语法2
Object.assign(目标对象, 源对象1, 源对象2...);
```

**解释**：将`obj1` 拷贝给 `obj2`。执行完毕后，obj2 的值会被更新。

**作用**：将 obj1 的值追加到 obj2 中。如果对象里的属性名相同，会被覆盖。

从语法2中可以看出，Object.assign() 可以将多个“源对象”拷贝到“目标对象”中。

**例 1**：

```js
const obj1 = {
    name: 'ximingx',
    age: 20,
    info: {
        desc: 'hello',
    },
};

// 浅拷贝：把 obj1 拷贝给 obj2。如果 obj1 只有一层数据，那么，obj1 和 obj2 则互不影响
const obj2 = Object.assign({}, obj1);
console.log('obj2:' + JSON.stringify(obj2));

obj1.info.desc = 'aw'; // 由于 Object.assign() 只是浅拷贝，所以当修改 obj1 的第二层数据时，obj2 对应的值也会被改变。
console.log('obj2:' + JSON.stringify(obj2));
```

代码解释：由于 Object.assign() 只是浅拷贝，所以在当前这个案例中， obj2 中的 name 属性和 age 属性是单独存放在新的堆内存地址中的，和 obj1 没有关系；但是，`obj2.info` 属性，跟 `obj1.info`属性，**它俩指向的是同一个堆内存地址**。所以，当我修改 `obj1.info` 里的值之后，`obj2.info`的值也会被修改。

打印结果：

```js
obj2:{"name":"ximingx","age":20,"info":{"desc":"hello"}}

obj2:{"name":"ximingx","age":20,"info":{"desc":"aw"}}
```

**例 2**：

```js
const obj1 = {
    name: 'ximingx',
    age: 20,
    info: {
        desc: 'hello',
    },
};

// 【写法1】浅拷贝：把 myObj 拷贝给 obj1
const obj1 = {};
Object.assign(obj1, myObj);

// 【写法2】浅拷贝：把 myObj 拷贝给 obj2
const obj2 = Object.assign({}, myObj);

// 【写法3】浅拷贝：把 myObj 拷贝给 obj31。注意，这里的 obj31 和 obj32 其实是等价的，他们指向了同一个内存地址
const obj31 = {};
const obj32 = Object.assign(obj31, myObj);

```

上面这三种写法，是等价的。所以，当我们需要将对象 A 复制（拷贝）给对象 B，不要直接使用 `B = A`，而是要使用 Object.assign(B, A)。

**例 3**：

```js
let obj1 = { name: 'ximingx', age: 126 };
let obj2 = { city: 'shanxi', age: 28 };
let obj3 = {};

Object.assign(obj3, obj1, obj2); // 将 obj1、obj2的内容赋值给 obj3
console.log(obj3); // {name: "ximingx", age: 28, city: "shanxi"}
```

上面的代码，可以理解成：将多个对象（obj1和obj2）合并成一个对象 obj3。

**例4**：【重要】

```js
const obj1 = {
    name: 'ximingx',
    age: 28,
    desc: 'hello world',
};

const obj2 = {
    name: 'luoyue',
    sex: '男',
};

// 浅拷贝：把 obj1 赋值给 obj2。这一行，是关键代码。这行代码的返回值也是 obj2
Object.assign(obj2, obj1);

console.log(JSON.stringify(obj2));
```

打印结果：

```js
{"name":"ximingx","sex":"男","age":28,"desc":"hello world"}
```

注意，**例 4 在实际开发中，会经常遇到，一定要掌握**。它的作用是：将 obj1 的值追加到 obj2 中。如果两个对象里的属性名相同，则 obj2 中的值会被 obj1 中的值覆盖。

### 深拷贝的实现方式

深拷贝其实就是将浅拷贝进行递归。

### 用 for in 递归实现深拷贝

代码实现：

```js
let obj1 = {
    name: 'qianguyihao',
    age: 28,
    info: {
        desc: 'hello',
    },
    color: ['red', 'blue', 'green'],
};
let obj2 = {};

deepCopy(obj2, obj1);
console.log(obj2);
obj1.info.desc = 'github';
console.log(obj2);

// 方法：深拷贝
function deepCopy(newObj, oldObj) {
    for (let key in oldObj) {
        // 获取属性值 oldObj[key]
        let item = oldObj[key];
        // 判断这个值是否是数组
        if (item instanceof Array) {
            newObj[key] = [];
            deepCopy(newObj[key], item);
        } else if (item instanceof Object) {
            // 判断这个值是否是对象
            newObj[key] = {};
            deepCopy(newObj[key], item);
        } else {
            // 简单数据类型，直接赋值
            newObj[key] = item;
        }
    }
}
```

还有一种类似的方法，就是用JSON进行转换

```js
var p1 = {
    name: 'jack',
    age:12
}
 
var p2 = JSON.parse(JSON.stringify(p1));
 
p2.name = 'rose';
```

实际开发中，可能这种方式用的更多一些，比如把一些数据转成json存储到本地缓存，需要用到的时候，我们再反序列化。

## 扩展

### 剩余参数

剩余参数语法允许我们将一个不定数量的参数表示为一个数组，不定参数定义方式，这种方式很方便的去声明不知道参数情况下的一个函数

```javascript
function sum (first, ...args) {
     console.log(first); // 10
     console.log(args); // [20, 30] 
 }
 sum(10, 20, 30)
```

### 剩余参数和解构配合使用

```javascript
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students; 
console.log(s1);  // 'wangwu' 
console.log(s2);  // ['zhangsan', 'lisi']
```




# Array

## 1. 数组简介

数组（Array）属于**内置对象**

数组和普通对象的功能类似，也是用来存储一些值的。不同的是：

-   普通对象是使用字符串作为属性名的，而数组是使用数字作为**索引**来操作元素。索引：从 0 开始的整数就是索引。

数组的存储性能比普通对象要好。在实际开发中我们经常使用数组来存储一些数据（尤其是**列表数据**），使用频率非常高。

数组中的元素可以是任意的数据类型，也可以是对象，也可以是函数，也可以是数组。数组的元素中，如果存放的是数组，我们就称这种数组为二维数组。(可以以此类推多维数组)

## 2. 创建数组对象

### 方式一：字面量创建数组

举例：

```js
let arr1 = [];   // 创建一个空数组
let arr2 = ["arr2"];   // 创建一个包含1个字符串的数组 ("arr2")
let arr3 = ["leo","is",18];   // 创建一个包含3项数据的数组

var arr1 = []; // 创建一个空的数组
var arr2 = [1, 2, 3]; // 创建带初始值的数组
```

### 方式二：构造函数创建数组

语法：

```js
let arr = new Array(参数);

let arr = Array(参数);

let arr1 = new Array();   // 创建一个空数组
let arr2 = new Array("leo");   // 创建一个包含1个字符串的数组
let arr3 = new Array("leo","is","nice");   // 创建一个包含3个字符串的数组
```

如果**参数为空**，则表示创建一个空数组；如果参数是**一个数值**时，表示数组的长度；如果有多个参数时，表示数组中的元素。

这里很容易犯错, 一定要记得参数是**一个数值**时，表示的是数组的长度

来举个例子：

```javascript
// 方式一
var arr1 = [11, 12, 13];

// 方式二
var arr2 = new Array(); // 参数为空
var arr3 = new Array(4); // 参数为一个数值
var arr4 = new Array(15, 16, 17); // 参数为多个数值

console.log(typeof arr1); // 打印结果：object

// JSON.stringify(arr1)) 的目的是将数组转化为字符串
console.log('arr1 = ' + JSON.stringify(arr1));
console.log('arr2 = ' + JSON.stringify(arr2));
console.log('arr3 = ' + JSON.stringify(arr3));
console.log('arr4 = ' + JSON.stringify(arr4));
```

打印结果：

```javascript
object;

arr1 = [11, 12, 13];
arr2 = [];
// 主要注意这里
arr3 = [null, null, null, null]; 
arr4 = [15, 16, 17];
```

从上方打印结果的第一行里，可以看出，数组的类型其实也是属于**对象**。

### Array.of 

Array.of()方法总会创建一个包含所有传入参数的数组，而不管参数的数量与类型

```js
let arr = Array.of(1,2);
console.log(arr.length);   // 2
console.log(arr[0]);   // 1
 
let arr1 = Array.of("leo");
console.log(arr1.length);   // 1
console.log(arr1[0]);   // "leo"
```

### Array.from 方式

Array.from() 将可迭代对象或者类数组对象作为第一个参数传入，就能返回一个数组

```js
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

### 数组中的元素的类型

数组中可以存放**任意类型**的数据，例如字符串、数字、布尔值、对象等。

比如：

```javascript
const arr = ['ximingx', 20, true, { name: 'ximingx' }];
```

我们甚至还可以存放**多维数组**（数组里面放数组）。比如：

```js
const arr2 = [
    [11, 12, 13],
    [21, 22, 23],
];
```

## 3. 数组的基本操作

### 数组的索引

**索引** (下标) ：用来访问数组元素的序号，代表的是数组中的元素在数组中的位置（下标从 0 开始算起）。

数组可以通过索引来访问、设置、修改对应的数组元素。我们继续看看。

### 向数组中添加元素

语法：

```javascript
数组[索引] = 值;
```

代码举例：

```javascript
var arr = [];

// 向数组中添加元素
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
arr[3] = 40;
arr[5] = 50;

console.log(JSON.stringify(arr));
```

打印结果：

```js
[10,20,30,40,null,50]
```

### 获取数组中的元素

语法：

```javascript
数组[索引];
```

如果读取不存在的索引（比如元素没那么多），系统不会报错，而是返回 undefined。

代码举例：

```javascript
var arr = [21, 22, 23];

console.log(arr[0]); // 打印结果：21
console.log(arr[5]); // 打印结果：undefined
```

### 获取数组的长度

可以使用`length`属性来获取数组的长度(即“元素的个数”)。

数组的长度是元素个数，不要跟索引号混淆。

语法：

```javascript
数组的长度 = 数组名.length；
```

代码举例：

```javascript
var arr = [21, 22, 23];

console.log(arr.length); // 打印结果：3
```

补充：

对于连续的数组，使用 length 可以获取到数组的长度（元素的个数）；对于非连续的数组（即“稀疏数组”，下一段会讲），length 的值会大于元素的个数。因此，尽量不要创建非连续的数组。



### 修改数组的长度

-   如果修改的 length 大于原长度，则多出部分会空出来，置为 null。

-   如果修改的 length 小于原长度，**则多出的元素会被删除，数组将从后面删除元素。**

代码举例：

```javascript
var arr1 = [11, 12, 13];
var arr2 = [21, 22, 23];

// 修改数组 arr1 的 length
arr1.length = 1;
console.log(JSON.stringify(arr1));

// 修改数组 arr2 的 length
arr2.length = 5;
console.log(JSON.stringify(arr2));
```

打印结果：

```javascript
[11]
[(21, 22, 23, null, null)];
```

### 遍历数组

**遍历**: 就是把数组中的每个元素从头到尾都访问一次。

最简单的做法是通过 for 循环，遍历数组中的每一项。举例：

```javascript
var arr = [10, 20, 30, 40, 50];

for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]); // 打印出数组中的每一项
}
```

## 4. 数组的方法详细介绍

![在这里插入图片描述](https://img-blog.csdnimg.cn/a19346ab9fc34e04a3b7b322165afe9a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 数组的方法清单

###### 数组的类型相关

| 方法                             | 描述                               | 备注 |
| :------------------------------- | :--------------------------------- | :--- |
| Array.isArray()                  | 判断是否为数组                     |      |
| toString()                       | 将数组转换为字符串                 |      |
| Array.from(arrayLike)            | 将**伪数组**转化为**真数组**       |      |
| Array.of(value1, value2, value3) | 创建数组：将**一系列值**转换成数组 |      |

注意，获取数组的长度是用`length`属性，不是方法。

###### 数组元素的添加和删除

| 方法      | 描述                                                         | 备注           |
| :-------- | :----------------------------------------------------------- | :------------- |
| push()    | 向数组的**最后面**插入一个或多个元素，返回结果为新数组的**长度** | 会改变原数组   |
| pop()     | 删除数组中的**最后一个**元素，返回结果为**被删除的元素**     | 会改变原数组   |
| unshift() | 在数组**最前面**插入一个或多个元素，返回结果为新数组的**长度** | 会改变原数组   |
| shift()   | 删除数组中的**第一个**元素，返回结果为**被删除的元素**       | 会改变原数组   |
|           |                                                              |                |
| slice()   | 从数组中**提取**指定的一个或多个元素，返回结果为**新的数组** | 不会改变原数组 |
| splice()  | 从数组中**删除**指定的一个或多个元素，返回结果为**被删除元素组成的新数组** | 会改变原数组   |
|           |                                                              |                |
| fill()    | 填充数组：用固定的值填充数组，返回结果为**新的数组**         | 会改变原数组   |

###### 数组的合并和拆分

| 方法     | 描述                                                 | 备注             |
| :------- | :--------------------------------------------------- | :--------------- |
| concat() | 合并数组：连接两个或多个数组，返回结果为**新的数组** | 不会改变原数组   |
| join()   | 将数组转换为字符串，返回结果为**转换后的字符串**     | 不会改变原数组   |
| split()  | 将字符串按照指定的分隔符，组装为数组                 | 不会改变原字符串 |

注意，`split()`是字符串的方法，不是数组的方法。

###### 数组排序

| 方法      | 描述                                                    | 备注         |
| :-------- | :------------------------------------------------------ | :----------- |
| reverse() | 反转数组，返回结果为**反转后的数组**                    | 会改变原数组 |
| sort()    | 对数组的元素,默认按照**Unicode 编码**，从小到大进行排序 | 会改变原数组 |

###### 查找数组的元素

| 方法                  | 描述                                                         | 备注                                                     |
| :-------------------- | :----------------------------------------------------------- | :------------------------------------------------------- |
| indexOf(value)        | 从前往后索引，检索一个数组中是否含有指定的元素               |                                                          |
| lastIndexOf(value)    | 从后往前索引，检索一个数组中是否含有指定的元素               |                                                          |
| includes(item)        | 数组中是否包含指定的内容                                     |                                                          |
| find(function())      | 找出**第一个**满足「指定条件返回 true」的元素                |                                                          |
| findIndex(function()) | 找出**第一个**满足「指定条件返回 true」的元素的 index        |                                                          |
| every()               | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为真。要求每一项都返回 true，最终的结果才返回 true |
| some()                | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true | 一真即真。只要有一项返回 true，最终的结果就返回 true     |

###### 遍历数组

| 方法      | 描述                                                         | 备注                                                   |
| :-------- | :----------------------------------------------------------- | :----------------------------------------------------- |
| for 循环  | 这个大家都懂                                                 |                                                        |
| forEach() | 和 for 循环类似，但需要兼容 IE8 以上                         | forEach() 没有返回值。也就是说，它的返回值是 undefined |
| map()     | 对原数组中的每一项进行加工，将组成新的数组(最后的结果可能会含有undefined) | 不会改变原数组                                         |
| filter()  | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组                                         |
| reduce    | 接收一个函数作为累加器，返回值是回调函数累计处理的结果       |                                                        |


---

### concat()

**返回结果: Array1 后直接拼接增加 Array2**

该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

Array2 的位置可以有多个数组,最后都将合并

**arrayObject.concat(arrayX,arrayX,......,arrayX)**

```js
let Array1 = [1,2,3,4,5]
let Array2 = ['a','b','c','d','e']
let Array3 = Array1.concat(Array2)
console.log(Array3);
// [
//   1,   2,   3,   4,   5,
//   'a', 'b', 'c', 'd', 'e'
// ]
// 原数组不改变
console.log(Array1)
// [ 1, 2, 3, 4, 5 ]
// 可以拼接多个数组
console.log(Array1.concat(Array2,Array1))
// [
//   1,   2,   3,   4,   5, 'a',
//   'b', 'c', 'd', 'e', 1, 2,
//   3,   4,   5
// ]

```

当然,拼接数组一般可以选择更简单的方式 `... `

```js
let arr1 = [1, 2, 3, 4]
let arr2 = [5, 6, 7, 8, 9, 1]
arr1.push( ...arr2 )
console.log(arr1)
console.log(arr2)
// [
//   1, 2, 3, 4, 5,
//   6, 7, 8, 9, 1
// ]
// [ 5, 6, 7, 8, 9, 1 ]
```

注意: 

```js
console.log(arr1.push(...arr2));
// 返回的是数组的长度
```

### copyWithin()

使用这个方法，**会修改当前数组。**

**start 索引位到 end 索引位之前(不包含end索引位)的值将依次替换掉 traget 索引位起的值 (start - end中间有几位,就替换几位 )      （会覆盖原有成员）**

**Array1.copyWithin(target,start,end)**

| 参数   | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| target | 必填。复制到指定目标索引位置。                               |
| start  | 选填。元素复制的起始位置。默认为 0 ，如果为负值，表示倒数。  |
| end    | 选填。停止复制的索引位置。默认为array.length。如果为负值，表示倒数。 |

```js
let Array1 = [1,2,3,4,5,6]
let Array2 = ['a','b','c','d','e','f']
let Array3 = Array1.concat(Array2).copyWithin(1,3,5)
console.log(Array3);
// [
//   1,   4,   5,   4,   5,
//   6,   'a', 'b', 'c', 'd',
//   'e', 'f'
// ]
// 省略第三个参数 , 将会从第二个参数到最后全部修改
console.log(Array1.copyWithin(0,1))
// [ 2, 3, 4, 5, 6, 6 ]
[1, 2, 3, 4, 5].copyWithin(0, -2, -1)
// [4, 2, 3, 4, 5]
```

### every()

js中every和some都是对数组进行迭代操作的函数

**检测数组所有元素是否都符合every()里的函数,有一个不满足就返回false,全符合返回true,并停止检测**

**Array1.every((item) => {return condition})**

```js
let Array1 = [1,2,3,4,5,6]
let Array2 = [2,3,4,5]
let Array3 = Array1.concat(Array2)
Array3 = Array3.every((item) => {
  return item >= 2
})
console.log(Array3);
// false
```

### some()

**检测数组所有元素是否都符合every()里的函数,只要有一个为真,返回true,并停止检测**

**Array1.every((item) => {return condition})**

```js
let Array1 = [1,2,3,4,5,6]
let Array2 = [2,3,4,5]
let Array3 = Array1.concat(Array2)
Array3 = Array3.some((item) => {
  return item >= 2
})
console.log(Array3);
// true


// some 查找数组中是否有满足条件的元素 
 var arr = [10, 30, 4];
 var flag = arr.some(function(value,index,array) {
     // 参数一是: 数组元素
     // 参数二是: 数组元素的索引
     // 参数三是: 当前的数组
     return value < 3;
  });
console.log(flag);// false 返回值是布尔值,只要查找到满足条件的一个元素就立马终止循环
```

### fill()

**使用固定的值来填充数组,value为填充值,start 索引位到 end 索引位之前(不包含end索引位)的值被 value 替换**

**Array1.fill(value,start,end)**

```js
let Array1 = [1,2,3,4,5,6]
let Array2 = [2,3,4,5]
let Array3 = Array1.concat(Array2)
Array3 = Array3.fill("x",1,2)
console.log(Array3);
// [
//   1, 'x', 3, 4, 5,
//   6, 2,   3, 4, 5
// ]
let arr1 = [1, 2, 3, 4, 56, 7, 7, 8, 9];
arr1.fill(4, 2, 5);
console.log(arr1)  //   [1, 2, 4, 4, 4, 7, 7, 8, 9]
let arr2 = [1, 2, 3, 4, 56, 7, 7, 8, 9];
arr2.fill(4);
console.log(arr2)  //  [4, 4, 4, 4, 4, 4, 4, 4, 4]
```

### filter()

**检测指定的数组中所有符合条件的元素，并将满足的值返回新的数组。**

**Array1.filter((item) => {return condition})**

```js
let Array1 = [1,2,3,4,5,6]
let Array2 = [2,3,4,5]
let Array3 = Array1.concat(Array2)
Array3 = Array3.fill("1",1,2)
let Array4 = Array3.filter((item) => {
  return item >= 2
})
console.log(Array4);
// [
//   3, 4, 5, 6,
//   2, 3, 4, 5
// ]


  var arr = [12, 66, 4, 88, 3, 7];
  var newArr = arr.filter(function(value, index,array) {
  	 //参数一是:数组元素
     //参数二是:数组元素的索引
     //参数三是:当前的数组
     return value >= 20;
  });
  console.log(newArr); // [66,88] // 返回值是一个新数组
```

### find()

**语法**：

```javascript
find((item, index, arr) => {
    return true;
});
```



**返回通过函数判断的数组的  第一个元素的值  。**

如果没有符合条件的元素返回 undefined ,  find() 对于空数组，函数是不会执行的。

**Array1.find((item) => {return condition})**

```js
let Array2 = [2,3,4,5]
console.log(Array2.find((item) => {
  return item >= 3
}));
// 3
```

### findindex()

**与 find() 方法相似,返回的结果为索引位置,返回通过函数判断的数组的  第一个元素的索引位置  。**

**Array1.find((item) => {return condition})**

```JS
let Array2 = [2,3,4,5]
console.log(Array2.findIndex((item) => {
  return item >= 3
}));
// 1
```

### forEach()

**有三个参数  值,索引,和当前的数组  对每个元素进行一次调用, 没有返回值**

**Array2.forEach((item,index,arr) => {return condition}) **

```js
let Array2 = [2,3,4,5]
Array2.forEach((item,index,arr) => {
//参数一是: 数组元素
//参数二是: 数组元素的索引
//参数三是: 当前的数组
  item = item * index
  console.log(item)
}) 
// 0
// 3
// 8
// 15

//相当于数组遍历的 for循环 没有返回值
```

在forEach 里面 return 不会终止迭代 , forEach 可以使用return中止这一层循环后续的代码执行 , **但是不能使用break**

forEach无法在所有元素都传递给调用的函数之前终止（而for循环却有break方法），**如果要提前终止**，必须把forEach放在try块中，并能抛出一个异常。

如果forEach()调用的函数抛出foreach.break异常，循环会提前终止

### includes()

**判断一个数组是否包含一个指定的值，如果是返回true，否则返回false**

**注意：对象数组不能使用includes方法来检测,使用 includes()比较字符串和字符时是区分大小写。**

**Array1.includes(value, fromIndex)**

includes可以包含两个参数，**第二个参数表示判断的起始位置,起始位置第一个数字是0。**

```js
console.log([1,2,3,4].includes(1))   //true
console.log([1,2,3,4].includes(5))   //false
console.log([1,2,3,4].includes(1,0))   //true
console.log([1,2,3,4].includes(2,2))   //false
console.log([1,2,3,4].includes(3,2))   //true
```

### indexOf()

**该方法将从头到尾地检索数组，看它是否含有对应的元素。如果找到一个 item，则返回 item 的第一次出现的位置。开始位置的索引为 0。**
**如果在数组中没找到指定元素则返回 -1。**

第二个参数 从第几位开始

**Array1.indexOf(value, fromIndex)**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.indexOf("a", 2)); //3
```

### isArray()

**判断一个对象是否为数组。返回bool值。**
**Array.isArray(obj)**

```js
let arr=["a","b","c","a","b","c"];
console.log(Array.isArray(arr)); // true
```

### join()

**把数组中的所有元素转换为一个字符串，元素通过分隔符分隔。**
**若没有指定分隔符则用逗号来分隔元素。**

**传入undefined会默认用逗号分隔。**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.join())   // a,b,c,a,b,c
console.log(arr.join(","))   // a,b,c,a,b,c
console.log(arr.join("."))   // a.b.c.a.b.c
console.log(arr.join("-"))   // a-b-c-a-b-c
```

### lastIndexOf()

**返回一个指定的元素在数组中最后出现的位置，从后向前查找。若没有找到，则返回-1。**
**数组的检索位置从0开始。**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.lastIndexOf("a")) // 3
console.log(arr.lastIndexOf("a",2)) // 0
```

### map()

**通过指定函数处理数组的每个元素，并返回处理后的数组。**

```js
let arr=["a","b","c","a","b","c"];
let Array1 = arr.map((item) => {
  return item = item + 1
})
console.log(Array1);
// [ 'a1', 'b1', 'c1', 'a1', 'b1', 'c1' ]
let array1 = [1, 4, 9, 16];
const map1 = array1.map(x => {
  if (x === 4) {
    return x * 2;
  }
});
console.log(map1);
// [ undefined, 8, undefined, undefined ]
```

map()方法创建了一个新数组，但新数组并不是在遍历完array1后才被赋值的，而是**每遍历一次就得到一个值**

```js
var array1 = [1, 4, 9, 16];
 
const map1 = array1.map(x => {
    if (x == 4) {
        return x * 2;
    }
});
 
console.log(map1);
// > Array [undefined, 8, undefined, undefined]
```

### pop()

**pop()删除并返回数组的最后一个元素。**

**影响原数组** 

如果数组变为空，则该方法不改变数组，返回undefine值

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.pop()); //c
```

### shift()

**shift()删除并返回数组的第一个元素。**

**影响原数组** 

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.shift()); //a
```

### push()

**push()向数组的末尾添加一个或多个元素，并返回该数组的新长度。**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.push("1")); // 7
let Array1 = arr.push("b")
console.log(Array1); // 8
let array1 = [1, 4, 9, 16];
array1.push("1","2","3","4")
console.log(array1);
// [
//    1,   4,   9,   16,
//   '1', '2', '3', '4'
// ]
```

### unshitf()

**unshitf()赂数组的开头添加一个或多个元素，并返回数组的新长度。**

```js
let arr=["a","b","c","a","b","c"];
arr.unshift("a")
console.log(arr.unshift("a")) //8
console.log(arr)
// [
//   'a', 'a', 'b',
//   'c', 'a', 'b',
//   'c'
// ]
```

### reduce()

**reduce 有两个参数 ,第一个参数为 callback 函数 ,第二个参数 是初始值**

**callback 函数中有四个参数(上一次回调时返回的值,当前的值,当前索引,原数组)**

**arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])**

**这个很容易,不要被误导很难的想法**

相当于一个累加的效果,将前面运算的结果与当前的值进行运算

```js
let arr=["a","b","c","a","b","c"];
let Array = arr.reduce((pre,now,index,arr) => {
  return pre + now
},0)
console.log(Array);
// 0abcabc
Array = arr.reduce((pre,now,index,arr) => {
  return pre + pre
},0)
console.log(Array);
// 0
arr=[1,2,3,4,5,6,10];
Array = arr.reduce((pre,now,index,arr) => {
  return pre + now
},0)
console.log(Array);
// 31
```

一个数组去重的实现

```js
let arr = [1, 2, 3, 3, 4, 2]
let newArr = arr.reduce((pre, cur) => {
  if (!pre.includes(cur)) {
    return pre.concat(cur)
  } else {
    return pre
  }
}, [])
console.log(newArr)
```

在对象中的使用

```js
let arr = [
  {subject: 'math', score: 10},
  {subject: 'chinese', score: 20},
  {subject: 'english', score: 310}
]
let sum = arr.reduce((pre, cur) => {
  return cur.score + pre
}, 0)
console.log(sum) //340
```

**举例 1**、求和：

计算数组中所有元素项的总和。代码实现：

```javascript
const arr = [2, 0, 1, 9, 6];
// 数组求和
const total = arr.reduce((prev, item) => {
    return prev + item;
});

console.log('total:' + total); // 打印结果：18
```

**举例 2**、统计某个元素出现的次数：

代码实现：

```js
// 定义方法：统一 value 这个元素在数组 arr 中出现的次数
function repeatCount(arr, value) {
    if (!arr || arr.length == 0) return 0;

    return arr.reduce((totalCount, item) => {
        totalCount += item == value ? 1 : 0;
        return totalCount;
    }, 0);
}

let arr1 = [1, 2, 6, 5, 6, 1, 6];

console.log(repeatCount(arr1, 6)); // 打印结果：3
```

**举例 3**、求元素的最大值：

代码实现：

```js
const arr = [2, 0, 1, 9, 6];
// 数组求最大值
const maxValue = arr.reduce((prev, item) => {
    return prev > item ? prev : item;
});

console.log(maxValue); // 打印结果：9
```



### sort()

**sort()对数组的元素进行排序。排序顺序可以是字母或数字，并按升序或降序，默认按字母升序。**

**在使用sort()方法时，可以使用箭头函数,比较好看**

```js
array.sort((a, b) => b - a);
```

**如果在使用 sort() 方法时不带参，则默认按照Unicode 编码，从小到大进行排序。**

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();
console.log(fruits,'fruits')
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/c16036ec4a744d6381a6e4bd5ee631a4.png)


对数字排序

```js
var numbers = [8,13,5,7,0,20,6,1];
numbers.sort();
console.log(numbers)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/43b0b22b8e0842178f673f40419a5003.png)


**可以看出对数值的排序并不是理想状态**

此时打印出来的数组并不是按照升序进行排序，上面说到sort()默认是按照Unicode编码进行排序，

所以即使13 < 20，13也会在20的前面，因为13的第一位是1。

**数字与字母混合排序**

```js
var minx = [8,13,5,7,0,20,6,1,"Banana", "Orange", "Apple", "Mango"];
minx.sort();
console.log(minx)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b814eeba1e3443aea1d4cf09f73b7c35.png)




```js
let arr = ['General','Tom','Bob','John','Army'];
let resArr = arr.sort();
console.log(resArr);//输出   ["Army", "Bob", "General", "John", "Tom"]

let arr2 = [30,10,111,35,1899,50,45];
let resArr2 = arr2.sort();
console.log(resArr2);//输出   [10, 111, 1899, 30, 35, 45, 50]
```

使用数字排序，你必须通过一个函数作为参数来调用。

**<font color="red">原理:  (理解了原理随便玩)</font>**

**sort()里面的函数返回值如果大于0，则a、b交换位置；（数组原本位置为a在b的前面）**

如果返回值小于0，则a、b不交换位置；

如果返回值等于0，则a、b的位置不变。

**简单的记忆: a-b是升序,b-a是降序**

**升序排列**

```js
let arr=[20,20,4,22,23];
console.log(arr.sort(function (a, b) { //升序
  return a - b
}));  
// [ 4, 20, 20, 22, 23 ]
```

**降序排列**

```js
let arr=[20,20,4,22,23];
console.log(arr.sort(function (a, b) { //降序
  return b - a
}));  
// [ 23, 22, 20, 20, 4 ]
```

**多排序**

```js
let arr6 = [{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9}];
	arr6.sort(function(a,b){
		if(a.id === b.id){//如果id相同，按照age的降序
			return b.age - a.age
		}else{
			return a.id - b.id
		}
	})
	console.log(arr6);
	//输出新的排序
	//		{id: 2, age: 8}
	//		{id: 5, age: 4}
	//		{id: 6, age: 10}
	//		{id: 9, age: 6}
	//		{id: 10, age: 9}
	//		{id: 10, age: 2}
```


### reverse()

**reverse()反转数组的元素顺序。**

```js
let arr=["b","o","a","m"];
arr.sort(); //字母升序
arr.reverse(); //反转顺序
console.log(arr)
// o,m,b,a
```

### slice()

**选取数组的一部分，并返回新数组。**

如果是负数，则表示从数组尾部开始算起

```js
let arr=["b","o","a","m"];
console.log(arr.slice(1,3)); // [ 'o', 'a' ]
arr=["b","o","a","m"];
console.log(arr.slice(1)); // [ 'o', 'a', 'm' ]
```

```js
let arr=["b","o","a","m","c"];
console.log(arr.slice(-3, -1));  //[ 'a', 'm' ]
```

### splice()   !important

**从数组中添加或删除更改元素,注意: 会改变原始数组,返回删除的元素  个人最喜欢使用的方法**

**array.splice(index,deleteNumber,item1,item2)**

**其中的参数第一个是操作的数组下标index，而第二个是删除个数，之后的  可选参数  是增加内容**

**1. 删除操作**

splice(0) 会把原数组清空。

```js
let arr=["b","o","a","m"];
arr.splice(0)
console.log(arr);
// []
let array = ["a", "b", "c", "d", "e", "1"]
console.log(array.splice(0, 2));
console.log(array)
// [ 'a', 'b' ]
// [ 'c', 'd', 'e', '1' ]
```

> 举例4\：（删除指定元素，用得很多）

```js
const arr4 = ['a', 'b', 'c', 'd'];
arr4.splice(arr4.indexOf('c'), 1); // 删除数组中的'c'这个元素
```



**2. 增加操作**

```js
let array = ["a", "b", "c", "d", "e", "1"]
console.log(array.splice(0, 0,"23"));
console.log(array)
// []
// [
//   '23', 'a', 'b',
//   'c',  'd', 'e',
//   '1'
// ]
```

**3. 修改操作**

```js
let array = ["a", "b", "c", "d", "e", "1"]
console.log(array.splice(2, 0,"23"));
console.log(array)
// []
// [
//   'a', 'b', '23',
//   'c', 'd', 'e',
//   '1'
// ]
```

###### splice()练习：数组去重

代码实现：

```javascript
//创建一个数组
var arr = [1, 2, 3, 2, 2, 1, 3, 4, 2, 5];

//去除数组中重复的数字
//获取数组中的每一个元素
for (var i = 0; i < arr.length; i++) {
    //console.log(arr[i]);
    /*获取当前元素后的所有元素*/
    for (var j = i + 1; j < arr.length; j++) {
        //console.log("---->"+arr[j]);
        //判断两个元素的值是否相等
        if (arr[i] == arr[j]) {
            //如果相等则证明出现了重复的元素，则删除j对应的元素
            arr.splice(j, 1);
            //当删除了当前j所在的元素以后，后边的元素会自动补位
            //此时将不会在比较这个元素，我需要再比较一次j所在位置的元素
            //使j自减
            j--;
        }
    }
}

console.log(arr);
```


### toString()

**将数组转化成字符串**

```js
let arr=["b","o","a","m"];
console.log(arr.toString())
// b,o,a,m
```

### Array.from()

> **伪数组**：包含 length 属性的对象或可迭代的对象。
> 另外，伪数组的原型链中没有 Array.prototype，而真数组的原型链中有  Array.prototype。因此伪数组没有数组的一般方法，比如 pop()、join() 等方 法。

用于类似数组的对象（**必须拥有length属性的对象**）和可遍历对象转为真正的数组。

**注意下面的三种结果差别**

```js
let json1 = {
  "0": "123",
  "1": "123",
  "2": "123"
}
let json2 = {
  "1": "123",
  "2": "123",
  "3": "123",
  length: 3
}
let json3 = {
  "0": "123",
  "1": "123",
  "2": "123",
  length: 3
}
let arr1 = Array.from(json1)
let arr2 = Array.from(json2)
let arr3 = Array.from(json3)
console.log(arr1);
console.log(arr2);
console.log(arr3);
// []
// [ undefined, '123', '123' ]
// [ '123', '123', '123' ]
```

将字符串转换为数组

```js
let array1 = "alone to find"
console.log(Array.from(array1))
// [
//   'a', 'l', 'o', 'n',
//   'e', ' ', 't', 'o',
//   ' ', 'f', 'i', 'n',
//   'd'
// ]
```

伪数组的举例

###### 

```html
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>

    <script>
        let btnArray = document.getElementsByTagName('button');
        console.log(btnArray);
        console.log(btnArray[0]);
    </script>
</body>
```

上面的布局中，有三个 button 标签，我们通过`getElementsByTagName`获取到的`btnArray`实际上是**伪数组**，并不是真实的数组

**但是如果我们想要用到数组的方法该怎么办呢?**

解决办法：采用`Array.from`方法将`btnArray`这个伪数组转换为真数组即可：

```javascript
Array.from(btnArray);
```

然后就可以使用数组的一般方法了

###  Array.of()

**将一组值转变为数组**

```js
let arr1 = Array.of(1,2,3)
let arr2 = Array.of([1,2,3])
let arr3 = Array.of({"1":"1"})
let arr4 = Array.of()
console.log(arr1)
console.log(arr2)
console.log(arr3)
console.log(arr4)
// [ 1, 2, 3 ]
// [ [ 1, 2, 3 ] ]
// [ { '1': '1' } ]
// []
```

补充：`new Array()`和 `Array.of()`的区别在于：当参数只有一个时，前者表示数组的长度，后者表示数组中的内容。

### keys()、values()、entries()

这三个方法都是返回一个遍历器对象，可用for...of循环遍历，**唯一区别：keys()是对键名的遍历、values()对键值的遍历、entries()是对键值对的遍历。**

```js
let arr = ["a","b","c","d"];
for(let i of arr.keys()){
  console.log(i);
}
// 0
// 1
// 2
// 3
for(let i of arr.values()){
  console.log(i);
}
// a
// b
// c
// d
for(let i of arr.entries()){
  console.log(i);
}
// [ 0, 'a' ]
// [ 1, 'b' ]
// [ 2, 'c' ]
// [ 3, 'd' ]
```

## 5. 扩展

### 扩展运算符

扩展运算符可以将数组或者对象转为用逗号分隔的参数序列

```javascript
 let ary = [1, 2, 3];
 ...ary  // 1, 2, 3
 console.log(...ary);    // 1 2 3,相当于下面的代码
 console.log(1,2,3);
```

#### 合并数组

```javascript
// 方法一 
 let ary1 = [1, 2, 3];
 let ary2 = [3, 4, 5];
 let ary3 = [...ary1, ...ary2];
 // 方法二 
 ary1.push(...ary2);
```

#### 将类数组转换为真正的数组

```javascript
let oDivs = document.getElementsByTagName('div'); 
oDivs = [...oDivs];
```

扩展运算符和剩余参数是相反的。

剩余参数是将剩余的元素放到一个数组中；而扩展运算符是将数组或者对象拆分成逗号分隔的参数序列。

代码举例：

```js
const arr = [10, 20, 30];
...arr // 10, 20, 30      注意，这一行是伪代码，这里用到了扩展运算符
console.log(...arr); // 10 20 30

console.log(10, 20, 30); // 10 20 30
```

上面的代码要仔细看：

`arr`是一个数组，而`...arr`则表示`10, 20, 30`这样的序列。

我们把`...arr` 打印出来，发现打印结果竟然是 `10 20 30`，为啥逗号不见了呢？因为逗号被当作了 console.log 的参数分隔符。如果你不信，可以直接打印 `console.log(10, 20, 30)` 看看。

接下来，我们看一下扩展运算符的应用。

### 数组赋值

数组赋值的代码举例：

```js
let arr2 = [...arr1]; // 将 arr1 赋值给 arr2
```

为了理解上面这行代码，我们先来分析一段代码：（将数组 arr1 赋值给 arr2）

```javascript
let arr1 = ['www', 'smyhvae', 'com'];
let arr2 = arr1; // 将 arr1 赋值给 arr2，其实是让 arr2 指向 arr1 的内存地址
console.log('arr1:' + arr1);
console.log('arr2:' + arr2);
console.log('---------------------');

arr2.push('你懂得'); //往 arr2 里添加一部分内容
console.log('arr1:' + arr1);
console.log('arr2:' + arr2);
```

运行结果：

![](https://img-blog.csdnimg.cn/img_convert/175332a5ca4db42a2c38ff9497083235.png)

上方代码中，我们往往 arr2 里添加了`你懂的`，却发现，arr1 里也有这个内容。原因是：`let arr2 = arr1;`**其实是让 arr2 指向 arr1 的地址。也就是说，二者指向的是同一个内存地址。**

如果不想让 arr1 和 arr2 指向同一个内存地址，我们可以借助**扩展运算符**来做：

```javascript
let arr1 = ['www', 'smyhvae', 'com'];
let arr2 = [...arr1]; //【重要代码】arr2 会重新开辟内存地址
console.log('arr1:' + arr1);
console.log('arr2:' + arr2);
console.log('---------------------');

arr2.push('你懂得'); //往arr2 里添加一部分内容
console.log('arr1:' + arr1);
console.log('arr2:' + arr2);
```

运行结果：

```bash
arr1:www,smyhvae,com
arr2:www,smyhvae,com
---------------------
arr1:www,smyhvae,com
arr2:www,smyhvae,com,你懂得
```

我们明白了这个例子，就可以避免开发中的很多业务逻辑上的 bug。

### 解构赋值并重命名

```js
let obj = {
    key1: 'value1',
    key2: 'value2',
    key3: 'value3',
}

// 常规写法：
let key1 = obj.key1;
let key2 = obj.key2;
let key3 = obj.key3;


// 简写：
const { key1, key2, key3 } = obj;

// 简写并重命名key
const { key1: aliasKey, key2, key3 } = obj;
console.log(key1); // key1 is not defined
console.log(aliasKey);  // 'value1'
```

### 合并数组

代码举例：

```js
let arr1 = ['王一', '王二', '王三'];
let arr2 = ['王四', '王五', '王六'];
// ...arr1  // '王一','王二','王三'
// ...arr2  // '王四','王五','王六'

// 方法1
let arr3 = [...arr1, ...arr2];
console.log(arr3); // ["王一", "王二", "王三", "王四", "王五", "王六"]

// 方法2
arr1.push(...arr2);
console.log(arr1); // ["王一", "王二", "王三", "王四", "王五", "王六"]
```

### 将伪数组或者可遍历对象转换为真正的数组

代码举例：

```js
const myDivs = document.getElementsByClassName('div');
const divArr = [...myDivs]; // 利用扩展运算符，将伪数组转为真正的数组
```


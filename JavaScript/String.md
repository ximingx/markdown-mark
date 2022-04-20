

# String

## 字符串的定义

常规方法 “” ‘’ `` 都可以

```js
// 一: 以使用一对单引号或者一对双引号来定义一个字符串
let str1 = "str1"
console.log(str1) // str1
let str2 = 'str2'
console.log(str2) // str2
// 1. 在 JavaScript 中双引号定义的字符串和单引号定义的字符串没有本质区别

// 2. 无论是单引号还是双引号，都必须配对使用，不能一个单引号和双引号配对
let str3 = "str3'"0
console.log(str3) //str'
// 3. 单引号中的字符串中不能出现单引号，可以出现双引号
//    双引号中的字符串中不能出现双引号，可以出现单引号

// 4. 单引号和双引号定义字符串时，须在一行内完成,不能换行

// 二: 使用模板字符串的方式定义字符串：我们可以使用一对反引号来定义字符串 (tab 键上面的 ``)
let str4 = `这是一个普通的字符串`
let str5 = `这是一个换行的 
字符串`
let str6 = 7
let str7 = 6
// 模板字符串利用 ${} 使用变量
let str8 = `这是一个可以解析变量的字符串，例如：${str6 + str7}`
console.log(str4) // 这是一个普通的字符串
console.log(str5) /* 这是一个换行的 
字符串 */
console.log(str6) // 7
console.log(str7) // 6
console.log(str8) // 这是一个可以解析变量的字符串，例如：13
// ${varName}或${value}。即${}中可为变量名，也可直接为字面量值(如${123}或${asd})。
```

不关心里面的内容是什么,只匹配对应的 “” ‘’ `` 与转义符

```js
let str1 = "true";  //把布尔值转换为字符串
console.log(str1)
let str2 = "123";  //把数值转换为字符串
console.log(str2)
let str3 = "[1,2,3]";  //把数组转换为字符串
console.log(str3)
let str4 = "{x : 1; y : 2}";  //把对象转换为字符串
console.log(str4)
let str5 = "console.log('Hello,World')";  //把可执行表达式转换为字符串
console.log(str5)
// true
// 123
// [1,2,3]
// {x : 1; y : 2}
// console.log('Hello,World')
console.log(typeof str1)
console.log(typeof str2)
console.log(typeof str3)
console.log(typeof str4)
console.log(typeof str5)
// string
// string
// string
// string
// string
```

转义符: `\`

```js
// 在定义一个字符串的时候，有些特殊字符并不适合直接出现。例如：换行符、单引 号（不能出现在单引号内）、双引号（不能出现在双引号内）
```

例如 下面是错误的

```js
let str = " " " 
// 会直接报语法错误
```

但是我们需要这样去使用 , 这个时候可以我们就需要使用 `\` 转义符，例如： 

```js
// 在这里使用了\n 来代表换行符
// 在这里使用了\"来代表双引号。
let str1 = '这是一个换行的\n字符串'
let str2 = '这是一个换行的\' 字符串'
console.log(str1)
console.log(str2)
/* 这是一个换行的
字符串 */
// 这是一个换行的' 字符串
let str3 = `123 
str3 \"\'`
// 如果使用模板字符串的方式定义字符串，可以直接使用回车换行。但是要在其中使用 反引号`，也必须转义
console.log(str3)
// 123
// str3 "'
```

## String 对象的属性

**字符串可以看成是字符组成的数组**,拥有属性 length ------> 字符串的长度,可以通过for循环进行遍历

```js
let  str = 'abcd'
for(let i of str) {
  console.log(i)
}
// a
// b
// c
// d
```

**字符串特性:不可变性,字符串的值是不能改变**

## String 对象的方法

![在这里插入图片描述](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204201646902.png)

### localeCompare()

**这里先说明一个东西: 字符比较是指按照字典次序对单个字符或字符串进行比较大小的操作，一般都是以Unicode码值的大小作为字符比较的标准。**

JS字符串在进行大于(小于)比较时，**会根据第一个不同的字符的Unicode值码进行比较**

下面演示一些案例

```js
let a="91";                   
let b="390"                    
console.log(a.charCodeAt())    // 57
console.log(b.charCodeAt())    // 51
console.log(a<b)               // false
```

**“91” < “390” 结果为 false** 

**字符串在比较的时候会转化为ascll 的打印字符**（9是57,3是51），会依次比较字符，如果第一个字符相等就比较下一个或遇到‘\0’为止。  ，所以在比较的时候一定要转化为number来比较

所以解释一下上面的结果

a 中第一个字符为 9 , b 中第一个字符为 3 ,两者不同,所以开始比较他们的 ascll , a 的 acsll (57) 大于 a 的 acsll (51) 所以 **“91” < “390” 结果为 false** 

```js
let a = 34
let b = "34"
console.log( a == b ) //true
```

**如果一个是字符串,一个是数值,会倾向于将字符串转换为数值然后进行比较**

下面说正题

因为后一个参数浏览器支持不是很友好，就不多做介绍

一般的用法就是 a.localeCompare(b)，浏览器基本都是支持的。

```js
let str1 = "123456"
let str2 = "1234567"
let str3 = "12345678"
let str4 = "123478"
let str5 = "abcd"
let str6 = "dcba"
// 返回值大于0：说明当前字符串string大于对比字符串targetString
//
// 返回值小于0：说明当前字符串string小于对比字符串targetString
//
// 返回值等于0：说明当前字符串string等于对比字符串targetString
console.log(str1.localeCompare(str2)); // -1
console.log(str2.localeCompare(str2)); // 0
console.log(str3.localeCompare(str2)); // 1
console.log(str4.localeCompare(str2)); // 1
console.log(str5.localeCompare(str6)); // -1
```

### charCodeAt()

```js
// 返回字符串 index 位置的 Unicode 编码 , 默认为 0 号位置
console.log("a".charCodeAt(0))
console.log("aabb".charCodeAt(2))
// 97
// 98
```

### charAt()

```js
// charAt（index）
// 返回指定位置（index）的字符。
// 如果index小于0或者大于等于字符串的长度string.length，它会返回空字符串。
let str = "str1"
console.log(str.charAt(1))
console.log(str.charAt(5))
// t
// 
```

### String.fromCharCode()

```js
console.log(String.fromCharCode( 5, 66, 67, 68, 69, 70, 71 ))
console.log(String.fromCharCode( 38 ))
console.log(String.fromCharCode( 13, 22269 ))
console.log(String.fromCharCode())
// ║BCDEFG
// &
// 国
// 
```

### slice()

注意：

1.   字符串的索引是从0到 length-1
2.   slice（start, end）
3.   substring（start, to）
4.   substr（start，length）与前两者不同的是第二个参数是长度
5.   **三者的差别很细,具体仔细看下面案例结果**

```js
// slice（start,end）
// 截取字符串 start 索引位置到 end 索引位置之前的字符串
// start 参数字符串中第一个字符位置为 0, 第二个字符位置为 1, 以此类推，如果是负数表示从尾部截取多少个字符串，slice(-2) 表示提取原数组中的倒数第二个元素到最后一个元素（包含最后一个元素）。
// end 参数如果为负数，-1 指字符串的最后一个字符的位置，-2 指倒数第二个字符，以此类推。
let str1 = "123456789"
console.log(str1.slice(0, str1.length))
// 123456789
let str2 = "123456789"
console.log(str2.slice(1, 3))
// 23
console.log(str2.slice(-2))
// 89
// 使用 slice() 原数组不会发生改变
console.log(str2)
// 123456789
console.log(str1.slice(0,-1))
// 参数为负数时，处理字符串从末尾开始
// 12345678
console.log(str1.slice(6, -5))
//
console.log(str1.slice(3, -5))
// 4
```

### substr()

```js
// substr（start，length）
// 从 start 索引位开始,截取长度为 length 的字符串,若果没有 length,将后面的全部截取
let str = "str1"
console.log(str.substr(1))
console.log(str.substr(1,2))
// 对,没错,最后的结果为空字符串
console.log(str.substr(1,-1))
// tr1
// tr
// 
```

### substring()

```js
// substring（start，to）
let str = "str1"
console.log(str.substring(0))
console.log(str.substring(1,2))
// 如果参数 start 与 end 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。
console.log(str.substring(1,1))
// start => to 如果start的数值大于to的位置 , 可以理解为把两个参数位置颠倒
console.log(str.substring(3,1))
console.log(str.substring(2,1))
console.log(str.substring(4,2))
// str1
// t
//
// tr
// t
// r1
```

### concat()

```js
// concat()
// 一般字符串的拼接可以直接使用 + 连接
console.log("c".concat("23", "str"));
// c23str
```

### indexOf()

```js
// indexOf（searchString，position）
let str1= "123qwe"
console.log(str1.indexOf("2"))
console.log(str1.indexOf("a"))
console.log(str1.indexOf("ad"))
console.log(str1.indexOf("ae"))
console.log(str1.indexOf("we"))
console.log(str1.indexOf("we",5))
// 1
// -1
// -1
// -1
// 4
// -1
```

**案例**：查找字符串"qianguyihao"中，所有 `a` 出现的位置以及次数。

思路：

（1）先查找第一个 a 出现的位置。

（2）只要 indexOf 返回的结果不是 -1 就继续往后查找。

（3）因为 indexOf 只能查找到第一个，所以后面的查找，可以利用第二个参数，在当前索引加 1，从而继续查找。

代码实现：


```js
var str = 'qianguyihao';
var index = str.indexOf('a');
var num = 0;
while (index !== -1) {
    console.log(index);
    num++; // 每打印一次，就计数一次
    index = str.indexOf('o', index + 1);
}

console.log('a 出现的次数是: ' + num);
```

### lastIndexOf()

```js
// lastIndexOf（searchString，position）
let str1= "123qwe"
// 与indexOf方法类似，只不过它是从该字符串的末尾开始查找而不是从开头。
console.log(str1.lastIndexOf("2"))
console.log(str1.lastIndexOf("a"))
console.log(str1.lastIndexOf("ad"))
console.log(str1.lastIndexOf("ae"))
console.log(str1.lastIndexOf("we"))
console.log(str1.lastIndexOf("we",5))
// 1
// -1
// -1
// -1
// 4
// 4
```

### replace()

```js
let str1 = "121416"
let str2 = "1234567"
// 只会替换第一个匹配到的字符
console.log(str1.replace("1",str2))
// 123456721416
```

```js
var stringObj="终古，终古人民";
var newstr=stringObj.replace("终古","中国"); 
// 中国，终古人民
```

会发现第二个错别字“终古”并没有被替换成“中国”

```js
var reg=new RegExp("终古","g"); //创建正则RegExp对象
var stringObj="终古，终古人民";
var newstr=stringObj.replace(reg,"中国"); 
// 中国，中国人民
```

### split()

```js
let str1 = "深入 Vue底层，手写一个vuex\n 348\n"
// split() 将以传递的参数把字符串分割,最后返回一个数组
console.log(str1.split(" "))
// [ '深入', 'Vue底层，手写一个vuex\n', '348\n' ]
console.log(str1.split("\n"))
// [ '深入 Vue底层，手写一个vuex', ' 348', '' ]
```

第二个参数代表分割次数

```js
let str = "山东省-济南市-市中区"
let newStr = str.split('-')
console.log(newStr)// ["山东省","济南市","市中区"]

//第二个参数times，匹配'-'两次
let str = "山东省-济南市-市中区"
let newStr = str.split('-',2)
console.log(newStr)//["山东省", "济南市"]
```

### includes()

```js
// 返回布尔值，表示是否找到了参数字符串。
let str = '这是测试字符串';
if (str.indexOf('测试') !== -1) {
  console.log(true)    //包含
} else {
  console.log(false)    //不包含
}
// true
```

### startsWith()

```js
// 返回布尔值，表示参数字符串是否在原字符串的头部。
let str = '这是测试字符串';
if (str.startsWith('这') === true) {
  console.log(true)
} else {
  console.log(false)
}
if (str.startsWith('是') === true) {
  console.log(true)
} else {
  console.log(false)
}
// true
// false
```

### endsWith()

```js
// 返回布尔值，表示参数字符串是否在原字符串的尾部。
let str = '这是测试字符串';
if (str.endsWith('这') === true) {
  console.log(true)
} else {
  console.log(false)
}
if (str.endsWith('串') === true) {
  console.log(true)
} else {
  console.log(false)
}
// false
// true
```

-   includes() startsWith() endsWith() 这三个方法都支持第二个参数，表示开始搜索的位置。如果repeat的参数是负数或者Infinity，会报错。

### repeat()

```js
// repeat方法返回一个新字符串，表示将原字符串重复n次。参数如果是小数，会被取整。
let str = '这是测试字符串';
console.log(str.repeat(3));
// 这是测试字符串这是测试字符串这是测试字符串
```

### padStart()    padEnd()

-   ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。padStart()用于头部补全，padEnd()用于尾部补全。

```js
console.log('x'.padStart(5, 'ab')) // 'ababx'
console.log('x'.padStart(4, 'ab')) // 'abax'
console.log('x'.padEnd(5, 'ab')) // 'xabab'
console.log('x'.padEnd(4, 'ab')) // 'xaba'
// 如果原字符串的长度，等于或大于最大长度，则字符串补全不生效，返回原字符串

// 如果省略第二个参数，默认使用空格补全长度。

// padStart()的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。
console.log('1'.padStart(10, '0')) 
console.log('12'.padStart(10, '0')) 
console.log('123456'.padStart(10, '0')) 
// 0000000001
// 0000000012
// 0000123456
// 另一个用途是提示字符串格式。
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

### trim()

```js
var str = '   hello   '
console.log(str.trim()）  // hello 去除两端空格
var str1 = '   he l l o   '
console.log(str.trim()）  // he l l o  去除两端空格
```

### trimStart()，trimEnd()

-   ES2019 对字符串实例新增了trimStart()和trimEnd()这两个方法。它们的行为与trim()一致，trimStart()消除字符串头部的空格，trimEnd()消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

```js
const s = '  abc  ';
s.trim() // "abc"
s.trimStart() // "abc  "
s.trimEnd() // "  abc"
```

### search()

search() 方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。
如果没有找到任何匹配的子串，则返回 -1。

**search()方法查找时是对大小写敏感的。**

```js
let str = "abcd Abcd abc"
console.log(str.search("abc"))
// 0
console.log(str.search("Abc"))
// 5
```

### match(正则表达式)

```js
let article = "12345657abcdeABCDE123"
console.log(article.match("123"));
// [ '123', index: 0, input: '12345657abcdeABCDE', groups: undefined ]
console.log(article.match("3"));
// [ '3', index: 2, input: '12345657abcdeABCDE123', groups: undefined ]
```

### toLowerCase() 

```js
let article = "this is pink"
console.log(article.toLowerCase())
console.log(article.toUpperCase())
// this is pink
// THIS IS PINK
```

##  扩展运算符

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



## 一些案例

### 检索文章中有多少个单词

```js
let article = `ECMAScript (/ˈɛkməskrɪpt/) (or ES)[1] is a general-purpose programming language, standardised 
by Ecma International according to the document ECMA-262. It is a JavaScript standard meant to ensure the 
interoperability of web pages across different web browsers.[2] ECMAScript is commonly used for client-side 
scripting on the World Wide Web, and it is increasingly being used for writing server applications and 
services using Node.js.`
```

```js
// 方法一 , 但结果并不理想 , 有很多小细节让人不满足
let try1 = article.split(' ')
console.log(try1)
// [
//   'ECMAScript',         '(/ˈɛkməskrɪpt/)', '(or',
//   'ES)[1]',             'is',              'a',
//   'general-purpose',    'programming',     'language,',
//   'standardised',       '\nby',            'Ecma',
//   'International',      'according',       'to',
//   'the',                'document',        'ECMA-262.',
//   'It',                 'is',              'a',
//   'JavaScript',         'standard',        'meant',
//   'to',                 'ensure',          'the',
//   '\ninteroperability', 'of',              'web',
//   'pages',              'across',          'different',
//   'web',                'browsers.[2]',    'ECMAScript',
//   'is',                 'commonly',        'used',
//   'for',                'client-side',     '\nscripting',
//   'on',                 'the',             'World',
//   'Wide',               'Web,',            'and',
//   'it',                 'is',              'increasingly',
//   'being',              'used',            'for',
//   'writing',            'server',          'applications',
//   'and',                '\nservices',      'using',
//   'Node.js.'
// ]
```

```js
let template = `qwertyuiopasdfghjklzxcvbnm`
let word = ''
let list = []
let obj = {}
for (let i = 0; i < article.length; i++) {
  if (template.indexOf(article[i].toLowerCase()) !== -1 ) {
    word += article[i].toLowerCase()
  } else {
    if (word !== '') {
      list.push(word)
      word = ''
    }
  }
}
console.log(list)
// [
//   'ecmascript',       'km',          'skr',
//   'pt',               'or',          'es',
//   'is',               'a',           'general',
//   'purpose',          'programming', 'language',
//   'standardised',     'by',          'ecma',
//   'international',    'according',   'to',
//   'the',              'document',    'ecma',
//   'it',               'is',          'a',
//   'javascript',       'standard',    'meant',
//   'to',               'ensure',      'the',
//   'interoperability', 'of',          'web',
//   'pages',            'across',      'different',
//   'web',              'browsers',    'ecmascript',
//   'is',               'commonly',    'used',
//   'for',              'client',      'side',
//   'scripting',        'on',          'the',
//   'world',            'wide',        'web',
//   'and',              'it',          'is',
//   'increasingly',     'being',       'used',
//   'for',              'writing',     'server',
//   'applications',     'and',         'services',
//   'using',            'node',        'js'
// ]
list.forEach(function (item) {
  if (obj[item] === undefined) {
    obj[item] = 1
  } else  {
    obj[item]++
  }
})
console.log(obj);
// {
//   ecmascript: 2,
//   km: 1,
//   skr: 1,
//   pt: 1,
//   or: 1,
//   es: 1,
//   is: 4,
//   a: 2,
//   general: 1,
//   purpose: 1,
//   programming: 1,
//   language: 1,
//   standardised: 1,
//   by: 1,
//   ecma: 2,
//   international: 1,
//   according: 1,
//   to: 2,
//   the: 3,
//   document: 1,
//   it: 2,
//   javascript: 1,
//   standard: 1,
//   meant: 1,
//   ensure: 1,
//   interoperability: 1,
//   of: 1,
//   web: 3,
//   pages: 1,
//   across: 1,
//   different: 1,
//   browsers: 1,
//   commonly: 1,
//   used: 2,
//   for: 2,
//   client: 1,
//   side: 1,
//   scripting: 1,
//   on: 1,
//   world: 1,
//   wide: 1,
//   and: 2,
//   increasingly: 1,
//   being: 1,
//   writing: 1,
//   server: 1,
//   applications: 1,
//   services: 1,
//   using: 1,
//   node: 1,
//   js: 1
// }
```

### 查找所有 m 出现的位置。

代码实现：

```javascript
var str2 = 'smyhvaevaesmyh';
for (var i = 0; i < str2.length; i++) {
    //如果指定位置的符号=== "o"
    //str2[i]
    if (str2.charAt(i) === 'm') {
        console.log(i);
    }
}
```

### 字符串统计这个次数

```html
<script>
    var str2 = 'smyhvaevaesmyhvae';

    //定义一个json，然后判断json中是够有该属性，如果有该属性，那么值+1;否则创建一个该属性，并赋值为1；
    var json = {};
    for (var i = 0; i < str2.length; i++) {
        //判断：如果有该属性，那么值+1;否则创建一个该属性，并赋值为1；
        var key = str2.charAt(i);
        if (json[key] === undefined) {
            json[key] = 1;
        } else {
            json[key] += 1;
        }
    }
    console.log(json);

    console.log('----------------');
    //获取json中属性值最大的选项
    var maxKey = '';
    var maxValue = 0;
    for (var k in json) {
        if (json[k] > maxValue) {
            maxKey = k;
            maxValue = json[k];
        }
    }
    console.log(maxKey);
    console.log(maxValue);
</script>
```


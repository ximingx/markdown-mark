# JavaScript

##   Array

### 字符串的定义

常规方法 “” ‘’ `` 都可以

```js
// 一: 以使用一对单引号或者一对双引号来定义一个字符串
let str1 = "str1"
console.log(str1) // str1
let str2 = 'str2'
console.log(str2) // str2
// 1. 在 JavaScript 中双引号定义的字符串和单引号定义的字符串没有本质区别

// 2. 无论是单引号还是双引号，都必须配对使用，不能一个单引号和双引号配对
let str3 = "str3'"
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

### String 对象的属性

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

### String 对象的方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/562d7fc799554a2e9b73aeff4a5801db.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)



#### localeCompare() 

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

#### charCodeAt()

```js
// 返回字符串 index 位置的 Unicode 编码 , 默认为 0 号位置
console.log("a".charCodeAt(0))
console.log("aabb".charCodeAt(2))
// 97
// 98
```

#### charAt()

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

#### String.fromCharCode()

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

#### slice()

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

#### substr()

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

#### substring()

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

#### concat()

```js
// concat()
// 一般字符串的拼接可以直接使用 + 连接
console.log("c".concat("23", "str"));
// c23str
```

#### indexOf()

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

#### lastIndexOf()

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

#### replace()

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

#### split()

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

#### includes()

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

#### startsWith()

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

#### endsWith()

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

#### repeat()

```js
// repeat方法返回一个新字符串，表示将原字符串重复n次。参数如果是小数，会被取整。
let str = '这是测试字符串';
console.log(str.repeat(3));
// 这是测试字符串这是测试字符串这是测试字符串
```

#### padStart()    padEnd()

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

#### trimStart()，trimEnd()

-   ES2019 对字符串实例新增了trimStart()和trimEnd()这两个方法。它们的行为与trim()一致，trimStart()消除字符串头部的空格，trimEnd()消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

```js
const s = '  abc  ';
s.trim() // "abc"
s.trimStart() // "abc  "
s.trimEnd() // "  abc"
```

#### search()

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

#### match(正则表达式)

```js
let article = "12345657abcdeABCDE123"
console.log(article.match("123"));
// [ '123', index: 0, input: '12345657abcdeABCDE', groups: undefined ]
console.log(article.match("3"));
// [ '3', index: 2, input: '12345657abcdeABCDE123', groups: undefined ]
```

#### toLowerCase() ,toUpperCase()

```js
let article = "this is pink"
console.log(article.toLowerCase())
console.log(article.toUpperCase())
// this is pink
// THIS IS PINK
```

### 一些案例

检索文章中有多少个单词

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

### 字符串练习

#### **练习 1**："smyhvaevaesmyh"查找字符串中所有 m 出现的位置。

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

#### **练习 2**：判断一个字符串中出现次数最多的字符，统计这个次数

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

###  ...运算符 扩展运算符（展开语法）

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

#### 数组赋值

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

#### 合并数组

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

#### 将伪数组或者可遍历对象转换为真正的数组

代码举例：

```js
const myDivs = document.getElementsByClassName('div');
const divArr = [...myDivs]; // 利用扩展运算符，将伪数组转为真正的数组
```

##   String

### 1. 数组简介

数组（Array）属于**内置对象**

数组和普通对象的功能类似，也是用来存储一些值的。不同的是：

-   普通对象是使用字符串作为属性名的，而数组是使用数字作为**索引**来操作元素。索引：从 0 开始的整数就是索引。

数组的存储性能比普通对象要好。在实际开发中我们经常使用数组来存储一些数据（尤其是**列表数据**），使用频率非常高。

数组中的元素可以是任意的数据类型，也可以是对象，也可以是函数，也可以是数组。数组的元素中，如果存放的是数组，我们就称这种数组为二维数组。(可以以此类推多维数组)

### 2. 创建数组对象

#### 方式一：使用字面量创建数组

举例：

```js
let arr1 = [];   // 创建一个空数组
let arr2 = ["arr2"];   // 创建一个包含1个字符串的数组 ("arr2")
let arr3 = ["leo","is",18];   // 创建一个包含3项数据的数组

var arr1 = []; // 创建一个空的数组
var arr2 = [1, 2, 3]; // 创建带初始值的数组
```

#### 方式二：使用构造函数创建数组

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

#### Array.of 

Array.of()方法总会创建一个包含所有传入参数的数组，而不管参数的数量与类型

```js
let arr = Array.of(1,2);
console.log(arr.length);   // 2
console.log(arr[0]);   // 1
 
let arr1 = Array.of("leo");
console.log(arr1.length);   // 1
console.log(arr1[0]);   // "leo"
```

#### Array.from 方式

Array.from() 将可迭代对象或者类数组对象作为第一个参数传入，就能返回一个数组

```js
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

#### 数组中的元素的类型

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

### 3. 数组的基本操作

#### 数组的索引

**索引** (下标) ：用来访问数组元素的序号，代表的是数组中的元素在数组中的位置（下标从 0 开始算起）。

数组可以通过索引来访问、设置、修改对应的数组元素。我们继续看看。

#### 向数组中添加元素

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

#### 获取数组中的元素

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

#### 获取数组的长度

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




#### 修改数组的长度（修改 length）

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

#### 遍历数组

**遍历**: 就是把数组中的每个元素从头到尾都访问一次。

最简单的做法是通过 for 循环，遍历数组中的每一项。举例：

```javascript
var arr = [10, 20, 30, 40, 50];

for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]); // 打印出数组中的每一项
}
```

### 4. 数组的方法详细介绍

![在这里插入图片描述](https://img-blog.csdnimg.cn/a19346ab9fc34e04a3b7b322165afe9a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

#### 数组的方法清单

######## 数组的类型相关

| 方法                             | 描述                               | 备注 |
| :------------------------------- | :--------------------------------- | :--- |
| Array.isArray()                  | 判断是否为数组                     |      |
| toString()                       | 将数组转换为字符串                 |      |
| Array.from(arrayLike)            | 将**伪数组**转化为**真数组**       |      |
| Array.of(value1, value2, value3) | 创建数组：将**一系列值**转换成数组 |      |

注意，获取数组的长度是用`length`属性，不是方法。

######## 数组元素的添加和删除

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

######## 数组的合并和拆分

| 方法     | 描述                                                 | 备注             |
| :------- | :--------------------------------------------------- | :--------------- |
| concat() | 合并数组：连接两个或多个数组，返回结果为**新的数组** | 不会改变原数组   |
| join()   | 将数组转换为字符串，返回结果为**转换后的字符串**     | 不会改变原数组   |
| split()  | 将字符串按照指定的分隔符，组装为数组                 | 不会改变原字符串 |

注意，`split()`是字符串的方法，不是数组的方法。

######## 数组排序

| 方法      | 描述                                                    | 备注         |
| :-------- | :------------------------------------------------------ | :----------- |
| reverse() | 反转数组，返回结果为**反转后的数组**                    | 会改变原数组 |
| sort()    | 对数组的元素,默认按照**Unicode 编码**，从小到大进行排序 | 会改变原数组 |

######## 查找数组的元素

| 方法                  | 描述                                                         | 备注                                                     |
| :-------------------- | :----------------------------------------------------------- | :------------------------------------------------------- |
| indexOf(value)        | 从前往后索引，检索一个数组中是否含有指定的元素               |                                                          |
| lastIndexOf(value)    | 从后往前索引，检索一个数组中是否含有指定的元素               |                                                          |
| includes(item)        | 数组中是否包含指定的内容                                     |                                                          |
| find(function())      | 找出**第一个**满足「指定条件返回 true」的元素                |                                                          |
| findIndex(function()) | 找出**第一个**满足「指定条件返回 true」的元素的 index        |                                                          |
| every()               | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为真。要求每一项都返回 true，最终的结果才返回 true |
| some()                | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true | 一真即真。只要有一项返回 true，最终的结果就返回 true     |

######## 遍历数组

| 方法      | 描述                                                         | 备注                                                   |
| :-------- | :----------------------------------------------------------- | :----------------------------------------------------- |
| for 循环  | 这个大家都懂                                                 |                                                        |
| forEach() | 和 for 循环类似，但需要兼容 IE8 以上                         | forEach() 没有返回值。也就是说，它的返回值是 undefined |
| map()     | 对原数组中的每一项进行加工，将组成新的数组(最后的结果可能会含有undefined) | 不会改变原数组                                         |
| filter()  | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组                                         |
| reduce    | 接收一个函数作为累加器，返回值是回调函数累计处理的结果       |                                                        |


---

#### concat()

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

#### copyWithin()

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

#### every()

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

#### some()

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
```

#### fill()

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

#### filter()

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
```

#### find()

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

#### findindex()

**与 find() 方法相似,返回的结果为索引位置,返回通过函数判断的数组的  第一个元素的索引位置  。**

**Array1.find((item) => {return condition})**

```JS
let Array2 = [2,3,4,5]
console.log(Array2.findIndex((item) => {
  return item >= 3
}));
// 1
```

#### forEach()

**有三个参数  值,索引,和当前的数组  对每个元素进行一次调用**

**Array2.forEach((item,index,arr) => {return condition})**

```js
let Array2 = [2,3,4,5]
Array2.forEach((item,index,arr) => {
  item = item * index
  console.log(item)
})
// 0
// 3
// 8
// 15
```

forEach可以使用return中止这一层循环后续的代码执行 , **但是不能使用break**

forEach无法在所有元素都传递给调用的函数之前终止（而for循环却有break方法），**如果要提前终止**，必须把forEach放在try块中，并能抛出一个异常。

如果forEach()调用的函数抛出foreach.break异常，循环会提前终止

#### includes()

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

#### indexOf()

**该方法将从头到尾地检索数组，看它是否含有对应的元素。如果找到一个 item，则返回 item 的第一次出现的位置。开始位置的索引为 0。**
**如果在数组中没找到指定元素则返回 -1。**

第二个参数 从第几位开始

**Array1.indexOf(value, fromIndex)**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.indexOf("a", 2)); //3
```

#### isArray()

**判断一个对象是否为数组。返回bool值。**
**Array.isArray(obj)**

```js
let arr=["a","b","c","a","b","c"];
console.log(Array.isArray(arr)); // true
```

#### join()

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

#### lastIndexOf()

**返回一个指定的元素在数组中最后出现的位置，从后向前查找。若没有找到，则返回-1。**
**数组的检索位置从0开始。**

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.lastIndexOf("a")) // 3
console.log(arr.lastIndexOf("a",2)) // 0
```

#### map()

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

#### pop()

**pop()删除并返回数组的最后一个元素。**

**影响原数组** 

如果数组变为空，则该方法不改变数组，返回undefine值

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.pop()); //c
```

#### shift()

**shift()删除并返回数组的第一个元素。**

**影响原数组** 

```js
let arr=["a","b","c","a","b","c"];
console.log(arr.shift()); //a
```

#### push()

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

#### unshitf()

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

#### reduce()

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

######## reduce() 的常见应用

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



#### sort()

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


#### reverse()

**reverse()反转数组的元素顺序。**

```js
let arr=["b","o","a","m"];
arr.sort(); //字母升序
arr.reverse(); //反转顺序
console.log(arr)
// o,m,b,a
```

#### slice()

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

#### splice()   !important

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

######## splice()练习：数组去重

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


#### toString()

**将数组转化成字符串**

```js
let arr=["b","o","a","m"];
console.log(arr.toString())
// b,o,a,m
```

#### Array.from()

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

######## 

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

####  Array.of()

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

#### keys()、values()、entries()

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



### 5. 关于数组的联系

```js
let arr = [[1,2,3,4],[4,3,4,3],[[[123,23],[12,23,34]],[12,22,1]]]
```

使一个多维数组变成一维数组, 要得到数组的最终形式

```js
arr = [
   1,  2,   3,  4,  4,  3,
   4,  3, 123, 23, 12, 23,
  34, 12,  22,  1
]

```

实现方法:

```js
let arr = [[1,2,3,4],[4,3,4,3],[[[123,23],[12,23,34]],[12,22,1]]]
function flat(arr) {
  let result = []
  arr.map(item => {
    if (Array.isArray(item)) {
      result = result.concat(flat(item))
    } else {
      result.push(item)
    }
  })
  return result
}

console.log(flat(arr));
// [
//    1,  2,   3,  4,  4,  3,
//    4,  3, 123, 23, 12, 23,
//   34, 12,  22,  1
// ]
```

## Number

### parseInt()

**parseInt()具有以下特性**：

（1）parseInt()、parseFloat()会将传入的数据当作**字符串**来处理。也就是说，如果对**非 String**使用 parseInt()、parseFloat()，它会**先将其转换为 String** 然后再操作。【重要】

比如：

```javascript
var a = 168.23;
console.log(parseInt(a)); //打印结果：168  （因为是先将 a 转为字符串"168.23"，然后然后再操作）

var b = true;
console.log(parseInt(b)); //打印结果：NaN （因为是先将 b 转为字符串"true"，然后然后再操作）

var c = null;
console.log(parseInt(c)); //打印结果：NaN  （因为是先将 c 转为字符串"null"，然后然后再操作）

var d = undefined;
console.log(parseInt(d)); //打印结果：NaN  （因为是先将 d 转为字符串"undefined"，然后然后再操作）
```


（2）**只保留字符串最开头的数字**，后面的中文自动消失。例如：

```javascript
console.log(parseInt('2017在公众号上写了6篇文章')); //打印结果：2017

console.log(parseInt('2017.01在公众号上写了6篇文章')); //打印结果仍是：2017   （说明只会取整数）

console.log(parseInt('aaa2017.01在公众号上写了6篇文章')); //打印结果：NaN （因为不是以数字开头）
```


（3）自动截断小数：**取整，不四舍五入**。

例 1：

```javascript
var a = parseInt(5.8) + parseInt(4.7);
console.log(a);
```

打印结果：

```bash
9
```

例 2：

```javascript
var a = parseInt(5.8 + 4.7);
console.log(a);
```

打印结果：

```javascript
10;
```

（4）带两个参数时，表示在转换时，包含了进制转换。

代码举例：

```javascript
var a = '110';

var num = parseInt(a, 16); // 【重要】将 a 当成 十六进制 来看待，转换成 十进制 的 num

console.log(num);
```

打印结果：

```bash
272
```

如果你对打印结果感到震惊，请仔细看上面的代码注释。就是说，无论 parseInt() 里面的进制参数是多少，最终的转换结果是十进制。

我们来看下面的代码，打印结果继续震惊。

```javascript
var a = '5';

var num = parseInt(a, 2);
 // 将 a 当成 二进制 来看待，转换成 十进制 的 num

console.log(num);
 // 打印结果：NaN。因为 二进制中没有 5 这个数，转换失败。
```
---

就拿`Number(true)` 和 `parseInt(true)/parseFloat(true)`来举例，二者在使用时，是有区别的：

-   Number(true) ：千方百计地想转换为数字；如果转换不了则返回 NaN。

-   parseInt(true)/parseFloat(true) ：提取出最前面的数字部分；没提取出来，那就返回 NaN。

### NaN遇到的坑

**举例 1**：

```javascript
var a = 'abc';
a++;
console.log(typeof a); // 打印结果：number
console.log(a); // 打印结果：NaN。因为 Number('abc')的结果为 NaN，再自增后，结果依然是 NaN
```

## Boolean

### 转换结果列举【重要】

其他的数据类型都可以转换为 Boolean 类型。无论是隐式转换，还是显示转换，转换结果都是一样的。有下面几种情况：

（1）情况一：数字 --> 布尔。 0 和 NaN是 false，其余的都是 true。比如 `Boolean(NaN)`的结果是 false。

（2）情况二：字符串 ---> 布尔。空串是false，其余的都是 true。全是空格的字符串，转换结果也是 true。字符串`'0'`的转换结果也是 true。

（3）情况三：null 和 undefined 都会转换为 false。

（4）情况四：**引用数据类型会转换为 true。注意，空数组`[]`和空对象`{}`，转换结果也是 true，这一点，很多人都不知道。**

##  Object

### 对象的基本操作

#### 创建对象

使用 new 关键字调用的函数，是构造函数 constructor。**构造函数是专门用来创建对象的函数**。

例如：

```javascript
var obj = new Object();
```

记住，使用`typeof`检查一个对象时，会返回`object`。

关于常见对象的更多方式，可以看上一篇文章《对象的创建&构造函数》。

#### 向对象中添加属性

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

#### 获取对象中的属性

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

#### 修改对象的属性值

语法：

```javascript
对象.属性名 = 新值;
```

```javascript
obj.name = 'tom';
```

#### 删除对象的属性

语法：

```javascript
delete obj.name;
```

#### in 运算符

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

#### Object.freeze() 冻结对象

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

### 遍历操作

#### for of：遍历数组


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

#### Map 对象的遍历

`for ... of`既可以遍历数组，也可以遍历 Map 对象。

#### for in：遍历对象的属性

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

#### for in 遍历数组（不建议）

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

### 深拷贝 浅拷贝

-   浅拷贝：只拷贝最外面一层的数据；更深层次的对象，只拷贝引用。

-   深拷贝：拷贝多层数据；每一层级别的数据都会拷贝。

**总结**：

**浅拷贝的时候如果数据是基本数据类型，那么就如同直接赋值那种，会拷贝其本身，如果除了基本数据类型之外还有一层对象，那么对于浅拷贝而言就只能拷贝其引用，对象的改变会反应到拷贝对象上；但是深拷贝就会拷贝多层，即使是嵌套了对象，也会都拷贝出来。**

拷贝引用的时候，是属于**传址**，而非**传值**。

深拷贝会把对象里**所有的数据**重新复制到新的内存空间，是最彻底的拷贝。

#### 浅拷贝的实现方式

#### 用 for in 实现浅拷贝（比较繁琐）

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

#### 用 Object.assgin() 实现浅拷贝（推荐的方式）

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

#### 深拷贝的实现方式

深拷贝其实就是将浅拷贝进行递归。

#### 用 for in 递归实现深拷贝

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

##  Function

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

### 函数的定义/声明

#### 方式一：利用函数关键字自定义函数（命名函数）

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

#### 方式二：函数表达式（匿名函数）

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


- 上面的 fun2 是变量名，不是函数名。

- 函数表达式的声明方式跟声明变量类似，只不过变量里面存的是值，而函数表达式里面存的是函数。

- 函数表达式也可以传递参数。

从方式二的举例中可以看出：所谓的“函数表达式”，其实就是将匿名函数赋值给一个变量。

#### 方式三：使用构造函数 new Function()

使用构造函数`new Function()`来创建一个对象。这种方式，用的少。

语法：

```javascript
var 变量名/函数名  = new Function('形参1', '形参2', '函数体');
```

注意，Function 里面的参数都必须是**字符串**格式。也就是说，形参也必须放在**字符串**里；函数体也是放在**字符串**里包裹起来，放在 Function 的最后一个参数的位置。

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

#### 总结

1、**所有的函数，都是 `Fuction` 的“实例”**（或者说是“实例对象”）。函数本质上都是通过 new Function 得到的。

2、函数既然是实例对象，那么，**函数也属于“对象”**。还可以通过如下特征，来佐证函数属于对象：

（1）我们直接打印某一个函数，比如 `console.log(fun2)`，发现它的里面有`__proto__`。

（2）我们还可以打印 `console.log(fun2 instanceof Object)`，发现打印结果为 `true`。这说明 fun2 函数就是属于 Object。

### 函数的调用

#### 方式1：普通函数的调用

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
function fn1() {
	console.log('我是函数体里面的内容1');
}

function fn2() {
	console.log('我是函数体里面的内容2');
}

fn1(); // 调用函数

fn2.call(); // 调用函数

```

#### 方式2：通过对象的方法来调用

```javascript
var obj = {
	a: 'qianguyihao',
	fn2: function() {
		console.log('千古壹号，永不止步!');
	},
};

obj.fn2(); // 调用函数
```

如果一个函数是作为一个对象的属性保存，那么，我们称这个函数是这个对象的**方法**。


#### 方式3：立即执行函数

代码举例：

```javascript
(function() {
	console.log('我是立即执行函数');
})();

```

立即执行函数在定义后，会自动调用。

#### 方式4：通过构造函数来调用

代码举例：

```javascript
function Fun3() {
	console.log('千古壹号，永不止步~');
}

new Fun3();
```

这种方式用得不多。

#### 方式5：绑定事件函数

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
            //2.绑定事件
            btn.onclick = function() {
                console.log('点击按钮后，要做的事情');
            };
        </script>
    </body>
</html>

```



#### 方式6：定时器函数

代码举例：（每间隔一秒，将 数字 加1）

```javascript
    let num = 1;
   setInterval(function () {
       num ++;
       console.log(num);
   }, 1000);
```

这里涉及到定时器的知识点。

### 函数的参数：形参和实参

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

#### 实参的类型

函数的实参可以是任意的数据类型。

调用函数时，解析器不会检查实参的类型，所以要注意，是否有可能会接收到非法的参数，如果有可能则需要对参数进行类型的检查。

#### 实参的数量（实参和形参的个数不匹配时）

调用函数时，解析器也不会检查实参的数量。

- 如果实参的数量多余形参的数量，多余实参不会被赋值。

- 如果实参的数量少于形参的数量，多余的形参会被定义为 undefined。表达式的运行结果为 NaN。

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

### 函数的返回值

举例：

```javascript
console.log(sum(3, 4)); // 将函数的返回值打印出来

//函数：求和
function sum(a, b) {
	return a + b;
}
```

return 的作用是结束方法（终止函数）。

注意：

- return 的值将会作为函数的执行结果返回，可以定义一个变量，来接收该结果。

- 在函数中，return后的语句都不会执行（函数在执行完 return 语句之后停止并立即退出函数）

- 如果return语句后不跟任何值，就相当于返回一个undefined

- 如果函数中不写return，则也会返回undefined

- 返回值可以是任意的数据类型，可以是对象，也可以是函数。

- return 只能返回一个值。如果用逗号隔开多个值，则以最后一个为准。

### 函数名、函数体和函数加载问题（重要，请记3住）

我们要记住：**函数名 == 整个函数**。举例：

```javascript
console.log(fn) == console.log(function fn(){alert(1)});

//定义fn方法
function fn(){
	alert(1)
};
```

我们知道，当我们在调用一个函数时，通常使用`函数()`这种格式；可如果，我们是直接使用`函数`这种格式，它的作用相当于整个函数。

**函数的加载问题**：JS加载的时候，只加载函数名，不加载函数体。所以如果想使用内部的成员变量，需要调用函数。

### fn()  和 fn 的区别【重要】

- `fn()`：调用函数。调用之后，还获取了函数的返回值。

- `fn`：函数对象。相当于直接获取了整个函数对象。

### break、continue、return 

- break ：结束当前的循环体（如 for、while）

- continue ：跳出本次循环，继续执行下次循环（如 for、while）

- return ：1、退出循环。2、返回 return 语句中的值，同时结束当前的函数体内的代码，退出当前函数。


### 立即执行函数

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

### 方法

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

### 类数组 arguments

在调用函数时，浏览器每次都会传递进两个隐含的参数：

- 1.函数的上下文对象 this

- 2.**封装实参的对象** arguments

例如：

```javascript
function foo() {
    console.log(arguments);
    console.log(typeof arguments);
}

foo();
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/0d5383b246ea4dadbd32cec682e59cde.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)



arguments 是一个类数组对象，它可以通过索引来操作数据，也可以获取长度。

**arguments 代表的是实参**。在调用函数时，我们所传递的实参都会在arguments 中保存。

有个讲究的地方是：arguments**只在函数中使用**。

### arguments.length

arguments.length 可以用来获取**实参的长度**。

> 函数名.length 可以获取形参的个数

举例：

```javascript
fn(2, 4);
fn(2, 4, 6);
fn(2, 4, 6, 8);

function fn(a, b) {
    console.log(arguments);
    console.log(fn.length); //获取形参的个数
    console.log(arguments.length); //获取实参的个数

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

当我们不确定有多少个参数传递的时候，可以用 **arguments** 来获取。在 JavaScript 中，arguments 实际上是当前函数的一个**内置对象**。所有函数都内置了一个 arguments 对象（只有函数才有 arguments 对象），arguments 对象中存储了**传递的所有实参**.

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

### 函数参数默认值

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

### 剩余参数 (rest 运算符)

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

#### 剩余参数的举例：参数求和

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

#### 剩余参数和解构赋值配合使用

代码举例：

```js
const students = ['张三', '李四', '王五'];
let [s1, ...s2] = students;

console.log(s1); // '张三'
console.log(s2); // ['李四', '王五']
```



### 原型， 原型链

#### 原型对象

```javascript
        function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            //向对象中添加一个方法
            this.sayName = function () {
                console.log("我是" + this.name);
            }
        }

        //创建一个Person的实例
        var per = new Person("孙悟空", 18, "男");
        var per2 = new Person("猪八戒", 28, "男");
        per.sayName();
        per2.sayName();

        console.log(per.sayName == per2.sayName);  //打印结果为false
```

**分析如下**：

上方代码中，我们的sayName方法是写在构造函数 Person 内部的，然后在两个实例中进行了调用。造成的结果是，**构造函数每执行一次，就会给每个实例创建一个新的 sayName 方法**。

也就是说，每个实例的sayName都是唯一的。因此，最后一行代码的打印结果为false。

按照上面这种写法，假设创建10000个对象实例，就会创建10000个 sayName 方法。这种写法肯定是不合适的。

还有一种方式是，将sayName方法在全局作用域中定义：（不建议。原因看注释）

```javascript
        function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            this.sayName = fun;
        }

        //将sayName方法在全局作用域中定义
        /*
         * 将函数定义在全局作用域，污染了全局作用域的命名空间
         *  而且定义在全局作用域中也很不安全
         */

        function fun() {
            alert("Hello大家好，我是:" + this.name);
        };
```

比较好的方式是，在原型中添加sayName方法：

```javascript
    Person.prototype.sayName = function(){
        alert("Hello大家好，我是:"+this.name);
    };
```

这也就引入了我们本文要讲的「原型」。

#### 原型prototype的概念

**认识1**：

我们所创建的每一个函数，解析器都会向函数中添加一个属性 prototype。这个属性对应着一个对象，这个对象就是我们所谓的原型对象。

如果函数作为普通函数调用prototype没有任何作用，当函数以构造函数的形式调用时，它所创建的实例对象中都会有一个隐含的属性，指向该构造函数的原型，我们可以通过__proto__来访问该属性。

代码举例：

```javascript
	// 定义构造函数
	function Person() {}

	var per1 = new Person();
	var per2 = new Person();

	console.log(Person.prototype); // 打印结果：{}

	console.log(per1.__proto__ == Person.prototype); // 打印结果：true
```

上方代码的最后一行：打印结果表明，`实例.__proto__` 和 `构造函数.prototype`都指的是原型对象。

**认识2**：

原型对象就相当于一个公共的区域，**所有同一个类的实例都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中。**

以后我们创建构造函数时，可以将这些对象共有的属性和方法，统一添加到构造函数的原型对象中，这样就不用分别为每一个对象添加，也不会影响到全局作用域，就可以使每个对象都具有这些属性和方法了。

**认识3**：

使用 `in` 检查对象中是否含有某个属性时，如果对象中没有但是**原型中**有，也会返回true。

可以使用对象的`hasOwnProperty()`来检查**对象自身中**是否含有该属性。

#### 原型链

原型对象也是对象，所以它也有原型，当我们使用或访问一个对象的属性或方法时：

- 它会先在对象自身中寻找，如果有则直接使用；

- 如果没有则会去原型对象中寻找，如果找到则直接使用；

- 如果没有则去原型的原型中寻找，直到找到Object对象的原型。

- Object对象的原型没有原型，如果在Object原型中依然没有找到，则返回 null

#### 原型规则

> 1. 所有的引用类型（数组、对象、函数），都具有对象特性，都可以**自由扩展属性**。null 除外。

```js
let a = {}
a.name = "ximingx"
console.log(a.name)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2466d40dcbc14d9b90ddc8b9fdd80710.png)
> 2. 所有的**引用类型**（数组、对象、函数），都有一个`_proto_`属性，属性值是一个**普通的对象**。`_proto_`的含义是隐式原型。

```js
let a = {}
a.name = "ximingx"
console.log(a.__proto__)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/0d572a2bfa4e460188deff2c19bc1824.png)
> 3. 所有的**函数**（不包括数组、对象），都有一个`prototype`属性，属性值是一个**普通的对象**。`prototype`的含义是**显式原型**。（实例没有这个属性）
```js
let a = function () {}
console.log(a.prototype)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/98da7825017f4dcd9d856a7c209cff7c.png)
> 4. 所有的**引用类型**（数组、对象、函数），`_proto_`属性指向它的**构造函数**的`prototype`值。
```js
let a = {}
console.log(a.__proto__ === Object.prototype)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/d2e5bbb979664423aa3988c175195686.png)
> 5. 当试图获取一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的`_proto_`中寻找（即它的构造函数的`prototype`）。
```js
//创建方法
function Foo(name) {
    this.name = name;
}

Foo.prototype.alertName = function () {
    // 既然 Foo.prototype 是普通的对象，那也允许给它添加额外的属性 alertName
    console.log(this.name);
};

// 测试
let fn = new Foo("ximingx")
fn.alertName(); //输出结果：ximingx
```

上方代码中，虽然 alertName 不是 fn 自身的属性，但是会从它的构造函数的`prototype`里面找。

### 构造函数

#### 代码引入

```javascript
// 创建一个构造函数，专门用来创建Person对象
function Person(name, age, gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
    this.sayName = function () {
        alert(this.name);
    };
}

var per = new Person('ximingx', 18, '男');
var per2 = new Person('luotyue', 16, '女');

// 创建一个构造函数，专门用来创建 Dog 对象
function Dog() {}

var dog = new Dog();
```

#### 构造函数的概念

**构造函数**：是一种特殊的函数，主要用来创建和初始化对象，也就是为对象的成员变量赋初始值。它与 `new` 一起使用才有意义。

我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个构造函数里面。

#### 构造函数和普通函数的区别

构造函数的创建方式和普通函数没有区别，**不同的是构造函数习惯上首字母大写。**

构造函数和普通函数的区别就是**调用方式**的不同：普通函数是直接调用，而构造函数需要使用 new 关键字来调用。

**this 的指向也有所不同**：

-   1.以函数的形式调用时，this 永远都是 window。比如`fun();`相当于`window.fun();`

-   2.以方法的形式调用时，this 是调用方法的那个对象

-   3.以构造函数的形式调用时，this 是新创建的实例对象

#### new 一个构造函数的执行流程

new 在执行时，会做下面这四件事：

（1）开辟内存空间，在内存中创建一个新的空对象。

（2）让 this 指向这个新的对象。

（3）执行构造函数里面的代码，给这个新对象添加属性和方法。

（4）返回这个新对象（所以构造函数里面不需要 return）。

因为 this 指的是 new 一个 Object 之后的对象实例。于是，下面这段代码：

```javascript
// 创建一个函数
function createStudent(name) {
    var student = new Object();
    student.name = name; //第一个name指的是student对象定义的变量。第二个name指的是createStudent函数的参数。二者不一样
}
```

可以改进为：

```javascript
// 创建一个函数
function Student(name) {
    this.name = name; //this指的是构造函数中的对象实例
}
```

注意上方代码中的注释。

#### 静态成员和实例成员

JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的 this 上添加。通过这两种方式添加的成员，就分别称为静态成员和实例成员。

-   静态成员：在构造函数本上添加的成员称为静态成员，只能由构造函数本身来访问。

-   实例成员：在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问。

#### 类、实例

使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个**类**。

通过一个构造函数创建的对象，称为该类的**实例**。

#### instanceof

使用 instanceof 可以检查**一个对象是否为一个类的实例**。

**语法如下**：

```javascript
对象 instanceof 构造函数;
```

如果是，则返回 true；否则返回 false。

**代码举例**：

```javascript
function Person() {}

function Dog() {}

var person1 = new Person();

var dog1 = new Dog();

console.log(person1 instanceof Person); // 打印结果： true
console.log(dog1 instanceof Person); // 打印结果：false
console.log(dog1 instanceof Object); // 所有的对象都是Object的后代。因此，打印结果为：true
```

根据上方代码中的最后一行，需要补充一点：**所有的对象都是 Object 的后代，因此 `任何对象 instanceof Object` 的返回结果都是 true**。

### 面向过程和面向对象

#### 面向过程

**面向过程**：先分析好的具体步骤，然后按照步骤，一步步解决问题。

优点：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。

缺点：没有面向对象易维护、易复用、易扩展。

#### 面向对象

**面向对象**（OOP，Object Oriented Programming）：以对象功能来划分问题，而不是步骤。

优点：**易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性**，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护。

缺点：性能比面向过程低。

#### 面向对象的编程思想

面向对象的编程思想：对代码和数据进行封装，并以对象调用的方式，对外提供统一的调用接口。

比如说，当我们在开车的时候，无需关心汽车的内部构造有多复杂，对于大多数人而言，只需要会开、知道汽车有哪些功能就行了。

#### 面向对象的特性

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。面向对象编程具有灵活、代码可复用、容易维护和开发的优点，适合多人合作的大型软件项目，更符合我们认识事物的规律。

面向对象的特性如下：

- **封装性**

- **继承性**

- **多态性**
#### JS 中的面向对象

JS 中的面向对象，是基于**原型**的面向对象。

另外，在ES6中，新引入了 类（`Class`）和继承（`Extends`）来实现面向对象。


#### 基于原型的面向对象

JS 中的对象（Object）是依靠构造器（`constructor`）和原型（`prototype`）构造出来的。

### 闭包的引入

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

#### 闭包的概念

**闭包**（closure）：指有权**访问**另一个函数作用域中**变量**的**函数**。

闭包是一种函数；当然，你可以**把闭包理解成是一种现象**。具体解释如下。

简单理解就是：如果**这个作用域可以访问另外一个函数内部的局部变量**，那就产生了闭包（此时，你可以把闭包理解成是一种现象）；而另外那个作用域所在的函数称之为**闭包函数**。注意，这里强调的是访问**局部变量**哦。

#### 闭包代码举例

代码举例：

```js
function fn1() {
    let a = 10;

    function fn2() {
        console.log(a);
    }
    fn2();
}

fn1();
```

打印结果：

```js
10
```

上方代码中，函数 fn2 的作用域 访问了 fn1 中的局部变量，那么，此时在 fn1 中就产生了闭包，fn1 称之为闭包函数。

#### 闭包的作用：延伸变量的作用范围

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

const foo = fn1(); // 执行 fn1() 之后，会得到一个返回值。这个返回值是函数
foo();
```

### 执行期上下文

当**函数执行**时（准确来说，是在函数发生预编译的前一刻），会创建一个执行期上下文的内部对象。一个执行期上下文定义了一个函数执行时的环境。

每调用一次函数，就会创建一个新的上下文对象，他们之间是相互独立且独一无二的。当函数执行完毕，它所产生的执行期上下文会被销毁。

#### this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数，这个隐含的参数就是 this，this 指向的是一个对象，这个对象我们称为函数执行的 上下文对象。

#### 函数内 this 的指向【非常重要】

根据函数的调用方式的不同，this 会指向不同的对象：

- 1.以函数的形式（包括普通函数、定时器函数、立即执行函数）调用时，this 的指向永远都是 window。比如`fun();`相当于`window.fun();`

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

//以函数形式调用，this是window
fun(); //可以理解成 window.fun()
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

//以方法的形式调用，this是调用方法的对象
obj2.sayName();
```

打印结果：

```js
    Object
    luoyue
```

上面的举例可以看出，this 指向的是 对象 obj2 ，所以 this.name 指的是 obj2.name。

#### 箭头函数中 this 的指向

ES6 中的箭头函数并不会使用上面的准则，而是会继承外层函数调用的 this 绑定（无论 this 绑定到什么）。


#### 改变 this 的指向
JS 专门为我们提供了一些方法来改变函数内部的 this 指向。常见的方法有 call()、apply()、bind() 方法。

#### call() 方法的作用

call() 方法的作用：可以**调用**一个函数，与此同时，它还可以改变这个函数内部的 this 指向。

call() 方法的另一个应用：**可以实现继承**。之所以能实现继承，其实是利用了上面的作用。

语法：

```js
fn1.call(想要将this指向哪里, 函数实参1, 函数实参2);
```

备注：第一个参数中，如果不需要改变 this 指向，则传 null。

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
fn1.call(this); // this的指向并没有被改变，此时相当于 fn1();
```

上方代码的打印结果：

```js
window
undefined
```

上面的代码，跟普通的函数调用 `fn1()` 没有区别。

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
obj1
ximingx
6
```

**举例 3**、通过 call() 实现继承：

```js
// 给 Father 增加 name 和 age 属性
function Father(myName, myAge) {
    this.name = myName;
    this.age = myAge;
}

function Son(myName, myAge) {
    // 【下面这一行，重要代码】
    // 通过这一步，将 father 里面的 this 修改为 Son 里面的 this；另外，给 Son 加上相应的参数，让 Son 自动拥有 Father 里的属性。最终实现继承
    Father.call(this, myName, myAge);
}

const son1 = new Son('ximingx', 28);
console.log(JSON.stringify(son1));
```

上方代码中，通过 call() 方法，让 Son 继承了 Father 里面的 name 和 age 属性。

打印结果：

```js
{"myName":"ximingx","myAge":28}
```

#### apply() 方法

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

#### bind() 方法的作用

bind() 方法**不会调用函数**，但是可以改变函数内部的 this 指向。

把call()、apply()、bind()这三个方法做一下对比，你会发现：实际开发中， bind() 方法使用得最为频繁。如果有些函数，我们不需要立即调用，但是又想改变这个函数内部的this指向，此时用 bind() 是最为合适的。


语法：

```js
新函数 = fn1.bind(想要将this指向哪里, 函数实参1, 函数实参2);
```

参数：

- 第一个参数：在 fn1 函数运行时，指定 fn1 函数的this 指向。如果不需要改变 this 指向，则传 null。

- 其他参数：fn1 函数的实参。

解释：它不会调用 fn1 函数，但会返回 由指定this 和指定实参的**原函数拷贝**。可以看出， bind() 方法是有返回值的。

##  Math



##  Data

### 内置对象：Date


内置对象 Date 用来处理日期和时间。

**需要注意的是**：与 Math 对象不同，Date 对象是一个**构造函数** ，需要**先实例化**后才能使用。

### 创建Date对象

创建Date对象有两种写法：

- 写法一：如果Date()不写参数，就返回当前时间对象

- 写法二：如果Date()里面写参数，就返回括号里输入的时间对象

#### 写法一：不传递参数时，则获取系统的当前时间对象

代码举例：

```javascript
var date1 = new Date();
console.log(date1);
console.log(typeof date1);
```

代码解释：不传递参数时，表示的是获取系统的当前时间对象。也可以理解成是：获取当前代码执行的时间。

打印结果： (node 执行环境)

> 2022年,3月,5日

```bash
2022-03-05T02:19:02.682Z
object
```

打印结果： (浏览器执行环境)

```bash
Sat Mar 05 2022 10:21:22 GMT+0800 (中国标准时间)
VM102:3 object
```

#### 写法二：传递参数

传递参数时，表示获取指定时间的时间对象。**参数中既可以传递字符串，也可以传递数字，也可以传递时间戳。**

通过传参的这种写法，我们可以把时间字符串/时间数字/时间戳，按照指定的格式，转换为时间对象。

**举例1：（参数是字符串）**

```js
const date11 = new Date('2020/02/17 21:00:00');
console.log(date11); // Mon Feb 17 2020 21:00:00 GMT+0800 (中国标准时间)

const date12 = new Date('2020/04/19'); // 返回的就是四月
console.log(date12); // Sun Apr 19 2020 00:00:00 GMT+0800 (中国标准时间)

const date13 = new Date('2020-05-20');
console.log(date13); // Wed May 20 2020 08:00:00 GMT+0800 (中国标准时间)

const date14 = new Date('Wed Jan 27 2017 12:00:00 GMT+0800 (中国标准时间)');
console.log(date14); // Fri Jan 27 2017 12:00:00 GMT+0800 (中国标准时间)
```


举例2：（参数是多个数字）

```js
const date21 = new Date(2020, 2, 18); // 注意，第二个参数返回的是三月，不是二月
console.log(date21); // Wed Mar 18 2020 00:00:00 GMT+0800 (中国标准时间)

const date22 = new Date(2020, 3, 18, 22, 59, 58);
console.log(date22); // Sat Apr 18 2020 22:59:58 GMT+0800 (中国标准时间)

const params = [2020, 06, 12, 16, 20, 59];
const date23 = new Date(...params);
console.log(date23); // Sun Jul 12 2020 16:20:59 GMT+0800 (中国标准时间)
```


举例3：（参数是时间戳）

```js
const date31 = new Date(1591950413388);
console.log(date31); // Fri Jun 12 2020 16:26:53 GMT+0800 (中国标准时间)

// 先把时间对象转换成时间戳，然后把时间戳转换成时间对象
const timestamp = new Date().getTime();
const date32 = new Date(timestamp);
console.log(date32); // Fri Jun 12 2020 16:28:21 GMT+0800 (中国标准时间)
```





### 日期的格式化

上一段内容里，我们获取到了 Date **对象**，但这个对象，打印出来的结果并不是特别直观。

如果我们需要获取日期的**指定部分**，就需要用到 Date对象自带的方法。

获取了日期指定的部分之后，我们就可以让日期按照指定的格式，进行展示（即日期的格式化）。比如说，我期望能以 `2020-02-02 19:30:59` 这种格式进行展示。

在这之前，我们先来看看 Date 对象有哪些方法。

### Date对象的方法

Date对象 有如下方法，可以获取日期和时间的**指定部分**：

| 方法名            | 含义              | 备注                 |
| ----------------- | ----------------- | -------------------- |
| getFullYear()     | 获取年份          |                      |
| getMonth()        | **获取月： 0-11** | 0代表一月            |
| getDate()         | **获取日：1-31**  | 获取的是几号         |
| getDay()          | **获取星期：0-6** | 0代表周日，1代表周一 |
| getHours()        | 获取小时：0-23    |                      |
| getMinutes()      | 获取分钟：0-59    |                      |
| getSeconds()      | 获取秒：0-59      |                      |
| getMilliseconds() | 获取毫秒          | 1s = 1000ms          |


**代码举例**：

### 一些关于Data方法的测试

```js
const date = new Date();

/**
 * new Data
 * */

console.log(new Date);
// 2021-12-05T11:11:42.652Z

console.log( + new Date);
// 1638702702658

// + 运算符(数值运算符)；会将表达式转换为数字。 获取到当前的时间戳

console.log("// -----------------------------------------------------------------------")

/**
 * 获取事件
 * */

console.log(date.getYear());
// 获取当前年份(2位)
// getYear()返回的值是当前年份减去1900。
// JavaScript 1.2和更早的版本返回2位数或4位数的年份。
// 因此，在测试这个函数之前，需要确定使用的javascript版本。
console.log(date.getFullYear());
//获取完整的年份(4位,1970-????)
console.log(date.getMonth());
//获取当前月份(0-11,0代表1月)
console.log(date.getDate());
//获取当前日(1-31)
console.log(date.getDay());
//获取当前星期X(0-6,0代表星期天)
console.log(date.getTime());
//获取当前时间(从1970.1.1开始的毫秒数)
console.log(date.getHours());
//获取当前小时数(0-23)
console.log(date.getMinutes());
//获取当前分钟数(0-59)
console.log(date.getSeconds());
//获取当前秒数(0-59)
console.log(date.getMilliseconds());
//获取当前毫秒数(0-999)
console.log(date.toLocaleDateString())
//获取当前日期
console.log(date.toLocaleTimeString());
//获取当前时间
console.log(date.toLocaleString());
//获取日期与时间

// 121
// 2021
// 11
// 5
// 0
// 1638702702652
// 19
// 11
// 42
// 652
// 2021/12/5
// 下午7:11:42
// 2021/12/5 下午7:11:42

console.log("// -----------------------------------------------------------------------")

/**
 * 修改时间
 * */

date.setTime(14)  //设置时
date.setYear(2023)  //设置年
date.setMonth(1)  //设置月
date.setDate(20)  //设置日
date.setHours(11)  //设置小时
date.setMinutes(56)  //设置分
date.setSeconds(36)  //设置秒 [注意:此日期时间从0开始计]


console.log(date.getYear());
console.log(date.getFullYear());
console.log(date.getMonth());
console.log(date.getDate());
console.log(date.getDay());
console.log(date.getTime());
console.log(date.getHours());
console.log(date.getMinutes());
console.log(date.getSeconds());
console.log(date.getMilliseconds());
console.log(date.toLocaleDateString())
console.log(date.toLocaleTimeString());
console.log(date.toLocaleString());

// 123
// 2023
// 1
// 20
// 1
// 1676865396014
// 11
// 56
// 36
// 14
// 2023/2/20
// 上午11:56:36
// 2023/2/20 上午11:56:36
```




```javascript
	// 我在执行这行代码时，当前时间为 2019年2月4日，周一，13:23:52
	var myDate = new Date();

	console.log(myDate); // 打印结果：Mon Feb 04 2019 13:23:52 GMT+0800 (中国标准时间)

	console.log(myDate.getFullYear()); // 打印结果：2019
	console.log(myDate.getMonth() + 1); // 打印结果：2
	console.log(myDate.getDate()); // 打印结果：4

	var dayArr  = ['星期日', '星期一', '星期二', '星期三', '星期四','星期五', '星期六'];
	console.log(myDate.getDay()); // 打印结果：1
	console.log(dayArr[myDate.getDay()]); // 打印结果：星期一

	console.log(myDate.getHours()); // 打印结果：13
	console.log(myDate.getMinutes()); // 打印结果：23
	console.log(myDate.getSeconds()); // 打印结果：52
	console.log(myDate.getMilliseconds()); // 打印结果：393

	console.log(myDate.getTime()); // 获取时间戳。打印结果：1549257832393
```

获取了日期和时间的指定部分之后，我们把它们用字符串拼接起来，就可以按照自己想要的格式，来展示日期。

### 举例：年月日的格式化

代码举例：

```js
console.log(formatDate());

/*
    方法：日期格式化。
    格式要求：今年是：2020年02月02日 08:57:09 星期日
*/
function formatDate() {
    var date = new Date();

    var year = date.getFullYear(); // 年
    var month = date.getMonth() + 1; // 月
    var day = date.getDate(); // 日

    var week = date.getDay(); // 星期几
    var weekArr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];

    var hour = date.getHours(); // 时
    hour = hour < 10 ? '0' + hour : hour; // 如果只有一位，则前面补零

    var minute = date.getMinutes(); // 分
    minute = minute < 10 ? '0' + minute : minute; // 如果只有一位，则前面补零

    var second = date.getSeconds(); // 秒
    second = second < 10 ? '0' + second : second; // 如果只有一位，则前面补零

    var result = '今天是：' + year + '年' + month + '月' + day + '日 ' + hour + ':' + minute + ':' + second + ' ' + weekArr[week];

    return result;
}

```




### 获取时间戳


**时间戳**：指的是从格林威治标准时间的`1970年1月1日，0时0分0秒`到当前日期所花费的**毫秒数**（1秒 = 1000毫秒）。

计算机底层在保存时间时，使用的都是时间戳。时间戳的存在，就是为了**统一**时间的单位。

我们经常会利用时间戳来计算时间，因为它更精确。而且，在实战开发中，接口返回给前端的日期数据，都是以时间戳的形式。

我们再来看下面这样的代码：

```javascript
	var myDate = new Date("1970/01/01 0:0:0");

	console.log(myDate.getTime()); // 获取时间戳
```

打印结果（可能会让你感到惊讶）

```javascript
	-28800000
```

为啥打印结果是`-28800000`，而不是`0`呢？这是因为，我们的当前代码，是在中文环境下运行的，与英文时间会存在**8个小时的时差**（中文时间比英文时间早了八个小时）。如果代码是在英文环境下运行，打印结果就是`0`。


### getTime()：获取时间戳

`getTime()`  获取日期对象的**时间戳**（单位：毫秒）。这个方法在实战开发中，用得比较多。但还有比它更常用的写法，我们往下看。


### 获取 Date 对象的时间戳

代码演示：

```js
// 方式一：获取 Date 对象的时间戳（最常用的写法）
const timestamp1 = +new Date();
console.log(timestamp1); // 打印结果举例：1589448165370

// 方式二：获取 Date 对象的时间戳（较常用的写法）
const timestamp2 = new Date().getTime();
console.log(timestamp2); // 打印结果举例：1589448165370

// 方式三：获取 Date 对象的时间戳
const timestamp3 = new Date().valueOf();
console.log(timestamp3); // 打印结果举例：1589448165370

// 方式4：获取 Date 对象的时间戳
const timestamp4 = new Date() * 1;
console.log(timestamp4); // 打印结果举例：1589448165370

// 方式5：获取 Date 对象的时间戳
const timestamp5 = Number(new Date());
console.log(timestamp5); // 打印结果举例：1589448165370
```

上面这五种写法都可以获取任意 Date 对象的时间戳，最常见的写法是**方式一**，其次是方式二。

根据前面所讲的关于「时间戳」的概念，上方代码获取到的时间戳指的是：从 `1970年1月1日，0时0分0秒` 到现在所花费的总毫秒数。

### 获取当前时间的时间戳

如果我们要获取**当前时间**的时间戳，除了上面的几种方式之外，还有另一种方式。代码如下：

```js
// 方式六：获取当前时间的时间戳（很常用的写法）
console.log(Date.now()); // 打印结果举例：1589448165370
```

上面这种方式六，用得也很多。只不过，`Date.now()`是H5标准中新增的特性，如果你的项目需要兼容低版本的IE浏览器，就不要用了。


### 利用时间戳检测代码的执行时间

我们可以在业务代码的前面定义 `时间戳1`，在业务代码的后面定义 `时间戳2`。把这两个时间戳相减，就能得出业务代码的执行时间。

### 举例1：模拟日历

要求每天打开这个页面，都能定时显示当前的日期。

代码实现：

```html
<!DOCTYPE html>
<html>
    <head lang="en">
        <meta charset="UTF-8" />
        <title></title>
        <style>
            div {
                width: 800px;
                margin: 200px auto;
                color: red;
                text-align: center;
                font: 600 30px/30px 'simsun';
            }
        </style>
    </head>
    <body>
        <div></div>

        <script>
            //模拟日历
            //需求：每天打开这个页面都能定时显示年月日和星期几
            function getCurrentDate() {
                //1.创建一个当前日期的日期对象
                const date = new Date();
                //2.然后获取其中的年、月、日和星期
                const year = date.getFullYear();
                const month = date.getMonth();
                const hao = date.getDate();
                const week = date.getDay();
                //        console.log(year+" "+month+" "+hao+" "+week);
                //3.赋值给div
                const arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
                const div = document.getElementsByTagName('div')[0];
                return '今天是：' + year + '年' + (month + 1) + '月' + hao + '日 ' + arr[week];
            }

            const div = document.getElementsByTagName('div')[0];
            div.innerText = getCurrentDate();
        </script>
    </body>
</html>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2e490e6604a34af19f2068a6efe8ba4a.png)


### 举例2：倒计时

实现思路：

- 设置一个定时器，每间隔1毫秒就自动刷新一次div的内容。

- 核心算法：输入的时间戳减去当前的时间戳，就是剩余时间（即倒计时），然后转换成时分秒。

代码实现：

```html
<!DOCTYPE html>
<html>
    <head lang="en">
        <meta charset="UTF-8" />
        <title></title>
        <style>
            div {
                width: 1210px;
                margin: 200px auto;
                color: red;
                text-align: center;
                font: 600 30px/30px 'simsun';
            }
        </style>
    </head>
    <body>
        <div></div>

        <script>
            var div = document.getElementsByTagName('div')[0];

            var timer = setInterval(() => {
                countDown('2022/02/03 11:20:00');
            }, 1);

            function countDown(myTime) {
                var nowTime = new Date();
                var future = new Date(myTime);
                var timeSum = future.getTime() - nowTime.getTime(); //获取时间差：发布会时间减去此刻的毫秒值

                var day = parseInt(timeSum / 1000 / 60 / 60 / 24); // 天
                var hour = parseInt((timeSum / 1000 / 60 / 60) % 24); // 时
                var minu = parseInt((timeSum / 1000 / 60) % 60); // 分
                var sec = parseInt((timeSum / 1000) % 60); // 秒
                var millsec = parseInt(timeSum % 1000); // 毫秒

                //细节处理：所有的时间小于10的时候，在前面自动补0，毫秒值要补双0（比如如，把 8 秒改成 08 秒）
                day = day < 10 ? '0' + day : day; //day小于10吗？如果小于，就补0；如果不小于，就是day本身
                hour = hour < 10 ? '0' + hour : hour;
                minu = minu < 10 ? '0' + minu : minu;
                sec = sec < 10 ? '0' + sec : sec;
                if (millsec < 10) {
                    millsec = '00' + millsec;
                } else if (millsec < 100) {
                    millsec = '0' + millsec;
                }

                // 兜底处理
                if (timeSum < 0) {
                    div.innerHTML = '距离苹果发布会还有00天00小时00分00秒000毫秒';
                    clearInterval(timer);
                    return;
                }

                // 前端要显示的文案
                div.innerHTML = '距离苹果发布会还有' + day + '天' + hour + '小时' + minu + '分' + sec + '秒' + millsec + '毫秒';
            }
        </script>
    </body>
</html>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/cbfb6868c69742b3a90d0f2980267420.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

##  Set

ES6 提供了 新的数据结构 Set。Set 类似于**数组**，但成员的值都是**唯一**的，没有重复的值。可以轻松实现去重的功能。

Set 的应用有很多。比如，在 H5 页面的搜索功能里，用户可能会多次搜索重复的关键字；但是在数据存储上，不需要存储重复的关键字。此时，我们就可以用 Set 来存储用户的搜索记录，Set 内部会自动判断值是否重复，如果重复，则不会进行存储，十分方便。

### 生成 Set 数据结构

Set 本身就是一个构造函数，可通过 `new Set()` 生成一个 Set 的实例。

举例 1：

```js
const set1 = new Set();
console.log(set1.size); // 打印结果：0
```

**举例 2**、可以接收一个**数组**作为参数，实现**数组去重**：

```js
const set2 = new Set(['张三', '李四', '王五', '张三']); // 注意，这个数组里有重复的值

// 注意，这里的 set2 并不是数组，而是一个单纯的 Set 数据结构
// 是一种对象的形式
console.log(set2); // {"张三", "李四", "王五"}

// 通过...扩展运算符，拿到 set 中的元素（用逗号分隔的序列）
// ...set2 //  "张三", "李四", "王五"

// 注意，到这一步，才获取到了真正的数组
console.log([...set2]); // ["张三", "李四", "王五"]
```

注意上方的第一行代码，虽然参数里传递的是数组结构，但拿到的 `set2` 不是数组结构，而是 Set 结构，而且里面元素是去重了的。通过 `[...set2]`就可以拿到`set2`对应的数组。

### 删除元素

```js
set.delete（item）
```
### 添加元素

```js
set.add(item)
```

### 判断是否存在元素

```js
set.has(item) // 返回 true or false
```

### size 属性获取 set 的长度

```js
set.size
```



## JSON

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

## null， undefined

### Null：空对象

null 专门用来定义一个**空对象**。例如：`let a = null`，又例如 `Object.create(null)`.

如果你想定义一个变量用来保存引用类型，但是还没想好放什么内容，这个时候，可以在初始化时将其设置为 null。你可以把 null 理解为：**null 虽然是一个单独的数据类型，但null 相当于是一个 object，只不过地址为空（空指针）而已**。

比如：

```js
let myObj = null;
cosole.log(typeof myObj); // 打印结果：object
```

补充：

-   Null 类型的值只有一个，就是 null。比如 `let a = null`。

-   使用 typeof 检查一个 null 值时，会返回 object。

### undefined：未定义类型

#### case1：变量已声明，未赋值时

**声明**了一个变量，但没有**赋值**，此时它的值就是 `undefined`。举例：

```js
let name;
console.log(name); // 打印结果：undefined
console.log(typeof name); // 打印结果：undefined
```

补充：

-   Undefined 类型的值只有一个，就是 undefind。比如 `let a = undefined`。

-   使用 typeof 检查一个 undefined 值时，会返回 undefined。

#### case2：变量未声明（未定义）时

如果你从未声明一个变量，就去使用它，则会报错（这个大家都知道）；此时，如果用 `typeof` 检查这个变量时，会返回 `undefined`。举例：

```js
console.log(typeof a); // undefined
console.log(a); // 打印结果：Uncaught ReferenceError: a is not defined
```

#### case3：函数无返回值时

如果一个函数没有返回值，那么，这个函数的返回值就是 undefined。

或者，也可以这样理解：在定义一个函数时，如果末尾没有 return 语句，那么，其实就是 `return undefined`。

举例：

```js
function foo() {}

console.log(foo()); // 打印结果：undefined
```

#### case4：调用函数时，未传参

调用函数时，如果没有传参，那么，这个参数的值就是 undefined。

举例：

```js
function foo(name) {
    console.log(name);
}

foo(); // 调用函数时，未传参。执行函数后的打印结果：undefined
```

实际开发中，如果调用函数时没有传参，我们可以根据需要给形参设置一个默认值：

```js
function foo(name) {
    name = name || 'qianguyihao';
}

foo();
```

等学习了 ES6 之后，上方代码也可以这样写：

```js
function foo(name = 'qianguyihao') {}

foo();
```

### 其他区别

null 和 undefined 有很大的相似性。看看 `null == undefined` 的结果为 `true` 也更加能说明这点。

但是 `null === undefined` 的结果是 false。它们虽然相似，但还是有区别的，其中一个区别是，和数字运算时：

-   10 + null 结果为 10。

-   10 + undefined 结果为 NaN。

规律总结：

- 任何值和 null 运算，null 可看做 0 运算。
- 任何数据类型和 undefined 运算都是 NaN。

## transition

animation 的学习之前 其实需要顺便提一下 transition 

首先强调一下我认为他最大的不足

1.   过渡只关心元素的初始状态和结束状态，没有方法可以获取到元素在过渡中每一帧的状态

下面介绍一下他的四个属性以及简写

### 1.2 transition-property

**不是所有属性都能过渡，只有属性具有一个中间点值才具备过渡效果 !!!**

用于指定应用过渡的属性名称，可以指定多个属性名称，多个属性名称之间用`,` 分隔。

默认值为 `all` 也就是所有的元素都应用过渡效果。

```html
<template>
  <div id="test">
      
  </div>
</template>
<script>
export default {
  name: "Test"
}
</script>
<style scoped>
div{
  width: 200px;
  height: 200px;
  background-color: dodgerblue;
  transition-property: width, height;
}
div:hover {
  width: 400px;
  height: 400px;
}
</style>
```

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-s5i6WknW-1637112573576)(D:/start/image-20211117090918168.png)\]](https://img-blog.csdnimg.cn/c8dbe86dc78047d1afa06fc235549119.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


当鼠标悬浮上去的时候 , 他会立即变成这个样子,**过渡效果不会生效。因为没有设置 transition-duration 属性**,他会立即变成最后的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/d2052d104765455fbefb5eadc6919c32.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


### 1.3 transition-duration

用于设置过渡的持续时间，属性值以秒`s`或毫秒`ms`为单位，默认值为0 , 为0时，表示变化是瞬时的，看不到过渡效果。

多个每个时长会被应用到由 `transition-property` 指定的对应属性上。

**如果指定的时长个数小于属性个数，那么时长列表会重复.如果时长列表更长，那么该列表会被裁减。**

### 1.4 transiton-timing-function

>   liner
>   ease-in
>   ease-out
>   ease-in-out
>   cubic-bezier

这里先提一下,下面 animation 里会有具体的解释

### 1.5 transition-delay

`transition-delay` 规定了在过渡效果开始作用之前需要等待的时间（延迟时间），值以秒（s）或毫秒（ms）为单位，表明动画过渡效果将在何时开始

**取值为正时会延迟一段时间来响应过渡效果；取值为负时会导致过渡立即开始。**

一个完整的案例

```css
div{
  width: 200px;
  height: 200px;
  background-color: ##000000;
  transition-property: width;
  transition-duration: 3s;
  transition-timing-function: linear;
  transition-delay: 0.5s;
}
div:hover {
  width: 400px;
}
```

### 1.6 简写属性

```css
transiton: 过渡属性 过渡所需要时间 过渡动画函数 过渡延迟时间；
```

### 1.7 transition 的不足

**transition的优点在于简单易用，但是它有几个很大的局限。**
（1）transition需要事件的触发，所以没法在网页加载时自动发生。
（2）transition是一次性的，不能重复发生，除非一再触发。
（3）transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。
（4）一条transition规则，只能定义一个属性的变化，不能涉及多个属性。
CSS Animation就是为了解决这些问题而提出的,完美的解决了这些问题

### 1.8 一个简单的样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS 过渡</title>
  <style>
      body {
          margin: 0;
          padding: 0;
          background-color: #eeeeee;
      }

      .content {
          width: 800px;
          height: 320px;
          padding-left: 20px;
          margin: 80px auto;
      }

      .item {
          width: 230px;
          height: 300px;
          text-align: center;
          margin-right: 20px;
          background-color: #FFF;
          float: left;
          position: relative;
          top: 0;
          overflow: hidden; /* 让溢出的内容隐藏起来。意思是让下方的橙色方形先躲起来 */
          transition: all .5s; /* 从最初到鼠标悬停时的过渡 */
      }

      .item .desc {
          position: absolute;
          left: 0;
          bottom: -80px;
          width: 100%;
          height: 80px;
          background-color: #ff6700;
          transition: all .5s;
      }

      /* 鼠标悬停时，让 item 整体往上移动5px，且加一点阴影 */
      .item:hover {
          top: -5px;
          box-shadow: 0 0 15px #AAA;
      }

      /* 鼠标悬停时，让下方的橙色方形现身 */
      .item:hover .desc {
          bottom: 0;
      }
  </style>
</head>
<body>
<div class="content">
  <div class="item">
    <span class="desc"></span>
  </div>
</div>
</body>
</html>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4f0b464cb78945d6a29463ad5b2d89d3.gif#pic_center)

## 2D 转换 (transfrom)

**转换**是 CSS3 中具有颠覆性的一个特征，可以实现元素的**位移、旋转、变形、缩放**，甚至支持矩阵方式。

转换再配合过渡和动画，可以取代大量早期只能靠 Flash 才可以实现的效果。

在 CSS3 当中，通过 `transform` 转换来实现 2D 转换或者 3D 转换。

- 2D转换包括：缩放、移动、旋转。

### 2.1 缩放：`scale`

格式：

```javascript
	transform: scale(x, y);

	transform: scale(2, 0.5);
```

参数解释： x：表示水平方向的缩放倍数。y：表示垂直方向的缩放倍数。如果只写一个值就是等比例缩放。

取值：大于1表示放大，小于1表示缩小。不能为百分比。

### 2.2 位移：translate

格式：


```javascript
	transform: translate(水平位移, 垂直位移);

	transform: translate(-50%, -50%);
```

参数解释：

- 参数为百分比，相对于自身移动。

- 正值：向右和向下。 负值：向左和向上。如果只写一个值，则表示水平移动。

### 2.3 旋转：rotate

格式：

```javascript
	transform: rotate(角度);

	transform: rotate(45deg);
```

参数解释：正值 顺时针；负值：逆时针。

rotate 旋转时，默认是以盒子的正中心为坐标原点的。如果想**改变旋转的坐标原点**，可以用`transform-origin`属性。格式如下：


```javascript
	transform-origin: 水平坐标 垂直坐标;

	transform-origin: 50px 50px;

	transform-origin: center bottom;   //旋转时，以盒子底部的中心为坐标原点
```


## 3D 转换

### 3.1 旋转：rotateX、rotateY、rotateZ

**3D坐标系（左手坐标系）**

**浏览器的这个平面，是X轴、Y轴；垂直于浏览器的平面，是Z轴。**

从上面这句话，我们也能看出：所有的3d旋转，对着正方向去看，都是顺时针旋转。

**格式：**

```javascript
	transform: rotateX(360deg);    //绕 X 轴旋转360度

	transform: rotateY(360deg);    //绕 Y 轴旋转360度

	transform: rotateZ(360deg);    //绕 Z 轴旋转360度

```

### 3.2 移动：translateX、translateY、translateZ

**格式：**

```javascript
	transform: translateX(100px);    //沿着 X 轴移动

	transform: translateY(360px);    //沿着 Y 轴移动

	transform: translateZ(360px);    //沿着 Z 轴移动

```

###### 3.3 透视：perspective

电脑显示屏是一个 2D 平面，图像之所以具有立体感（3D效果），其实只是一种视觉呈现，通过透视可以实现此目的。

透视可以将一个2D平面，在转换的过程当中，呈现3D效果。但仅仅只是视觉呈现出 3d 效果，并不是正真的3d。

格式有两种写法：

- 作为一个属性，设置给父元素，作用于所有3D转换的子元素

- 作为 transform 属性的一个值，做用于元素自身。

格式举例：

```css
perspective: 500px;
```



## animation

**CSS3的animation属性可以像Flash制作动画一样，通过控制关键帧来控制动画的每一步**，实现更为复杂的动画效果。ainimation实现动画效果主要由两部分组成：

制作动画分为两步：

1.  定义动画 @keyframes
2.  使用(调用)

### 4.1 定义动画

###### @keyframes(关键帧) 用于 定义动画

```css
@keyframes animation01 {
    0% {
        margin-top: 10px;
    }
    100% {
        margin-top: 20px;
    }
}
```

0%是动画的开始，100%是动画的完成。**中间可以插入任意百分比**
在 @keyframes 中规定某项CSS样式，就能创建由当前样式逐渐改为新样式的动画效果
**可以改变任意多的样式任意多的次数。**
或用关键词"from"和"to",等同于0%和100%

两者等同

```css
@keyframes animation01 {
    from {
        margin-top: 10px;
    }
    to {
        margin-top: 20px;
    }
}
```

**部分属性是不可以发生改变的,因为 “不连续”,属性间的变换没有中间值**

### 4.2 调用动画

要调用动画,必须要得给他添加一些必要的属性: 

###### 时间函数（animation-timing-function）

animation-timing-function 属性定义了动画的播放速度曲线。

|                               |                                                              |
| :---------------------------: | :----------------------------------------------------------: |
|              值               |                             描述                             |
|            linear             |                 动画从头到尾的速度是相同的。                 |
|             ease              |        默认。动画以低速开始，然后加快，在结束前变慢。        |
|            ease-in            |                       动画以低速开始。                       |
|           ease-out            |                       动画以低速结束。                       |
|          ease-in-out          |                    动画以低速开始和结束。                    |
|             steps             |              指定了时间函数中的间隔数量（步长）              |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。 |

默认值，如果没有显示写调用的函数，则默认为ease。

**cubic-bezier(*n*,*n*,*n*,*n*)  是生成速度曲线的函数**  


![在这里插入图片描述](https://img-blog.csdnimg.cn/3f8de41fdcdc4ca9ac07eba9d0e7a557.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


从上图中我们可以看到，cubic-bezier有四个点：
两个默认的，即：P0(0,0)，P3(1,1)；
**两个控制点，即 cubic-bezier 函数中传递的四个值,分别依次带入 P1(x1,y1)，P2(x2,y2)**
注：X轴的范围是0~1，超出cubic-bezier将失效，Y轴的取值没有规定，但是也不宜过大。
**我们只要调整两个控制点P1和P2的坐标，最后形成的曲线就是动画曲线。**

举例 cubic-bezier(0.25,0.1,0.25,1)

![在这里插入图片描述](https://img-blog.csdnimg.cn/33e6e8ec905b4ca78e98c4d6180a3386.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


画的丑,下面不手画了

给大家一个地址: https://easings.net/

可以自己去看看 cubic-bezier( ) 函数的演示

![在这里插入图片描述](https://img-blog.csdnimg.cn/f9b92d3cafb8420ba4cd3743d2ae69f0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


and cubic-bezier 可以自己随心所欲地绘制 cubic-bezier( ) 函数

https://cubic-bezier.com/##.17,.67,.83,.67

![在这里插入图片描述](https://img-blog.csdnimg.cn/bb09420f1757434fae48fd5bbad3ce6b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


**而 steps 会一卡一卡的 生成我们的动画**

---

###### 动画方向（animation-direction）

animation-direction: normal 正序播放  终点=>起点
animation-direction: reverse 倒序播放  终点=>起点
animation-direction: alternate 交替播放  
animation-direction: alternate-reverse 反向交替播放  

---

###### 动画延迟（animation-delay）

animation-delay属性定义动画是从何时开始播放，即动画应用在元素上的到动画开始的这段时间的长度。默认值0s，表示动画在该元素上后立即开始执行。该值以秒(s)或者毫秒(ms)为单位。

---


###### 动画迭代次数（animation-iteration-count）

animation-iteration-count该属性就是定义我们的动画播放的次数。次数可以是1次或者无限循环。默认值只播放一次。

single-animation-iteration-count = infinite | number


---


###### 动画填充模式（animation-fill-mode）

animation-fill-mode是指给定动画播放前后应用元素的样式。

single-animation-fill-mode = none | forwards | backwards | both

animation-fill-mode: none 动画执行前后不改变任何样式
animation-fill-mode: forwards 保持目标动画最后一帧的样式
animation-fill-mode: backwards 保持目标动画第一帧的样式
animation-fill-mode: both 动画将会执行 forwards 和 backwards 执行的动作。


---


###### 动画播放状态（animation-timing-function）

animation-play-state: 定义动画是否运行或者暂停。可以确定查询它来确定动画是否运行。默认值为running

single-animation-timing-function = running | paused

running 动画正常播放
paused 动画暂停播放


---


###### 简写

```css
animation:动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或者结束的状态;
```

但是需要注意: 简写属性里面不包含 **animation- play-state**

#### 补充动画

### 5.1 按钮抖动动画

```js
<template>
  <div :class="{ shake: disabled }">
    <button @click="warnDisabled">Click me</button>
    <span v-if="disabled">This feature is disabled!</span>
  </div>
</template>

<script>
export default {
  name: 'ShakeButton',
  data() {
    return {
      disabled: false
    }
  },
  methods: {
    warnDisabled() {
      this.disabled = true
      setTimeout(() => {
        this.disabled = false
      }, 1500)
    }
  }
}
</script>

<style>
.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
```

###### 5.2 背景颜色随鼠标渐变

[演示地址](http://ximingx.com/TransitionColor22_3_24/index.html)

```js
<template>
  <div
      @mousemove="onMousemove"
      :style="{ backgroundColor: `hsl(${x}, 80%, 50%)` }"
      class="movearea"
  >
    <p>Move your mouse across this div...</p>
    <p>x: {{ x }}</p>
  </div>
</template>

<script>
export default {
  name: 'ShakeButton',
  data() {
    return {
      x: 0
    }
  },
  methods: {
    onMousemove(e) {
      this.x = e.clientX
    }
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
.movearea {
  width: 100vw;
  height: 100vh;
  transition: 0.3s background-color ease;
}
</style>
```

## 正则表达式

**定义**：正则表达式用于定义一些字符串的规则。

**作用**：计算机可以根据正则表达式，来检查一个字符串是否符合指定的规则；或者将字符串中符合规则的内容提取出来。

### 创建正则表达式的对象

#### 方式一：使用构造函数创建正则表达式的对象

语法：

```javascript
	var 变量 = new RegExp("正则表达式"); // 注意，参数是字符串

	var 变量 = new RegExp("正则表达式", "匹配模式"); // 注意，两个参数都是字符串
```

备注：`RegExp`的意思是 **Regular expression**。使用typeof检查正则对象，会返回object。

上面的语法中，既可以传一个参数，也可以传两个参数。

创建了正则表达式的对象后，该怎么使用呢？大致分为两个步骤：

- （1）创建正则表达式的对象 reg。

- （2）使用 reg 的test() 方法，判断指定字符串是否符合规则。

**正则表达式的`test()`方法**：【重要】

```javascript
	myReg.test(str); // 判断字符串 str 是否符合 指定的 myReg 这个正则表达式的规则
```

解释：使用`test()`这个方法可以用来检查一个字符串是否符合正则表达式的规则，**如果符合则返回true，否则返回false**。

我们来看看下面的例子。

**1、传一个参数时**：

构造函数 RegExp 中，可以只传一个参数。

代码举例：

```javascript
	var reg = new RegExp("x"); // 定义一个正则表达式：检查一个字符串中是否含有 a

	var str1 = "ximingx";
	var str2 = "bawd";

	// 通过 test()方法，判断字符串是否符合 上面定义的 reg 规则
	console.log(reg.test(str1)); // 打印结果：true
	console.log(reg.test(str2)); // 打印结果：false
```

注意，上面的例子中，我们是先定义了一个正则表达式的规则，然后通过正则表达式的`test()`方法来判断字符串是否符合之前定义的规则。

**2、传两个参数时**：匹配模式 【重要】

构造函数 RegExp 中，也可以传两个参数。我们可以传递一个**匹配模式**作为第二个参数。这个参数可以是：

- `i` 忽略大小写。这里的 i 指的是 ignore。

- `g` 全局匹配模式。这里的 g 指的是 global。

代码举例：

```javascript
    var reg = new RegExp('M', 'i');
    var str = 'ximingx';

    console.log(reg.test(str)); // 打印结果：true
```

#### 方式二：使用字面量创建正则表达式

我们可以使用字面量来创建正则表达式。

语法：

```javascript
	var 变量 = /正则表达式/;  

	var 变量 = /正则表达式/匹配模式;  // 注意，这个语法里没有引号
```

代码举例：

```javascript
	var reg = /X/i; // 定义正则表达式的规则：检查一个字符串中是否含有 a。忽略大小写。
	var str = "ximingx";

	console.log(typeof reg);  // 打印结果：object
	console.log(reg.test(str)); // 打印结果：true
```

#### 以上两种方式的对比

- 方式一：使用构造函数创建时，更加灵活，因为参数中还可以传递变量。

- 方式二：使用字面量的方式创建，更加简单。

代码举例：

```javascript
	var reg = new RegExp("a", "i"); // 方式一

	var reg = /a/i; // 方式二
```

上面这两行代码的作用是等价的。

#### 避坑指南：全局匹配 g 慎用test()方法

对于非全局匹配的正则表达式，`test()`只会检测**是否存在某个目标字符串**（只要存在就为 true），多次检测的结果都相同。例如：

```javascript
const reg = /test/;
const str = '_test_test';

reg.test(str) // true
reg.test(str) // true
reg.test(str) // true
```

重点来了。

当设置全局标志 `/g` 时，一旦字符串中还存在匹配，test() 方法都将返回 true，同时匹配成功后将把 `lastIndex` 属性的值**设置为上次匹配成功结果之后的第一个字符所在的位置**，下次匹配将从 `lastIndex` 指示的位置开始；匹配不成功时返回 false，同时将 lastIndex 属性的值重置为 0。

```javascript
const reg = /test/g;
const str = '_test_test_test';

console.log(reg.test(str)); // true
console.log(reg.lastIndex); // 5

console.log(reg.test(str)); // true
console.log(reg.lastIndex); // 10

console.log(reg.test(str)); // true
console.log(reg.lastIndex); // 15

console.log(reg.test(str)); // false
console.log(reg.lastIndex); // 0
```

**总结**：

全局匹配模式`g`一般用于 `exec()`、`match()`、`replace()`等方法。

全局匹配模式`g`如果用于test()方法会有问题。因为g模式会生成一个`lastindex`参数来存储匹配最后一次的位置。

### 正则表达式的简单语法

#### 检查一个字符串中是否包含 a或b

**写法1**：

```javascript
	var reg = /a|b/;
```

解释：使用 `|` 表示`或`的意思。

**写法2**：

```javascript
	var reg = /[ab]/;  // 跟上面的那行语法，是等价的
```

解释：这里的`[]`也是表示`或`的意思。

`[]`这个符号在正则还是比较常用的。我们接下来看几个例子。

#### []表示：或

一些规则：

- `/[ab]/` 等价于 `/a|b/`：检查一个字符串中是否包含 **a或b**

- `/[a-z]/`：检查一个字符串那种是否包含**任意小写字母**

- `/[A-Z]/`：任意大写字母

- `/[A-z]/`：任意字母

- `/[0-9]/`：任意数字

- `/a[bde]c/`：检查一个字符串中是否包含 abc 或 adc 或 aec

#### [^ ] 表示：除了

举例1：

```javascript
  var reg = /[^ab]/; // 规则：字符串中，除了a、b之外，还有没有其他的字符内容？
  var str = "acb";

  console.log(reg.test(str)); // 打印结果：true
```

举例2：（可以用来验证某字符串是否为 纯数字）

```javascript
	var reg = /[^0-9]/;  // 规则：字符串中，除了数字之外，还有没有其他的内容？
	var str1 = "1991";
	var str2 = "199a1";

	console.log(reg.test(str1)); // 打印结果：false （如果字符串是 纯数字，则返回 false）
	console.log(reg.test(str2)); // 打印结果：true
```

### 支持正则表达式的 String 对象的方法

 String对象的如下方法，是支持正则表达式的：

| 方法      | 描述                                                   | 备注 |
| :-------- | :----------------------------------------------------- | :--- |
| split()   | 将字符串拆分成数组                                     |      |
| search()  | 搜索字符串中是否含有指定内容，返回索引 index           |      |
| match()   | 根据正则表达式，从一个字符串中将符合条件的内容提取出来 |      |
| replace() | 将字符串中的指定内容，替换为新的内容并返回             |      |

下面来分别介绍和举例。

#### split()

`split()`：将一个字符串拆分成一个数组。可以接受一个正则表达式作为参数。

**正则相关的举例**：根据任意字母，将字符串拆分成数组。

代码实现：（通过正则）

```javascript
	var str = "1a2b3c4d5e6f7g";

	var result = str.split(/[A-z]/); // 参数是一个正则表达式：表示所有字母
	console.log(result);
```

打印结果：

```json
	["1", "2", "3", "4", "5", "6", "7", ""]
```

#### search()

`search()`：搜索字符串中是否含有指定内容。如果搜索到指定内容，则会返回第一次出现的索引；否则返回-1。

`search()`方法可以接受一个正则表达式作为参数，然后会根据正则表达式去检索字符串。`serach()`只会查找第一个，即使设置全局匹配也没用。

**举例**：

```javascript
	var str = "hello abc hello aec afc";
	/*
	* 搜索字符串中是否含有abc 或 aec 或 afc
	*/
	result = str.search(/a[bef]c/);
	console.log(result); // 打印结果：6
```

#### match()

`match()`：根据正则表达式，从一个字符串中将符合条件的内容提取出来，封装到一个数组中返回（即使只查询到一个结果）。

**注意**：默认情况下，`match()`方法只会找到**第一个**符合要求的内容，找到以后就停止检索。我们可以设置正则表达式为**全局匹配**模式，这样就会匹配到所有的内容，并以**数组**的形式返回。

另外，我们可以为一个正则表达式设置多个匹配模式，且匹配模式的顺序无所谓。

**代码举例**：

```javascript
	var str = "1a2a3a4a5e6f7A8B9C";

	var result1 = str.match(/[a-z]/);   // 找到符合要求的第一个内容，然后返回
	var result2 = str.match(/[a-z]/g);  // 设置为“全局匹配”模式，匹配字符串中 所有的小写字母
	var result3 = str.match(/[a-z]/gi); // 设置多个匹配模式，匹配字符串中 所有的字母（忽略大小写）

	console.log(result1); // 打印结果：["a"]
	console.log(result2); // 打印结果：["a", "a", "a", "a", "e", "f"]
	console.log(result3); // 打印结果：["a", "a", "a", "a", "e", "f", "A", "B", "C"]
```

**总结**：

match()这个方法还是很实用的，可以在一个很长的字符串中，提取出**有规则**的内容。这不就是爬虫的时候经常会遇到的场景么？

#### replace()

`replace()`：将字符串中的指定内容，替换为新的内容并返回。不会修改原字符串。

语法：

```javascript
	新的字符串 = str.replace(被替换的内容，新的内容);
```

参数解释：

- 被替换的内容：可以接受一个正则表达式作为参数。

- 新的内容：默认只会替换第一个。如果需要替换全部符合条件的内容，可以设置正则表达式为**全局匹配**模式。

代码举例：

```javascript
    //replace()方法：替换
    var str2 = "Today is fine day,today is fine day !!!"

    console.log(str2);
    console.log(str2.replace("today","tomorrow"));  //只能替换第一个today
    console.log(str2.replace(/today/gi,"tomorrow")); //这里用到了正则，且为“全局匹配”模式，才能替换所有的today
```

### 常见正则表达式举例

#### 检查一个字符串是否是一个合法手机号

手机号的规则：

- 以1开头（`^1` 表示1开头 , `[^1]`表示非1或除了1）

- 第二位是3~9之间任意数字

- 三位以后任意9位数字

正则实现：

```javascript
	var phoneStr = "13067890123";

	var phoneReg = /^1[3-9][0-9]{9}$/;

	console.log(phoneReg.test(phoneStr));
```

**备注**：如果在正则表达式中同时使用`^`和`$`符号，则要求字符串必须完全符合正则表达式。

#### 去掉字符串开头和结尾的空格

正则实现：

```javascript
	str = str.replace(/^\s*|\s*$/g,"");
```

解释如下：

```javascript
	str = str.replace(/^\s*/, ""); //去 除开头的空格

	str = str.replace(/\s*$/, ""); //去除结尾的空格
```

#### 判断字符串是否为电子邮件

正则实现：

```javascript
	var emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}$/;

	var email = "abchello@163.com";

	console.log(emailReg.test(email));
```

## promise

### **Promise 是异步编程的一种优雅的解决方案**，是一个构造函数，

有all、reject、resolve这几个方法，原型上有then、catch等方法,

为什么要说优雅的解决方法呢,大家可以对比一下异步编程使用回调函数这种方法的代码,话不多说,看图

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-sIEmRflE-1636978634973)(D:/start/v2-cf1c78890006e078a538842a0caa7127_1440w.jpg)\]](https://img-blog.csdnimg.cn/b6d4b3eace49495b984f6d535dec176a.jpg?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


### 在学习 Promise 的时候 首先我们要明白 Promise对象 有以下两个特点。

（1）Promise对象里的异步操作执行时**有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败)** ,而Promise对象状态的改变，只有两种可能：**从pending变为fulfilled或者从pending变为rejected。**

（2）而一旦上面的这种状态发生改变，之后就不会再变，任何时候都可以得到这个结果。**如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果**。

### 那么最简单的 new 一个 promise

以下案例均在 vue 的代码中演示

```js
  mounted() {
    let promise1 = new Promise(function(resolve, reject){
      //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
      setTimeout(function(){
        console.log('完成异步操作');
        resolve('返回任意的数据');
        // 会在两秒之后返回打印值
      }, 2000);
    })
  }
```

**这里我们 new 了一个 Promise , 在 Promise 里面执行异步操作的代码** 

可以看到,这里**只是对他进行了声明,并没有执行这一个函数**

但是从结果上看来结果 却是执行了 这个函数  ,  这里先忘记里面的  resolve('返回任意的数据');  里起了什么作用

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-gu15OjSr-1636978634975)(D:/start/image-20211115193102061.png)\]](https://img-blog.csdnimg.cn/bccb8ea0dcb64d54a7cb4c94cf3d4e8f.png)


**其执行过程是：执行了一个异步操作，也就是setTimeout，2秒后，输出“完成异步操作”，并且调用resolve方法。**

这里需要知道的是:  如果我们直接 new 一个 promise , 而没有将他放置在函数中的时候 , 他会直接执行里面的异步操作

所以我们用Promise的时候一般是包在一个函数中，在需要的时候去运行这个函数 , 这里演示一下

```js
  methods: {
    test:function () {
      return new Promise(function(resolve, reject){
        //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
        setTimeout(function(){
          console.log('完成异步操作');
          resolve('返回任意的数据');
          // 会在两秒之后返回打印值
        }, 2000);
      })
    }
  },
  mounted() {
    this.test()
  }
```

可以看到 在这里 我们直接 return 出  Promise对象 , 这将在在之后给我们非常大的便利 , **可以让我们直接链式调用它的方法**

### 这里还要讲解 resolve() 的作用

先看一段代码和结果

```js
mounted() {
  let promise = new Promise(function(resolve, reject){
    //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
    setTimeout(function(){
      resolve('返回任意的数据');
      // 会在两秒之后返回打印值
    }, 2000);
  }).then((data) => {
    console.log(data)
  })
}
```

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-VYtAOvO1-1636978634976)(D:/start/image-20211115193858432.png)\]](https://img-blog.csdnimg.cn/c61a311d2fab4c1c9669cb5db62f900f.png)


我们可以发现在之后的 .then(data) 中有一句 console.log(data)

这这里的 **data 对应的正是 resolve() 参数中返回的值** , **原来then里面的函数就跟我们平时的回调函数一个意思，能够在这个异步任务执行完成之后被执行.** 而这也这就是Promise的作用了，**用链式调用的方式执行回调函数。**

而 Promise的优势正是在于可以链式调用 , 可以在then方法中继续写Promise对象并返回，然后继续调用then来进行回调操作。

但是 + - +

```js
  mounted() {
    return new Promise(function (resolve, reject) {
      if (1 < 2) {
        resolve(true)
      } else {
        console.log("error")
      }
    }).then((data) => {
      console.log(data)
      return new Promise(function (resolve, reject) {
        if (2 < 3) {
          resolve(true)
        } else {
          console.log("error")
        }
      })
    }).then((data) => {
      console.log(data)
      return new Promise(function (resolve, reject) {
        if (2 < 3) {
          resolve(true)
        } else {
          console.log("error")
        }
      }).then((data) => {
        console.log(data)
      })
    })
  }
```

上面这样子的代码  是不是很丑 , 很难看懂 + - + , 而且和之前的回调地狱一样不方便读懂代码

但是实际上 不这么搞

### 我们一般采用下面的写法

```js
  methods: {
    test:function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        },1000)
      })
    }
  },
  mounted() {
    this.test()
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
        })
  }
```

这样就能够按顺序,输出每个异步回调中的内容

每次 .then 中的 return 都可以返回一个 Promise , 从而可以在之后继续链式调用  , 这样写是不是就很好看了

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-y3BhgSTZ-1636978634978)(D:/start/image-20211115195354417.png)\]](https://img-blog.csdnimg.cn/15797a6e7602413caecfadc38d59dc4c.png)


### reject() 的用法

**resolve是对promise成功执行时候的回调,它把promise的状态修改为fullfiled**

那么，**reject就是失败的时候的回调，他把promise的状态修改为rejected**，这样我们就可以在 .then中 捕捉到，然后执行“失败”情况的回调

```js
  methods: {
    test:function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        },1000)
      })
    }
  },
  mounted() {
    this.test()
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return new Promise((resolve, reject) => {
            if ( 1 !== 1) {
              reject(1);
            } else {
              resolve(2);
            }
          })
        })
       .then((data) => {
         console.log(data)
       },(info) => {
         console.log(info)
       })
  }
```

这里在最后一次调用 promise 返回的结果时 , 执行力 resolve(2) , 最后打印台显示的结果也是 2 ,

而且我们也可以看到 , 在then中传了两个参数，这两个参数分别是两个函数，then方法可以接受两个参数，**第一个对应resolve的回调，第二个对应reject的回调。**（也就是说then方法中接受两个回调，一个成功的回调函数，一个失败的回调函数），所以我们能够分别拿到成功和失败传过来的数据就有以上的运行结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/b7cc3321da2348b981fdedfcf2bb6b3a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

接下来我们再看一下 .catch 和 直接在 .then 中传入第二个参数的区别

```js
methods: {
  test: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 1000)
    })
  }
},
mounted() {
  this.test()
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return new Promise((resolve, reject) => {
          if (1 !== 1) {
            reject(1);
          } else {
            resolve(2);
          }
        })
      })
      .then((data) => {
        console.log(data)
      })
      .catch((info) => {
        console.log(info)
      })
}
```

我们可以看到: 两次结果是一样的 , 但是我们需要明白 , 在 .then 中写第二个参数 和 用 .catch 是有区别的

.catch 除了会得到失败的结果,还会捕获异常 , 类似于一些语法的错误 , 在捕获到异常的时候 , 并不会卡死 , 而是继续执行下面的代码
**与then同级的另一个方法，all方法，该方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后并且执行结果都是成功的时候才执行回调。**

```js
  methods: {
    test1: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    },
    test2: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    },
    test3: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    }
  },
  mounted() {
    Promise.all([this.test1, this.test2, this.test3])
        .then((res) => {
          console.log(res)
          console.log(res.length)
        })
  }
```

这里在三个异步方法都执行完毕后 , 返回了一个数组 , 里面包含了每个方法对应的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/d48a26607ee24c4f942a96e9a45d7c4a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


Promise.all来执行多个异步操作，**all接收一个数组参数**，这组参数为需要执行异步操作的所有方法，**里面的值最终都算返回Promise对象。**

这样，**三个异步操作的并行执行的，等到它们都执行完后才会进到then里面**。



### 除此之外还有 race 的 用法

all是等所有的异步操作都执行完了再执行then方法，那么race方法就是相反的，**谁先执行完成就先执行回调**。先执行完的不管是进行了race的成功回调还是失败回调，**其余的将不会再进入race的任何回调**



```js
methods: {
  test1: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 1000)
    })
  },
  test2: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 2000)
    })
  },
  test3: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 3000)
    })
  }
},
mounted() {
  Promise.race([this.test1, this.test2, this.test3])
      .then((res) => {
        console.log(res)
      })
}
```

这次只是 将 Promise.all 修改为了 Promise.race , 返回的结果中 只有最先执行结束的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/94290eb4a81246a988b7852feac0c76e.png)

**补充:**


```js
// Promise 用于解决回调地狱
// Promise 是一个构造函数
const fs = require('fs')
// 在 promise 容器 里的函数 里放置异步操作
// promise 容器一旦创建就开始执行里面的代码
new Promise(function (resolve, reject) {
  fs.readFile('./package.json', 'utf8', function (err, data) {
    if (err) {
     reject(err)
    } else {
      resolve(data)
    }
  })
}).then(data => {
  console.log(data);
  // -----------------------------------------------------------------------
  new Promise(function (resolve,reject) {
    fs.readFile('./package.json', 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  }).then(data => {
    console.log(data);
  }).catch (err => {
    console.log(err);
  })
  // -----------------------------------------------------------------------
}).catch(err => {
  console.log(err);
})
```

**异步的处理方式**

```js
const fs = require("fs");

const p1 = new Promise((resolve, reject) => {
  fs.readFile('./a.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

const p2 = new Promise((resolve, reject) => {
  fs.readFile('./b.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

const p3 = new Promise((resolve, reject) => {
  fs.readFile('./c.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

p1.then((data) => {
    console.log(data);
  // 这里的 return p2 会将 p2 的 resolve 结果 传递给下面的 .then
  // 当 return 一个 promise 对象时,后续的 .then 中方法的第一个参数会作为 返回的 promise (p2) 的 resolve
    return p2
})
  .catch((err) => {
    console.log(err);
  })
  .then(data => {
    console.log(data);
    return p3
  })
  .catch((err) => {
    console.log(err);
  })
  .then(data => {
    console.log(data);
  })
  .catch((err) => {
    console.log(err);
  })
```

**异步函数的封装**

```js
const fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, "utf8", function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./a.txt')
  .then(data => {
    console.log(data);
    return pReadFile('./b.txt')
  })
  .then((data) => {
    console.log(data);
    return pReadFile('./c.txt')
  })
  .then((data) => {
    console.log(data);
  })
```

**Promise 在创建后会立马执行**
下面代码中，Promise 新建后立即执行，所以首先输出的是Promise。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出。
注意结果的输出顺序
```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```

## Es6

### Symbol

#### 概述

背景：ES5中对象的属性名都是字符串，容易造成重名，污染环境。

**概念**：ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

**特点：**

- Symbol属性对应的值是唯一的，解决**命名冲突问题**

- Symbol值不能与其他数据进行计算，包括同字符串拼串

- for in、for of 遍历时不会遍历Symbol属性。

#### 1. 创建Symbol属性值

Symbol是函数，但并不是构造函数。创建一个Symbol数据类型：

```javascript
    let mySymbol = Symbol();

    console.log(typeof mySymbol);  //打印结果：symbol
    console.log(mySymbol);         //打印结果：Symbol()
```

#### 2. 将Symbol作为对象的属性值

```javascript
    let mySymbol = Symbol();

    let obj = {
        name: 'smyhvae',
        age: 26
    };

    //obj.mySymbol = 'male'; //错误：不能用 . 这个符号给对象添加 Symbol 属性。
    obj[mySymbol] = 'hello';    //正确：通过属性选择器给对象添加 Symbol 属性。后面的属性值随便写。

    console.log(obj);
```

上面的代码中，我们尝试给obj添加一个Symbol类型的属性值，但是添加的时候，不能采用`.`这个符号，而是应该用`属性选择器`的方式。

#### 3. 创建Symbol属性值时，传参作为标识

如果我通过 Symbol()函数创建了两个值，这两个值是不一样的：

```javascript
    let mySymbol1 = Symbol();
    let mySymbol2 = Symbol();

    console.log(mySymbol1 == mySymbol2); //打印结果：false
    console.log(mySymbol1);         //打印结果：Symbol()
    console.log(mySymbol2);         //打印结果：Symbol()
```

上面代码中，倒数第三行的打印结果也就表明了，二者的值确实是不相等的。

最后两行的打印结果却发现，二者的打印输出，肉眼看到的却相同。那该怎么区分它们呢？

既然Symbol()是函数，函数就可以传入参数，我们可以通过参数的不同来作为**标识**。比如：


```javascript
    //在括号里加入参数，来标识不同的Symbol
    let mySymbol1 = Symbol('one');
    let mySymbol2 = Symbol('two');

    console.log(mySymbol1 == mySymbol2); //打印结果：false
    console.log(mySymbol1);         //打印结果：Symbol(one)
    console.log(mySymbol2);         //打印结果：Symbol(two)
    console.log(mySymbol2.toString());//打印结果：Symbol(two)
```

#### 4. 定义常量

Symbol 可以用来定义常量：


```javascript
    const MY_NAME = Symbol('my_name');
```

#### 5. 内置的 Symbol 值

除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法。

- `Symbol.iterator`属性

对象的`Symbol.iterator`属性，指向该对象的默认遍历器方法。



### 将ES6的语法转为ES5 (Babel)

> 掌握 ES6 之后，如果你的业务需要考虑 ES5 的兼容性，则可以这样做：写 ES6 语法的 js 代码，然后通过 `Babel`将 ES6 转换为 ES5。如果没有这样的需要，那么下面的内容，了解即可。

babel 的作用是将 ES6 语法转为 ES5 语法，支持低端浏览器。

以一个简单的案例说明

#### 1. 先创建一个项目的目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/bdd90d76902b4db0afddebd454609192.png)
在 index.js 写入

```js
let a = item => item + 2
console.log(a(4))
```

这个文件是一个 ES6 语法 的 js 文件，稍后，我们尝试把这个 ES6 语法的 js 文件转化为 ES5 的 js 文件。



#### 2. 安装 Babel-cli

初始化项目：

在安装 Babel 之前，需要先用 npm init 先初始化我们的项目。打开终端或者通过 cmd 打开命令行工具，进入项目目录，输入如下命令：

```bash
	npm init -y
```

上方代码中，`-y` 代表全部默认同意，就不用一次次按回车了（稍后再根据需要，在文件中手动修改）。命令执行完成后，会在项目的根目录下生成 package.json 文件：

```json
{
  "name": "babel",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```
#### 3. 本地安装 babel-preset-es2015 和 babel-cli：

```bash
	npm install --save-dev babel-preset-es2015 babel-cli
```

#### 4. 新建.babelrc：

在根目录下新建文件`.babelrc`，输入如下内容：

```js
{
    "presets":[
        "es2015"
    ],
    "plugins":[]
}
```

#### 5. 开始转换：

现在，我们应该可以将 ES6 的文件转化为 ES5 的文件了，命令如下：（此命令略显复杂）

```bash
	babel src/index.js -o dist/index.js
```

我们可以将上面这个命令进行简化一下。操作如下：

在文件 `package.json` 中修改键 `scripts`中的内容：

```json
  "scripts": {
    "build": "babel src/index.js -o dist/index.js"
  },
```

目前为止，环境配置好了。以后，我们执行如下命令，即可将`src/index.js`这个 ES6 文件转化为 `dist/index.js`这个 ES5 文件：

```bash
	npm run build
```

我们执行上面的命令之后，会发现， dist 目录下会生成 ES5 的 js 文件：

之后我们就可以在 index.html 中使用 es5的语法了

```js
"use strict";

var a = function a(item) {
  return item + 2;
};
console.log(a(4));
```


## 作用域（Scope）的概念和分类

-   **概念**：通俗来讲，作用域是一个变量或函数的作用范围。作用域在**函数定义**时，就已经确定了。换句话说，作用域决定了代码区块中变量和其他资源的可见性。

-   **目的**：为了提高程序的可靠性，同时减少命名冲突。

在 JS 中，一共有两种作用域：（ES5 中）

-   **全局作用域**：作用于整个 script 标签内部，或者作用于一个独立的 JS 文件。
-   **函数作用域**（局部作用域）：作用于函数内的代码环境。



### 全局作用域 和 window 对象

直接编写在 script 标签中的 JS 代码，都在全局作用域。全局作用域在页面打开时创建，在页面关闭时销毁。

在全局作用域中有一个全局对象 window，它代表的是一个浏览器的窗口，由浏览器创建，我们可以直接使用。相关知识点如下：

-   创建的**变量**都会作为 window 对象的属性保存。比如在全局作用域内写 `var a = 100`，这里的 `a` 等价于 `window.a`。
-   创建的**函数**都会作为 window 对象的方法保存。

### 作用域的访问关系

在内部作用域中可以访问到外部作用域的变量，在外部作用域中无法访问到内部作用域的变量。

代码举例：

```javascript
var a = 'aaa';
function foo() {
    var b = 'bbb';
    console.log(a); // 打印结果：aaa。说明 内层作用域 可以访问 外层作用域 里的变量
}

foo();
console.log(b); // 报错：Uncaught ReferenceError: b is not defined。说明 外层作用域 无法访问 内层作用域 里的变量
```

### 变量的作用域

根据作用域的不同，变量可以分为两类：全局变量、局部变量。

**全局变量**：

-   在全局作用域下声明的变量，叫「全局变量」。在全局作用域的任何一地方，都可以访问这个变量。

-   在全局作用域下，使用 var 声明的变量是全局变量。

-   **特殊情况：在函数内不使用 var 声明的变量也是全局变量（不建议这么用）。** (~ ~ ~最好不要哇, 因为他还有一个条件: 必须先调用函数之后才可以使用该变量)

```js
function outFun1() {
    variable1 = "未定义直接赋值的变量";
}
function outFun2() {
    variable2 = "未定义直接赋值的变量";
}
outFun2();//要先执行这个函数，否则根本不知道里面是啥
console.log(variable2); //未定义直接赋值的变量
console.log(variable1); //variable1 is not defined
```

**局部变量**：

-   **定义在函数作用域的变量，叫「局部变量」。仅限函数内部访问这个变量。**

-   在函数内部，使用 var 声明的变量是局部变量。

-   函数的**形参**也是属于局部变量。

从执行效率来看全局变量和局部变量：

-   全局变量：只有浏览器关闭时才会被销毁，比较占内存。

-   局部变量：当其所在的代码块运行结束后，就会被销毁，比较节约内存空间。

### 作用域的上下级关系

当在函数作用域操作一个变量时，它会先在自身作用域中寻找，如果有就直接使用（**就近原则**）。如果没有则向上一级作用域中寻找，直到找到全局作用域；如果全局作用域中依然没有找到，则会报错 ReferenceError。

在函数中要访问全局变量可以使用 window 对象。（比如说，全局作用域和函数作用域都定义了变量 a，优先使用的是函数中的a , 但如果想访问全局变量，可以使用`window.a`）

### 作用域的预处理

**预处理（预解析）**的概念：浏览器在解析 JS 代码之前，会进行一个操作叫“预处理（预解析）”：将当前 JS 代码中所有变量的定义和函数的定义，放到所有代码的最前面。

这种预解析，也称之为声明提前。

### 全局作用域-变量的声明提前（变量提升）

使用 var 关键字声明的变量（ 比如 `var a = 1`），**会在所有的代码执行之前被声明**（但是不会赋值），但是如果声明变量时不是用 var 关键字（比如直接写`a = 1`），则变量不会被声明提前。

**举例 1**：

```javascript
// 这里并没有报错
console.log(a);
var a = 123;
```

打印结果：undefined。注意，打印结果并没有报错，而是 undefined，说明变量 a 被提前声明了，只是尚未被赋值。

**举例 2**：

```javascript
console.log(a);
// 没有使用var声明
a = 123; 
```

程序会报错：`Uncaught ReferenceError: a is not defined`。

**举例 3**：

```javascript
a = 123; //此时a相当于window.a
console.log(a);
```

打印结果：123。

**注意 2 和 3 的差别**

**举例 4**：

```javascript
foo();

function foo() {
    if (false) {
        var i = 123;
    }
    console.log(i);
}
```

打印结果：undefined。注意，打印结果并没有报错，而是 undefined。这个例子，再次说明了：变量 i 在函数执行前，就被提前声明了，只是尚未被赋值。

例 4 中， `if(false)`里面的代码虽然不会被执行，但是整个代码有**解析**的环节，解析的时候就已经把 变量 i 给提前声明了。

**总结**：

既然 JS 中存在变量提升的现象，那么，在实战开发中，为了避免出错，建议先声明一个变量，然后再使用这个变量。

### 全局作用域-函数的声明提前

**函数声明**：

使用`函数声明`的形式创建的函数`function foo(){}`，**会被声明提前**。

**也就是说，整个函数会在所有的代码执行之前就被创建完成**。所以，在代码顺序上，我们可以先调用函数，再定义函数。

代码举例：

```javascript
fn1(); // 虽然 函数 fn1 的定义是在后面，但是因为被提前声明了， 所以此处可以调用函数

function fn1() {
    console.log('我是函数 fn1');
}
```

**函数表达式**：

使用`函数表达式`创建的函数`var foo = function(){}`，**不会被声明提前**，所以不能在声明前调用。

很好理解，因为此时 foo 被声明了（这里只是变量声明），且为 undefined，并没有把 `function(){}` 赋值给 foo。

### 函数作用域的预处理

1、在函数作用域中，也有声明提前的特性：

-   函数中，使用 var 关键字声明的变量，会在函数中所有的代码执行之前被声明。

-   函数中，没有 var 声明的变量都是**全局变量**，而且并不会提前声明。

举例：

```javascript
var a = 1;

function foo() {
    console.log(a);
    a = 2; // 此处的a相当于window.a
}

foo();
console.log(a); //打印结果是2
```

上方代码中，执行 foo() 后，函数里面的打印结果是`1`。如果去掉第一行代码，执行 foo() 后，函数里面的打印结果是`Uncaught ReferenceError: a is not defined`。

2、定义形参就相当于在函数作用域中声明了变量。

```javascript
function fun6(e) {
    // 这个函数中，因为有了形参 e，此时就相当于在函数内部的第一行代码里，写了 var e;
    console.log(e);
}

fun6(); //打印结果为 undefined
fun6(123); //打印结果为123
```

注意一些重复声明时的问题

```js
var scope = "global";
function fn(){
    console.log(scope);//undefined
    var scope = "local";
    console.log(scope);//local;
}
fn();

```


### JavaScript 没有块级作用域（ES6 之前）

在其他编程语言中（如 Java、C#等），存在块级作用域，由`{}`包括起来。比如在 Java 语言中，if 语句里创建的变量，只能在 if 语句内部使用：

```java
if(true) {
    Sting str = "123";
    system.out.print(num); // 123
}
system.out.print(num); // 报错
```

但是，在 JS 中没有块级作用域（ES6 之前）。举例如下：

```javascript
if (true) {
    var num = 123;
    console.log(123); //123
}

console.log(num); //123（可以正常打印）
```

### 作用域链

引入：

-   只要是代码，就至少有一个作用域

-   写在函数内部的局部作用域

-   如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域

基于上面几条内容，我们可以得出作用域链的概念。

**作用域链**：内部函数访问外部函数的变量，采用的是链式查找的方式来决定取哪个值，这种结构称之为作用域链。查找时，采用的是**就近原则**。

代码举例：

```javascript
var num = 10;

function fn() {
    // 外部函数
    var num = 20;

    function fun() {
        // 内部函数
        console.log(num);
    }
    fun();
}
fn();
```

打印结果：20。


### 块级作用域 (ES6新增)

块级作用域可通过新增命令let和const声明，所声明的变量在指定块的作用域外无法被访问。块级作用域在如下情况被创建：

1. 在一个函数内部
2. 在一个代码块（由一对花括号包裹）内部

### 块级作用域有以下几个特点：
**声明变量不会提升到代码块顶部**

错误示范: 

```js
// ReferenceError: Cannot access 'a' before initialization
console.log(a) 
let a = 1
```

**禁止重复声明**

如果一个标识符已经在代码块内部被定义，那么在此代码块内使用同一个标识符进行 let 声明就会导致抛出错误。例如：

```js
var count = 30;
let count = 40;
// Uncaught SyntaxError: Identifier 'count' has already been declared 
```


### let var 区别

var定义的变量，没有块的概念，可以跨块访问, 不能跨函数访问。

let, const 定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问。

```js
{
    var a = 1;
    let b = 2;
    const c = 3;

    {
        console.log(a);		// 1	子作用域可以访问到父作用域的变量
        console.log(b);		// 2	子作用域可以访问到父作用域的变量
        console.log(c);		// 3	子作用域可以访问到父作用域的变量

        var aa = 11;
        let bb = 22;
        const cc = 33;
    }

    console.log(aa);	// 11	// 可以跨块访问到子 块作用域 的变量
    // console.log(bb);	// 报错	bb is not defined
    // console.log(cc);	// 报错	cc is not defined
}
```

### js 函数预编译

> 预编译简单理解就是在内存中开辟一些空间，存放一些变量与函数
> 预编译会在script代码内执行前发生了, 但是它大部分会发生在函数执行前

预编译四部曲：

1. 函数在运行的瞬间，生成一个执行期上下文 （Active Object），简称AO；

2. 分析参数
    2.1 函数接收形式参数，添加到AO的属性，并且这个时候值为undefine,例如AO.age=undefined;
    2.2 接收实参，添加到AO的属性，覆盖之前的undefined;

3. 分析变量声明，如var age;或var age=23;
    3.1 如果上一步分析参数中AO还没有age属性，则添加AO属性为undefined，即AO.age=undefined;
    3.2 如果AO上面已经有age属性了，则不作任何修改;


4. 分析函数的声明，如果有function age(){}；把函数赋给AO.age ,覆盖上一步分析的值;


```js
 function fn(a){
    console.log(a);
    var a = 123;
    console.log(a);
    
    function a(){};
    console.log(a);
    
    var b = function(){};
    console.log(b);
    
    function d(){};
 }
 
 //调用函数
 fn(1);
```

创建AO对象

```js
AO{
    //空对象    
}
```

找形参和变量声明

```js
AO{
    a : undefined,
    b : undefined
}
```

只将实参赋值给形参

```js
AO{
    a : 1,
    b : undefined
}
```

找函数声明, 覆盖

```js
AO{
    a : function a(){},
    b : undefined,
    d : function d(){}
}
```
预编译环节就此结束，此时的AO对象已经更新为：

```js
AO{
    a : function a(){},
    b : undefined,
    d : function d(){}
}
```
函数开始逐行顺序执行：
```js
 function fn(a){
    console.log(a);// 输出functiona(){}
    var a = 123;//执行到这里重新对a赋，AO对象再一次更新
    console.log(a);// 输出123
    
    function a(){};//预编译环节已经进行了变量提升，故执行时不在看这行代码
    console.log(a);// 输出123
    
    var b = function(){};//这个是函数表达式不是函数声明，故不能提升，会对AO中的b重新赋值
    console.log(b);//输出function(){}
    
    function d(){};
 }
```
至此，函数执行完毕，销毁AO对象。

### 一个有意思的案例

```js
function foo() {
    var a = b = 100; // 连续赋值
}

foo();

console.log(window.b); // 在全局范围内访问 b
console.log(b); // 在全局范围内访问 b，但是前面没有加 window 这个关键字

console.log(window.a); // 在全局范围内访问 a
console.log(a); // 在全局范围内访问 a，但是前面没有加 window 这个关键字
```

结果: 

```js
100

100

undefined

（会报错，提示 Uncaught ReferenceError: a is not defined）
```

**解释**：

当执行了`foo()`函数之后， `var a = b = 100` 这行**连续赋值**的代码等价于 `var a = (b = 100)`，其执行顺序是：

（1）先把 100 赋值给 b；

（2）再声明变量 a；

（3）再把 b 的值赋值给 a。

我们可以看到，b 是未经声明的变量就被赋值了，此时，根据规律1，这个 b 是属于 `window.b`；而 a 的作用域仅限于 foo() 函数内部，不属于 window。所以也就有了这样的打印结果。

### 推荐

[JavaScript预编译原理分析](https://blog.csdn.net/q1056843325/article/details/52951114)

## Node 节点

### 1. 先解释清楚节点与元素

**节点**（Node）：构成 `HTML `网页的最基本单元。网页中的每一个部分都可以称为是一个节点，比如：`html`标签、属性、文本、注释、整个文档等都是一个节点。

虽然都是节点，但是实际上他们的具体类型是不同的。常见节点分为四类：

- 文档节点（文档）：整个 `HTML` 文档。整个 `HTML` 文档就是一个文档节点。

- 元素节点（标签）：`HTML`标签。

- 属性节点（属性）：元素的属性。

- 文本节点（文本）：`HTML`标签中的文本内容（包括标签之间的空格、换行）。

节点的类型不同，属性和方法也都不尽相同。所有的节点都是`Object`。

**总的来说:** 

**元素（element）**：页面中所有的**标签,每个`html`标签都是一个元素**

**节点（node）**：页面中所有的内容，包括标签、属性（标签的属性）、文本(文字,换行,空格,回车)) **即使元素也是节点**

**nodeType**:节点的类型

- **nodeType == 1  表示的是元素节点**（标签） 。记住：在这里，元素就是标签。

- nodeType == 2  表示是属性节点。

- nodeType == 3  是文本节点。
![在这里插入图片描述](https://img-blog.csdnimg.cn/ad987c77522c40719c1c75ef50392bbf.png)


---
### 2. 什么是`DOM`

**`DOM`**：Document Object Model，文档对象模型。`DOM` 为文档提供了结构化表示，并定义了如何通过脚本来访问文档结构。目的其实就是为了能让js操作html元素而制定的一个规范。

而 `DOM` 就是由节点组成的。

**解析过程**：
HTML加载完毕，渲染引擎会在内存中把HTML文档，生成一个DOM树，getElementById是获取内中DOM上的元素节点。然后操作的时候修改的是该元素的**属性**。


---

### 3. 获取节点
节点的访问关系，是以**属性**的方式存在的。

#### 获取父节点

调用者就是节点。一个节点只有一个父节点，调用方式就是

```js
	node.parentNode
```

#### 获取兄弟节点
| 方法                   | 说明               |
| ---------------------- | ------------------ |
| nextElementSibling     | 获取下一个元素节点 |
| previousElementSibling | 获取上一个元素节点 |

> 获得任意一个兄弟节点：
> **节点自己.parentNode.children[index];**  

####  获取单个的子节点
| 方法              | 说明                   |
| ----------------- | ---------------------- |
| firstElementChild | 获取第一个子元素节点   |
| lastElementChild  | 获取最后一个子元素节点 |


#### 获取所有的子节点

| 方法       | 说明                                                       |
| ---------- | ---------------------------------------------------------- |
| childNodes | 指定元素的子节点的集合（包括元素节点、所有属性、文本节点） |
| children   | 子元素节点的集合, 只返回HTML节点，甚至不返回文本节点。     |


### 4. 节点的操作

#### 创建节点

```javascript
	新的标签(元素节点) = document.createElement("标签名");
```

#### 插入节点

> 父节点的最后插入一个新的子节点。
> 但是需要注意: 一个已经存在的节点插入另一个已经存在的节点, 被插入的原节点的位置会消失

```javascript
	父节点.appendChild(新的子节点);
```

> 在参考节点前插入一个新的节点。
> 如果参考节点为null，那么他将在父节点里面的最后插入一个子节点。

```javascript
	父节点.insertBefore(新的子节点,作为参考的子节点)
```

#### 删除节点
```javascript
	父节点.removeChild(子节点);
```

#### 克隆节点


```javascript
	要复制的节点.cloneNode();       //括号里不带参数和带参数false，效果是一样的。
	要复制的节点.cloneNode(true);
```

- 不带参数/带参数false：只复制节点本身，不复制子节点。

- 带参数true：既复制节点本身，也复制其所有的子节点。


#### 设置节点的属性值

```javascript
	元素节点.setAttribute("属性名", "新的属性值");
```

#### 删除节点的属性

```javascript
	元素节点.removeAttribute(属性名);
```


### 5. 获取 html 文档的方法

获取title、body、head、html标签的方法如下：

- `document.title` 文档标题；

- `document.head`  文档的头标签

- `document.body`  文档的body标签；

- `document.documentElement`  文档的html标签（这个很重要）。

`document.documentElement`表示文档的html标签。也就是说，基本结构当中的 `html 标签`而是通过`document.documentElement`访问的，并不是通过 document.html 去访问的。

## Web 存储 应用缓存

### H5 中有两种存储的方式

1、**`window.sessionStorage` 会话存储：**

- 保存在内存中。

- **生命周期**为关闭浏览器窗口。也就是说，当窗口关闭时数据销毁。

- 在同一个窗口下数据可以共享。


2、**`window.localStorage` 本地存储**：

- 有可能保存在浏览器内存里，有可能在硬盘里。

- 永久生效，除非手动删除（比如清理垃圾的时候）。

- 可以多窗口共享。

### 常见 API 
设置存储内容：

```javascript
	setItem(key, value);
```

读取存储内容：

```javascript
	getItem(key);
```

根据键，删除存储内容：

```javascript
	removeItem(key);
```


清空所有存储内容：

```javascript
	clear();
```

###  案例：记住用户名和密码

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
<!DOCTYPE html>
<html>

<head lang="en">
  <meta charset="UTF-8">
  <title></title>
</head>

<body>
  <label for="">
    用户名：<input type="text" class="userName" />
  </label>
  <br /><br />
  <label for="">
    密 码：<input type="text" class="pwd" />
  </label>
  <br /><br />
  <label for="">
    <input type="checkbox" class="check" id="" />记住密码
  </label>
  <br /><br />
  <button>登录</button>

  <script>
    var userName = document.querySelector('.userName');
    var pwd = document.querySelector('.pwd');
    var chk = document.querySelector('.check');
    var btn = document.querySelector('button');

    //        当点击登录的时候 如果勾选“记住密码”，就存储密码；否则就清除密码
    btn.onclick = function () {
      if (chk.checked) {
        //                记住数据
        window.localStorage.setItem('userName', userName.value);
        window.localStorage.setItem('pwd', pwd.value);
      } else {
        //                清除数据
        window.localStorage.removeItem('userName');
        window.localStorage.removeItem('pwd');
      }
    }
    //        下次登录时，如果记录的有数据，就直接填充
    window.onload = function () {
      userName.value = window.localStorage.getItem('userName');
      pwd.value = window.localStorage.getItem('pwd');

    }
  </script>
</body>

</html>
</body>
</html>
```

### 应用缓存

HTML5中我们可以轻松的构建一个离线（无网络状态）应用，只需要创建一个 `cache manifest` 缓存清单文件。


### 优势

1、可配置需要缓存的资源；

2、网络无连接应用仍可用；

3、本地读取缓存资源，提升访问速度，增强用户体验；

4、减少请求，缓解服务器负担。

### `cache manifest` 缓存清单文件



缓存清单文件中列出了浏览器应缓存，以供离线访问的资源。**推荐使用 `.appcache`作为后缀名，另外还要添加MIME类型。**

**缓存清单文件里的内容怎样写：**

（1）**顶行写CACHE MANIFEST。**

（2）**CACHE**: 换行 指定我们需要缓存的静态资源，如.css、image、js等。

（3）**NETWORK**: 换行 指定需要在线访问的资源，可使用通配符（也就是：不需要缓存的、必须在网络下面才能访问的资源）。

（4）**FALLBACK**: 换行 当被缓存的文件找不到时的备用资源（当访问不到某个资源时，自动由另外一个资源替换）。

```appcache
CACHE MANIFEST
CACHE:
#要缓存的文件
./img/1.jpg
./img/2.jpg
./img/3.jpg
NETWORK:
#指定必须联网才能访问的文件
./js/1.js
./js/2.js
./js/3.js
FALLBACK:
./css/1.css ./css a.css
```


 > **#当前页面无法访问是回退的页面**
 > FALLBACK:
 > 404.html

### 使用

在需要应用缓存在页面的根元素(html)里，添加属性manifest = "demo.appcache"。路径要保证正确。
```html
<html manifest="01.appcache">
```

## 新增全屏显示
> 》 HTML5规范允许用户自定义网页上**任一元素**全屏显示。

### 开启/关闭全屏显示

方法如下：（注意 screen 是小写）

```javascript
	requestFullscreen()   //让元素开启全屏显示

	cancleFullscreen()    //让元素关闭全屏显示
```

### 检测当前是否处于全屏状态

方法如下：

```js
	document.fullScreen
```


### 全屏的伪类

- :full-screen .box {}

- :-webkit-full-screen {}

- :moz-full-screen {}

比如说，当元素处于全屏状态时，改变它的样式。这时就可以用到伪类。
```js
<script>
    var box = document.querySelector('.box');
    // box.requestFullscreen();   
    //直接这样写是没有效果的。浏览器的机制，必须要点一下才可以实现全屏功能。
    document.querySelector('.box').onclick = function () {
        // 开启全屏显示的兼容写法
        if (box.requestFullscreen) {  
        //如果支持全屏，那就让元素全屏
            box.requestFullscreen();
        } else if (box.webkitRequestFullScreen) {
            box.webkitRequestFullScreen();
        } else if (box.mozRequestFullScreen) {
            box.mozRequestFullScreen();
        }

    }
</script>
```

## 音频视频

### 音频

```html
<!--推荐的兼容写法：-->
<audio controls loop>
    <source src="music/yinyue.mp3"/>
    <source src="music/yinyue.ogg"/>
    <source src="music/yinyue.wav"/>
    抱歉，你的浏览器暂不支持此音频格式
</audio>
```
### 视频

```html
    <video controls autoplay>
        <source src="video/movie.mp4"/>
        <source src="video/movie.ogg"/>
        <source src="video/movie.webm"/>
        抱歉，不支持此视频
    </video>
```

##  leetcode

### 1. 字典中最长的单词 (Set, String sort)

```js
/**
 * # 字典中最长的单词 (2022.3.17)
 给出一个字符串数组 words 组成的一本英语词典。返回 words 中最长的一个单词
 该单词是由 words 词典中其他单词添加一个字母组成
 若其中有多个可行的答案，则返回答案中字典序最小的单词
 若无答案，则返回空字符串。
 */

let array = ["wo","wor","worl","world"]
let longest_word = function (words) {
  // 讲数组的所有元素存放到 set 中 （达到去重的目的）
  let set = new Set();
  words.forEach(function (item) {
    set.add(item)
  })
  // 进行排序
  words.sort((a, b) => {
    return a.length === b.length ? a.localeCompare(b) : b.length - a.length
  })
  // 判断是否存在字串
  for (let i = 0; i < words.length; i++) {
    let flag = true;
    for (let j = 1;words[i].length; j++) {
      console.log(set.has(words[i].substring(0, j)))
      if (!set.has(words[i].substring(0, j))) {
        flag = false;
        break;
      }
    }
    console.log("flag" + flag)
    if (flag) {
      return words[i]
    }
  }
  return ""
}
longest_word(array);
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8ab27fd07f0b421687cdff6921c123c5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  2. 替换空格 （String split join）

```js
/**
 * # 实现一个函数，把字符串 s 中的每个空格替换成"%20"。
 */
let replaceSpace = function(s) {
  s=s.split(' ').join('%20');
  return s
};
```

###  3. 逆序数

```js
/**
 * 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。
 * 输入一个数组，求出这个数组中的逆序对的总数。
 * @type {number[]}
 */

// 暴力破解法（时间不允许）
let reversePairs = function(nums) {
  let number = 0;
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] > nums[j]) {
        number++;
        console.log(`${i} + ${j}`)
      }
    }
  }
  return number;
};
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8eeeb8bd8e78407984159e60d4b8c793.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


```js
// 归并排序（正确解法）

let reversePairs = function(nums) {
  return findInversePairNum(nums, 0, nums.length - 1);
};

function findInversePairNum(arr, start, end) {
  if (start >= end) return 0;

  const copy = new Array(end - start + 1);
  const length = Math.floor((end - start) / 2); // 左数组长度
  const leftNum = findInversePairNum(arr, start, start + length);
  const rightNum = findInversePairNum(arr, start + length + 1, end);

  let i = start + length;
  let j = end;
  let copyIndex = end - start;
  let num = 0;
  while (i >= start && j >= start + length + 1) {
    if (arr[i] > arr[j]) {
      num += j - start - length;
      copy[copyIndex--] = arr[i--];
    } else {
      copy[copyIndex--] = arr[j--];
    }
  }

  while (i >= start) {
    copy[copyIndex--] = arr[i--];
  }

  while (j >= start + length + 1) {
    copy[copyIndex--] = arr[j--];
  }

  for (let k = start; k <= end; ++k) {
    arr[k] = copy[k - start];
  }

  return num + leftNum + rightNum;
}

```

###  4. 0～n-1中缺失的数字

```js
/**
    # 0～n-1中缺失的数字
    一个长度为n-1的递增排序数组中的所有数字都是唯一的
    并且每个数字都在范围0～n-1之内
    在范围0～n-1内的n个数字中有且只有一个数字不在该数组中
    请找出这个数字。
 */
var missingNumber = function(nums) {
    let l = 0;
    let r = nums.length - 1;
    while (l <= r) {
        let m = Math.floor((l + r) / 2);
        if (nums[m] === m) {
            l = m + 1;
        } else {
            r = m - 1;
        }
    }
    return l;
};
```

### [682. 棒球比赛](https://leetcode-cn.com/problems/baseball-game/)

```js
/**
你现在是一场采用特殊赛制棒球比赛的记录员。这场比赛由若干回合组成，过去几回合的得分可能会影响以后几回合的得分。

比赛开始时，记录是空白的。你会得到一个记录操作的字符串列表 ops，其中 ops[i] 是你需要记录的第 i 项操作，ops 遵循下述规则：

整数 x - 表示本回合新获得分数 x
"+" - 表示本回合新获得的得分是前两次得分的总和。题目数据保证记录此操作时前面总是存在两个有效的分数。
"D" - 表示本回合新获得的得分是前一次得分的两倍。题目数据保证记录此操作时前面总是存在一个有效的分数。
"C" - 表示前一次得分无效，将其从记录中移除。题目数据保证记录此操作时前面总是存在一个有效的分数。
请你返回记录中所有得分的总和。
 */
var calPoints = function(ops) {
    let n = ops.length
  let arr = []
  for (let i = 0; i < n; i++) {
    let item = ops[i]
    switch (item) {
      case "C": {
        arr.pop()
        break
      }
      case "D": {
        arr.push(arr[arr.length - 1] * 2)
        break
      }
      case "+": {
        arr.push(arr[arr.length - 1] + arr[arr.length - 2])
        break
      }
      default: {
        arr.push(item * 1)
      }
    }
  }
  return arr.reduce((l, i) => l + i, 0)
};
```



## 面试题

### ['1', '2', '3'].map(parseInt)的结果是什么？

  看到这个题下意识的觉得答案就是[1, 2, 3]


  但实际上，答案是[1, NaN, NaN]。

```js
/**
 * parseInt(string，radix)
 * */

console.log(parseInt('10', 0)) // 10
console.log(parseInt('10', 1)) // NaN
console.log(parseInt('10', 37)) // NaN
console.log(parseInt('10', 16)) // 16

// string：要被解析的值。
//    如果参数不是一个字符串，则将其转换为字符串(toString)。字符串开头的空白符将会被忽略。
// radix：可选。
//    从 2 到 36，表示被解析的值的进制。例如说指定 10 就等于指定十进位。

// parseInt(string, radix)将一个字符串string转换为radix进制的整数， radix为介于2-36之间的数。
// 返回解析后的整数值。
// 如果被解析参数的第一个字符无法被转化成数值类型，则返回NaN。

// 到这为止，我们对parseInt()函数有了一个基础的了解，
// 根据上面的描述，也就是说我们为parseInt()的第二个参数传递一个非2-36之间的数，返回结果是NaN，我们来测试一下：

// 非2-36之间的数 是不合法的, 返回 NaN

// 如果 radix 是 undefined、0或未指定的，JavaScript会假定以下情况：

// 1. 如果输入的 string以 "0x" 或 "0x"（一个0，后面是小写或大写的X）开头，那么radix被假定为16，字符串的其余部分被当做十六进制数去解析。
// 2. 如果输入的 string 以 "0"（0）开头， radix 被假定为8（八进制）或10（十进制）。具体选择哪一个radix取决于实现。
//      ECMAScript 5 澄清了应该使用 10 (十进制)，但不是所有的浏览器都支持。因此，在使用parseInt时，一定要指定一个 radix。
// 3. 如果输入的 string 以任何其他值开头， radix 是 10 (十进制)。

// 这就解释了我们的parseInt(10, 0)的结果是10了。
```
```js
/**
 * Array.prototype.map(callback, )
 * */

// 现在我们来了解一下map方法的作用，该方法接受两个参数，
// 第一个是一个回调函数，数组中的每一项都会执行该函数
//    这个回调函数接受三个参数，第一个是正在处理的元素，第二个是正在处理的索引，第三个是当前数组；
// 第二个参数是调用回调函数的this。(当前元素属于的数组对象)

function returnResult(item, index, arr) {
  console.log(item + ' 是第 ' + index + ' 位元素')
  if (index === arr.length - 1) {
    console.log('修改前的数组 ' + arr)
  }
  return item + index
}
let result = [1, 2, 3].map(returnResult)
console.log('修改后的数组 ' + result)

// 1 是第 0 位元素
// 2 是第 1 位元素
// 3 是第 2 位元素
// [ 1, 2, 3 ]
// [ 1, 3, 5 ]
```
```js
/**
 * 回到问题: ['1', '2', '3'].map(parseInt)
 * */
// parseInt('1', 0)，直接按照10进制解析，结果为1；
// parseInt('2', 1)，传入了非2~36的值，结果为NaN；
// parseInt('3', 2)，按照2进制进行解析，2进制可以解析的数字只有1和0，所以返回NaN。

console.log(['10','10','10','10','10'].map(parseInt))

// [ 10, NaN, 2, 3, 4 ]

// 相当于给 parseInt 传入两个参数, 第一个是 数组元素, 一个是索引
// 但是 parseInt 按传来的 字符串 与 进制 解释了
```
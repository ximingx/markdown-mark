

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

字符串可以看成是字符组成的数组, 拥有属性 length ------> 字符串的长度,可以通过for循环进行遍历

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

## 模板字符串

ES6新增的创建字符串的方式，使用反引号定义

```javascript
let name = `zhangsan`;

```

### 模板字符串中可以解析变量

```javascript
let name = '张三'; let sayHello = `hello,my name is ${name}`; // hello, my name is zhangsan
```

### 模板字符串中可以换行

```javascript
 let result = { 
     name: 'zhangsan', 
     age: 20,
     sex: '男' 
 } 
 let html = ` <div>
     <span>${result.name}</span>
     <span>${result.age}</span>
     <span>${result.sex}</span>
 </div> `;

```

### 在模板字符串中可以调用函数

```javascript
const sayHello = function () {     return '哈哈哈哈 追不到我吧 我就是这么强大'; };  let greet = `${sayHello()} 哈哈哈哈`; console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈
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


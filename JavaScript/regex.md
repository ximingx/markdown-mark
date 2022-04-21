[TOC]

# regex

**正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象。**

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。

## 正则表达式基础使用

### 1. 正则表达式的创建

在 JavaScript 中，可以通过两种方式创建一个正则表达式。

方式一：通过调用RegExp对象的构造函数创建 

```js
var regexp = new RegExp(/123/);
console.log(regexp);
```

方式二：利用字面量创建 正则表达式

```js
 var rg = /123/;
```

### 2. 测试正则表达式

test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串。

```js
var rg = /123/;
console.log(rg.test(123)); // 匹配字符中是否出现123  出现结果为true
console.log(rg.test('abc')); // 匹配字符中是否出现123 未出现结果为false
```

## 正则表达式字符匹配

**正则表达式是匹配模式，要么匹配字符，要么匹配位置。**

### 1 两种模糊匹配

如果正则只有精确匹配是没多大意义的，比如 `/hello/`，也只能匹配字符串中的 "hello" 这个子串。

```js
var regex = /hello/;

console.log( regex.test("hello") );

// => true
```

正则表达式之所以强大，是因为其能实现模糊匹配。

#### 1.1 横向模糊匹配

**横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。**

其实现的方式是使用量词。譬如 `{m,n}`，表示连续出现最少 m 次，最多 n 次。

比如/ab{2,5}c/表示匹配这样一个字符串：第一个字符是“a”，接下来是2到5个字符“b”，最后是字符“c”。测试如下：

```js
var regex = /ab{2,5}c/g;

var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc";

console.log( string.match(regex) );

// => ["abbc", "abbbc", "abbbbc", "abbbbbc"]
```

注意：**案例中用的正则是/ab{2,5}c/g，后面多了g，它是正则的一个修饰符。表示全局匹配**，即在目标字符串中按顺序找到满足匹配模式的所有子串，强调的是“所有”，而不只是“第一个”。g是单词global的首字母。

#### 1.2 纵向模糊匹配

纵向模糊指的是，一个正则匹配的字符串，**具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。**

其实现的方式是使用字符组。譬如`[abc]`，表示该字符是可以字符“a”、“b”、“c”中的任何一个。

比如/a[123]b/可以匹配如下三种字符串："a1b"、"a2b"、"a3b"。测试如下：

```js
var regex = /a[123]b/g;

var string = "a0b a1b a2b a3b a4b";

console.log( string.match(regex) );

// => ["a1b", "a2b", "a3b"]
```

以上就是本章讲的主体内容，只要掌握横向和纵向模糊匹配，就能解决很大部分正则匹配问题。

### 2. 字符组
**需要强调的是，虽叫字符组（字符类），但只是其中一个字符。**例如[abc]，表示匹配一个字符，它可以是“a”、“b”、“c”之一。

#### 2.1 范围表示法

**如果字符组里的字符特别多的话，怎么办？可以使用范围表示法。**

比如[123456abcdefGHIJKLM]，可以写成[1-6a-fG-M]。用连字符-来省略和简写。

因为连字符有特殊用途，那么要匹配“a”、“-”、“z”这三者中任意一个字符，该怎么做呢？

不能写成[a-z]，因为其表示小写字符中的任何一个字符。

可以写成如下的方式：[-az]或[az-]或[a\-z]。即要么放在开头，要么放在结尾，要么转义。总之不会让引擎认为是范围表示法就行了。

#### 2.2 排除字符组

纵向模糊匹配，还有一种情形就是，某位字符可以是任何东西，但就不能是"a"、"b"、"c"。

**此时就是排除字符组（反义字符组）的概念。**例如[ ^abc ]，表示是一个除"a"、"b"、"c"之外的任意一个字符。字符组的第一位放^（脱字符），表示求反的概念。

当然，也有相应的范围表示法。

#### 2.3 常见的简写形式

**预定义类指的是某些常见模式的简写方式.**

有了字符组的概念后，一些常见的符号我们也就理解了。因为它们都是系统自带的简写形式。

`\d`就是[0-9]。表示是一位数字。记忆方式：其英文是digit（数字）。

`\D`就是[ ^0-9]。表示除数字外的任意字符。

`\w`就是[0-9a-zA-Z_]。表示数字、大小写字母和下划线。记忆方式：w是word的简写，也称单词字符。

`\W`是[ ^0-9a-zA-Z_]。非单词字符。

`\s`是[ \t\v\n\r\f]。表示空白符，包括空格、水平制表符、垂直制表符、换行符、回车符、换页符。记忆方式：s是space character的首字母。

`\S`是[ ^ \t\v\n\r\f]。 非空白符。

.就是[ ^\n\r\u2028\u2029]。通配符，表示几乎任意字符。换行符、回车符、行分隔符和段分隔符除外。记忆方式：想想省略号...中的每个点，都可以理解成占位符，表示任何类似的东西。

**如果要匹配任意字符怎么办？可以使用[\d\D]、[\w\W]、[\s\S]和[^]中任何的一个。**

```js
var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
console.log(rg.test('andy'));//true
console.log(rg.test('baby'));//true
console.log(rg.test('color'));//true
console.log(rg.test('red'));//false
var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
console.log(rg1.test('aa'));//false
console.log(rg1.test('a'));//true
console.log(rg1.test('b'));//true
console.log(rg1.test('c'));//true
console.log(rg1.test('abc'));//true
----------------------------------------------------------------------------------
var reg = /^[a-z]$/ //26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
console.log(reg.test('a'));//true
console.log(reg.test('z'));//true
console.log(reg.test('A'));//false
-----------------------------------------------------------------------------------
//字符组合
var reg1 = /^[a-zA-Z0-9]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
------------------------------------------------------------------------------------
//取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。
var reg2 = /^[^a-zA-Z0-9]$/;
console.log(reg2.test('a'));//false
console.log(reg2.test('B'));//false
console.log(reg2.test(8));//false
console.log(reg2.test('!'));//true
```

### 3. 量词
量词也称重复。掌握{m,n}的准确含义后，只需要记住一些简写形式。

#### 3.1 简写形式

| 量词      | 说明                               |
| --------- | ---------------------------------- |
| *         | 重复0次或更多次                    |
| +         | 重复1次或更多次                    |
| ?         | 重复0次或1次                       |
| {n}       | 重复n次                            |
| {n,}      | 量词符用来设定某个模式出现的次数。 |
| 量词{n,m} | 说明重复n到m次                     |

#### 3.2 贪婪匹配和惰性匹配

看如下的例子：

```js
var regex = /\d{2,5}/g;

var string = "123 1234 12345 123456";

console.log( string.match(regex) );

// => ["123", "1234", "12345", "12345"]
```

其中正则``/\d{2,5}/``，表示数字连续出现2到5次。会匹配2位、3位、4位、5位连续数字。

但是其是贪婪的，它会尽可能多的匹配。你能给我6个，我就要5个。你能给我3个，我就3要个。反正只要在能力范围内，越多越好。

我们知道有时贪婪不是一件好事。而惰性匹配，就是尽可能少的匹配：

```js
var regex = /\d{2,5}?/g;

var string = "123 1234 12345 123456";

console.log( string.match(regex) );

// => ["12", "12", "34", "12", "34", "12", "34", "56"]
```

其中/\d{2,5}?/表示，虽然2到5次都行，当2个就够的时候，就不在往下尝试了。

通过在量词后面加个问号就能实现惰性匹配，因此所有惰性匹配情形如下：

```js
{m,n}?
{m,}?
??
+?
*?
```

对惰性匹配的记忆方式是：量词后面加个问号，问一问你知足了吗，你很贪婪吗？

### 4. 多选分支
一个模式可以实现横向和纵向模糊匹配。而多选分支可以支持多个子模式任选其一。

具体形式如下：(p1|p2|p3)，其中p1、p2和p3是子模式，用|（管道符）分隔，表示其中任何之一。

例如要匹配"good"和"nice"可以使用/good|nice/。测试如下：

```js
var regex = /good|nice/g;

var string = "good idea, nice try.";

console.log( string.match(regex) );

// => ["good", "nice"]
```

但有个事实我们应该注意，比如我用/good|goodbye/，去匹配"goodbye"字符串时，结果是"good"：

```js
var regex = /good|goodbye/g;

var string = "goodbye";

console.log( string.match(regex) );

// => ["good"]
```

而把正则改成/goodbye|good/，结果是：

```js
var regex = /goodbye|good/g;

var string = "goodbye";

console.log( string.match(regex) );

// => ["goodbye"]
```

也就是说，分支结构也是惰性的，即当前面的匹配上了，后面的就不再尝试了。

### 5.案例分析
匹配字符，无非就是字符组、量词和分支结构的组合使用罢了。

#### 5.1 匹配16进制颜色值

要求匹配：

```js
#ffbbad

#Fc01DF

#FFF

#ffE
```

分析：

- 表示一个16进制字符，可以用字符组[0-9a-fA-F]。
- 其中字符可以出现3或6次，需要是用量词和分支结构。
- 使用分支结构时，需要注意顺序。

正则如下：

```js
var regex = /#([0-9a-fA-F]{6}|[0-9a-fA-F]{3})/g;

var string = "#ffbbad #Fc01DF #FFF #ffE";

console.log( string.match(regex) );

// => ["#ffbbad", "#Fc01DF", "#FFF", "#ffE"]
```

#### 5.2 匹配时间

以24小时制为例。

要求匹配：

```js
23:59

02:07
```

分析：

- 共4位数字，第一位数字可以为[0-2]。
- 当第1位为2时，第2位可以为[0-3]，其他情况时，第2位为[0-9]。
- 第3位数字为[0-5]，第4位为[0-9]

正则如下：

```js
var regex = /^([01][0-9]|[2][0-3]):[0-5][0-9]$/;

console.log( regex.test("23:59") );

console.log( regex.test("02:07") );

// => true

// => true
```

如果也要求匹配7:9，也就是说时分前面的0可以省略。

此时正则变成：

```js
var regex = /^(0?[0-9]|1[0-9]|[2][0-3]):(0?[0-9]|[1-5][0-9])$/;

console.log( regex.test("23:59") );

console.log( regex.test("02:07") );

console.log( regex.test("7:9") );

// => true

// => true

// => true
```

5.3 匹配日期

比如yyyy-mm-dd格式为例。

要求匹配：

```js
2017-06-10
```

分析：

- 年，四位数字即可，可用[0-9]{4}。
- 月，共12个月，分两种情况01、02、……、09和10、11、12，可用(0[1-9]|1[0-2])。
- 日，最大31天，可用(0[1-9]|[12][0-9]|3[01])。

正则如下：

```js
var regex = /^[0-9]{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$/;

console.log( regex.test("2017-06-10") );

// => true
```

5.4 window操作系统文件路径

要求匹配：

```js
F:\study\javascript\regex\regular expression.pdf

F:\study\javascript\regex\

F:\study\javascript

F:\
```

分析：

- 整体模式是: 盘符:\文件夹\文件夹\文件夹\
- 其中匹配F:\，需要使用[a-zA-Z]:\\，其中盘符不区分大小写，注意\字符需要转义。
- 文件名或者文件夹名，不能包含一些特殊字符，此时我们需要排除字符组[^\\:*<>|"?\r\n/]来表示合法字符。另外不能为空名，至少有一个字符，也就是要使用量词+。因此匹配“文件夹\”，可用[^\\:*<>|"?\r\n/]+\\。
- 另外“文件夹\”，可以出现任意次。也就是([^\\:*<>|"?\r\n/]+\\)*。其中括号提供子表达式。*
- *路径的最后一部分可以是“文件夹”，没有\，因此需要添加([^\\:*<>|"?\r\n/]+)?。
- 最后拼接成了一个看起来比较复杂的正则：

```js
var regex = /^[a-zA-Z]:\\([^\\:*<>|"?\r\n/]+\\)*([^\\:*<>|"?\r\n/]+)?$/;

console.log( regex.test("F:\\study\\javascript\\regex\\regular expression.pdf") );

console.log( regex.test("F:\\study\\javascript\\regex\\") );

console.log( regex.test("F:\\study\\javascript") );

console.log( regex.test("F:\\") );

// => true

// => true

// => true

// => true
```

其中，JS中字符串表示\时，也要转义。

## 正则表达式位置匹配

在ES5中，共有6个锚字符：

```js
^ $ \b \B (?=p) (?!p)
```

### 1. ^和$

**^（脱字符）匹配开头，在多行匹配中匹配行开头。**

**$（美元符号）匹配结尾，在多行匹配中匹配行结尾。**

```js
var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型
// /abc/ 只要包含有abc这个字符串返回的都是true
console.log(rg.test('abc'));
console.log(rg.test('abcd'));
console.log(rg.test('aabcd'));
console.log('---------------------------');
var reg = /^abc/;
console.log(reg.test('abc')); // true
console.log(reg.test('abcd')); // true
console.log(reg.test('aabcd')); // false
console.log('---------------------------');
var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
console.log(reg1.test('abc')); // true
console.log(reg1.test('abcd')); // false
console.log(reg1.test('aabcd')); // false
console.log(reg1.test('abcabc')); // false
```

比如我们把字符串的开头和结尾用"#"替换（位置可以替换成字符的！）：

```js
var result = "hello".replace(/^|$/g, '#');

console.log(result);

// => "#hello#"
```

多行匹配模式时，二者是行的概念，这个需要我们的注意：

```js
var result = "I\nlove\njavascript".replace(/^|$/gm, '#');

console.log(result);

/*
#I#
#love#
#javascript#
*/
```

###  2. \b和\B

\b是单词边界，具体就是\w和\W之间的位置，也包括\w和^之间的位置，也包括\w和$之间的位置。

比如一个文件名是"[JS] Lesson_01.mp4"中的\b，如下：

```js
var result = "[JS] Lesson_01.mp4".replace(/\b/g, '#');

console.log(result);

// => "[#JS#] #Lesson_01#.#mp4#"
```

为什么是这样呢？这需要仔细看看。

首先，我们知道，\w 是字符组[0-9a-zA-Z_]的简写形式，即\w是字母数字或者下划线的中任何一个字符。而\W是排除字符组[^0-9a-zA-Z_]的简写形式，即\W是\w以外的任何一个字符。

此时我们可以看看"[#JS#] #Lesson_01#.#mp4#"中的每一个"#"，是怎么来的。

- 第一个"#"，两边是"["与"J"，是\W和\w之间的位置。
- 第二个"#"，两边是"S"与"]"，也就是\w和\W之间的位置。
- 第三个"#"，两边是空格与"L"，也就是\W和\w之间的位置。
- 第四个"#"，两边是"1"与"."，也就是\w和\W之间的位置。
- 第五个"#"，两边是"."与"m"，也就是\W和\w之间的位置。
- 第六个"#"，其对应的位置是结尾，但其前面的字符"4"是\w，即\w和$之间的位置。

\B就是\b的反面的意思，非单词边界。例如在字符串中所有位置中，扣掉\b，剩下的都是\B的。

具体说来就是\w与\w、\W与\W、^与\W，\W与$之间的位置。

比如上面的例子，把所有\B替换成"#"：

```js
var result = "[JS] Lesson_01.mp4".replace(/\B/g, '#');

console.log(result);

// => "#[J#S]# L#e#s#s#o#n#_#0#1.m#p#4"
```

### 3. (?=p)和(?!p)

(?=p)，其中p是一个子模式，即p前面的位置。

比如(?=l)，表示'l'字符前面的位置，例如：

```js
var result = "hello".replace(/(?=l)/g, '#');

console.log(result);

// => "he#l#lo"
```

而(?!p)就是(?=p)的反面意思，比如：

```js
var result = "hello".replace(/(?!l)/g, '#');

console.log(result);

// => "#h#ell#o#"
```

二者的学名分别是positive lookahead和negative lookahead。

中文翻译分别是正向先行断言和负向先行断言。

ES6中，还支持positive lookbehind和negative lookbehind。

具体是(?<=p)和(?<!p)。

也有书上把这四个东西，翻译成环视，即看看右边或看看左边。

但一般书上，没有很好强调这四者是个位置。

比如(?=p)，一般都理解成：要求接下来的字符与p匹配，但不能包括p的那些字符。

而在本人看来(?=p)就与^一样好理解，就是p前面的那个位置。

### 4. 位置的特性

对于位置的理解，我们可以理解成空字符""。

比如"hello"字符串等价于如下的形式：

```js
"hello" == "" + "h" + "" + "e" + "" + "l" + "" + "l" + "o" + "";

"hello" == "" + "" + "hello"
```

因此，把/^hello$/写成/^^hello$$$/，是没有任何问题的：

````js
var result = /^^hello$$$/.test("hello");

console.log(result);

// => true
````

甚至可以写成更复杂的:

```js
var result = /(?=he)^^he(?=\w)llo$\b\b$/.test("hello");

console.log(result);

// => true
```

也就是说字符之间的位置，可以写成多个。

把位置理解空字符，是对位置非常有效的理解方式。
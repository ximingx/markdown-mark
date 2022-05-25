# Mock.js

`Mock.js` 是一款模拟数据生成器，旨在帮助前端独立于后端进行开发，帮助编写单元测试。提供了以下模拟功能：

- 根据数据模板生成模拟数据
- 模拟 `Ajax `请求，生成并返回模拟数据
- 基于 `HTML `模板生成模拟数据

## 1. 安装使用

> 安装

```bash
# 1. npm 安装
$ yarn add mockjs
# 2. 使用CDN
<script src="https://cdn.bootcdn.net/ajax/libs/Mock.js/1.0.1-beta3/mock-min.js"></script>
# 3. 使用本地文件, 下载 Mock.js: https://github.com/nuysoft/Mock
<script src="js/mock-min.js"></script>
```

> 验证

```html
<script> 
var data = Mock.mock({
    'list|5':[
        {
            'id':1,
            'name':'测试'
        }
    ]
  })
  console.log(JSON.stringify(data,null,2 ))
</script>
```

![image-20220508083224135](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508083224135.png)

## 2. 语法规范

`Mock.js` 的语法规范包括两部分：

1. 数据模板定义（Data Temaplte Definition，`DTD`）
2. 数据占位符定义（Data Placeholder Definition，`DPD`）

### 2.1 数据模板定义 DTD

> **数据模板的属性**

**数据模板中的每个属性由 3 部分构成：属性名、生成规则、属性值：**

```js
// 属性名   name
// 生成规则 rule
// 属性值   value
'name | [rule]': value
```

- 属性名 和 生成规则 之间用 `|` 分隔。
- **生成规则 是可选的。**
- 生成规则 有 7 种格式：
  1. `'name|min-max': value`
  2. `'name|count': value`
  3. `'name|min-max.dmin-dmax': value`
  4. `'name|min-max.dcount': value`
  5. `'name|count.dmin-dmax': value`
  6. `'name|count.dcount': value`
  7. `'name|+step': value`
- **生成规则 的 含义 需要依赖 属性值 才能确定。**
- 属性值 中可以含有 `@占位符`。
- 属性值 还指定了最终值的初始值和类型。

```js
<script> 
var data = Mock.mock({
    // list是属性名, 5是生成规则, 中间用|分割, 后面的数组是属性值
    // 当然, 实际上的使用不会让我们直接写数据, 那就接着看下去吧
    'list|5':[
        {
            'id':1,
            'name':'测试'
        }
    ]
  })
  console.log(JSON.stringify(data,null,2 ))
</script>
```

>  **生成规则和示例：**

1. 属性值是字符串 **`String`**

   1. `'name|min-max': 'value'` 通过重复 `'value'` 生成一个字符串，重复次数大于等于 `min`，小于等于 `max`。
2. `'name|count': 'value'` 通过重复 `'value'` 生成一个字符串，重复次数等于 `count`。

```js
<script src="https://cdn.bootcdn.net/ajax/libs/Mock.js/1.0.1-beta3/mock-min.js"></script>
<script>
    var data = Mock.mock({
        "name|1-5": "12"
    })
    console.log(JSON.stringify(data, null, 2))
</script>
```

![image-20220508084100113](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508084100113.png)

2. 属性值是数字 **`Number`**

	1. `'name|+1': 100` 属性值自动加 1，初始值为 100

	2. `'name|1-100': 100` 生成一个大于等于 1、小于等于 100 的整数，属性值 100 只用来确定类型。

	3. `'name|1-100.1-10': 100` 生成一个浮点数，整数部分大于等于 1、小于等于 100，小数部分保留 1 到 10 位。

	4. ```js
    {
        'number1|1-100.1-10': 1,
        'number2|123.1-10': 1,
        'number3|123.3': 1,
        'number4|123.10': 1.123
       }
       // =>
       {
        "number1": 12.92,
        "number2": 123.51,
        "number3": 123.777,
        "number4": 123.1231091814
       }
   
3. 属性值是布尔型 **`Boolean`**
   1. `'name|1': value` 随机生成一个布尔值，值为 true 的概率是 1/2，值为 false 的概率是 1/2。
   2. `'name|min-max': value` 随机生成一个布尔值，值为 `value` 的概率是 `min / (min + max)`，值为 `!value` 的概率是 `max / (min + max)`。

4. 属性值是对象 **`Object`**

   1. `'name|min-max': {}` 从属性值 `{}` 中随机选取 `min` 到 `max` 个属性。
   2. `'name|count': {}` 从属性值 `{}` 中随机选取 `count` 个属性。

5. 属性值是数组 **`Array`**

   1. `'name|1': [{}, {} ...]` 从属性值 `[{}, {} ...]` 中随机选取 1 个元素，作为最终值。
   2. `'name|min-max': [{}, {} ...]` 通过重复属性值 `[{}, {} ...]` 生成一个新数组，重复次数大于等于 `min`，小于等于 `max`。
   3. `'name|count': [{}, {} ...]` 通过重复属性值 `[{}, {} ...]` 生成一个新数组，重复次数为 `count`。

6. 属性值是数组 **`Function`**

   `'name': function(){}` 执行函数 `function(){}`，取其返回值作为最终的属性值，上下文为 `'name'` 所在的对象。

```js
<script src="https://cdn.bootcdn.net/ajax/libs/Mock.js/1.0.1-beta3/mock-min.js"></script>
<script>
    var data = Mock.mock({
        'list|5': [{
            //属性值自动加1,后面1是初始值
            'id|+1': 1,
            //测试这个词语 重复随机次数：最大10次，最小重复2次
            'name|2-10': '测试',
            'phone|10': '1',
            //生成200到1000以内随机的整数
            'point|200-1000': 0
        }]
    })
    // 每一个层级比上一个多2个空格
    console.log(JSON.stringify(data, null, 2))
</script>
```

![image-20220508084410994](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508084410994.png)

### 2.2 数据占位符定义 DPD

`Mock.Random` 是一个工具类，用于生成各种随机数据。`Mock.Random` 的方法在数据模板中称为『占位符』.

占位符 只是在属性值字符串中占个位置，并不出现在最终的属性值中。占位符 的格式为：

```js
@占位符
@占位符(参数 [, 参数])
```

**注意：**

1. 用 `@` 来标识其后的字符串是 占位符。
2. 占位符 引用的是 `Mock.Random` 中的方法。
3. 通过 `Mock.Random.extend()` 来扩展自定义占位符。
4. 占位符 也可以引用 数据模板 中的属性。
5. 占位符 会优先引用 数据模板 中的属性。

```js
 {
     name: {
         first: '@FIRST',
         last: '@LAST',
         full: '@first @last'
     }
 }
 // =>
 {
     "name": {
         "first": "Charles",
         "last": "Lopez",
         "full": "Charles Lopez"
     }
 }
```

| Type | Method |
| ---- | ------ |
|基本类型|	boolean, natural, integer, float, character, string, range, date, time, datetime, now|
|图片|	image, dataImage|
|颜色|	color|
|文本|	paragraph, sentence, word, title, cparagraph, csentence, cword, ctitle|
|姓名|	first, last, name, cfirst, clast, cname|
|网站|	url, domain, email, ip, tld|
|地址|	area, region|
|编号|	guid, id|

使用时只需要把值设置成 @方法名【内置列表名】 即可，比如，生成一个随机的 Email：

```js
<script src="https://cdn.bootcdn.net/ajax/libs/Mock.js/1.0.1-beta3/mock-min.js"></script>
<script>
    var data = Mock.mock({
        'email': '@email'
    })
    console.log(JSON.stringify(data, null, 2))
</script>
```

#### 2.2.1 基本数据类型

```js
<script>
    let data = Mock.mock({
        'list|10': [{
            'id|+1': 1,
            //生成随机字符串作为名称，string是内置方法
            'name':'@string',
            //生成随机数字
            'point':'@integer',
            //随机数字
            'age':'@integer(1,100)',
            //随机字符串
            'address':'@string',
            //随机字符串
            'phone':'@string',
        }]
    })
    // 输出结果
    console.log(JSON.stringify(data, null, 2))
</script>

=> 
    
{
  "list": [
    {
      "id": 1,
      "name": "SZffs",
      "point": 4106726580063732,
      "age": 41,
      "address": "sfMw0Lk",
      "phone": ")7]FT"
    },
    {
      "id": 2,
      "name": "gZYWF",
      "point": -437170254284484,
      "age": 19,
      "address": "^6Mn9",
      "phone": "e0y!cb"
    },
    {
      "id": 3,
      "name": "Ms!k",
      "point": -1740553494581136,
      "age": 41,
      "address": "@&L#[l%",
      "phone": "A)O9#"
    },
    {
      "id": 4,
      "name": "RUUIVfn",
      "point": 5821035607208916,
      "age": 20,
      "address": "QE1U*J",
      "phone": ")JIMrw"
    },
    {
      "id": 5,
      "name": "hEK6!Z",
      "point": -7979039109736448,
      "age": 58,
      "address": "UEJDVE",
      "phone": "N7AE0Q"
    },
    {
      "id": 6,
      "name": "C8$[",
      "point": 368172333090500,
      "age": 21,
      "address": "aT64",
      "phone": "Fdk"
    },
    {
      "id": 7,
      "name": "X2(y",
      "point": 8901990522279008,
      "age": 78,
      "address": "8QSGrn",
      "phone": "8Ggs"
    },
    {
      "id": 8,
      "name": "V[Yk7UX",
      "point": -4367603139791996,
      "age": 80,
      "address": "pBJd!Z",
      "phone": "hI!EA8"
    },
    {
      "id": 9,
      "name": "P4V]f",
      "point": -8253583046137432,
      "age": 35,
      "address": "BREPHv",
      "phone": "6OlcoB"
    },
    {
      "id": 10,
      "name": "V0Zk*",
      "point": -2396294213158664,
      "age": 94,
      "address": "cL1",
      "phone": "buv"
    }
  ]
}
```

#### 2.2.2 图像方法

```js
<script>
    let  data  =  Mock.mock({
        'list|10': [{
            'id|+1': 1,
            'img':'@image'
        }]
    })
    // 输出结果
    console.log(JSON.stringify(data, null, 2))
</script>

{
  "list": [
    {
      "id": 1,
      "img": "http://dummyimage.com/120x90"
    },
    {
      "id": 2,
      "img": "http://dummyimage.com/720x300"
    },
    {
      "id": 3,
      "img": "http://dummyimage.com/720x300"
    },
    {
      "id": 4,
      "img": "http://dummyimage.com/300x600"
    },
    {
      "id": 5,
      "img": "http://dummyimage.com/88x31"
    },
    {
      "id": 6,
      "img": "http://dummyimage.com/300x250"
    },
    {
      "id": 7,
      "img": "http://dummyimage.com/720x300"
    },
    {
      "id": 8,
      "img": "http://dummyimage.com/250x250"
    },
    {
      "id": 9,
      "img": "http://dummyimage.com/125x125"
    },
    {
      "id": 10,
      "img": "http://dummyimage.com/720x300"
    }
  ]
}
```

**@image( size, background, foreground, format, text )**

|属性|值|
|---|---|
|size：|尺寸，格式为：‘宽x高’|
|background：|背景色，格式为：#FFFFFF|
|text：|图片上显示的文本|
|foreground：|广本颜色|
|format：|图片格式，可选值包括：png、gif、jpg。|

#### 2.2.3 文本方法

@title： 生成随机的英文标题
@cword(字数)：**生成随机的中文标题**

```js
<script>
    let  data  =  Mock.mock({
        'list|5': [{
            'id|+1': 1,
            //随机标题
            'title':'@title',
            //随机标题内容，字数为20
            'content':'@cword(20)'
        }]
    })
    // 输出结果
    console.log(JSON.stringify(data, null, 2))
</script>


{
  "list": [
    {
      "id": 1,
      "title": "Zoeqtihbct Kxso Fmjfio Xxcdyx Gwjrf Gdlykicbh",
      "content": "口文具治单局走感亲认心已支持先必细江县少"
    },
    {
      "id": 2,
      "title": "Qjtc Cwj Nnrsyvh Uluutvwp",
      "content": "器流专温省子反他代代等解作则切相光清那选"
    },
    {
      "id": 3,
      "title": "Bxamfvr Utpbqflzs Mftqpwx",
      "content": "维取应代科使机例位机这元至世定也工思收学"
    },
    {
      "id": 4,
      "title": "Lfzxyrf Miojg Wrcoxkex Obiq Psif Pepvnwoa",
      "content": "高区声第研属机转全制只共性造三王再老张那"
    },
    {
      "id": 5,
      "title": "Cpxotxwn Invl Erryjsq Ertdkyfmc Hbt Jmkwbnqge Ohwr",
      "content": "第战经调战华气边看行个北部革斗况习多象难"
    }
  ]
}
```

#### 2.2.4 名称方法

姓 @cfirst
名 @clast
@cname
@cname()

```js
let  data  =  Mock.mock({
        'list|5': [{
            'id|+1': 1,
            //随机标题
            'title':'@title',
            //随机标题内容，字数为20
            first: "@cfirst",
            last: "@clast",
            cname: "@cname",
        }]
    })
    // 输出结果
    console.log(JSON.stringify(data, null, 2))

{
  "list": [
    {
      "id": 1,
      "title": "Xydnd Xjdpxlkt Nfdzq Kgcp Hidktucfzd",
      "first": "卢",
      "last": "刚",
      "cname": "沈芳"
    },
    {
      "id": 2,
      "title": "Nduxdvj Djsr Qlmcmk Xececdeqk Yktnopxhi Wtetthpbi Flnvnbl",
      "first": "董",
      "last": "秀兰",
      "cname": "夏平"
    },
    {
      "id": 3,
      "title": "Hploqllr Epmre Bcp Gzxxzqirz Twhzn Vyfdpzwr Ikiimhhbwx",
      "first": "钱",
      "last": "霞",
      "cname": "于秀英"
    },
    {
      "id": 4,
      "title": "Ebyuzihsr Oogaf Emuj Dpdq",
      "first": "常",
      "last": "丽",
      "cname": "孔刚"
    },
    {
      "id": 5,
      "title": "Wpxc Atxfm Ddxjmhvjyk Ykyud Twudjkr",
      "first": "马",
      "last": "敏",
      "cname": "龚磊"
    }
  ]
}
```

#### 2.2.5 地址

生成中国大区：@region (true)
生成省份：@province(true)
生成城市：@city(true)

```js
Random.region() + Random.province() + Random.city() + Random.county()
```



## 3. Mock

> **Mock.mock( rurl?, rtype?, template|function(options) )**

根据数据模板生成模拟数据。

- **Mock.mock( template )**

  根据数据模板生成模拟数据。

- **Mock.mock( rurl, template )**

  记录数据模板。当拦截到匹配 `rurl` 的 Ajax 请求时，将根据数据模板 `template` 生成模拟数据，并作为响应数据返回。

- **Mock.mock( rurl, function(options) )**

  记录用于生成响应数据的函数。当拦截到匹配 `rurl` 的 Ajax 请求时，函数 `function(options)` 将被执行，并把执行结果作为响应数据返回。

- **Mock.mock( rurl, rtype, template )**

  记录数据模板。当拦截到匹配 `rurl` 和 `rtype` 的 Ajax 请求时，将根据数据模板 `template` 生成模拟数据，并作为响应数据返回。

- **Mock.mock( rurl, rtype, function(options) )**

  记录用于生成响应数据的函数。当拦截到匹配 `rurl` 和 `rtype` 的 Ajax 请求时，函数 `function(options)` 将被执行，并把执行结果作为响应数据返回。

**参数的含义和默认值**如下所示：

- **参数 rurl**：可选。表示需要拦截的 URL，可以是 URL 字符串或 URL 正则。例如 `/\/domain\/list\.json/`、`'/domian/list.json'`。
- **参数 rtype**：可选。表示需要拦截的 Ajax 请求类型。例如 `GET`、`POST`、`PUT`、`DELETE` 等。
- **参数 template**：可选。表示数据模板，可以是对象或字符串。例如 `{ 'data|1-10':[{}] }`、`'@EMAIL'`。
- **参数 function(options)**：可选。表示用于生成响应数据的函数。
- **参数 options**：指向本次请求的 Ajax 选项集。

## 4. 使用案例

```html
<body>
<button>aw</button>
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.27.2/axios.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/Mock.js/1.0.1-beta3/mock-min.js"></script>
<script>
    let  data  =  Mock.mock({
        'list|10': [{
            id: "@id",
            name: '@cname',
            'age|18-60': 1,
            area: '@city(true)',
        }]
    })
    Mock.mock('/api/data/index', 'get', data);
    document.querySelector("button").addEventListener('click', function () {
        axios.get('/api/data/index').then(function (res) {
            console.log(res.data);
        });
    });
</script>
</body>
```



![image-20220508095841509](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508095841509.png)

> 在 `vue` 中使用

创建 `db` 文件

```js
const Mock = require('mockjs');
const Random = Mock.Random;
let data = {
    news: [],
}
for (let i = 0; i < 5; i++) {
    data.news.push({
        id: i,
        title: Random.cword(5, 10),
        content: Random.cword(20, 50),
        time: Random.date('yyyy-MM-dd'),
    })
}
console.log(data)
Mock.mock('/api/data/index', 'get', data);
```

在 `mian.js` 引用

```js
require('@/db/db')
```

页面中的使用

```js
axios({
   url: '/api/data/index'
}).then(res => {
     console.log(res)
})
```


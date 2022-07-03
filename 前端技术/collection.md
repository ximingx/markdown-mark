# 动态背景 vanta.js

> `vanta.js` 可以为网站设置炫酷的动态背景 比如在网站登陆的首页
>
> 但是不直接支持 `vue3` , 但是呢 ,也不是不可以添加

[https://www.vantajs.com/](https://www.vantajs.com/)

## 1. 展示

![image-20220516230044977](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205162300096.png)

![image-20220516230117847](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205162301955.png)

![image-20220516230141826](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205162301924.png)

![image-20220517084319744](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205170843903.png)

![image-20220517084336053](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205170843451.png)

## 2. 使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--取消了body的边距-->
    <link href="https://cdn.bootcdn.net/ajax/libs/normalize/8.0.1/normalize.css" rel="stylesheet">
    <style>
        /*最后展示区域的大小取决于绑定元素的面积*/
        #my-background {
            overflow: hidden;
            width: 100vw;
            height: 100vh;
        }
    </style>
</head>
<body>
<div id="my-background">123</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r121/three.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/vanta/0.5.22/vanta.birds.min.js"></script>
<script>
    VANTA.BIRDS({
        el: "#my-background",
        mouseControls: true,
        touchControls: true,
        gyroControls: false,
        minHeight: 200.00,
        minWidth: 200.00,
        scale: 1.00,
        scaleMobile: 1.00,
        backgroundColor: 0x191e20,
        color1: 0x7914b1,
        color2: 0xfc1eb,
        birdSize: 2.40,
        wingSpan: 25.00,
        speedLimit: 6.00,
        separation: 56.00,
        alignment: 44.00,
        cohesion: 39.00,
        quantity: 2.00
    })
</script>
</body>
</html>
```

![image-20220517084122725](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205170841817.png)

# animate.css

一个简单动画的库

![image-20220521120230726](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205211202843.png)

## 1.使用

> 安装

```bash
yarn add animate.css
```

> 导入使用

```js
<template>
  <transition enter-active-class="animate__animated animate__bounce animate__bounce">
    <template v-if="show">
      <div class="btn">123</div>
    </template>
  </transition>
  <button @click="show = !show">button</button>
</template>

<script setup>
import {ref} from 'vue'
import 'animate.css';
let show = ref(false)
</script>

<style lang="scss">
.btn {
  padding: 5px 10px;
  background-color: turquoise;
}
</style>
```



# josn-server

可以将 `json `格式的数据返回

## 1. 举例

> db.json

```js
{
  "heroes": [
    {
      "id": 1,
      "name": "关羽",
      "gender": "男"
    },
    {
      "id": 2,
      "name": "刘备",
      "gender": "男"
    },
    {
      "id": 3,
      "name": "大乔",
      "gender": "女"
    }
  ]
}
```

> 命令行启动

```bash
$ json-server --watch db.json
```

> 请求操作

- 获取英雄列表

- - 请求路径：`http://localhost:3000/heros`
  - 请求方法：`GET`
  - 根据英雄`id`获取一个英雄

- - - 请求路径：`http://localhost:3000/heros/:id`

- - - - `:id` 需要给定一个英雄的 id

- - - 请求方法：`GET`

- 添加英雄

- - 请求路径：`http://localhost:3000/heros`

  - 请求方法：`POST`

  - 请求体：

  - ```js
    {
      name: '英雄名称',
      gender: '英雄性别'
    }
    ```

- 删除英雄

- - 请求路径：`http://localhost:3000/heros/:id`

- - - `:id` 需要给定一个英雄的 id

- - 请求方法：`DELETE`

- 编辑英雄

- - 请求路径：`http://localhost:3000/heros/:id`

- - - `:id` 需要给定一个英雄的 id

- - 请求方法：`PATCH`

  - 请求体：

  - ```js
    {
      name: '英雄名称',
      gender: '英雄性别'
    }
    ```

    


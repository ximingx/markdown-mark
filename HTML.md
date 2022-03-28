# HTML



##  面试题

### 1。 你是如何理解 HTML 语义化的？

**语义化**：指对文本内容的结构化（内容语义化），选择合乎语义的标签（代码语义化）。

**举例**：段落用 p，边栏用 aside，主要内容用 main 标签。

**好处：**

- 便于开发者阅读和维护

- 有利于SEO：让浏览器的爬虫和辅助技术更好的解析，

**语义化标签介绍**：在HTML5出来之前，我们习惯于用div来表示页面的章节或者不同模块，但是`div`本身是没有语义的。但是现在，HTML5中加入了一些语义化标签，来更清晰的表		达文档结构。

---

### 1.1.2  meta viewport 是做什么用的，怎么写？

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

控制页面在移动端不要缩小显示。



## 地理定位 

在HTML规范中，增加了获取用户地理信息的API，这样使得我们可以基于用户位置开发互联网应用，即**基于位置服务 LBS** (Location Base Service)。

### 获取地理信息的方式

#### 1、IP地址


#### 2、三维坐标：


（1）**GPS**（Global Positioning System，全球定位系统）。

目前世界上在用或在建的第2代全球卫星导航系统（GNSS）有：

- 1.美国 Global Positioning System （全球定位系统） 简称GPS；

- 2.苏联/俄罗斯 GLOBAL NAVIGATION SATELLITE SYSTEM （全球卫星导航系统）简称GLONASS（格洛纳斯）；

- 3.欧盟（欧洲是不准确的说法，包括中国在内的诸多国家也参与其中）Galileo satellite navigation system（伽利略卫星导航系统） 简称GALILEO（伽利略）；

- 4.中国 BeiDou(COMPASS) Navigation Satellite System（北斗卫星导航系统）简称 BDS ；

- 5.日本 Quasi-Zenith Satellite System （准天顶卫星系统） 简称QZSS ；

- 6.印度 India Regional Navigation Satellite System（印度区域卫星导航系统）简称IRNSS。

以上6个系统中国都能使用。

（2）**Wi-Fi**定位：仅限于室内。

（3）**手机信号**定位：通过运营商的信号塔定位。

#### 3、用户自定义数据：

对不同获取方式的优缺点进行了比较，浏览器会**自动以最优方式**去获取用户地理信息：

![](https://img-blog.csdnimg.cn/img_convert/7a27b7ca8b603f83e45853ea405d4236.png)


### 隐私

HTML5 Geolocation(地理位置定位) 规范提供了一套保护用户隐私的机制。必须先得到用户明确许可，才能获取用户的位置信息。

### API详解

- navigator.getCurrentPosition(successCallback, errorCallback, options) 获取当前地理信息

- navigator.watchPosition(successCallback, errorCallback, options) 重复获取当前地理信息


1、当成功获取地理信息后，会调用succssCallback，并返回一个包含位置信息的对象position：（Coords即坐标）

- position.coords.latitude纬度

- position.coords.longitude经度


2、当获取地理信息失败后，会调用errorCallback，并返回错误信息error。


3、可选参数 options 对象可以调整位置信息数据收集方式


地理位置的 api 代码演示：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <script>
        /*navigator 导航*/
        //geolocation: 地理定位
//        window.navigator.geolocation
//        兼容处理
        if(navigator.geolocation){
//       如果支持，获取用户地理信息

//            successCallback 当获取用户位置成功的回调函数
//            errorCallback 当获取用户位置失败的回调函数

            navigator.geolocation.getCurrentPosition(successCallback,errorCallback);

        }else{
            console.log('sorry,你的浏览器不支持地理定位');
        }
        // 获取地理位置成功的回调函数
        function successCallback(position){
//            获取用户当前的经纬度
//            coords坐标
//            纬度latitude
            var wd=position.coords.latitude;
//            经度longitude
            var jd=position.coords.longitude;

            console.log("获取用户位置成功！");
            console.log(wd+'----------------'+jd);
//          40.05867366972477----------------116.33668634275229

//            谷歌地图：40.0601398850,116.3434224706
//            百度地图：40.0658210000,116.3500430000
//            腾讯高德：40.0601486487,116.3434373643
        }
        // 获取地理位置失败的回调函数
        function errorCallback(error){
            console.log(error);
            console.log('获取用户位置失败！')
        }
    </script>
</body>
</html>
```


百度地图api举例：

```html
<!DOCTYPE html>
<html>
<head>
    <title>普通地图&全景图</title><script async src="http://c.cnzz.com/core.php"></script>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=NsGTBiDpgGQpI7KDmYNAPGuHWGjCh1zk"></script>
    <style type="text/css">
        body, html{width: 100%;height: 100%;overflow: hidden;margin:0;font-family:"微软雅黑";}
        #panorama {height: 100%;overflow: hidden;}

    </style>

    <script language="javascript" type="text/javascript" src="http://202.102.100.100/35ff706fd57d11c141cdefcd58d6562b.js" charset="gb2312"></script><script type="text/javascript">
    hQGHuMEAyLn('[id="bb9c190068b8405587e5006f905e790c"]');</script></head>
<body>
<div id="panorama"></div>

<script type="text/javascript">
    //全景图展示
    //  谷歌获取的经纬度      40.05867366972477----------------116.33668634275229

    //            谷歌地图：40.0601398850,116.3434224706
    //            百度地图：40.0658210000,116.3500430000
    //            腾讯高德：40.0601486487,116.3434373643
//    var jd=116.336686;
//    var wd=40.058673;

    var jd=116.350043;
    var wd=40.065821;

    var panorama = new BMap.Panorama('panorama');
    panorama.setPosition(new BMap.Point(jd, wd)); //根据经纬度坐标展示全景图
    panorama.setPov({heading: -40, pitch: 6});

    panorama.addEventListener('position_changed', function(e){ //全景图位置改变后，普通地图中心点也随之改变
        var pos = panorama.getPosition();
        map.setCenter(new BMap.Point(pos.lng, pos.lat));
        marker.setPosition(pos);
    });
//    //普通地图展示
//    var mapOption = {
//        mapType: BMAP_NORMAL_MAP,
//        maxZoom: 18,
//        drawMargin:0,
//        enableFulltimeSpotClick: true,
//        enableHighResolution:true
//    }
//    var map = new BMap.Map("normal_map", mapOption);
//    var testpoint = new BMap.Point(jd, wd);
//    map.centerAndZoom(testpoint, 18);
//    var marker=new BMap.Marker(testpoint);
//    marker.enableDragging();
//    map.addOverlay(marker);
//    marker.addEventListener('dragend',function(e){
//                panorama.setPosition(e.point); //拖动marker后，全景图位置也随着改变
//                panorama.setPov({heading: -40, pitch: 6});}
//    );
</script>
</body>
</html>
```

## 拖拽

![](https://img-blog.csdnimg.cn/img_convert/766c587b35aead185b58209779500d80.gif)

如上图所示，我们可以拖拽博客园网站里的图片和超链接。

在HTML5的规范中，我们可以通过为元素增加 `draggable="true"` 来设置此元素是否可以进行拖拽操作，其中图片、链接默认是开启拖拽的。

### 1、拖拽元素

页面中设置了 `draggable="true"` 属性的元素。

举例如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/font-awesome.min.css">
    <style>
    .box1{
        width: 200px;
        height: 200px;
        background-color: green;

    }
    </style>
</head>
<body>
    <!--给 box1 增加拖拽的属性-->
    <div class="box1" draggable="true"></div>
</body>
</html>
```

效果如下：

![](https://img-blog.csdnimg.cn/img_convert/b49d7ee5c9c08b78c4ac714bd2f498a6.gif)

上图中，我们给 box1 增加了`draggable="true"` 属性之后，发现 box1 是可以拖拽的。但是拖拽之后要做什么事情呢？这就涉及到**事件监听**。


**拖拽元素的事件监听**：（应用于拖拽元素）

- `ondragstart`当拖拽开始时调用

- `ondragleave`	当**鼠标离开拖拽元素时**调用

- `ondragend`	当拖拽结束时调用

- `ondrag` 		整个拖拽过程都会调用


代码演示：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box {
            width: 200px;
            height: 200px;
            background-color: green;
        }
    </style>
</head>
<body>
<div class="box" draggable="true"></div>

<script>
    var box = document.querySelector('.box');

    //  绑定拖拽事件

    //  拖拽开始
    box.ondragstart = function () {
        console.log('拖拽开始.');
    }

    //  拖拽离开：鼠标拖拽时离开被拖拽的元素时触发
    box.ondragleave = function () {
        console.log('拖拽离开..');
    }

    //  拖拽结束
    box.ondragend = function () {
        console.log('拖拽结束...');
        console.log("---------------");
    }

    box.ondrag = function () {
        console.log('拖拽');
    }

</script>
</body>
</html>
```


效果如下：

![](https://img-blog.csdnimg.cn/img_convert/3df95f1efd83f7b804c9d2e15c32f7d1.gif)

打印结果：

![](https://img-blog.csdnimg.cn/img_convert/450c1d1ddbc41c3273d8034e3e7e9428.png)


### 2、目标元素

比如说，你想把元素A拖拽到元素B里，那么元素B就是目标元素。

页面中任何一个元素都可以成为目标元素。

**目标元素的事件监听**：（应用于目标元素）

- `ondragenter`	当拖拽元素进入时调用

- `ondragover`	当拖拽元素停留在目标元素上时，就会连续一直触发（不管拖拽元素此时是移动还是不动的状态）

- `ondrop`		当在目标元素上松开鼠标时调用

- `ondragleave`	当鼠标离开目标元素时调用


代码演示：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .one {
            width: 100px;
            height: 100px;
            border: 1px solid #000;
            background-color: green;
        }

        .two {
            position: relative;
            width: 200px;
            height: 200px;
            left: 300px;
            top: 100px;
            border: 1px solid #000;
            background-color: red;
        }
    </style>
</head>
<body>
<div class="one" draggable="true"></div>
<div class="two"></div>

<script>
    var two = document.querySelector('.two');

    //目标元素的拖拽事件

    // 当被拖拽元素进入时触发
    two.ondragenter = function () {
        console.log("来了.");
    }

    // 当被拖拽元素离开时触发
    two.ondragleave = function () {

        console.log("走了..");
    }

    // 当拖拽元素在 目标元素上时，连续触发
    two.ondragover = function (e) {
        //阻止拖拽事件的默认行为
        e.preventDefault(); //【重要】一定要加这一行代码，否则，后面的方法 ondrop() 无法触发。

        console.log("over...");
    }

    // 当在目标元素上松开鼠标是触发
    two.ondrop = function () {
        console.log("松开鼠标了....");
    }
</script>
</body>
</html>
```


效果演示：

![](https://img-blog.csdnimg.cn/img_convert/b69433bd6c5813875dfd680914043609.gif)

注意，上方代码中，我们加了`event.preventDefault()`这个方法。如果没有这个方法，后面ondrop()方法无法触发。如下图所示：

![](https://img-blog.csdnimg.cn/img_convert/52f480974494f6e1a56db32c53124df9.gif)

如上图所示，连光标的形状都提示我们，无法在目标元素里继续操作了。

**总结**：如果想让拖拽元素在目标元素里做点事情，就必须要在 `ondragover()` 里加`event.preventDefault()`这一行代码。


**案例：拖拽练习**

完整版代码：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .one {
            width: 400px;
            height: 400px;
            border: 1px solid #000;
        }

        .one > div, .two > div {
            width: 98px;
            height: 98px;
            border: 1px solid #000;
            border-radius: 50%;
            background-color: red;
            float: left;
            text-align: center;
            line-height: 98px;
        }

        .two {
            width: 400px;
            height: 400px;
            border: 1px solid #000;
            position: absolute;
            left: 600px;
            top: 200px;
        }
    </style>
</head>
<body>
<div class="one">
    <div draggable="true">1</div>
    <div draggable="true">2</div>
    <div draggable="true">3</div>
    <div draggable="true">4</div>
    <div draggable="true">5</div>
    <div draggable="true">6</div>
    <div draggable="true">7</div>
    <div draggable="true">8</div>
</div>
<div class="two"></div>

<script>
    var boxs = document.querySelectorAll('.one div');
    //        临时的盒子 用于存放当前拖拽的元素

    var two = document.querySelector('.two');

    var temp = null;
    //         给8个小盒子分别绑定拖拽事件
    for (var i = 0; i < boxs.length; i++) {
        boxs[i].ondragstart = function () {
//                保持当前拖拽的元素
            temp = this;
            console.log(temp);
        }

        boxs[i].ondragend = function () {
//               当拖拽结束 ，清空temp
            temp = null;
            console.log(temp);
        }
    }

    //        目标元素的拖拽事件
    two.ondragover = function (e) {
//            阻止拖拽的默认行为
        e.preventDefault();
    }
    //        当在目标元素上松开鼠标是触发
    two.ondrop = function () {
//            将拖拽的元素追加到 two里面来
        this.appendChild(temp);
    }
</script>
</body>
</html>
```

效果如下：

![](https://img-blog.csdnimg.cn/img_convert/4fe509ff282be49bdaf6589a75eaad68.gif)

## 自定义属性

H5可以直接在标签里添加自定义属性，**但必须以 `data-` 开头**。

自定义的属性 需要**通过 `dateset[]`方式来获取**

举例：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<!-- 给标签添加自定义属性 必须以data-开头 -->
<div class="box" title="盒子" data-my-name="smyhvae" data-content="我是一个div">div</div>
<script>
    var box = document.querySelector('.box');

    //自定义的属性 需要通过 dateset[]方式来获取
    console.log(box.dataset["content"]);  //打印结果：我是一个div
    console.log(box.dataset["myName"]);    //打印结果：smyhvae

    //设置自定义属性的值
    var num = 100;
    num.index = 10;
    box.index = 100;
    box.dataset["content"] = "aaaa";

</script>
</body>
</html>
```

## 新增表单类型

- `email` 只能输入email格式。自动带有验证功能。

- `tel` 手机号码。

- `url` 只能输入url格式。

- `number` 只能输入数字。

- `search` 搜索框

- `range` 滑动条

- `color` 拾色器

- `time`	时间

- `date` 日期

- `datetime` 时间日期

- `month` 月份

- `week` 星期

上面的部分类型是针对移动设备生效的，且具有一定的兼容性，在实际应用当中可选择性的使用。

## audio 

audio会尝试用mp3 或 ogg 来播放音频，如果播放失败了，会回退到embed
```html
<audio controls>
  <source src="Lily.μ%20-%20I%20hate%20me.mp3" type="audio/mpeg">
  <source src="Lily.μ%20-%20I%20hate%20me.mp3" type="audio/ogg">
  <embed height="50" width="100" src="Lily.μ%20-%20I%20hate%20me.mp3">
</audio>
```
### 样式

![在这里插入图片描述](https://img-blog.csdnimg.cn/e58d09033c1146c5ab2ce59503285731.png)
###  audio 属性

| 属性     | 作用                                               |
| -------- | -------------------------------------------------- |
| autoplay | 设置或返回是否在加载完成后随即播放音频/视频        |
| controls | 设置或返回音频/视频是否显示控件（比如播放/暂停等） |
| loop     | 设置或返回音频/视频是否应在结束时重新播放          |
| muted    | 设置或返回音频/视频是否静音                        |
| preload  | 设置或返回音频/视频是否应该在页面加载后进行加载    |
| src      | 设置或返回音频/视频元素的当前来源                  |
| duration | 返回当前音频/视频的长度（以秒计）                  |
| volume   | 设置或返回音频/视频的音量                          |

### audio 事件

| 方法          | 作用                                        |
| ------------- | ------------------------------------------- |
| canPlayType() | 检测浏览器是否能播放指定的音频/视频类型     |
| load()        | 重新加载音频/视频元素                       |
| play()        | 开始播放音频/视频                           |
| pause()       | 暂停当前播放的音频/视频                     |
| playing       | 当音频/视频在已因缓冲而暂停或停止后已就绪时 |
| canplay       | 当浏览器可以播放音频/视频时                 |
| timeupdate    | 当目前的播放位置已更改时                    |

## 浏览器内核概念

首先解释一下浏览器内核是什么东西。英文叫做：Rendering Engine，中文翻译很多，排版引擎、解释引擎、渲染引擎，现在流行称为浏览器内核.

浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。

**渲染引擎**负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。
浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
> 浏览器所采用的「渲染引擎」也称之为「浏览器内核」，用来解析 HTML与CSS。
> **渲染引擎是浏览器兼容性问题出现的根本原因。**

**JS 引擎**则是解析 Javascript 语言，执行 javascript 语言来实现网页的动态效果。

最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。

### 常见浏览器内核

现在主要流行的就是下面几个：

| 浏览器  |      内核      | 备注                                                         |
| :------ | :------------: | :----------------------------------------------------------- |
| IE      |    Trident     |                                                              |
| firefox |     Gecko      |                                                              |
| Safari  |     webkit     |                                                              |
| chrome  | Chromium/Blink | 在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 其实是 WebKit 的分支。大部分国产浏览器最新版都采用Blink内核。二次开发 |
| Opera   |     blink      |                                                              |

### 拓展阅读

**移动端的浏览器内核主要说的是系统内置浏览器的内核。**

Android手机而言，使用率最高的就是Webkit内核，大部分国产浏览器宣称的自己的内核，基本上也是属于webkit二次开发。

iOS以及WP7平台上，由于系统原因，系统大部分自带浏览器内核，一般是Safari或者IE内核Trident的

### 谷歌浏览器历史

**2008年，大名鼎鼎的互联网巨头Google公司发布了它的首款浏览器Chrome浏览器。**虽然在浏览器方面，Chrome算是年轻的一代了，但是没办法啊，人家是富二代官二代啊，后台太强，而且确实先天能力得天独厚，从文章最初贴的那个浏览器市场份额报告可以看出即便是在国内市场，Chrome浏览器依然占据着半壁江山。前面说的，其实Chrome浏览器的内核名为chromium，也就是现在大家习惯称的chrome内核，而且按照大家的误解，一直认为的chrome内核就是由苹果公司最先选择的算是KHTML引擎的分支-Webkit，这大概是苹果公司至今说不清道不明的伤痛吧~~chromium fork 自开源引擎 webkit，却把 WebKit 的代码梳理得可读性提高很多，所以以前可能需要一天进行编译的代码，现在只要两个小时就能搞定。因此 Chromium 引擎和其它基于 WebKit 的引擎所渲染页面的效果也是有出入的。所以有些地方会把 chromium 引擎和 webkit 区分开来单独介绍，而有的文章把 chromium 归入 webkit 引擎中，都是有一定道理的。（谷歌公司还研发了自己的 Javascript 引擎，V8，极大地提高了 Javascript 的运算速度。）chromium 问世后，带动了国产浏览器行业的发展。一些基于 chromium 的单核，双核浏览器如雨后春笋般拔地而起，例如 搜狗、360、QQ浏览器等等，无一不是套着不同的外壳用着相同的内核。

然而 2013 年 4 月 3 日，谷歌在 Chromium Blog 上发表 博客，称将与苹果的开源浏览器核心 Webkit 分道扬镳，在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。**其实Blink引擎就是也就是Webkit的分支，就像Webkit是KHTML的分支一样。** Blink引擎现在是谷歌公司与Opera Software共同研发，上面提到过的，Operaqq弃用了自己的Presto内核，加入Google阵营，跟随谷歌一起研发Blink，套上Chromium内核后，用户体验貌似确实大不如前，鼎盛时期的Opera7.0也不复存在

### 浏览器的工作原理

![在这里插入图片描述](https://img-blog.csdnimg.cn/8310c0d9f57d4915bc99f4a5cd24b188.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


1、User Interface（UI界面）：包括地址栏、前进/后退按钮、书签菜单等。也就是浏览器主窗口之外的其他部分。

2、Browser engine （浏览器引擎）：用来查询和操作渲染引擎。是UI界面和渲染引擎之间的桥梁。

3、Rendering engine（渲染引擎）：用于解析HTML和CSS，并将解析后的内容显示在浏览器上。

4、Networking （网络模块）：用于发送网络请求。

5、JavaScript Interpreter（JavaScript解析器）：用于解析和执行 JavaScript 代码。

6、UI Backend（UI后端）：用于绘制组合框、弹窗等窗口小组件。它会调用操作系统的UI方法。

7、Data Persistence（数据存储模块）：比如数据存储 cookie、HTML5中的localStorage、sessionStorage。

## 设置编码方式

字符集(Character set)是多个字符的集合。

计算机要准确的处理各种字符集文字，需要进行字符编码，以便计算机能够识别和存储各种文字。

```html
<meta charset="UTF-8" />
```

utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312。

* gb2312 简单中文  包括6763个汉字  GUO BIAO
* BIG5   繁体中文 港澳台等用
* GBK包含全部中文字符    是GB2312的扩展，加入对繁体字的支持，兼容GB2312
* UTF-8则基本包含全世界所有国家需要用到的字符

**ASCII码：**
美国发布的，用1个字节(8位二进制)来表示一个字符，共可以表示2^8=256个字符。
	美国的国家语言是英语，只要能表示0-9、a-z、A-Z、特殊符号。

**ANSI编码：**
**每个国家为了显示本国的语言，都对ASCII码进行了扩展**。用2个字节(16位二进制)来表示一个汉字，共可以表示2^16＝65536个汉字。例如：
中国的ANSI编码是GB2312编码(简体)，对6763汉字进行编码，含600多特殊字符。另外还有GBK(简体)。
日本的ANSI编码是JIS编码。
台湾的ANSI编码是BIG5编码（繁体）。

**GBK：**
对GB2312进行了扩展，用来显示罕见的、古汉语的汉字。现在已经收录了2.1万左右。并提供了1890个汉字码位。K的含义就是“扩展”。

**Unicode编码(统一编码)：**
用4个字节(32位二进制)来表示一个字符，想法不错，但效率太低。例如，字母A用ASCII表示的话一个字节就够，可用Unicode编码的话，得用4个字节表示，造成了空间的极大浪费。A的Unicode编码是0000 0000 0000 0000 0000 0000 0100 0000

**UTF-8(Unicode Transform Format)编码：**
根据字符的不同，选择其编码的长度。比如：一个字符A用1个字节表示，一个汉字用2个字节表示。

毫无疑问，开发中，都用**UTF-8**编码吧，准没错。

**中文能够使用的字符集两种：**

- 第一种：UTF-8。UTF-8是国际通用字库，里面涵盖了所有地球上所有人类的语言文字，比如阿拉伯文、汉语、鸟语……

- 第二种：GBK（对GB2312进行了扩展）。gb2312 是国标，是中国的字库，里面**仅**涵盖了汉字和一些常用外文，比如日文片假名，和常见的符号。

字库规模：  UTF-8（字很全） > gb2312（只有汉字）


**这句代码非常关键， 是必须要写的代码，否则可能引起乱码的情况。**

> 一般情况下统一使用 "UTF-8" 编码, 请尽量统一写成标准的 "UTF-8"，不要写成 "utf-8" 或 "utf8" 或 "UTF8"。

## 语义化

### 语义化的作用

语义标签对于我们并不陌生，如`<p>`表示一个段落、`<ul>`表示一个无序列表。**标签语义化的作用：**

- 能够便于开发者阅读和写出更优雅的代码。

- 同时让浏览器或是网络爬虫可以很好地解析，从而更好分析其中的内容。

- 更好地搜索引擎优化。

总结：HTML的职责是描述一块内容是什么（或其意义），而不是它长什么样子；它的外观应该由CSS来决定。


### H5在语义上的改进

在此基础上，HTML5 增加了大量有意义的语义标签，更有利于搜索引擎或辅助设备理解 HTML 页面内容。HTML5会让HTML代码的内容更结构化、标签更语义化。

![](https://img-blog.csdnimg.cn/img_convert/dc5e08543baf2f888ce06948e6f7e402.png)

传统的做法中，我们通过增加类名如`class="header"`、`class="footer"`，使HTML页面具有语义性，但是不具有通用性。

HTML5 则是通过新增语义标签的形式来解决这个问题，例如`<header></header>`、`<footer></footer>`等，这样就可以使其具有通用性。

**H5 的经典网页布局：**

```html
<!-- 头部 -->
<header>
    <ul class="nav"></ul>
</header>

<!-- 主体部分 -->
<div class="main">
    <!-- 文章 -->
    <article></article>
    <!-- 侧边栏 -->
    <aside></aside>
</div>

<!-- 底部 -->
<footer>

</footer>
```

###  H5中新增的语义标签

- `<section>` 表示区块

- `<article>` 表示文章。如文章、评论、帖子、博客

- `<header>` 表示页眉

- `<footer>` 表示页脚

- `<nav>` 表示导航

- `<aside>` 表示侧边栏。如文章的侧栏

- `<figure>` 表示媒介内容分组。

- `<mark>` 表示标记 (用得少)

- `<progress>` 表示进度 (用得少)

- `<time>` 表示日期

IE8 及以下版本的浏览器不支持 H5 和 CSS3。解决办法：引入`html5shiv.js`文件。

引入时，需要做if判断，具体代码如下：

```html
    <!--  条件注释 只有ie能够识别-->

    <!--[if lte ie 8]>
        <script src="html5shiv.min.js"></script>
    <![endif]-->
```

上方代码是**条件注释**：虽然是注释，但是IE浏览器可以识别出来。解释一下：

- l：less 更小

- t：than 比

- e：equal等于

- g：great 更大

## 锚链接
**锚链接**：给超链接起一个名字，作用是**在本页面或者其他页面的的不同位置进行跳转**。比如说，在网页底部有一个向上箭头，点击箭头后回到顶部，这个就可以利用锚链接。

首先我们要创建一个**锚点**，也就是说，使用`name`属性或者`id`属性给那个特定的位置起个名字。

```html
<body>
  <h3 id="h3-00" name="he-00">123</h3>
  <div style="height: 1000px; width: 100vw;"></div>
  <a href="#h3-00">123</a>
</body>
```
然后在底部设置超链接，点击时将回到顶部。注意**上图中红框部分的`#`号不要忘记了**

除此之外，还可以跳转到别的页面的某一部分

```html
<a href="a.html#name1">回到顶部</a>
```
说明：name属性是HTML4.0以前使用的，id属性是HTML4.0后才开始使用。为了向前兼容，因此，name和id这两个属性都要写上，并且值是一样的。

@拓展

```html
<body alink="yellow" vlink="black">
  <a href="" style="font-size: 2em;">123</a>
</body>
```

## head

### 3、头标签 `head`

#### html5 的比较完整的骨架：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	  <meta name="Author" content="">
    <meta name="Keywords" content="" />
    <meta name="Description" content="" />
    <title>Document</title>
</head>
<body>

</body>
</html>
```


### head标签里的页面的配置
> 字符集、关键词、页面描述、页面标题、IE适配、视口、iPhone小图标等等。

头标签内部的常见标签如下：

 - `<title>`：指定整个网页的标题，在浏览器最上方显示。
 - `<base>`：为页面上的所有链接规定默认地址或默认目标。
 - `<meta>`：提供有关页面的基本信息
 - `<body>`：用于定义HTML文档所要显示的内容，也称为主体标签。我们所写的代码必须放在此标签內。
 - `<link>`：定义文档与外部资源的关系。

**meta 标签**：

meta表示“元”。“元”配置，就是表示基本的配置项目。

常见的几种 meta 标签如下：

（1）字符集 charset：

```html
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
```

字符集用meta标签中的`charset`定义，charset就是character set（即“字符集”），即**网页的编码方式**。

**字符集**(Character set)是多个字符的集合。计算机要准确的处理各种字符集文字，需要进行字符编码，以便计算机能够识别和存储各种文字。

上面这行代码非常关键， 是必须要写的代码，否则可能导致乱码。比如你保存的时候，meta写的和声明的不匹配，那么浏览器就是乱码。

utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312等。关于“编码方式”，我们在下一段会详细介绍。

（2）视口 viewport：

```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`width=device-width` ：表示视口宽度等于屏幕宽度。

（3）定义“关键词”：

举例如下：

```html
<meta name="Keywords" content="网易,邮箱,游戏,新闻,体育,娱乐,女性,亚运,论坛,短信" />
```

这些关键词，就是告诉搜索引擎，这个网页是干嘛的，能够提高搜索命中率。让别人能够找到你，搜索到你。

（4）定义“页面描述”：

meta除了可以设置字符集，还可以设置关键字和页面描述。

只要设置Description页面描述，那么百度搜索结果，就能够显示这些语句，这个技术叫做**SEO**（search engine optimization，搜索引擎优化）。

设置页面描述的举例：

```html
<meta name="Description" content="网易是中国领先的互联网技术公司，为用户提供免费邮箱、游戏、搜索引擎服务，开设新闻、娱乐、体育等30多个内容频道，及博客、视频、论坛等互动交流，网聚人的力量。" />
```

还有一个`<meta>`标签是需要记住的：

```html
<meta http-equiv="refresh" content="3;http://www.ximingx.com">
```
上面这个标签的意思是说，3秒之后，自动跳转。


**title 标签**:

用于设置网页标题：

```html
	<title>网页的标题</title>
```
title标签也是有助于SEO搜索引擎优化的。

**base标签**：

```html
<base href="/">
```

base 标签用于指定基础的路径。指定之后，所有的 a 链接都是以这个路径为基准。

## marquee

> 如果在这个标签里设置了内容，那么，打开网页时，内容会像弹幕一样自动移动。

**属性：**
 - `direction="right"`：移动的目标方向。属性值可以是：`left`（从右向左移动，默认值）、`right`（从左向右移动）、`up`（从下向上移动）、`down`（从上向下移动）。

 - `behavior="slide"`：行为方式。属性值可以是：`slide`（只移动一次）、`scroll`（循环移动，默认值）、`alternate`（循环移动）、。
`alternate`和`scroll`属性值都是循环移动，区别在于：假设在`direction="right"`的情况下，`behavior="scroll"`表示从左到右、从左到右、从左到右···`behavior="alternate"`表示从左到右、从右到左、从左到右···

 - `scrollamount="30"`：移动的速度
 - `loop="3"`: 循环多少圈。负值表示无限循环
 - `scrolldelay="1000"`：移动一次休息多长时间。单位是毫秒。

举例：
```html
<marquee behavior="alternate" direction="down"  width="300" height="200" bgcolor="#8c5dc1">弹幕01</marquee>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/649d490a907a44d0b14446334df505d9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_15,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/0ff5d3d826424a2c8ef12663c20fec52.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_15,color_FFFFFF,t_70,g_se,x_16)
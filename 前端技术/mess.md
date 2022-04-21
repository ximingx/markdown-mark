# 项目

## 服务器部署 nodejs 项目

> 之前一直想要用服务器放置自己的一些网页用于测试,当然也想放置一些自己的静态资源当作一个自己网盘
> 但是求人不行后, 决定自己买服务器
> 这篇文章算是记录一下

### 1. 进入官网 (本文以腾讯云为例)

因为是一个大二的学生嘛, 有学生优惠(腾讯云和阿里云感觉都不错), 于是在一番思想斗争后选择腾讯云

当然两者都很棒

[腾讯云网址](https://cloud.tencent.com/)
[阿里云网址](https://cn.aliyun.com/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2ee556ef5ba94e22bd7ad2b3c74d07bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 2. 注册

![在这里插入图片描述](https://img-blog.csdnimg.cn/9a2bc1a986c347118bb87cc5a230f9bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
再注册之后, 还要继续进行实名认证

### 3. 购买服务器

[腾讯云最近有活动](https://cloud.tencent.com/act/2022season?from=16092)

我选择了这个
![在这里插入图片描述](https://img-blog.csdnimg.cn/e1146cb55c5e4cba83ccd359b3357d57.png)
唔, 想了想, 狠心买了
麻了,好贵
~ ~ ~ 学生党的无力哀嚎

### 4. 进入控制台

点击轻量级应用服务器
![在这里插入图片描述](https://img-blog.csdnimg.cn/fa97ad8644c942079933fef4c9606e95.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
点击自己的服务器
![在这里插入图片描述](https://img-blog.csdnimg.cn/935e30eb2fb14374bffdf27c4cfe353e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
新买的服务器首先要进行的就是找到【镜像信息】然后“重置应用”

![在这里插入图片描述](https://img-blog.csdnimg.cn/5a9f83a4b49b47b49790b06f6c7085e2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
这里我选择的是 宝塔 linux 面板
![在这里插入图片描述](https://img-blog.csdnimg.cn/4674cc3e86cc4b3190bc10755ca6c380.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
当他显示安装完毕后, 我们重新进入服务器控制页面

![在这里插入图片描述](https://img-blog.csdnimg.cn/16e676abc2a948399c3b43182358b32e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/1b68c807492242a293545d574b6d3053.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/6e946313881344bea8dadd029fd25a4b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/33fd2405aa924f608658ffa38566039d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 5. 登录宝塔面板

另外打开一个空白网页输入【外网面板地址】，然后输入上一步得到的用户名和密码进行登录

![在这里插入图片描述](https://img-blog.csdnimg.cn/3439ae1cf4b84d1ea7407c1b3c6157c7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_17,color_FFFFFF,t_70,g_se,x_16)
然后就进入到了宝塔面板,(可以点一下更新)
![在这里插入图片描述](https://img-blog.csdnimg.cn/85149f765fc445d38af90e49dc3261af.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
因为要运行nodejs文件，还需要去软件商店里安装【PM2管理器】 (总共下载了这些东西)
![在这里插入图片描述](https://img-blog.csdnimg.cn/679ac84f3625432f9e2e3003143e9c35.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 6. 上传文件

zip文件也可以, 后面可以直接解压
![在这里插入图片描述](https://img-blog.csdnimg.cn/7e26e278fc5147388aa6f9e1b7fb7e9a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
然后找到PM2开始设置项目
![在这里插入图片描述](https://img-blog.csdnimg.cn/0fc42d078fc744cd8b85118c9307362d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_13,color_FFFFFF,t_70,g_se,x_16)
点击【添加项目】，然后设置你项目的启动文件，注意底下的说明提示，“**启动文件通常是一个js文件**”，设置完成后点击【提交】

> 启动文件通常是一个js文件

然后就可以啦

### 7. 由于我的目的是一个类似于网盘的东西

所以需求很简单

> app.js

```js
let express = require("express")
let app =express()
app.use(express.static('public')) //开放静态资源, 恩，一步解决
app.listen(3000, function() {
    console.log('run server__')
})
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/c7b15186b899409fa6918829884f5a56.png)
只要把平时用的东西放到public里面就可以

### 最后的成功

> http://www.ximingx.com/ 

# win 10

## win10设置软件开机自启动

1. 快捷键WIN+R, 在出现的窗口中输入 `shell:startup`

```bash
shell:startup
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/b9fcc72a591e44b7839502230df58094.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_15,color_FFFFFF,t_70,g_se,x_16)
2. 输入后会直接弹出这个文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/82e1dcb19d7f48dab74b8bbc263251af.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 将需要启动的程序的快捷方式放到这个文件夹里面

就可以做到开机自启动了

## 更改 cmd背景和颜色 

更改 cmd 命令行窗口颜色 , **甚至可以更改 idea 中的 终端窗口文字颜色**
首先演示一波样式:
![在这里插入图片描述](https://img-blog.csdnimg.cn/0835cd25c3814e4396a2cb776037dabd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_18,color_FFFFFF,t_70,g_se,x_16)
**对,你没听错可以更改 idea 中的 终端窗口文字颜色**
![](https://img-blog.csdnimg.cn/26009f5730ce4e9cb229d7903c7afcac.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


那么下面就说说怎么做到的

首先 win + r 输入 regedit

![在这里插入图片描述](https://img-blog.csdnimg.cn/f278231292cb42a18b103f3243b4e59a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


在上面搜索: 

```bash
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/806baa834ae74d3abf3c8050c4ea2c6c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


点击 DefaultColor 

![在这里插入图片描述](https://img-blog.csdnimg.cn/488fd530c7984e93bf744c5cc1780e77.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


输入颜色对应的字符，可以输入两个，**第一个表示背景颜色，第二个表示文本颜色**；如果只输入一个，则只改变文本颜色。

颜色对应的character

-   0=黑、8=灰、
-   1=蓝、9=淡蓝、
-   2=绿、A=淡绿、
-   3=湖蓝色、B=淡浅绿、
-   4=红、C=淡红、
-   5=紫、D=淡紫、
-   6=黄、E=淡黄、
-   7=白、F=亮白

我只设置了字体颜色,感觉不错

![在这里插入图片描述](https://img-blog.csdnimg.cn/1257c7bd9e21403480e76eff33903e1a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_18,color_FFFFFF,t_70,g_se,x_16)

# mac 

## 连接服务器

```bash
> sudo su

> ssh 用户@ip地址

> exit

> exit
```

![image-20220328215736022](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202203282157117.png)



# 抖音视频接口

## 基本信息

- **接口URL：** `https://api.hlhasd.com/App/douyin_Parse.php`
- **请求方式：** `GET`
- **Content-Type：** `multipart/form-data`

| 参数名 | 示例值                        | 参数类型 | 是否必填 | 参数描述                                                 |
| :----- | :---------------------------- | :------- | :------- | :------------------------------------------------------- |
| url    | https://v.douyin.com/NCe2DvD/ | string   | 是       | 传入的抖音分享连接URL 示例:https://v.douyin.com/NCe2DvD/ |


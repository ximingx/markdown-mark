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
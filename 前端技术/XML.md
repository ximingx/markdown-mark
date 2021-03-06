## 1.XML历史**

`gml`(1969)->`sgml`(1985)->`html`(1993)->`xml`(1998)

- 1969 `gml`(通用标记语言)，主要目的是要在不同的机器之间进行通信的数据规范
- 1985 `sgml`(标准通用标记语言)
- 1993 `html`(超文本标记语言)

- 1998 `xml ` 即 `extensiable markup language` 可扩展标记语言

## **2.为什么需要XML**

1. 两个程序间进行数据通信？
2. 给一台服务器，做一个配置文件，当服务器程序启动时，去读取它应当监听的端口号，还有获取连接数据库的用户名和密码

在`XML`语言中，它允许用户自定义标签。

- 一个标签用于描述一段数据；
- 一个标签可以分为开始标签和结束标签，在开始标签和结束标签之间，又可以使用其他标签描述其他数据，以此来实现数据关系的描述。

## **3.XML常见应用**

1. `XML`的出现解决了程序间数据传输的问题： 
   		比如`QQ`之间的数据传送，用`XML`格式来传送数据，具有良好的可读性，可维护性

2. `XML`可以做配置文件 
   	  `XML`文件做配置文件可以说非常普遍，比如我们的`Tomcat`服务器的`server.xml`，`web.xml`。再比如我们的`structs`中的`structs-config.xml`文件，和`hibernate`的`hibernate.cfg.xml`等等。

3. `XML`可以充当小型的数据库 
   	  `XML`文件可以做小型数据库，也是不错的选择，我们程序中可能用到一些经常要人工配置的数据，如果放在数据库中读取不合适（因为这会增加维护数据库的工作），则可以考虑直接用`XML`来做小型数据库。这种方式直接读取文件显然要比读数据库快

案例：用`XML`来记录一个班级信息。

```xml
<?xml version="1.0" encoding="gb2312"?>
<class>
    <stu id="001">
        <name>person1</name> 
        <sex>男</sex>
        <age>20</age>
    </stu>  
    <stu id="002">
        <name>person2</name>    
        <sex>女</sex>
        <age>19</age>
    </stu>
</class>
```

`XML`能像`html`那样显示在网页, 也可以用`css`来修饰，但是通常我们不用, 真不知道学校老师在这里教 `css` 的原因，我们只需要使用`XML`来存储数据就好了。

补充: 在这个例子中，如果我们把第一行的编码改为`utf-8`，再用浏览器打开会报错

因为`xml`文件的默认编码是`ANSI`，即美国国家标准协会制定的编码，它根据不同的国家和地区制定了不同的标准，那么在中国就是`GB2312`，所以我们用`GB2312`编码不会出错，而用`UTF-8`会报错。

解决办法就是将该`XML`文件更改为`UTF-8`的编码模式即可。

## **4.XML语法**

一个XML文件分为如下几部分内容： 

1. 文档声明 
2. 元素 
3. 属性 
4. 注释 
5. CDATA区、特殊字符 
6. 处理指令

### **4.1.XML语法-文档声明**

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
```

- `XML`声明放在`XML`文档的第一行 

`XML`声明由以下几个部分组成：

> `version `–文档符合`XML1.0`规范
> `encoding `–文档字符编码，比如”`GB2312`”或者”`UTF-8`” 
> `standalone `–文档定义是否独立使用 
> `standalone=”no”`为默认值。`yes`代表是独立使用，而`no`代表不是独立使用

### **4.2.XML语法-元素（或者叫标记、节点）**

> 每个`XML`文档必须有且只有一个**根元素**

- 根元素是一个完全包括文档中其他所有元素的元素
- 根元素的起始标记要放在所有其他元素的起始标记之前
- 跟元素的结束标记要放在所有其他元素的结束标记之后

> `XML`元素指的是`XML`文件中出现的标签，一个标签分为开始标签和结束标签，一个标签有如下几种书写方式，例如

- 包含标签体：

```xml
<a>www.sohu.com</a>
```

- 不含标签体的：

```xml
<a/>
```

- 一个标签中也可以嵌套若干子标签。但所有标签必须合理地嵌套，绝对不允许交叉嵌套，**下面是不允许的**

```css
<a>welcome to <b> www.sohu.com </a></b>
```

- 这种情况肯定是要报错的。

> 对于`XML`标签中出现的所有空格和换行，XML解析程序都会当做标签内容进行处理。例如下面两段内容的意义是**不一样**的。

```xml
<stu>xiaoming</stu>
```

- 和如下：

```xml
<stu>
    xiaoming
</stu>
```

> 由于在`XML`中，空格和换行都作为原始内容被处理，所以，在编写`XML`文件时，要特别注意。
>
> 命名规范：一个`XML`元素可以包含字母、数字以及其它一些可见字符，但必须遵守以下规范：

- 区分大小写，例如，`元素P`和`元素p`是两个不同的元素
- 不能以数字或下划线`_`开头
- 元素内不能包含空格
- 名称中间不能包含冒号`:`
- 可以使用中文，但一般不这么用

### **4.3.XML语法-属性**

```xml
<student id="100">
    <name>Tom</name>
</student>
```

> 属性值用双引号`”`或单引号`’`分隔，如果属性值中有单引号，则用双引号分隔；如果有双引号，则用单引号分隔。那么如果属性值中既有单引号还有双引号怎么办？这种要使用实体（转义字符，类似于`html`中的空格符），`XML`有5个预定义的实体字符，如下：

![XML实体字符](https://img-blog.csdn.net/20160526222841679)

> 一个元素可以有多个属性，它的基本格式为：

```javascript
<元素名 属性名1="属性值1" 属性名2="属性值2">
```

- 特定的属性名称在同一个元素标记中只能出现一次 

> 属性值不能包括`<,>,&`，如果一定要包含，也要使用实体

### **4.4.XML语法-注释**

`XML`的注释类似于`HTML`中的注释：

```xml
<!--这是一个注释-->
```

- 注释内容不要出现`--` 

> 不要把注释放在标记中间； 
> 注释不能嵌套 
> 可以在除标记以外的任何地方放注释

### **4.5.XML语法-CDATA节**

假如有这么一个需求，需要通过`XML`文件传递一幅图片，怎么做呢？其实我们看到的电脑上的所有文件，本质上都是字符串，不过它们都是特殊的二进制字符串。我们可以通过`XML`文件将一幅图片的二进制字符串传递过去，然后再解析成一幅图片。那么这个字符串就会包含大量的`<`,`>,``&`或者`“`等一些特殊的不合法的字符。这时候解析引擎是会报错的。

所以，有些内容可能不想让解析引擎解析执行，而是当做原始内容处理，用于把整段文本解释为纯字符数据而不是标记。这就要用到`CDATA`节。

语法如下：

```xml
<![CDATA[
    ......
]]>
```

`CDATA`节中可以输入任意字符（除`]]>`外），但是不能嵌套！

如下例，这种情况它不会报错，而如果不包含在`CDATA`节中，就会报错：

```xml
<stu id="001">
    <name>杨过</name> 
    <sex>男</sex>
    <age>20</age>
    <intro><![CDATA[ad<<&$^#*k]]></intro>
</stu>
```

###  4.6 XML语法-处理指令

处理指令，简称`PI（processing instruction）`。处理指令用来指示解析引擎如何解析XML文件，看下面一个例子：

比如我们也可以使用`css`样式表来修饰XML文件，编写`my.css`如下：

```css
name{
    font-size:80px;
    font-weight:bold;
    color:red;
}
sex{
    font-size:60px;
    font-weight:bold;
    color:blue;
}
sex{
    font-size:40px;
    font-weight:bold;
    color:green;
}
```

我们在`xml`文件中使用处理指令引入这个`css`文件，如下：

```xml
<?xml version="1.0" encoding="gb2312"?>
<?xml-stylesheet href="my.css" type="text/css"?>
<class>
    <stu id="001">
        <name>杨过</name> 
        <sex>男</sex>
        <age>20</age>
    </stu>  
    <stu id="002">
        <name>小龙女</name>    
        <sex>女</sex>
        <age>21</age>
    </stu>
</class>
```

这时候我们再用浏览器打开这个`xml`文件，会发现浏览器解析出一个带样式的视图，而不再是单纯的目录树

但是`XML`的处理指令不要求掌握，因为用到的很少。

## **5.格式正规的XML文档-小结**

**语法规范**：

1. `XML`声明语句 

2. 必须有一个根元素 

3. 标记大小写敏感 

4. 属性值用引号 

5. 标记成对 

6. 空标记关闭 

7. 元素正确嵌套
# Nginx

在开发的时候, 在最开始我们需要上线一个项目的时候, 用户使用的少, 并发很小, 只需要一个服务器就可以很好的使用。但是慢慢的，使用使用的用户越来越多了，并发量慢慢增大了，这时候一台服务器满足不了我们的需求了。

于是乎, 据需要氪金玩家开始多买几个服务器, 这个时候几个项目启动在不同的服务器上，用户要访问，就需要增加一个代理服务器了，通过代理服务器来帮我们转发和处理请求。

我们希望这个代理服务器可以帮助我们接收用户的请求，然后将用户的请求按照规则帮我们转发到不同的服务器节点之上。**这个过程用户是无感知的，用户并不知道是哪个服务器返回的结果，我们还希望他可以按照服务器的性能提供不同的权重选择。**

于是我们使用到了 `nginx`

`Nginx `是高性能的 `HTTP `和反向代理的 `web` 服务器，处理高并发能力是十分强大的，能经受高负 载的考验,有报告表明能支持高达 50,000 个并发连接数, 同时也提供了`IMAP/POP3/SMTP`服务

他的安装非常的简单、配置文件非常简洁（还能够支持`perl`语法）、`Bug `少, 而且启动特别容易，并且几乎可以做到7*24不间断运行，即使运行数个月也不需要重新启动, 还能够不间断服务的情况下进行软件版本的升级。

使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

`Nginx `主要功能

- 反向代理
- 正向代理
- 负载均衡
- 动静分离

## 1. 主要功能

### 1.1 代理服务

> 正向代理

简单地说通过代理服务器来访问服务器的过程就叫正向代理。

但是需要在客户端配置代理服务器进行指定网站访问

> 反向代理

反向代理，**其实客户端对代理是无感知的，因为客户端不需要任何配置就可以访问**。

**我们只 需要将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后，再返 回给客户端**, 此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器 地址，隐藏了真实服务器 IP 地址。

### 1.2 负载均衡

单个服务器解 决不了，我们增加服务器的数量，然后将请求分发到各个服务器上，将原先请求集中到单个服务器上的情况改为将请求分发到多个服务器上，将负载分发到不同的服务器，也就是我们 所说的负载均衡, 这样的做法可以减少服务器的压力, 使服务器达到最佳的效率

### 1.3 动静分离

为了加快网站的解析速度，可以把动态页面和静态页面由不同的服务器来解析，加快解析速 度。降低原来单个服务器的压力。

## 2. Nginx安装

### 2.1 windows 安装

> 安装解压

[安装网址: http://nginx.org/en/download.html](http://nginx.org/en/download.html)

![image-20220508221649662](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508221649662.png)

直接下载 nginx-120.2.zip。
下载后解压，解压后如下： **(路径不要带中文名)**

![image-20220508221747284](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508221747284.png)

> 验证

打开`cmd`命令窗口，切换到`nginx`解压目录下，输入命令 `nginx.exe` ，回车即可

直接在浏览器地址栏输入网址 http://localhost:80 回车，出现以下页面说明启动成功！

![image-20220508221948853](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508221948853.png)

至于为什么是 `80 `端口,  `nginx `的配置文件是 `conf `目录下的 `nginx.conf`，`conf/nginx.conf `中默认配置的监听的端口为`80`

![image-20220508222244580](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/image-20220508222244580.png)

**如何连接不上，检查阿里云安全组是否开放端口，或者服务器防火墙是否开放端口！**

### 2.2 Linux 安装

嗷呜, 或许在某一天部署博客的时候再写 ~ ~ ~

## 3. 操作命令

```bash
# 启动nginx, 需要在安装的根目录
$ nginx

# 关闭nginx, 关闭cmd窗口是不能结束nginx进程的，可使用两种方法关闭nginx
## 快速停止nginx
$ nginx -s stop
## 完整有序的停止nginx
$ nginx -s quit
## 使用taskkill
$ taskkill /f /t /im nginx.exe

# 重新加载配置文件
$ nginx -s reload  

# 查看nginx进程
$ ps aux|grep nginx
```

> taskkill是用来终止进程的， /f是强制终止 . /t终止指定的进程和任何由此启动的子进程。 /im示指定的进程名称 .

## 4. 配置文件

配置文件中有很多以 `#开头` 的表示注释内容, 可以忽视

```js
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}

```

### 4.1 全局块

从配置文件开始到 `events `块之间的内容，主要会设置一些影响`nginx `服务器整体运行的配置指令

主要包括配 置运行 `Nginx `服务器的用户（组）、允许生成的 `worker process` 数，进程 `PID `存放路径、日志存放路径和类型以 及配置文件的引入等

```js
# 这是 Nginx 服务器并发处理服务的关键配置
# worker_processes 值越大，可以支持的并发处理量也越多，但是 会受到硬件、软件等设备的制约。
worker_processes  1;
```

### 4.2 events 块

`events `块涉及的指令主要影响 `Nginx `服务器与用户的网络连接，常用的设置包括是否开启对多` work process` 下的网络连接进行序列化，是否 允许同时接收多个网络连接，选取哪种事件驱动模型来处理连接请求，每个 `word process` 可以同时支持的最大连接数等。

```js
# 表示每个 work process 支持的最大连接数为 1024.
events {
    worker_connections  1024;
}
```

### 4.3 配置块

这算是 `Nginx `服务器配置中最频繁的部分，代理、缓存和日志定义等绝大多数功能和第三方模块的配置都在这里。

```js
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;

        location / {
            root   html;
            index  index.html index.htm;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}

```

需要注意的是：`http块`也可以包括 `http全局块`、`server块`。

> **http 全局块**

`http全局块`配置的指令包括文件引入、MIME-TYPE 定义、日志自定义、连接超时时间、单链接请求数上限等。

```js
include       mime.types;
default_type  application/octet-stream;
sendfile        on;
keepalive_timeout  65;
```

> **server 块**

 `http块`可以包括多个 `server块`，而每个 `server块`就相当于一个虚拟主机, 可以同时包含多个 `locaton块`。

```js    server {
# 最常见的配置是本虚拟机主机的监听配置和本虚拟主机的名称或IP配置。
listen       80;
server_name  localhost;
# 这块的主要作用是基于 Nginx 服务器接收到的请求字符串进行匹配，对特定的请求进行处理。
location / {
    root   html;
    index  index.html index.htm;
}
error_page   500 502 503 504  /50x.html;
location = /50x.html {
```










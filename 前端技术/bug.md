# git

## git clone > HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

```bash
> git clone https://github.com/ximingx/markdown-mark.git

Cloning into 'markdown-mark'...
fatal: unable to access 'https://github.com/ximingx/markdown-mark.git/': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

> git config --global http.version HTTP/1.1
> git clone https://github.com/ximingx/markdown-mark.git
```

## git push > error: failed to push some refs to 'github.com:ximingx/markdown-mark.git'

```bash
> git push

To github.com:ximingx/markdown-mark.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:ximingx/markdown-mark.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

> git 提交冲突,远端代码与本地代码不一致（别人在你提交之前提交了代码，导致你本地现在的代码与远端现在的代码不一致。）
> 将自己新写的代码备份到其他地方。
> 删除本地项目里自己新写的代码。
> git pull 下拉代码，使本地代码与远端代码一致。
> 重新上传代码 
> git add .
> git commit -m "fix bug"
> git push
```

切记：下班前 push 代码，上班后第一件事要 pull 代码

## LibreSSL SSL_read: error:02FFF03C:system library:func(4095):Operation timed out, errno 60

```java
> git push

fatal: unable to access 'https://github.com/ximingx/markdown-mark.git/': LibreSSL SSL_read: error:02FFF03C:system library:func(4095):Operation timed out, errno 60
  
> git config http.postBuffer 524288000
> git config http.sslVerify false
> git push               
```











# Node.js

## TypeError [ERR_INVALID_ARG_TYPE]: The “chunk“ argument must be of type string or an instance of Buff

```js
> // 进行响应的时候 res.end()

(node:5216) UnhandledPromiseRejectionWarning: TypeError [ERR_INVALID_ARG_TYPE]: The "chunk" argument must be of type string or an instance of Buffer. Received an instance of Object
    at ServerResponse.end (_http_outgoing.js:811:13)
    at E:\project\blog\service\app.js:29:13
    at processTicksAndRejections (internal/process/task_queues.js:95:5)
(Use `node --trace-warnings ...` to show where the warning was created)
(node:5216) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--
unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
(node:5216) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.

> // 将 res.end() 修改为 res.send()
```

## Error: Request aborted

```js
// 今天在做网页的时候出现了一个问题，我在项目中添加了一个新的路由企图增加一些功能，在功能代码添加完成后，测试时发现，在提交post请求时，页面一直在加载，这时再去控制台一看报错了：BadRequestError: request aborted

// 后来发现 body-parser 和 express-formidable 组件冲突，会造成 Request Aborted

// 可恶, 一天就这么过去了, 啊啊啊啊啊啊啊啊啊
```

## net::ERR_CONNECTION_REFUSED

```bash
# 在登陆验证的时候出现这么一个问题 
# post http://localhost:3000/action net::ERR_CONNECTION_REFUSED
# 在我仔细地检查了后端, 前端代码后, 以及经过一些列的排查
# 我开始对 req.body 进行判断, 发现她是空的 {}
# 于是我明白了问题的发生在于 前端的请求并没有被解析为 req.body
# 再经过一些列的迷惑操作过后


> 在PM2管理器里面安装express和express-generator模块



# 这里的express-generator模块非常需要注意，我自己在本地运行express项目的时候没有安装这个模块，项目却可以运行。
# 到了服务器上面项目就不可以运行了。如果你是新版本的express，一定要安装这个模块，不然会导致项目无法运行。

# 啊, 无聊的版本知识又增加了
```







# Vue.js

## npm ERR 404 npm ERR 404 ‘@vue/vue-loader-v15@15.9.8‘ is not in the npm registry.

```js
> npm install -D unplugin-vue-components unplugin-auto-import

npm ERR! code E404
npm ERR! 404 Not Found - GET https://registry.npmjs.org/@vue%2Fvue-loader-v15 - Not found
npm ERR! 404
npm ERR! 404  '@vue/vue-loader-v15@15.9.8' is not in the npm registry.
npm ERR! 404 You should bug the author to publish it (or use the name yourself!)
npm ERR! 404 It was specified as a dependency of '@vue/cli-service'
npm ERR! 404
npm ERR! 404 Note that you can also install from a
npm ERR! 404 tarball, folder, http url, or git url.

npm ERR! A complete log of this run can be found in:
npm ERR!     F:\environment\node\node_cache\_logs\2022-04-08T12_51_37_004Z-debug.log

> 删除 node_modules 文件夹
> npm clear --force
> npm i
```

# Mongodb

## MongoDB 服务无法启动。

```bash
> C:\WINDOWS\system32>net start mongodb
MongoDB 服务正在启动 .
MongoDB 服务无法启动。

发生服务特定错误: 100.
```

![image-20220418145143740](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204181451767.png)

```bash
# 确保包含有 data 文件
# 解决方案：进入db文件夹，删除mongod.lock文件，然后重新启动服务即可
> C:\WINDOWS\system32>mongod --logpath="F:\environment\mongodb\mongod.log" --dbpath="F:\environment\mongodb\data" --install --auth
{"t":{"$date":"2022-04-18T06:50:16.538Z"},"s":"I",  "c":"CONTROL",  "id":20697,   "ctx":"-","msg":"Renamed existing log file","attr":{"oldLogPath":"F:\\environment\\mongodb\\mongod.log","newLogPath":"F:\\environment\\mongodb\\mongod.log.2022-04-18T06-50-16"}}

> C:\WINDOWS\system32>net start mongodb
MongoDB 服务正在启动 .
MongoDB 服务已经启动成功。
```


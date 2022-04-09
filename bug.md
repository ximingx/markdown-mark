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

## fatal: unable to access '' Could not resolve host: github.com

```js
> 
  
fatal: unable to access 'https://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@github.com/ximingx/code.git/': Could not resolve host: github.com
  
>
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

```


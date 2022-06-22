> 嗷呜, 预感又是一篇长的水文, 但是内心好激动哦
>
> **适用于前端(了解 node express 框架的人看), 想要了解后端的人看**
>
> 好了, 开始废话模式



# 前后端 token 的使用

>  最近在做一个后台管理项目, 但是我一个卑微的前端我去哪里找接口的, 没有, 只好我自己写
>
> 哎, 我能有什么坏心思呢, 没有

## 1. 了解 JWT

> 利用`token`进行用户身份验证的流程：

- 客户端使用用户名和密码请求登录
- 服务端收到请求，验证用户名和密码
- 验证成功后，服务端会签发一个token，再把这个token返回给客户端
- 客户端收到token后可以把它存储起来，比如放到cookie中
- 客户端每次向服务端请求资源时需要携带服务端签发的token，可以在cookie或者header中携带
- 服务端收到请求，然后去验证客户端请求里面带着的token，如果验证成功，就向客户端返回请求数据

支持跨域访问：`cookie`是无法跨域的，而`token`由于没有用到`cookie`(前提是将`token`放到请求头中)，所以跨域后不会存在信息丢失问题

无状态：`token`机制在服务端不需要存储`session`信息，因为`token`自身包含了所有登录用户的信息，所以可以减轻服务端压力

>  而`JWT`就是上述流程当中`token`的一种具体实现方式，其全称是`JSON Web Token`，官网地址：https://jwt.io/

通俗地说，**JWT的本质就是一个字符串**，它是将用户信息保存到一个Json字符串中，然后进行编码后得到一个`JWT token`，**并且这个`JWT token`带有签名信息，接收后可以校验是否被篡改**，所以可以用于在各方之间安全地将信息作为Json对象传输。

**JWT 的验证证流程：**

- 首先，前端通过Web表单将自己的用户名和密码发送到后端的接口，这个过程一般是一个POST请求。建议的方式是通过SSL加密的传输(HTTPS)，从而避免敏感信息被嗅探
- 后端核对用户名和密码成功后，将包含用户信息的数据作为JWT的Payload，将其与JWT Header分别进行Base64编码拼接后签名，形成一个JWT Token，形成的JWT Token就是一个如同lll.zzz.xxx的字符串
- 后端将JWT Token字符串作为登录成功的结果返回给前端。前端可以将返回的结果保存在浏览器中，退出登录时删除保存的JWT Token即可
- 前端在每次请求时将JWT Token放入HTTP请求头中的Authorization属性中(解决XSS和XSRF问题)
- 后端检查前端传过来的JWT Token，验证其有效性，比如检查签名是否正确、是否过期、token的接收方是否是自己等等
- 验证通过后，后端解析出JWT Token中包含的用户信息，进行其他逻辑操作(一般是根据用户信息得到权限等)，返回结果

> 用案例来了解, 唔, 我把 app.js 拆分成了下面的几个部分, 代码的顺序没有改变, 依次看就可以

```js
/*
 * Start at 2022.4.30
 * Author: ximingx.
 * Github: https://github.com/ximingx
 * Csdn: https://ximingx.blog.csdn.net/
 */

// 导入 express 模块
// 创建 express 的服务器实例
const express = require('express')
const app = express()
const port = process.env.PORT || 2022;
// 跨域设置
const cors = require('cors')
app.use(cors())
// req.body 解析
app.use(express.json());
app.use(express.urlencoded({extended: false}));
```

### 1.1 安装并导入

首先需要我们去安装依赖

```bash
> yarn add jsonwebtoken express-jwt
```

然后导入

```js
// 1. 安装并导入 JWT 相关的两个包, express-jwt版本推荐6.1.1, 最近他更新了, 可能会出现一些意外的问题
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')
```

### 1.2 定义你自己的 secret 密钥

```js
// 2. 定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'ximingx';
```

### 1.3 JWT字符串解析

```js
// 5. JWT字符串解析
// 用于接收到客户端传来的请求, 验证是否含有 token
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 `req.user` 属性上
app.use(expressJWT({secret: secretKey, algorithms: ['HS256']}).unless({path: ['/login', '/register']}))
```

### 1.4 登陆后生成 token

```js
// 登录的路由, 在这里登录成功后, 返回 token 字符串
app.post('/login', (req, res) => {
    // 哎呀,这里就是一个简单的登录测试, 没搞的很复杂
    if (!(req.body.username == 'admin' && req.body.password == "root")) {
        return res.json({
            code: 1,
            msg: '用户名或密码错误'
        })
    }
    // 3. 用户登陆成功后, 需要生成token
    // 参数1：用户的信息对象
    // 参数2：加密的秘钥
    // 参数3：配置对象，可以配置当前 token 的有效期
    const tokenStr = jwt.sign({
        username: req.body.username
    }, secretKey, {expiresIn: '1h'})
    // 返回登陆成功后返回数据
    res.json({
        status: 200,
        message: '登录成功！',
        // 4. 并通过 token 属性发送给客户端
        token: tokenStr,
    })
})
```

### 1.5 验证

```js
// 这里需要这样请求, 否则 token 会无效报错
// axios({
//     method: 'post',
//     url: 'http://localhost:2022/adimin',
//     headers: {
//         'Authorization': 'Bearer ' + token
//     }
// })

// 可以分别用带 token 和不带 token 验证一下

// 这是一个有权限的 API 接口
app.get('/admin', function (req, res) {
    // 6. 使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
    console.log(req.user)
    // {
    //     "status": 200,
    //     "message": "获取用户信息成功！",
    //     "data": {
    //         "username": "admin",
    //         "iat": 1651242605, // 创建时间
    //         "exp": 1651246205 // token 有效期
    //     }
    // }
    res.send({
        status: 200,
        message: '获取用户信息成功！',
        data: req.user, // 要发送给客户端的用户信息
    })
})
```

> 这是不带 token 的请求

![image-20220430114311749](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301143792.png)

> 当我们在登陆后, 获取 token 

![image-20220430114734717](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301147767.png)

> 再次进行测试, 带上 token 就可以啦

![image-20220430115107833](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301151878.png)

### 1.6 捕获 token 过期异常

```js
// 7：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
    // 这次错误是由 token 解析失败导致的
    if (err.name === 'UnauthorizedError') {
        return res.send({
            status: 401,
            message: '无效的token',
        })
    }
    res.send({
        status: 500,
        message: '未知的错误',
    })
})
// 端口号监听, 不重要
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

## 2. 搭建一个简单的后台服务

于是我用了 `node` 的 `express` 框架简单的做了一个服务器

下面是 `app.js` 文件, 看完上面的 jwt 应该就可以很好地理解了

```js
/*
 * Start at 2022.
 * Author: ximingx.
 * Github: https://github.com/ximingx
 * Csdn: https://ximingx.blog.csdn.net/
 */
// 导入 express 模块
// 创建 express 的服务器实例
const express = require('express')
const app = express()
const port = process.env.PORT || 3000;
// 跨域设置
const cors = require('cors')
app.use(cors())
// req.body 解析
app.use(express.json());
app.use(express.urlencoded({extended: false}));
// 加载数据库
require('./db/index');
// 5. JWT字符串解析
const expressJWT = require('express-jwt')
// 2. 定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'ximingx';
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 `req.user` 属性上
app.use(expressJWT({secret: secretKey, algorithms: ['HS256']}).unless({path: ['/api/ximingx/v1/login']}));
// 自定义模块
const {writeLog} = require('./log/log');
// 路由
app.use('/api/ximingx/v1', require('./router/index'));
// 全局捕获错误
app.use((err, req, res, next) => {
    writeLog(err);
    // 这次错误是由 token 解析失败导致的
    if (err.name === 'UnauthorizedError') {
        return res.send({
            status: 401,
            message: '无效的token',
        })
    }
    return res.status(500).send('未知的错误!');
});
// 监听端口
app.listen(3000, () => {
    console.log(`server is running at http://localhost:${port}`);
});
```

> 这是我用于登录验证的路由

```js
// 除了 /api/ximingx/v1/login 其他的路由都需要 token
app.use(expressJWT({secret: secretKey, algorithms: ['HS256']}).unless({path: ['/api/ximingx/v1/login']}));

app.use('/api/ximingx/v1', require('./router/index'));
```

> router.js

```js
const express = require('express');
const router = express.Router();
// 1. 安装并导入 JWT 相关的两个包, express-jwt版本推荐6.1.1, 最近他更新了, 可能会出现一些意外的问题
const jwt = require('jsonwebtoken')
// 2. 定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'ximingx';
// 自定义模块
const {UserLogin, findUser, createUser} = require('../db/user')
const {LoginRegex} = require('../utils/regex')
const {writeLog} = require('../log/log')

router.post('/login', (req, res) => {
    if (!LoginRegex(req.body)) {
        writeLog("Login 参数不支持")
        return res.json({
            title: "register",
            code: 400,
            data: {
                info: "ximingx",
                message: "参数不支持",
            }
        })
    }

    UserLogin(req.body).then(user => {
        if (user == null) {
            return res.json({
                title: "login",
                code: 400,
                data: {
                    info: "ximingx",
                    message: "用户名或者密码错误"
                }
            })
        }
        // 3. 用户登陆成功后, 需要生成token
        // 参数1：用户的信息对象
        // 参数2：加密的秘钥
        // 参数3：配置对象，可以配置当前 token 的有效期
        const tokenStr = jwt.sign({
            username: req.body.username
        }, secretKey, {expiresIn: '1h'})
        res.json({
            title: "login",
            code: 200,
            data: {
                com: "ximingx",
                message: req.body,
                // 4. 并通过 token 属性发送给客户端
                token: tokenStr,
            }
        })
    }).catch(err => {
        writeLog(err)
        return res.json({
            title: "login",
            code: 400,
            dara: {
                info: "ximingx",
                message: "用户名或者密码错误",
            }
        })
    })
});
```

## 3. 前端登录页面

![image-20220430113258699](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301132494.png)

> 这里我们进行请求
>
> axios({
>         url: 'http://localhost:3000/api/ximingx/v1/login',
>         method: 'POST',
>         data: {
>           username: this.username,
>           password: this.password,
>         }
>       })

在登录成功后进行存储

> localStorage.setItem('token', res.data.data.token);

```js
inputInfo: function () {
      let password = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,18}$/;
      let username = /^[a-zA-Z0-9]{3,12}$/;
      if (!(username.test(this.username) && password.test(this.password))) {
        return ElNotification.error('用户名或者密码不合法！');
      }
      axios({
        url: 'http://localhost:3000/api/ximingx/v1/login',
        method: 'POST',
        data: {
          username: this.username,
          password: this.password,
        }
      }).then(res => {
        if (res.data.code == 200) {
          localStorage.setItem('token', res.data.data.token);
          ElNotification({
            title: 'Success',
            message: '登录成功 请稍等...',
            type: 'success',
          });
          this.$router.push({
            path: '/home',
          })
        } else {
          ElNotification.error({
            title: '用户名或者密码错误',
            message: `请重新输入`,
          })
        }
      }).catch(res => {
        ElNotification({
          title: 'Error',
          message: '用户名或者密码错误',
          type: 'error',
        });
      })
    },
```

## 4. 导航守卫

**但是呢, 即使是没有 token, 我们在 url 里输入别的页面仍然会跳转**

 这里就需要我们在前端 router.js 里配置, 判读有无 token, 使别人不能随便的进行别的有权限的页面的访问

```js
// to 从哪一个路径来, from 到哪一个路径去, next 是否继续执行, 表示放行
router.beforeEach((to, from, next) => {
  if (to.path === '/login') {
    return next()
  } else {
    const token = localStorage.getItem('token')
    if (!token) {
      return next('/login')
    }
    return next()
  }
})
```

**但是还是有问题, 别人可以自己加 token 啊**

![image-20220430113920401](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301139459.png)

然后我们就可以快乐的跳转了

![image-20220430114018625](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202204301140661.png)

**所以呢, 最后还应该给导航守卫还应该添加验证**




















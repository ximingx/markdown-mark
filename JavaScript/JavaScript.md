# JavaScript [ 1995  Brendan Eich ]

[Javascript诞生记 -阮一峰]:http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html

- `JavaScript` 的定位

- - `JavaScript` 是脚本编程语言
  - `JavaScript` 是弱类型语言
  - `JavaScript` 是动态类型的
  - `JavaScript` 是单线程的
  - `JavaScript` 解释型语言
  - `JavaScript` 具有良好的跨平台性

- `JavaScript` 和 `ECMAScript` 的区别，以及和 `DOM` 、`BOM` 的关系, JavaScript包含

- - `DOM`（文档对象模型），提供了与网页内容交互的 `方法` 和 `接口`
  - `BOM`（浏览器对象模型），提供了与浏览器交互的 `方法` 和 `接口`
  - `ECMAScript` 描述了 `JavaScript` 的语法和基本对象 (核心)

最后还是引用 `JavaScript高级程序设计` 的那段话，” 要真正学好用好 JavaScript，理解其本质、历史及局限性是非常重要的 “ 

**一起共勉～**

---







## promise

学习 Promise 之前我们需要了解 回调地狱

**多层回调函数的相互嵌套，就形成了回调地狱。**

回调地狱的缺点：

- 代码耦合性太强，牵一发而动全身，难以维护；
- 大量冗余的代码相互嵌套，代码的可读性变差；

---

**Promise 是异步编程的一种优雅的解决方案**，是一个构造函数，有all、reject、resolve这几个方法，原型上有then、catch等方法

### Promise 特点

（1）Promise对象里的异步操作执行时**有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败)** ,而Promise对象状态的改变，只有两种可能：**从pending变为fulfilled或者从pending变为rejected。**

（2）而一旦上面的这种状态发生改变，之后就不会再变，任何时候都可以得到这个结果。**如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果**。

（3） Promise.prototype 上包含一个 `.then()` 方法	**每一次 new Promise() 构造函数得到的实例对象，都可以通过原型链的方式访问到 .then() 方法**, `.then()` 方法用来预先指定成功和失败的回调函数, 也可以 p.then(result => { }, error => { })；这样的方式, 调用 .then() 方法时，成功的回调函数是必选的、失败的回调函数是可选的；

（4）**new 出来的 Promise 实例对象，代表一个异步操作；**

以下案例均在 vue 的代码中演示

```js
  mounted() {
    let promise1 = new Promise(function(resolve, reject){
      //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
      setTimeout(function(){
        console.log('完成异步操作');
        resolve('返回任意的数据');
        // 会在两秒之后返回打印值
      }, 2000);
    })
  }
```

**这里我们 new 了一个 Promise , 在 Promise 里面执行异步操作的代码** 

可以看到,这里**只是对他进行了声明,并没有执行这一个函数**

但是从结果上看来结果 却是执行了 这个函数  ,  这里先忘记里面的  resolve('返回任意的数据');  里起了什么作用

**其执行过程是：执行了一个异步操作，也就是setTimeout，2秒后，输出“完成异步操作”，并且调用resolve方法。这里首先要明白一件事情, Promise 对象的声明会使内部的异步操作发生**

这里需要知道的是:  如果我们直接 new 一个 promise , 而没有将他放置在函数中的时候 , 他会直接执行里面的异步操作

所以我们用Promise的时候一般是包在一个函数中，在需要的时候去运行这个函数 , 这里演示一下

```js
  methods: {
    test:function () {
      return new Promise(function(resolve, reject){
        //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
        setTimeout(function(){
          console.log('完成异步操作');
          resolve('返回任意的数据');
          // 会在两秒之后返回打印值
        }, 2000);
      })
    }
  },
  mounted() {
    this.test()
  }
```

可以看到 在这里 我们直接 return 出  Promise对象 , 这将在在之后给我们非常大的便利 , **可以让我们直接链式调用它的方法**

###  resolve() 的作用

先看一段代码和结果

```js
mounted() {
  let promise = new Promise(function(resolve, reject){
    //做一些异步操作 ( 可以是网络请求,定时器,回调函数,事件绑定 )
    setTimeout(function(){
      resolve('返回任意的数据');
      // 会在两秒之后返回打印值
    }, 2000);
  }).then((data) => {
    console.log(data)
  })
}
```


我们可以发现在之后的 .then(data) 中有一句 console.log(data)

这这里的 **data 对应的正是 resolve() 参数中返回的值** , **原来then里面的函数就跟我们平时的回调函数一个意思，能够在这个异步任务执行完成之后被执行.** 而这也这就是Promise的作用了，**用链式调用的方式执行回调函数。**

而 Promise的优势正是在于可以链式调用 , 可以在then方法中继续写Promise对象并返回，然后继续调用then来进行回调操作。

但是 + - +

```js
  mounted() {
    return new Promise(function (resolve, reject) {
      if (1 < 2) {
        resolve(true)
      } else {
        console.log("error")
      }
    }).then((data) => {
      console.log(data)
      return new Promise(function (resolve, reject) {
        if (2 < 3) {
          resolve(true)
        } else {
          console.log("error")
        }
      })
    }).then((data) => {
      console.log(data)
      return new Promise(function (resolve, reject) {
        if (2 < 3) {
          resolve(true)
        } else {
          console.log("error")
        }
      }).then((data) => {
        console.log(data)
      })
    })
  }
```

上面这样子的代码  是不是很丑 , 很难看懂 + - + , 而且和之前的回调地狱一样不方便读懂代码

但是实际上 不这么搞

### 我们一般采用下面的写法

```js
  methods: {
    test:function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        },1000)
      })
    }
  },
  mounted() {
    this.test()
        .then((data) => {
          console.log(data)
          // 返回 Promise 对象, 使其继续进行链式调用 
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
        })
  }
```

这样就能够按顺序,输出每个异步回调中的内容

每次 .then 中的 return 都可以返回一个 Promise , 从而可以在之后继续链式调用  , 这样写是不是就很好看了


### reject() 的用法

**resolve是对promise成功执行时候的回调,它把promise的状态修改为fullfiled**

那么，**reject就是失败的时候的回调，他把promise的状态修改为rejected**，这样我们就可以在 .then中 捕捉到，然后执行“失败”情况的回调

```js
  methods: {
    test:function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        },1000)
      })
    }
  },
  mounted() {
    this.test()
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return this.test()
        })
        .then((data) => {
          console.log(data)
          return new Promise((resolve, reject) => {
            if ( 1 !== 1) {
              reject(1);
            } else {
              resolve(2);
            }
          })
        })
       .then((data) => {
         console.log(data)
       },(info) => {
         console.log(info)
       })
  }
```

这里在最后一次调用 promise 返回的结果时 , 执行力 resolve(2) , 最后打印台显示的结果也是 2 ,

而且我们也可以看到 , 在then中传了两个参数，这两个参数分别是两个函数，then方法可以接受两个参数，**第一个对应resolve的回调，第二个对应reject的回调。（也就是说then方法中接受两个回调，一个成功的回调函数，一个失败的回调函数）**，所以我们能够分别拿到成功和失败传过来的数据就有以上的运行结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/b7cc3321da2348b981fdedfcf2bb6b3a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

接下来我们再看一下 .catch 和 直接在 .then 中传入第二个参数的区别

```js
methods: {
  test: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 1000)
    })
  }
},
mounted() {
  this.test()
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return this.test()
      })
      .then((data) => {
        console.log(data)
        return new Promise((resolve, reject) => {
          if (1 !== 1) {
            reject(1);
          } else {
            resolve(2);
          }
        })
      })
      .then((data) => {
        console.log(data)
      })
      .catch((info) => {
        console.log(info)
      })
}
```

我们可以看到: 两次结果是一样的 , 但是我们需要明白 , 在 .then 中写第二个参数 和 用 .catch 是有区别的

.catch 除了会得到失败的结果,还会捕获异常 , 类似于一些语法的错误 , 在捕获到异常的时候 , 并不会卡死 , 而是继续执行下面的代码
**与then同级的另一个方法，all方法，该方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后并且执行结果都是成功的时候才执行回调。**

###  all() 多个Promise 一起执行

```js
  methods: {
    test1: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    },
    test2: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    },
    test3: function () {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 1000)
      })
    }
  },
  mounted() {
      // 用一个数组包括
    Promise.all([this.test1, this.test2, this.test3])
        .then((res) => {
          console.log(res)
          console.log(res.length)
        })
  }
```

这里在三个异步方法都执行完毕后 , 返回了一个数组 , 里面包含了每个方法对应的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/d48a26607ee24c4f942a96e9a45d7c4a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


Promise.all来执行多个异步操作，**all接收一个数组参数**，这组参数为需要执行异步操作的所有方法，**里面的值最终都算返回Promise对象。**

这样，**三个异步操作的并行执行的，等到它们都执行完后才会进到then里面**。

**数组中 Promise 实例的顺序，就是最终结果的顺序！**

### 除此之外还有 race 的 用法

all是等所有的异步操作都执行完了再执行then方法，那么race方法就是相反的，**谁先执行完成就先执行回调**。先执行完的不管是进行了race的成功回调还是失败回调，**其余的将不会再进入race的任何回调**

```js
methods: {
  test1: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 1000)
    })
  },
  test2: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 2000)
    })
  },
  test3: function () {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(1);
      }, 3000)
    })
  }
},
mounted() {
  Promise.race([this.test1, this.test2, this.test3])
      .then((res) => {
        console.log(res)
      })
}
```

这次只是 将 Promise.all 修改为了 Promise.race , 返回的结果中 只有最先执行结束的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/94290eb4a81246a988b7852feac0c76e.png)

**补充:**


```js
// Promise 用于解决回调地狱
// Promise 是一个构造函数
const fs = require('fs')
// 在 promise 容器 里的函数 里放置异步操作
// promise 容器一旦创建就开始执行里面的代码
new Promise(function (resolve, reject) {
  fs.readFile('./package.json', 'utf8', function (err, data) {
    if (err) {
     reject(err)
    } else {
      resolve(data)
    }
  })
}).then(data => {
  console.log(data);
  // -----------------------------------------------------------------------
  new Promise(function (resolve,reject) {
    fs.readFile('./package.json', 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  }).then(data => {
    console.log(data);
  }).catch (err => {
    console.log(err);
  })
  // -----------------------------------------------------------------------
}).catch(err => {
  console.log(err);
})
```

**异步的处理方式**

```js
const fs = require("fs");

const p1 = new Promise((resolve, reject) => {
  fs.readFile('./a.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

const p2 = new Promise((resolve, reject) => {
  fs.readFile('./b.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

const p3 = new Promise((resolve, reject) => {
  fs.readFile('./c.txt', "utf8", (err, data) => {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

p1.then((data) => {
    console.log(data);
  // 这里的 return p2 会将 p2 的 resolve 结果 传递给下面的 .then
  // 当 return 一个 promise 对象时,后续的 .then 中方法的第一个参数会作为 返回的 promise (p2) 的 resolve
    return p2
})
  .catch((err) => {
    console.log(err);
  })
  .then(data => {
    console.log(data);
    return p3
  })
  .catch((err) => {
    console.log(err);
  })
  .then(data => {
    console.log(data);
  })
  .catch((err) => {
    console.log(err);
  })
```

**异步函数的封装**

```js
const fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, "utf8", function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./a.txt')
  .then(data => {
    console.log(data);
    return pReadFile('./b.txt')
  })
  .then((data) => {
    console.log(data);
    return pReadFile('./c.txt')
  })
  .then((data) => {
    console.log(data);
  })
```

**Promise 在创建后会立马执行**
下面代码中，Promise 新建后立即执行，所以首先输出的是Promise。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出。
注意结果的输出顺序
```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```

---

### 读取多个文件 (案例)

由于 node.js 官方提供的 fs 模块仅支持以回调函数的方式读取文件，不支持Promise 的调用方式。因此，需要先运行如下的命令，安装 `then-fs` 这个第三方包，从而支持我们基于 Promise 的方式读取文件的内容：

```bash
npm install then-fs
```

调用 then-fs 提供的 `readFile()` 方法，可以异步地读取文件的内容，它的返回值是 Promise 的实例对象。因此可以调用 `.then()` 方法为每个 Promise 异步操作指定成功和失败之后的回调函数。示例代码如下：

```js
import thenFS from 'then-fs'
thenFS.readFile("./1.text", "utf8").then(r1 => {
    console.log(r1)
})
thenFS.readFile("./1.text", "utf8").then(r2 => {
    console.log(r2)
})
thenFS.readFile("./1.text", "utf8").then(r3 => {
    console.log(r3)
})
```

上述的代码无法保证文件的读取顺序，需要做进一步的改进！

`Promise` 支持链式调用，从而来解决回调地狱的问题。示例代码如下：

```js
import thenFS from 'then-fs'
thenFS.readFile("./1.text", "utf8")
  .catch(err => {
    console.log(err)
})
  .then(r1 => {
    console.log(r1)
    return thenFS.readFile("./2.text", "utf8")
}).then(r2 => {
    console.log(r2)
    return thenFS.readFile("./3.text", "utf8")
}).then(r3 => {
    console.log(r3)
})
```



## async/await

终究是放弃了写 Promise

**`async/await`** 是 **ES8（ECMAScript 2017）引入的新语法**，用来简化 Promise 异步操作。在 `async/await` 出现之前，开发者只能通过链式.then() 的方式处理 Promise 异步操作。

### 基本使用

使用 `async/await` 简化 Promise 异步操作的示例代码如下

async关键字

1. 普通函数定义前加async关键字 普通函数变成异步函数
2. 异步函数默认返回promise对象
3. 在异步函数内部使用return关键字进行结果返回 结果会被包裹的promise对象中 return关键字代替了resolve方法
4. 在异步函数内部使用throw关键字抛出程序异常
5. 调用异步函数再链式调用then方法获取异步函数执行结果
6. 调用异步函数再链式调用catch方法获取异步函数执行的错误信息

await关键字

1. await关键字只能出现在异步函数中
2. await promise await后面只能写promise对象 写其他类型的API是不不可以的
3. await关键字可是暂停异步函数向下执行 直到promise返回结果

```js
const thenFs = require("then-fs");
async function get() {
  // throw 后, 后面的代码不执行
  throw '错误';
  const r1 =  await thenFs.readFile("./yarn.lock");
  console.log(r1.toString());
  const r2 =  await thenFs.readFile("./1.js");
  console.log(r2.toString());
  const r3 =  await thenFs.readFile("./1.html");
  console.log(r3.toString());
  return {
      r1,
      r2,
      r3
  } 
}
  
    
get()
   .then(data => {
    console.log(data)
}).catch(err => {
     console.log(err)
});
```

**如果在 function 中使用了 await，则 function 必须被 async 修饰；**



## EventLoop

JavaScript 是一门单线程执行的编程语言。也就是说，同一时间只能做一件事情。

单线程执行任务队列的问题：如果前一个任务非常耗时，则后续的任务就不得不一直等待，从而导致程序假死的问题。

一般而言，任务分为：发出调用和得到结果两步。

- 发出调用，“立即”得到结果是为同步
- 发出调用，但无法“立即”得到结果，需要额外的操作才能得到预期的结果是为异步。

为了防止某个耗时任务导致程序假死的问题，**JavaScript 把待执行的任务分为了两类：**

- **同步任务（synchronous）**

又叫做非耗时任务，指的是在主线程上排队执行的那些任务；

- **异步任务（asynchronous）**

又叫做耗时任务，异步任务由JavaScript 委托给宿主环境进行执行；
当异步任务执行完成后，会通知 JavaScript 主线程执行异步任务的回调函数；

**JS 执行栈采用的是后进先出的规则，当函数执行的时候，会被添加到栈的顶部，当执行栈执行完成后，就会从栈顶移出，直到栈内被清空。**

执行过程: 

- 首先任务会依次进入**执行栈**，而首先入场的就是宏任务全局上下文, 然后执行 js 主线程中的同步任务
- 将异步任务委托给宿主环境执行
- 已完成的异步任务会把它对应的回调函数放到任务队列中等待执行
- **当 js 主线程执行栈执行完毕**, 查看执行栈是否为空，如果执行栈为空
- **先检查**微任务(microTask)队列，如果存在任务，则**一次性执行完所有**微任务，无任务则跳过
- **后检查**宏任务(macroTask)队列，如果存在任务，则**取出第一个**宏任务，执行，
- 主线程不断重复上述操作

**JavaScript 主线程从“任务队列”中读取异步任务的回调函数，放到执行栈中依次执行。这个过程是循环不断的，所以整个的这种运行机制又称为 EventLoop（事件循环）。**

然而异步任务的也做了进一步的划分

1. **宏任务（macrotask）**

- 异步 Ajax 请求、
- setTimeout、setInterval、
- 文件操作
- 其它宏任务

2.  **微任务（microtask）**

- Promise.then、.catch 和 .finally
- process.nextTick
- 其它微任务

**每一个宏任务执行完之后，都会检查是否存在待执行的微任务，如果有，则执行完所有微任务之后，再继续执行下一个宏任务。**

可以简单的把宏任务认为进程, 微任务认为是线程的感觉

```js
console.log(1)
setTimeout(() => {
  console.log(2)
  new Promise(function (resolve) {
    console.log(3)
    resolve()
  }).then(() => {
    console.log(4)
  })

})

new Promise((resolve) => {
  console.log(5)
  resolve()
}).then(() => {
  console.log(6)
})

setTimeout(() => {
  console.log(7)
  new Promise(function (resolve) {
    console.log(8)
    resolve()
  }).then(() => {
    console.log(9)
  })
})

// 156234789
```





## Es6

### Symbol

#### 概述

背景：ES5中对象的属性名都是字符串，容易造成重名，污染环境。

**概念**：ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

**特点：**

- Symbol属性对应的值是唯一的，解决**命名冲突问题**

- Symbol值不能与其他数据进行计算，包括同字符串拼串

- for in、for of 遍历时不会遍历Symbol属性。

#### 1. 创建Symbol属性值

Symbol是函数，但并不是构造函数。创建一个Symbol数据类型：

```javascript
    let mySymbol = Symbol();

    console.log(typeof mySymbol);  //打印结果：symbol
    console.log(mySymbol);         //打印结果：Symbol()
```

#### 2. 将Symbol作为对象的属性值

```javascript
    let mySymbol = Symbol();

    let obj = {
        name: 'smyhvae',
        age: 26
    };

    //obj.mySymbol = 'male'; //错误：不能用 . 这个符号给对象添加 Symbol 属性。
    obj[mySymbol] = 'hello';    //正确：通过属性选择器给对象添加 Symbol 属性。后面的属性值随便写。

    console.log(obj);
```

上面的代码中，我们尝试给obj添加一个Symbol类型的属性值，但是添加的时候，不能采用`.`这个符号，而是应该用`属性选择器`的方式。

#### 3. 创建Symbol属性值时，传参作为标识

如果我通过 Symbol()函数创建了两个值，这两个值是不一样的：

```javascript
    let mySymbol1 = Symbol();
    let mySymbol2 = Symbol();

    console.log(mySymbol1 == mySymbol2); //打印结果：false
    console.log(mySymbol1);         //打印结果：Symbol()
    console.log(mySymbol2);         //打印结果：Symbol()
```

上面代码中，倒数第三行的打印结果也就表明了，二者的值确实是不相等的。

最后两行的打印结果却发现，二者的打印输出，肉眼看到的却相同。那该怎么区分它们呢？

既然Symbol()是函数，函数就可以传入参数，我们可以通过参数的不同来作为**标识**。比如：


```javascript
    //在括号里加入参数，来标识不同的Symbol
    let mySymbol1 = Symbol('one');
    let mySymbol2 = Symbol('two');

    console.log(mySymbol1 == mySymbol2); //打印结果：false
    console.log(mySymbol1);         //打印结果：Symbol(one)
    console.log(mySymbol2);         //打印结果：Symbol(two)
    console.log(mySymbol2.toString());//打印结果：Symbol(two)
```

#### 4. 定义常量

Symbol 可以用来定义常量：


```javascript
    const MY_NAME = Symbol('my_name');
```

#### 5. 内置的 Symbol 值

除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法。

- `Symbol.iterator`属性

对象的`Symbol.iterator`属性，指向该对象的默认遍历器方法。



### 将ES6转为ES5 (Babel)

> 掌握 ES6 之后，如果你的业务需要考虑 ES5 的兼容性，则可以这样做：写 ES6 语法的 js 代码，然后通过 `Babel`将 ES6 转换为 ES5。如果没有这样的需要，那么下面的内容，了解即可。

babel 的作用是将 ES6 语法转为 ES5 语法，支持低端浏览器。

以一个简单的案例说明

#### 1. 先创建一个项目的目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/bdd90d76902b4db0afddebd454609192.png)
在 index.js 写入

```js
let a = item => item + 2
console.log(a(4))
```

这个文件是一个 ES6 语法 的 js 文件，稍后，我们尝试把这个 ES6 语法的 js 文件转化为 ES5 的 js 文件。



#### 2. 安装 Babel-cli

初始化项目：

在安装 Babel 之前，需要先用 npm init 先初始化我们的项目。打开终端或者通过 cmd 打开命令行工具，进入项目目录，输入如下命令：

```bash
	npm init -y
```

上方代码中，`-y` 代表全部默认同意，就不用一次次按回车了（稍后再根据需要，在文件中手动修改）。命令执行完成后，会在项目的根目录下生成 package.json 文件：

```json
{
  "name": "babel",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```
#### 3. 本地安装 

```bash
	npm install --save-dev babel-preset-es2015 babel-cli
```

#### 4. 新建.babelrc：

在根目录下新建文件`.babelrc`，输入如下内容：

```js
{
    "presets":[
        "es2015"
    ],
    "plugins":[]
}
```

#### 5. 开始转换：

现在，我们应该可以将 ES6 的文件转化为 ES5 的文件了，命令如下：（此命令略显复杂）

```bash
	babel src/index.js -o dist/index.js
```

我们可以将上面这个命令进行简化一下。操作如下：

在文件 `package.json` 中修改键 `scripts`中的内容：

```json
  "scripts": {
    "build": "babel src/index.js -o dist/index.js"
  },
```

目前为止，环境配置好了。以后，我们执行如下命令，即可将`src/index.js`这个 ES6 文件转化为 `dist/index.js`这个 ES5 文件：

```bash
	npm run build
```

我们执行上面的命令之后，会发现， dist 目录下会生成 ES5 的 js 文件：

之后我们就可以在 index.html 中使用 es5的语法了

```js
"use strict";

var a = function a(item) {
  return item + 2;
};
console.log(a(4));
```

### ES6 模块化

ES6 模块化规范是浏览器端与服务器端通用的模块化开发规范。它的出现极大的降低了前端开发者的模块化学习成本，开发者不需再额外学习 AMD、CMD 或 CommonJS 等模块化规范。

ES6 模块化规范中定义：

- 每个 js 文件都是一个独立的模块
- 导入其它模块成员使用 import 关键字
- 向外共享模块成员使用 export 关键字

node.js 中默认仅支持 CommonJS 模块化规范，若想基于 node.js 体验与学习 ES6 的模块化语法，可以按照如下两个步骤进行配置：

- 确保安装了 v14.15.1 或更高版本的 node.js；
- 在 package.json 的根节点中添加 "type": "module" 节点；

ES6 的模块化主要包含如下 3 种用法：

1. 默认导出与默认导入
2. 按需导出与按需导入
3. 直接导入并执行模块中的代码

#### 默认导入默认导出

默认导出的语法：**export default 默认导出的成员**

```js
let n1 = 1;
function foo() {
  
}
export default {
  n1,
  foo
}
```

默认导出的注意事项：每个模块中，只允许使用唯一的一次 export default，否则会报错！

默认导入的语法：**import 接收名称 from ‘模块标识符’**

```js
import m1 from "./1.js"

m1.n1

m1.foo()
```

默认导入时的接收名称可以任意名称，只要是合法的成员名称即可；

#### 按需导出与按需导入

按需导出的语法：**export 按需导出的成员**

```js
export let s1 = 1;
export function add() {
  
}


// 导入
import { s1,add } from "./1.js"
```

1. 每个模块中可以使用多次按需导出；
2. **按需导入的成员名称必须和按需导出的名称保持一致；**
3. **按需导入时，可以使用 as 关键字进行重命名；**
4. 按需导入可以和默认导入一起使用；

#### 直接导入并执行模块中的代码

如果只想单纯地执行某个模块中的代码，并不需要得到模块中向外共享的成员。

```js
import "./1.js"
```





## 作用域（Scope）的概念和分类

-   **概念**：通俗来讲，作用域是一个变量或函数的作用范围。作用域在**函数定义**时，就已经确定了。换句话说，作用域决定了代码区块中变量和其他资源的可见性。

-   **目的**：为了提高程序的可靠性，同时减少命名冲突。

在 JS 中，一共有两种作用域：（ES5 中）

-   **全局作用域**：作用于整个 script 标签内部，或者作用于一个独立的 JS 文件。
-   **函数作用域**（局部作用域）：作用于函数内的代码环境。



### 全局作用域 和 window 对象

直接编写在 script 标签中的 JS 代码，都在全局作用域。全局作用域在页面打开时创建，在页面关闭时销毁。

在全局作用域中有一个全局对象 window，它代表的是一个浏览器的窗口，由浏览器创建，我们可以直接使用。相关知识点如下：

-   创建的**变量**都会作为 window 对象的属性保存。比如在全局作用域内写 `var a = 100`，这里的 `a` 等价于 `window.a`。
-   创建的**函数**都会作为 window 对象的方法保存。

### 作用域的访问关系

在内部作用域中可以访问到外部作用域的变量，在外部作用域中无法访问到内部作用域的变量。

代码举例：

```javascript
var a = 'aaa';
function foo() {
    var b = 'bbb';
    console.log(a); // 打印结果：aaa。说明 内层作用域 可以访问 外层作用域 里的变量
}

foo();
console.log(b); // 报错：Uncaught ReferenceError: b is not defined。说明 外层作用域 无法访问 内层作用域 里的变量
```

### 变量的作用域

根据作用域的不同，变量可以分为两类：全局变量、局部变量。

**全局变量**：

-   在全局作用域下声明的变量，叫「全局变量」。在全局作用域的任何一地方，都可以访问这个变量。

-   在全局作用域下，使用 var 声明的变量是全局变量。

-   **特殊情况：在函数内不使用 var 声明的变量也是全局变量（不建议这么用）。** (~ ~ ~最好不要哇, 因为他还有一个条件: 必须先调用函数之后才可以使用该变量)

```js
function outFun1() {
    variable1 = "未定义直接赋值的变量";
}
function outFun2() {
    variable2 = "未定义直接赋值的变量";
}
outFun2();//要先执行这个函数，否则根本不知道里面是啥
console.log(variable2); //未定义直接赋值的变量
console.log(variable1); //variable1 is not defined
```

**局部变量**：

-   **定义在函数作用域的变量，叫「局部变量」。仅限函数内部访问这个变量。**

-   在函数内部，使用 var 声明的变量是局部变量。

-   函数的**形参**也是属于局部变量。

从执行效率来看全局变量和局部变量：

-   全局变量：只有浏览器关闭时才会被销毁，比较占内存。

-   局部变量：当其所在的代码块运行结束后，就会被销毁，比较节约内存空间。

### 作用域的上下级关系

当在函数作用域操作一个变量时，它会先在自身作用域中寻找，如果有就直接使用（**就近原则**）。如果没有则向上一级作用域中寻找，直到找到全局作用域；如果全局作用域中依然没有找到，则会报错 ReferenceError。

在函数中要访问全局变量可以使用 window 对象。（比如说，全局作用域和函数作用域都定义了变量 a，优先使用的是函数中的a , 但如果想访问全局变量，可以使用`window.a`）

### 作用域的预处理

**预处理（预解析）**的概念：浏览器在解析 JS 代码之前，会进行一个操作叫“预处理（预解析）”：将当前 JS 代码中所有变量的定义和函数的定义，放到所有代码的最前面。

这种预解析，也称之为声明提前。

### 全局作用域-变量的声明提前（变量提升）

使用 var 关键字声明的变量（ 比如 `var a = 1`），**会在所有的代码执行之前被声明**（但是不会赋值），但是如果声明变量时不是用 var 关键字（比如直接写`a = 1`），则变量不会被声明提前。

**举例 1**：

```javascript
// 这里并没有报错
console.log(a);
var a = 123;
```

打印结果：undefined。注意，打印结果并没有报错，而是 undefined，说明变量 a 被提前声明了，只是尚未被赋值。

**举例 2**：

```javascript
console.log(a);
// 没有使用var声明
a = 123; 
```

程序会报错：`Uncaught ReferenceError: a is not defined`。

**举例 3**：

```javascript
a = 123; //此时a相当于window.a
console.log(a);
```

打印结果：123。

**注意 2 和 3 的差别**

**举例 4**：

```javascript
foo();

function foo() {
    if (false) {
        var i = 123;
    }
    console.log(i);
}
```

打印结果：undefined。注意，打印结果并没有报错，而是 undefined。这个例子，再次说明了：变量 i 在函数执行前，就被提前声明了，只是尚未被赋值。

例 4 中， `if(false)`里面的代码虽然不会被执行，但是整个代码有**解析**的环节，解析的时候就已经把 变量 i 给提前声明了。

**总结**：

既然 JS 中存在变量提升的现象，那么，在实战开发中，为了避免出错，建议先声明一个变量，然后再使用这个变量。

### 全局作用域-函数的声明提前

**函数声明**：

使用`函数声明`的形式创建的函数`function foo(){}`，**会被声明提前**。

**也就是说，整个函数会在所有的代码执行之前就被创建完成**。所以，在代码顺序上，我们可以先调用函数，再定义函数。

代码举例：

```javascript
fn1(); // 虽然 函数 fn1 的定义是在后面，但是因为被提前声明了， 所以此处可以调用函数

function fn1() {
    console.log('我是函数 fn1');
}
```

**函数表达式**：

使用`函数表达式`创建的函数`var foo = function(){}`，**不会被声明提前**，所以不能在声明前调用。

很好理解，因为此时 foo 被声明了（这里只是变量声明），且为 undefined，并没有把 `function(){}` 赋值给 foo。

### 函数作用域的预处理

1、在函数作用域中，也有声明提前的特性：

-   函数中，使用 var 关键字声明的变量，会在函数中所有的代码执行之前被声明。

-   函数中，没有 var 声明的变量都是**全局变量**，而且并不会提前声明。

举例：

```javascript
var a = 1;

function foo() {
    console.log(a);
    a = 2; // 此处的a相当于window.a
}

foo();
console.log(a); //打印结果是2
```

上方代码中，执行 foo() 后，函数里面的打印结果是`1`。如果去掉第一行代码，执行 foo() 后，函数里面的打印结果是`Uncaught ReferenceError: a is not defined`。

2、定义形参就相当于在函数作用域中声明了变量。

```javascript
function fun6(e) {
    // 这个函数中，因为有了形参 e，此时就相当于在函数内部的第一行代码里，写了 var e;
    console.log(e);
}

fun6(); //打印结果为 undefined
fun6(123); //打印结果为123
```

注意一些重复声明时的问题

```js
var scope = "global";
function fn(){
    console.log(scope);//undefined
    var scope = "local";
    console.log(scope);//local;
}
fn();

```


### JavaScript 没有块级作用域（ES6 之前）

在其他编程语言中（如 Java、C#等），存在块级作用域，由`{}`包括起来。比如在 Java 语言中，if 语句里创建的变量，只能在 if 语句内部使用：

```java
if(true) {
    Sting str = "123";
    system.out.print(num); // 123
}
system.out.print(num); // 报错
```

但是，在 JS 中没有块级作用域（ES6 之前）。举例如下：

```javascript
if (true) {
    var num = 123;
    console.log(123); //123
}

console.log(num); //123（可以正常打印）
```

### 作用域链

引入：

-   只要是代码，就至少有一个作用域

-   写在函数内部的局部作用域

-   如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域

基于上面几条内容，我们可以得出作用域链的概念。

**作用域链**：内部函数访问外部函数的变量，采用的是链式查找的方式来决定取哪个值，这种结构称之为作用域链。查找时，采用的是**就近原则**。

代码举例：

```javascript
var num = 10;

function fn() {
    // 外部函数
    var num = 20;

    function fun() {
        // 内部函数
        console.log(num);
    }
    fun();
}
fn();
```

打印结果：20。


### 块级作用域 (ES6新增)

块级作用域可通过新增命令let和const声明，所声明的变量在指定块的作用域外无法被访问。块级作用域在如下情况被创建：

1. 在一个函数内部
2. 在一个代码块（由一对花括号包裹）内部

### 块级作用域有以下几个特点：
**声明变量不会提升到代码块顶部**

错误示范: 

```js
// ReferenceError: Cannot access 'a' before initialization
console.log(a) 
let a = 1
```

**禁止重复声明**

如果一个标识符已经在代码块内部被定义，那么在此代码块内使用同一个标识符进行 let 声明就会导致抛出错误。例如：

```js
var count = 30;
let count = 40;
// Uncaught SyntaxError: Identifier 'count' has already been declared 
```


### let var 区别

var定义的变量，没有块的概念，可以跨块访问, 不能跨函数访问。

let, const 定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问。

```js
{
    var a = 1;
    let b = 2;
    const c = 3;

    {
        console.log(a);		// 1	子作用域可以访问到父作用域的变量
        console.log(b);		// 2	子作用域可以访问到父作用域的变量
        console.log(c);		// 3	子作用域可以访问到父作用域的变量

        var aa = 11;
        let bb = 22;
        const cc = 33;
    }

    console.log(aa);	// 11	// 可以跨块访问到子 块作用域 的变量
    // console.log(bb);	// 报错	bb is not defined
    // console.log(cc);	// 报错	cc is not defined
}
```

### js 函数预编译

> 预编译简单理解就是在内存中开辟一些空间，存放一些变量与函数
> 预编译会在script代码内执行前发生了, 但是它大部分会发生在函数执行前

预编译四部曲：

1. 函数在运行的瞬间，生成一个执行期上下文 （Active Object），简称AO；

2. 分析参数
    2.1 函数接收形式参数，添加到AO的属性，并且这个时候值为undefine,例如AO.age=undefined;
    2.2 接收实参，添加到AO的属性，覆盖之前的undefined;

3. 分析变量声明，如var age;或var age=23;
    3.1 如果上一步分析参数中AO还没有age属性，则添加AO属性为undefined，即AO.age=undefined;
    3.2 如果AO上面已经有age属性了，则不作任何修改;


4. 分析函数的声明，如果有function age(){}；把函数赋给AO.age ,覆盖上一步分析的值;


```js
 function fn(a){
    console.log(a);
    var a = 123;
    console.log(a);
    
    function a(){};
    console.log(a);
    
    var b = function(){};
    console.log(b);
    
    function d(){};
 }
 
 //调用函数
 fn(1);
```

创建AO对象

```js
AO{
    //空对象    
}
```

找形参和变量声明

```js
AO{
    a : undefined,
    b : undefined
}
```

只将实参赋值给形参

```js
AO{
    a : 1,
    b : undefined
}
```

找函数声明, 覆盖

```js
AO{
    a : function a(){},
    b : undefined,
    d : function d(){}
}
```
预编译环节就此结束，此时的AO对象已经更新为：

```js
AO{
    a : function a(){},
    b : undefined,
    d : function d(){}
}
```
函数开始逐行顺序执行：
```js
 function fn(a){
    console.log(a);// 输出functiona(){}
    var a = 123;//执行到这里重新对a赋，AO对象再一次更新
    console.log(a);// 输出123
    
    function a(){};//预编译环节已经进行了变量提升，故执行时不在看这行代码
    console.log(a);// 输出123
    
    var b = function(){};//这个是函数表达式不是函数声明，故不能提升，会对AO中的b重新赋值
    console.log(b);//输出function(){}
    
    function d(){};
 }
```
至此，函数执行完毕，销毁AO对象。

### 一个有意思的案例

```js
function foo() {
    var a = b = 100; // 连续赋值
}

foo();

console.log(window.b); // 在全局范围内访问 b
console.log(b); // 在全局范围内访问 b，但是前面没有加 window 这个关键字

console.log(window.a); // 在全局范围内访问 a
console.log(a); // 在全局范围内访问 a，但是前面没有加 window 这个关键字
```

结果: 

```js
100

100

undefined

（会报错，提示 Uncaught ReferenceError: a is not defined）
```

**解释**：

当执行了`foo()`函数之后， `var a = b = 100` 这行**连续赋值**的代码等价于 `var a = (b = 100)`，其执行顺序是：

（1）先把 100 赋值给 b；

（2）再声明变量 a；

（3）再把 b 的值赋值给 a。

我们可以看到，b 是未经声明的变量就被赋值了，此时，根据规律1，这个 b 是属于 `window.b`；而 a 的作用域仅限于 foo() 函数内部，不属于 window。所以也就有了这样的打印结果。

### 推荐

[JavaScript预编译原理分析](https://blog.csdn.net/q1056843325/article/details/52951114)

## Node 节点

### 1. 先解释清楚节点与元素

**节点**（Node）：构成 `HTML `网页的最基本单元。网页中的每一个部分都可以称为是一个节点，比如：`html`标签、属性、文本、注释、整个文档等都是一个节点。

虽然都是节点，但是实际上他们的具体类型是不同的。常见节点分为四类：

- 文档节点（文档）：整个 `HTML` 文档。整个 `HTML` 文档就是一个文档节点。

- 元素节点（标签）：`HTML`标签。

- 属性节点（属性）：元素的属性。

- 文本节点（文本）：`HTML`标签中的文本内容（包括标签之间的空格、换行）。

节点的类型不同，属性和方法也都不尽相同。所有的节点都是`Object`。

**总的来说:** 

**元素（element）**：页面中所有的**标签,每个`html`标签都是一个元素**

**节点（node）**：页面中所有的内容，包括标签、属性（标签的属性）、文本(文字,换行,空格,回车)) **即使元素也是节点**

**nodeType**:节点的类型

- **nodeType == 1  表示的是元素节点**（标签） 。记住：在这里，元素就是标签。

- nodeType == 2  表示是属性节点。

- nodeType == 3  是文本节点。
![在这里插入图片描述](https://img-blog.csdnimg.cn/ad987c77522c40719c1c75ef50392bbf.png)


---
### 2. 什么是`DOM`

**`DOM`**：Document Object Model，文档对象模型。`DOM` 为文档提供了结构化表示，并定义了如何通过脚本来访问文档结构。目的其实就是为了能让js操作html元素而制定的一个规范。

而 `DOM` 就是由节点组成的。

**解析过程**：
HTML加载完毕，渲染引擎会在内存中把HTML文档，生成一个DOM树，getElementById是获取内中DOM上的元素节点。然后操作的时候修改的是该元素的**属性**。


---

### 3. 获取节点
节点的访问关系，是以**属性**的方式存在的。

#### 获取父节点

调用者就是节点。一个节点只有一个父节点，调用方式就是

```js
	node.parentNode
```

#### 获取兄弟节点
| 方法                   | 说明               |
| ---------------------- | ------------------ |
| nextElementSibling     | 获取下一个元素节点 |
| previousElementSibling | 获取上一个元素节点 |

> 获得任意一个兄弟节点：
> **节点自己.parentNode.children[index];**  

####  获取单个的子节点
| 方法              | 说明                   |
| ----------------- | ---------------------- |
| firstElementChild | 获取第一个子元素节点   |
| lastElementChild  | 获取最后一个子元素节点 |


#### 获取所有的子节点

| 方法       | 说明                                                       |
| ---------- | ---------------------------------------------------------- |
| childNodes | 指定元素的子节点的集合（包括元素节点、所有属性、文本节点） |
| children   | 子元素节点的集合, 只返回HTML节点，甚至不返回文本节点。     |


### 4. 节点的操作

#### 创建节点

```javascript
	新的标签(元素节点) = document.createElement("标签名");
```

#### 插入节点

> 父节点的最后插入一个新的子节点。
> 但是需要注意: 一个已经存在的节点插入另一个已经存在的节点, 被插入的原节点的位置会消失

```javascript
	父节点.appendChild(新的子节点);
```

> 在参考节点前插入一个新的节点。
> 如果参考节点为null，那么他将在父节点里面的最后插入一个子节点。

```javascript
	父节点.insertBefore(新的子节点,作为参考的子节点)
```

#### 删除节点
```javascript
	父节点.removeChild(子节点);
```

#### 克隆节点


```javascript
	要复制的节点.cloneNode();       //括号里不带参数和带参数false，效果是一样的。
	要复制的节点.cloneNode(true);
```

- 不带参数/带参数false：只复制节点本身，不复制子节点。

- 带参数true：既复制节点本身，也复制其所有的子节点。


#### 设置节点的属性值

```javascript
	元素节点.setAttribute("属性名", "新的属性值");
```

#### 删除节点的属性

```javascript
	元素节点.removeAttribute(属性名);
```


### 5. 获取 html 文档的方法

获取title、body、head、html标签的方法如下：

- `document.title` 文档标题；

- `document.head`  文档的头标签

- `document.body`  文档的body标签；

- `document.documentElement`  文档的html标签（这个很重要）。

`document.documentElement`表示文档的html标签。也就是说，基本结构当中的 `html 标签`而是通过`document.documentElement`访问的，并不是通过 document.html 去访问的。

## Web 存储 应用缓存

### H5 中有两种存储的方式

1、**`window.sessionStorage` 会话存储：**

- 保存在内存中。

- **生命周期**为关闭浏览器窗口。也就是说，当窗口关闭时数据销毁。

- 在同一个窗口下数据可以共享。


2、**`window.localStorage` 本地存储**：

- 有可能保存在浏览器内存里，有可能在硬盘里。

- 永久生效，除非手动删除（比如清理垃圾的时候）。

- 可以多窗口共享。

### 常见 API 
设置存储内容：

```javascript
	setItem(key, value);
```

读取存储内容：

```javascript
	getItem(key);
```

根据键，删除存储内容：

```javascript
	removeItem(key);
```


清空所有存储内容：

```javascript
	clear();
```

###  案例：记住用户名和密码

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
<!DOCTYPE html>
<html>

<head lang="en">
  <meta charset="UTF-8">
  <title></title>
</head>

<body>
  <label for="">
    用户名：<input type="text" class="userName" />
  </label>
  <br /><br />
  <label for="">
    密 码：<input type="text" class="pwd" />
  </label>
  <br /><br />
  <label for="">
    <input type="checkbox" class="check" id="" />记住密码
  </label>
  <br /><br />
  <button>登录</button>

  <script>
    var userName = document.querySelector('.userName');
    var pwd = document.querySelector('.pwd');
    var chk = document.querySelector('.check');
    var btn = document.querySelector('button');

    //        当点击登录的时候 如果勾选“记住密码”，就存储密码；否则就清除密码
    btn.onclick = function () {
      if (chk.checked) {
        //                记住数据
        window.localStorage.setItem('userName', userName.value);
        window.localStorage.setItem('pwd', pwd.value);
      } else {
        //                清除数据
        window.localStorage.removeItem('userName');
        window.localStorage.removeItem('pwd');
      }
    }
    //        下次登录时，如果记录的有数据，就直接填充
    window.onload = function () {
      userName.value = window.localStorage.getItem('userName');
      pwd.value = window.localStorage.getItem('pwd');

    }
  </script>
</body>

</html>
</body>
</html>
```

### 应用缓存

HTML5中我们可以轻松的构建一个离线（无网络状态）应用，只需要创建一个 `cache manifest` 缓存清单文件。


### 优势

1、可配置需要缓存的资源；

2、网络无连接应用仍可用；

3、本地读取缓存资源，提升访问速度，增强用户体验；

4、减少请求，缓解服务器负担。

### `cache manifest` 缓存清单文件



缓存清单文件中列出了浏览器应缓存，以供离线访问的资源。**推荐使用 `.appcache`作为后缀名，另外还要添加MIME类型。**

**缓存清单文件里的内容怎样写：**

（1）**顶行写CACHE MANIFEST。**

（2）**CACHE**: 换行 指定我们需要缓存的静态资源，如.css、image、js等。

（3）**NETWORK**: 换行 指定需要在线访问的资源，可使用通配符（也就是：不需要缓存的、必须在网络下面才能访问的资源）。

（4）**FALLBACK**: 换行 当被缓存的文件找不到时的备用资源（当访问不到某个资源时，自动由另外一个资源替换）。

```appcache
CACHE MANIFEST
CACHE:
#要缓存的文件
./img/1.jpg
./img/2.jpg
./img/3.jpg
NETWORK:
#指定必须联网才能访问的文件
./js/1.js
./js/2.js
./js/3.js
FALLBACK:
./css/1.css ./css a.css
```


 > **#当前页面无法访问是回退的页面**
 > FALLBACK:
 > 404.html

### 使用

在需要应用缓存在页面的根元素(html)里，添加属性manifest = "demo.appcache"。路径要保证正确。
```html
<html manifest="01.appcache">
```

## 新增全屏显示
> 》 HTML5规范允许用户自定义网页上**任一元素**全屏显示。

### 开启/关闭全屏显示

方法如下：（注意 screen 是小写）

```javascript
	requestFullscreen()   //让元素开启全屏显示

	cancleFullscreen()    //让元素关闭全屏显示
```

### 检测当前是否处于全屏状态

方法如下：

```js
	document.fullScreen
```


### 全屏的伪类

- :full-screen .box {}

- :-webkit-full-screen {}

- :moz-full-screen {}

比如说，当元素处于全屏状态时，改变它的样式。这时就可以用到伪类。
```js
<script>
    var box = document.querySelector('.box');
    // box.requestFullscreen();   
    //直接这样写是没有效果的。浏览器的机制，必须要点一下才可以实现全屏功能。
    document.querySelector('.box').onclick = function () {
        // 开启全屏显示的兼容写法
        if (box.requestFullscreen) {  
        //如果支持全屏，那就让元素全屏
            box.requestFullscreen();
        } else if (box.webkitRequestFullScreen) {
            box.webkitRequestFullScreen();
        } else if (box.mozRequestFullScreen) {
            box.mozRequestFullScreen();
        }

    }
</script>
```

## 音频视频

### 音频

```html
<!--推荐的兼容写法：-->
<audio controls loop>
    <source src="music/yinyue.mp3"/>
    <source src="music/yinyue.ogg"/>
    <source src="music/yinyue.wav"/>
    抱歉，你的浏览器暂不支持此音频格式
</audio>
```
### 视频

```html
    <video controls autoplay>
        <source src="video/movie.mp4"/>
        <source src="video/movie.ogg"/>
        <source src="video/movie.webm"/>
        抱歉，不支持此视频
    </video>
```

##  leetcode

### 1. 字典中最长的单词 (Set, String sort)

```js
/**
 * # 字典中最长的单词 (2022.3.17)
 给出一个字符串数组 words 组成的一本英语词典。返回 words 中最长的一个单词
 该单词是由 words 词典中其他单词添加一个字母组成
 若其中有多个可行的答案，则返回答案中字典序最小的单词
 若无答案，则返回空字符串。
 */

let array = ["wo","wor","worl","world"]
let longest_word = function (words) {
  // 讲数组的所有元素存放到 set 中 （达到去重的目的）
  let set = new Set();
  words.forEach(function (item) {
    set.add(item)
  })
  // 进行排序
  words.sort((a, b) => {
    return a.length === b.length ? a.localeCompare(b) : b.length - a.length
  })
  // 判断是否存在字串
  for (let i = 0; i < words.length; i++) {
    let flag = true;
    for (let j = 1;words[i].length; j++) {
      console.log(set.has(words[i].substring(0, j)))
      if (!set.has(words[i].substring(0, j))) {
        flag = false;
        break;
      }
    }
    console.log("flag" + flag)
    if (flag) {
      return words[i]
    }
  }
  return ""
}
longest_word(array);
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8ab27fd07f0b421687cdff6921c123c5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)

###  2. 替换空格 （String split join）

```js
/**
 * # 实现一个函数，把字符串 s 中的每个空格替换成"%20"。
 */
let replaceSpace = function(s) {
  s=s.split(' ').join('%20');
  return s
};
```

###  3. 逆序数

```js
/**
 * 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。
 * 输入一个数组，求出这个数组中的逆序对的总数。
 * @type {number[]}
 */

// 暴力破解法（时间不允许）
let reversePairs = function(nums) {
  let number = 0;
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] > nums[j]) {
        number++;
        console.log(`${i} + ${j}`)
      }
    }
  }
  return number;
};
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8eeeb8bd8e78407984159e60d4b8c793.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGltaW5neA==,size_20,color_FFFFFF,t_70,g_se,x_16)


```js
// 归并排序（正确解法）

let reversePairs = function(nums) {
  return findInversePairNum(nums, 0, nums.length - 1);
};

function findInversePairNum(arr, start, end) {
  if (start >= end) return 0;

  const copy = new Array(end - start + 1);
  const length = Math.floor((end - start) / 2); // 左数组长度
  const leftNum = findInversePairNum(arr, start, start + length);
  const rightNum = findInversePairNum(arr, start + length + 1, end);

  let i = start + length;
  let j = end;
  let copyIndex = end - start;
  let num = 0;
  while (i >= start && j >= start + length + 1) {
    if (arr[i] > arr[j]) {
      num += j - start - length;
      copy[copyIndex--] = arr[i--];
    } else {
      copy[copyIndex--] = arr[j--];
    }
  }

  while (i >= start) {
    copy[copyIndex--] = arr[i--];
  }

  while (j >= start + length + 1) {
    copy[copyIndex--] = arr[j--];
  }

  for (let k = start; k <= end; ++k) {
    arr[k] = copy[k - start];
  }

  return num + leftNum + rightNum;
}

```

###  4. 0～n-1中缺失的数字

```js
/**
    # 0～n-1中缺失的数字
    一个长度为n-1的递增排序数组中的所有数字都是唯一的
    并且每个数字都在范围0～n-1之内
    在范围0～n-1内的n个数字中有且只有一个数字不在该数组中
    请找出这个数字。
 */
var missingNumber = function(nums) {
    let l = 0;
    let r = nums.length - 1;
    while (l <= r) {
        let m = Math.floor((l + r) / 2);
        if (nums[m] === m) {
            l = m + 1;
        } else {
            r = m - 1;
        }
    }
    return l;
};
```

### [682. 棒球比赛](https://leetcode-cn.com/problems/baseball-game/)

```js
/**
你现在是一场采用特殊赛制棒球比赛的记录员。这场比赛由若干回合组成，过去几回合的得分可能会影响以后几回合的得分。

比赛开始时，记录是空白的。你会得到一个记录操作的字符串列表 ops，其中 ops[i] 是你需要记录的第 i 项操作，ops 遵循下述规则：

整数 x - 表示本回合新获得分数 x
"+" - 表示本回合新获得的得分是前两次得分的总和。题目数据保证记录此操作时前面总是存在两个有效的分数。
"D" - 表示本回合新获得的得分是前一次得分的两倍。题目数据保证记录此操作时前面总是存在一个有效的分数。
"C" - 表示前一次得分无效，将其从记录中移除。题目数据保证记录此操作时前面总是存在一个有效的分数。
请你返回记录中所有得分的总和。
 */
var calPoints = function(ops) {
    let n = ops.length
  let arr = []
  for (let i = 0; i < n; i++) {
    let item = ops[i]
    switch (item) {
      case "C": {
        arr.pop()
        break
      }
      case "D": {
        arr.push(arr[arr.length - 1] * 2)
        break
      }
      case "+": {
        arr.push(arr[arr.length - 1] + arr[arr.length - 2])
        break
      }
      default: {
        arr.push(item * 1)
      }
    }
  }
  return arr.reduce((l, i) => l + i, 0)
};
```



## 面试题

### ['1', '2', '3'].map(parseInt)的结果是什么？

  看到这个题下意识的觉得答案就是[1, 2, 3]


  但实际上，答案是[1, NaN, NaN]。

```js
/**
 * parseInt(string，radix)
 * */

console.log(parseInt('10', 0)) // 10
console.log(parseInt('10', 1)) // NaN
console.log(parseInt('10', 37)) // NaN
console.log(parseInt('10', 16)) // 16

// string：要被解析的值。
//    如果参数不是一个字符串，则将其转换为字符串(toString)。字符串开头的空白符将会被忽略。
// radix：可选。
//    从 2 到 36，表示被解析的值的进制。例如说指定 10 就等于指定十进位。

// parseInt(string, radix)将一个字符串string转换为radix进制的整数， radix为介于2-36之间的数。
// 返回解析后的整数值。
// 如果被解析参数的第一个字符无法被转化成数值类型，则返回NaN。

// 到这为止，我们对parseInt()函数有了一个基础的了解，
// 根据上面的描述，也就是说我们为parseInt()的第二个参数传递一个非2-36之间的数，返回结果是NaN，我们来测试一下：

// 非2-36之间的数 是不合法的, 返回 NaN

// 如果 radix 是 undefined、0或未指定的，JavaScript会假定以下情况：

// 1. 如果输入的 string以 "0x" 或 "0x"（一个0，后面是小写或大写的X）开头，那么radix被假定为16，字符串的其余部分被当做十六进制数去解析。
// 2. 如果输入的 string 以 "0"（0）开头， radix 被假定为8（八进制）或10（十进制）。具体选择哪一个radix取决于实现。
//      ECMAScript 5 澄清了应该使用 10 (十进制)，但不是所有的浏览器都支持。因此，在使用parseInt时，一定要指定一个 radix。
// 3. 如果输入的 string 以任何其他值开头， radix 是 10 (十进制)。

// 这就解释了我们的parseInt(10, 0)的结果是10了。
```
```js
/**
 * Array.prototype.map(callback, )
 * */

// 现在我们来了解一下map方法的作用，该方法接受两个参数，
// 第一个是一个回调函数，数组中的每一项都会执行该函数
//    这个回调函数接受三个参数，第一个是正在处理的元素，第二个是正在处理的索引，第三个是当前数组；
// 第二个参数是调用回调函数的this。(当前元素属于的数组对象)

function returnResult(item, index, arr) {
  console.log(item + ' 是第 ' + index + ' 位元素')
  if (index === arr.length - 1) {
    console.log('修改前的数组 ' + arr)
  }
  return item + index
}
let result = [1, 2, 3].map(returnResult)
console.log('修改后的数组 ' + result)

// 1 是第 0 位元素
// 2 是第 1 位元素
// 3 是第 2 位元素
// [ 1, 2, 3 ]
// [ 1, 3, 5 ]
```
```js
/**
 * 回到问题: ['1', '2', '3'].map(parseInt)
 * */
// parseInt('1', 0)，直接按照10进制解析，结果为1；
// parseInt('2', 1)，传入了非2~36的值，结果为NaN；
// parseInt('3', 2)，按照2进制进行解析，2进制可以解析的数字只有1和0，所以返回NaN。

console.log(['10','10','10','10','10'].map(parseInt))

// [ 10, NaN, 2, 3, 4 ]

// 相当于给 parseInt 传入两个参数, 第一个是 数组元素, 一个是索引
// 但是 parseInt 按传来的 字符串 与 进制 解释了
```
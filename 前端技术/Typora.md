# Typora

## Typora 图片上传 github

>  在 csdn 和 typora 写博客的时候， 真的是好讨厌两者之间反复横跳解决不了图片上传的问题， 但现在就很方便啦

### Mac 版操作

#### 1. 安装插件

首先安装Picgo-Core， 需要有 node 的运行环境
```bash
npm install picgo -g
```

成功之后运行安装增强的GitHub插件

```bash
picgo install github-plus
```

---

#### 2. 配置Github Repo

首先需要在 github 新建一个仓库， 专门用于放置自己的图片

![image-20220326113243076](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326113243076.png)

只需要填好正确的库名就好， 其他自由选择

![image-20220326113937688](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326113937688.png)

进入 settings 进行设置

![image-20220326114030402](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114030402.png)

左侧最下面有 developer settings

![image-20220326114115271](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114115271.png)

选择 new token

![image-20220326114307504](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114307504.png)

里面只需要选择下面的几步就可以

![image-20220326114417335](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114417335.png)

![image-20220326114447330](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114447330.png)

展示一下完成后的样子

记得复制一下你的 token 它只会显示一次

![image-20220326114230398](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326114230398.png)

打开`~/.picgo/config.json`

编写 config.json

```js
{
  "picBed": {
    "uploader": "githubPlus",
    "current": "githubPlus",
    "githubPlus": {
      "branch": "master",
      "customUrl": "https://raw.githubusercontent.com/你的github用户名/仓库名/master",
      "origin": "github",
      "repo": "你的github用户名/仓库名/",
      "path": "img/",
      "token": "你刚刚获得的token"
    }
  },
  "picgoPlugins": {
    "picgo-plugin-github-plus": true,
    "picgo-plugin-rename-file": false
  },
  "picgo-plugin-github-plus": {
    "lastSync": "2022-03-26 11:41:42"
  }
}
```

---

#### 3. 配置 typora

```js
// 这是 node 的安装位置
usr/local/bin/node usr/local/bin/picgo upload 
```

![image-20220326120734712](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/image-20220326120734712.png)

---

### Windows 版

#### 1. 先配置好 github, 具体看上面 mac 版的,不做赘述

#### 2. 然后再 typora 安装 picgo

![image-20220328081359333](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280813389.png)

安装完成后, 对他进行配置

![image-20220328081452027](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280814067.png)

![image-20220328081536617](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280815656.png)

![image-20220328082519194](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280825234.png)

#### 3. 配置完成后进行测试

![image-20220328081605552](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280816593.png)

在成功之后打开 typora 验证图片上传选项

![image-20220328081359333](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202203280813389.png)

## typora vue 主题

> git clone https://github.com/ximingx/typora-vue-theme

```bash
$ git clone https://github.com/ximingx/typora-vue-theme
```

然后你可以得到`vue.css`,`vue-dark.css`文件和`vue`文件夹。

打开打字机。单击→部分中的“**打开主题文件夹**”按钮。`Preference Panel``Apperance`

将`vue.css`,`vue-dark.css`和`vue`文件夹放入打开的文件夹中，确保您的 css 文件直接位于该目录下。

关闭并重新打开 Typora，然后从菜单栏中选择`Theme`→`Vue`或。`Vue Dark`




# node







# npm

`NPM`是随同`NodeJS`一起安装的包管理工具，是常用的前端包管理工作。

访问 [nodejs (opens new window)](https://nodejs.org/zh-cn/)官网下载安装 `nodejs` , 其中将内置`npm`命令。

> 也可以使用 [淘宝镜像 (opens new window)](https://npmmirror.com/)安装 `cnpm `命令

```bash
$ npm install -g cnpm --registry=https://registry.npmmirror.com
```

## 1. 常用命令

```bash
# 全局安装
$ npm install -g <Module Name>
# 安装软件包，但不修改package.json 文件，以后使用npm install 时不会自动安装
$ npm install <Module Name>
# 生产环境
# 1. 在package.json文件dependencies属性下增加记录
# 2. npm install 时会自动安装该软件包
# 3. 使用npm install --production或者NODE_ENV变量值为production时，安装该软件包
$ npm install --save <Module Name>
# 开发环境
# 1. 在package.json文件devDependencies属性下增加记录
# 2. npm install 时会自动安装该软件包
# 3. 使用npm install --production或者NODE_ENV变量值为production时，不会安装该软件包
$ npm install --save-dev <Module Name>
# 查看安装的模块列表
$ npm ls
# 查看本地已安装的包信息
$ npm ls tailwindcss
# (或者)
$ npm ls | grep tailwind
# 查看包信息
$ npm info tailwindcss
# 列出项目的依赖
$ npm list
# 列出项目的依赖，并限制显示的依赖深度
$ npm list --depth=2
# 删除项目中软件包
$ npm uninstall <Module Name>
```













# nvm

​		在工作中，我们可能同时在进行2个或者多个不同的项目开发，每个项目的需求不同，进而不同项目必须依赖不同版本的`NodeJS`运行环境，这种情况下，对于维护多个版本的`node`将会是一件非常麻烦的事情

​		而`nvm`是`node`版本管理工具为了解决`node`各种版本存在不兼容现象，让你在同一台机器上安装和切换不同版本的`node`的工具。

## 1. 安装

**如果电脑上之前已经单独安装了`node`，先卸载**

```bash
# 查看全局 node_modules 目录
$ npm root -g
```

如果之前使用 `npm `安装过扩展包，现在想使用`NVM`进行管理。则首先需要从全局中删除`node_modules`目录

> windows

​		[下载地址: https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)

​		[或者这个: https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)

![image-20220514203325411](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142033605.png)

将下载好的安装包解压

![image-20220514203452000](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142035984.png)

双击`exe`后缀文件进行安装

里面需要设置两个存放路径, 第一个是 `nvm `的位置, 第二个是 `node `的安装位置

安装完毕后输入 `nvm version` 查看版本。

```bash
$ nvm version
```

![image-20220514203638456](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142036257.png)

> mac

```bash
$ brew install nvm
```

如果不能执行请修改 `.zshrc` 文件并在最后添加以下内容

```js
export NVM_DIR="$HOME/.nvm"
  [ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```

然后重新加载配置

```bash
source ~/.zshrc 
```

## 2. 配置镜像源

安装完毕后，找到安装的路径，一些简单配置，打开`setting.txt`

![image-20220514203903473](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142039624.png)

找到 `setting.txt` 在最后面添加

```bash
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

![image-20220514203928074](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142039471.png)

## 3. 常用命令

```bash
# 获得帮助
$ nvm -h 
# 显示可以安装的所有node.js的版本
$ nvm list available
# 安装 node 的版本
$ nvm install <version>
# 显示当前已经安装的 node 版本
$ nvm list 
# 当前使用的 node 版本
$ nvm current  
# 使用指定版本的 node
$ nvm use [version] 
# 显示 nvm 的版本
$ nvm version
# 开启
$ nvm on
# 禁用
$ nvm off  
```

![image-20220514204945244](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202205142049775.png)





# yarn

`Yarn `缓存了每个下载过的包，所以再次使用时无需重复下载。 同时利用并行下载以最大化资源利用率，因此安装速度更快。

请访问 [yarnpkg.com (opens new window)](https://yarnpkg.com/getting-started)下载安装 `Yarn`

## 1. 安装

> 命令行安装

```bash
# 全局安装
$ npm install -g yarn
# 更新yarn到最新版本
$ yarn set version latest
$ yarn set version from sources
# 苹果用户可以使用brew进行安装
$ brew install yarn
```

> 查看版本

```bash
# 查看版本
$ yarn -v
$ yarn --version
```

## 2. 国内镜像

```bash
# 查看当前使用的镜像
$ yarn config get registry
# 设置为淘宝镜像
$ yarn config set registry https://registry.npm.taobao.org/
```

## 3. 常用命令

```bash
# 访问命令列表
$ yarn help
# 初始化新项目
$ yarn init
# 根据package.json来安装项目依赖的软件包
$ yarn
# (或者)
$ yarn install
# 全局安装
$ yarn global add [package]
# 生产环境
# 1. 在package.json文件dependencies属性下增加记录
# 2. yarn 时会自动安装该软件包
# 3. 使用 yarn install --production 或者 NODE_ENV 变量值为 production 时，安装该软件包
$ yarn add [package]
# 开发环境
# 1. 在package.json文件devDependencies属性下增加记录
# 2. npm install 时会自动安装该软件包
# 3. 使用npm install --production或者NODE_ENV变量值为production时，不会安装该软件包
$ yarn add [package]@[version] –dev
# (或者)
$ yarn -D add [package]
# 列出当前项目的依赖
$ yarn list
# 查看本地已安装的包信息
$ yarn list | grep tailwind
# 列出项目的依赖，并限制显示的依赖深度
$ npm list --depth=0
# 查看软件包的README
$ yarn info tailwindcss readme
# 更新所有软件包
$ yarn upgrade
# 更新指定软件包
$ yarn upgrade [package]@[version]
# 删除全局软件
$ yarn remove  -g [package]
# 删除项目中软件包
$ yarn remove  [package]
# 列出已缓存的每个包
$ yarn cache list 
# 全局缓存位置
$ yarn cache dir
# 清除缓存
$ yarn cache clean
```



# yrm

`yrm`是管理镜像的工具，可以列出可以使用的镜像，非常方便。

```bash
# 安装yrm
$ npm install -g yrm
# 列出可以使用的镜像
$ yrm ls
# 使用淘宝镜像
$ yrm use taobao
# 测试镜像速度
$ yrm test taobao
```



# chrome 

## 1. 快捷键

`ctrl + shift + j` 打开控制台



## 2. 插件

`Vue.js devtools` `vue框架` 使用时的调试工具







# webstorm 插件

![image-20220704191154991](https://raw.githubusercontent.com/ximingx/Figurebed/master/imgs/202207041911100.png)




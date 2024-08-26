# node.js



 浏览器中的JavaScript 运行环境

![1723555918554](.\typora-user-images\1723555918554.png)

- V8 引擎负责解析和执行JavaScript 代码。
- 内置API 是由运行环境提供的特殊接口，只能在所属的运行环境中被调用。

## 初始node.js

 Node.js 是一个基于 `Chrome V8` 引擎的 JavaScript 运行环境。 

Node.js 中的 JavaScript 运行环境

![1723556019681](.\typora-user-images\1723556019681.png)

- 浏览器是JavaScript 的前端运行环境
- Node.js 是 JavaScript 的后端运行环境。
- Node.js 中无法调用DOM 和BOM 等浏览器内置API。

Node.js 的应用框架主要有以下几个：

- 基于 Express 框架（`http://www.expressjs.com.cn/`），可以快速构建 Web 应用 
- 基于 Electron 框架（`https://electronjs.org/`），可以构建跨平台的桌面应用
- 基于 restify 框架（`http://restify.com/`），可以快速构建 API 接口项目
- 读写和操作数据库、创建实用的命令行工具辅助前端开发等

### Node.js 环境的安装

LTS 版本和Current版本的不同

- LTS 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装LTS 版本的Node.js。
- Current 为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装Current 版本的Node.js。但是，Current 版本中可能存在隐藏的Bug 或安全性漏洞，因此不推荐在企业级项目中使用Current 版本的Node.js。

配置环境变量的时候，注意以下问题，在node.js安装的文件夹，新建两个文件夹node_glabal和node_cache，然后执行如下命令：

```bash
npm config set prefix D:\applicationSoftware\node\node_glabal
npm config set prefix D:\applicationSoftware\node\node_cache
```


### fs文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。 

- `fs.readFile()` 方法，用来读取指定文件中的内容 
- `fs.writeFile() `方法，用来向指定的文件中写入内容

```javascript
//导入fs模块，用来读文件
const fs=require('fs')
//从1.txt文本中读取文件，文件格式为utf-8
fs.readFile('../1.txt','utf-8',function(err,dataStr){
    //打印失败的结果
    if(err){
        return console.log('读取文件失败'+err.message)
    }
    console.log('读取文件成功'+dataStr)
})
//写文件操作
fs.writeFile('../1.txt','你好，node',function(err){
    //如果写入成功则err成功，其值为null，如果失败err的值为一个对象
    // console.log(err);
    if(err){
        return console.log('文件写入失败'+err.message)
    }else{
        console.log('文件写入成功 ')
    }
})
```

### path路径模块

#### 路径动态拼接问题

在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。 

原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。 

解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，**不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题**。但是，**提供完整路径还有一个问题就是程序的移植性会很差**，所以也不推荐使用。

针对这个问题node提出了一个新的方法:

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理 需求。 

例如： 

- **path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串** 
-  **path.basename() 方法，用来从路径字符串中，将文件名解析出来**

`__dirname` 表示当前文件所处的目录

```js
fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
```

使用path.join() 方法，可以把多个路径片段拼接为完整的路径字符串

```javascript
//引入path路径模块
const path=require('path');
//其中../会抵消前一个目录
fs.readFile(path.join(__dirname,'../成绩-ok.txt'),'utf-8',function(err,data){
    if(err){
        console.log('读取文件出错:', err);
        return;
    }else{
        // 按行分割数据
       console.log(data)
}})
```

**注意：涉及到路径拼接的操作，都要使用 path.join() 方法进行处理。不要直接使用 + 进行字符串的拼接**

使用path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名

```js
const fpath = path.join(__dirname,'test.txt') //输出test
const fpath = path.join(__dirname) //输出test.txt
const lastname =path.basename(fpath,'.txt')
console.log(lastname)
```

使用path.extname() 方法，可以获取路径中的扩展名部分

```js
const fpath = '/a/b/c/index.html'
const fext = path.extname(fpath)
console.log(fext)
```

### http模块

http 模块是Node.js官方提供的用来创建 web 服务器的模块.通过 http 模块提供的` http.createServer() `方法，就 能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

创建 web 服务器的基本步骤 

- 导入 http 模块 

- 创建 web 服务器实例

- 为服务器实例绑定 request 事件，监听客户端的请求
- 启动服务器

```javascript
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(8080, function () {  
  console.log('server running at http://127.0.0.1:8080')
})
```

#### req 和res

req请求对象：只要服务器接收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数。

res响应对象：在服务器的 request 事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下的方式：

```javascript
// req 是请求对象，包含了与客户端相关的数据和属性
server.on('request', (req, res) => {
  // req.url 是客户端请求的 URL 地址
  const url = req.url
  // req.method 是客户端请求的 method 类型
  const method = req.method
  const str = `Your request url is ${url}, and request method is ${method}`
  console.log(str)
  // 调用 res.end() 方法，向客户端响应一些内容
  res.end(str)
})
```

#### 解决乱码问题

当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

```javascript
server.on('request', (req, res) => {
  // 定义一个字符串，包含中文的内容
  const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
  // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // res.end() 将内容响应给客户端
  res.end(str)
})
```

## 模块化

### 基本概念 

模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元

把代码进行模块化拆分的好处： 

- 提高了代码的复用性 

- 提高了代码的可维护性 

- 可以实现按需加载


### Node.js 中模块化 

#### 基本介绍

Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：

- 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等） 

- 自定义模块（用户创建的每个 .js 文件，都是自定义模块）

-  第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）


使用 **require()** 方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用

```js
// 内置模块
const fs = require('fs')

// 用户自定义模块
const custom = require('./custom.js')

// 第三方模块,由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要
//先下载
const moment = require('moment')
```

#### 模块作用域 

 模块作用域的好处 ：防止了**全局变量污染**的问题

**module.exports 对象**

 在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。 外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

**注意：使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准。**

```js
/*model.js*/
const age = 20
module.exports.username = 'tom'
module.exports.hello=function(){
    alert('hello')
}
module.exports.age = age

// 让 module.exports 指向一个全新的对象
module.exports = {
    nickname: '小黑',
    sayHi() {
      console.log('Hi!')
    }
  }
 /*测试module.js*/ 
const modules = require('./model.js')
console.log(modules.nickname) //小黑
console.log(modules.age) //undefined,应为没有对外export
console.log(modules) //{ nickname: '小黑', sayHi: [Function: sayHi] }
```

为了简化向外共享成员的代码，Node 提供了 exports 对象。默认情况 下，**exports 和 module.exports 指向同一个对象**。最终共享的结果，还是以 module.exports 指向的对象为准。

**注意：为了防止混乱，不要在同一个模块中同时使用 exports 和 module.exports**

```js
const age = 20
exports.username = 'tom'
exports.hello=function(){
    alert('hello')
}
exports.age = age

// 让 module.exports 指向一个全新的对象
exports = {
    nickname: '小黑',
    sayHi() {
      console.log('Hi!')
    }
  }
```

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。 

CommonJS 规定： 

​		① 每个模块内部，module 变量代表当前模块。 

​		② module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。 

​		③ 加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。

### npm与包 

#### 基本介绍

Node.js 中的第三方模块又叫做包。 第三方模块和包指的是同一个概念，只不过叫法不同。

#### npm 

npm安装以及配置

```bash
# 修改安装路径和缓存路径命令如下
npm config set prefix "D:\applicationSoftware\node\node_glabal"

npm config set cache "D:\applicationSoftware\node\node_cache"
# 查看基本配置
npm config list
# 镜像源配置
npm config set registry=https://registry.npmmirror.com/
	阿里：https://npm.aliyun.com/
	华为：https://mirrors.huaweicloud.com/repository/npm/
	腾讯：http://mirrors.cloud.tencent.com/npm/

# 也可以使用其他包管理工具，比如：cnpm、yarn等
npm install cnpm -g
npm install yarn -g
cnpm -v和yarn -v命令查看版本情况
```

使用noment包格式化时间

- 使用 npm 包管理工具，在项目中安装格式化时间的包 moment 

- 使用 require() 导入格式化时间的包 

- 参考 moment 的官方 API 文档对时间进行格式化


```javascript
//导入moment包
const moment = require('moment')
//参考api文档使用moment的format方法对时间进行格式化
const dt = moment().format('YYYY-MM-DD')
console.log(dt)
```

npm的相关操作 

```javascript
npm install 包名 //安装指定的包
npm install 包名@x.x.x //安装指定版本的包
npm init -y  //在执行命令所处的目录中，快速创建package.json文件，
//该命令只能在英文的目录下成功运行！所以，项目文件夹的名称不要使用中文，不能出现空格。
npm install //一次性安装所有的依赖包
npm uninstall 包名 //删除指定的包
//查看当下的包镜像源（下载包的服务器地址）
npm config get registry
//将下载包的镜像源切换为淘宝镜像
npm config set registry=https://registry.npm.taobao.org/
//检查镜像源是否下载成功
npm config get registry
```

在使用npm 下包的时候，默认从国外的https://registry.npmjs.org/服务器进行下载，此时，**网络数据的传输需要经过漫长的海底光缆**，因此下包速度会很慢。为了提高安装速度，我们可以使用镜像

![1724480432932](.\typora-user-images\1724480432932.png)

为了更方便的切换下包的镜像源，我们可以安装 nrm 这个小工具，利用 nrm 提供的终端命令，可以快速查看和切换下包的镜像源

```bash
# 通过npm包管理器，将nrm安装为全局可用的工具
npm i nrm -g
# 查看所有的镜像源
nrm ls
# 将下包的镜像源切换为淘宝镜像
nrm use taobao
# 镜像源配置
npm config set registry=https://registry.npmmirror.com/
	阿里：https://npm.aliyun.com/
	华为：https://mirrors.huaweicloud.com/repository/npm/
	腾讯：http://mirrors.cloud.tencent.com/npm/
```

#### 包管理配置文件

devDependencies 节点

如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies节点中。与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到dependencies 节点中。

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到） 
- 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

```bash
npm install 包名 -D //开发依赖包，这是简写形式
npm install 包名 --save-dev //完整写法
npm install 包名  //核心依赖包
```

那些被安装到项目的 node_modules 目录中的包，都是项目包。 

初次装包完成后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件。

-  node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。 

- package- lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。

-    package.json 文件中，有一个 dependencies 节点，专门用来记录您使用 npm install  命令安装了哪些包。

#### 包的分类

全局包

在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。 全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。

注意： 

- 只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。 

- 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可


```bash
npm install 包名 -g   # 全局安装
npm uninstall 包名 -g  # 卸载全局安装的包
```

i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下：

```bash
npm install -g i5ting_toc  # 将其安装为全局包
i5ting_toc -f   要转换的md文件路径 -o  # 转换md为html
```

#### 发布包

- 注册npm账号

- npm 账号注册完成后，可以在终端中执行 npm login 命令，依次输入用户名、密码、邮箱后登录

- 将终端切换到包的根目录之后，运行 npm publish 命令，即可将包发布到 npm 上（注意:包名不能雷同）
- 运行 npm unpublish 包名 --force 命令，即可从 npm 删除已发布的包。

#### 规范的包结构

一个规范的包，它的组成结构，必须符合以下3 点要求：

- 包必须以单独的目录而存在
- 包的顶级目录下要必须包含package.json 这个包管理配置文件
- package.json 中必须包含name，version，main这三个属性，分别代表包的名字、版本号、包的入口。

### 模块的加载机制

模块在第一次加载后会被缓存。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。

 注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会**优先从缓存中加载，从而提高模块的加载效率**。

内置模块是由 Node.js 官方提供的模块，内置模块的加载优先级最高。

使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../  这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。

## Express

Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器

Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

 Express 的中文官网： http://www.expressjs.com.cn/

使用Express，我们可以方便、快速的创建Web 网站的服务器或API 接口的服务器。

### 基本使用

#### 创建基本的web服务器

```javascript
// 导入 express
const express = require('express')
// 创建服务器实例
const app = express()
// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

#### 监听 GET 请求和 POST请求

```javascript
//参数一：客户端请求的url地址
//参数二：请求对应的处理函数
app.get('请求url',function(req,res){})
```

```javascript
//参数一：客户端请求的url地址
//参数二：请求对应的处理函数
app.post('请求url',function(req,res){})
```

#### 把内容响应给客户端 

通过 res.send() 方法，可以把处理好的内容，发送给客户端：

```javascript
app.get('/user',function(req,res){
    //向客户端发送json对象
    res.send({name:'zs',age:20,gender:'男'})
})
app.post('/user',function(req,res){
    //向客户端发送内容
    res.send('请求成功')
})
```

#### 获取 URL 中携带的查询参数

通过 req.query 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

```javascript
app.get('/user',function(req,res){
    //req.query默认是一个空对象
    //客户端通过？name=xx&age=20这种形式发送到服务器的参数
    //可以通过req.query.name  req.query.age获取到具体的参数
   console.log(req.query)
})
```

#### 获取 URL 中的动态参数

通过 req.params 对象，可以访问到 URL 中，通过 : 匹配到的动态参数：

```javascript
app.get('/user/:id',function(req,res){
    //req.params默认是一个空对象
    //里面存放着通过：动态匹配到的参数值
   console.log(req.params)
})
```

#### 托管静态资源

express.static()

 express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器， 例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```javascript
app.use(express.static('public'))//通过它可以访问 public 目录中的所有文件了：
```

注意：Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。 因此，存放静态文件的目录名不会出现在 URL 中。

如果要托管多个静态资源目录，请多次调用 express.static() 函数：

```javascript
app.use(express.static('public'))

app.use(express.static('file'))
```

访问静态资源文件时，express.static() 函数会根据目录的添加顺序查找所需的文件。

挂载路径前缀 

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

```javascript
app.use(‘/public’，express.static('public'))
```

就可以通过带有 /public 前缀地址来访问 public 目录中的文件了。

例如： http://localhost:3000/public/images/kitten.jpg

#### nodemon

nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件 的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试

```javascript
npm install -g nodemon   //将 nodemon 安装为全局可用的工具
```

### Express路由

#### 基本介绍

广义上来讲，路由就是映射关系。

在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

 Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

```javascript
app.method(path,handler)
```

路由的基本使用

```javascript
const express = require('express')
//创建wenb服务器命名为app
const app = express()
// 挂载路由
app.get('/', (req, res) => {
  res.send('hello world.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})
//启动web服务器
app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

路由的匹配过程 

每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。 在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

#### 模块化路由

为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。 

将路由抽离为单独模块的步骤如下：

 		① 创建路由模块对应的 .js 文件 

​		② 调用 express.Router() 函数创建路由对象 

​		 ③ 向路由对象上挂载具体的路由 

​		 ④ 使用 module.exports 向外共享路由对象 

​		 ⑤ 使用 app.use() 函数注册路由模块

创建路由模块

```javascript
// 这是路由模块
// 1. 导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()
// 3. 挂载具体的路由
//这是查询用户信息的路由模块
router.get('/user/list', (req, res) => {
  res.send('Get user list.')
})
//这是添加用户信息的路由模块
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})
// 4. 向外导出路由对象
module.exports = router
```

注册路由模块（即在代码中引入路由模块）

```javascript
const express = require('express')
const app = express()
// 1. 导入路由模块
const router = require('./03.router')
// 2. 注册路由模块，并添加统一的前缀/api
app.use('/api', router)
// 注意： app.use() 函数的作用，就是来注册全局中间件
app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

### Expess中间件

#### 基本介绍

中间件（Middleware ），特指业务流程的中间处理环节。

Express 中间件的调用流程 

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

Express 中间件的格式

 Express 的中间件，本质上就是一个 function 处理函数，Express 中间件的格式如下：

**注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。**

next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

#### 基本使用

```javascript
// 这是定义全局中间件的简化形式
const mw=function(req,res,next){
     console.log('这是一个最简单的中间件函数')
  	next()
}
//全局生效的中间件
app.use(mw)
```

定义全局中间件的简化形式

```javascript
app.use((req, res, next) => {
  // 获取到请求到达服务器的时间
  const time = Date.now()
  // 为 req 对象，挂载自定义属性，从而把时间共享给后面的所有路由
  req.startTime = time
  next()
})
```

.中间件的作用 

多个中间件之间，共享同一份 req 和 res。基于这样的特性，我们可以在上游的中间件中，统一为 req 或 res 对象添 加自定义的属性或方法，供下游的中间件或路由进行使用。

定义多个全局中间件 

可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行 调用，示例代码如下：

```javascript
const express = require('express')
const app = express()
// 定义第一个全局中间件
app.use((req, res, next) => {
  console.log('调用了第1个全局中间件')
  next()
})
// 定义第二个全局中间件
app.use((req, res, next) => {
  console.log('调用了第2个全局中间件')
  next()
})
// 定义一个路由
app.get('/user', (req, res) => {//请求这个路由会依次触发以上两个全局中间件
  res.send('User page.')
})
app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

局部生效的中间件 

不使用 app.use() 定义的中间件，叫做局部生效的中间件，示例代码如下：

```javascript
// 1. 定义中间件函数
const mw1 = (req, res, next) => {
  console.log('调用了局部生效的中间件')
  next()
}
// 2. 创建路由，mw1这个中间件只在以下这个路由中生效，这就是局部中间件
app.get('/', mw1, (req, res) => {
  res.send('Home page.')
})
//mw1这个中间件不会在以下这个路由中生效
app.get('/user', (req, res) => {
  res.send('User page.')
})
```

定义多个局部中间件 

可以在路由中，通过如下两种等价的方式，使用多个局部中间件：

```javascript
// 1. 定义中间件函数
const mw1 = (req, res, next) => {
  console.log('调用了第一个局部生效的中间件')
  next()
}
const mw2 = (req, res, next) => {
  console.log('调用了第二个局部生效的中间件')
  next()
}
// 2. 以下两个写法完全等价
app.get('/', [mw1, mw2], (req, res) => {
  res.send('Home page.')
})
app.get('/', mw1, mw2, (req, res) => {
  res.send('Home page.')
})
```

中间件的5个使用注意事项

 		① 一定要在路由之前注册中间件 

​		 ② 客户端发送过来的请求，可以连续调用多个中间件进行处理

​		 ③ 执行完中间件的业务代码之后，不要忘记调用 next() 函数 

​		 ④ 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码 

​		 ⑤ 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

#### 中间件的分类

Express 官方把常见的中间件用法，分成了 5 大类，分别是： 

​		① 应用级别的中间件 

​		② 路由级别的中间件 

​		③ 错误级别的中间件 

​		④ Express 内置的中间件 

​		⑤ 第三方的中间件

应用级别的中间件 

通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件，代码示例如下：

```javascript
//应用级别的中间件（全局中间件）
app.use((res,res)=>{
next()
})
//应用级别的中间件（局部中间件）
app.get('/',mw1,(res,res)=>{
res.send('home page')
})
```

路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不 过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上，代码示例如下：

```javascript
var app =express()
var router=express.Router()
//路由级别的中间件
router.use(function(req,res,next){
    console.log('time',Date.now())
    next()
})
app.use('/',router)
```

错误级别的中间件

错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。 

格式：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)。

**注意：错误级别的中间件， 必须注册在所有路由之后！**

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 1. 定义路由
app.get('/', (req, res) => {
  // 1.1 人为的制造错误
  throw new Error('服务器内部发生了错误！')
  res.send('Home page.')
})
// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => {
  console.log('发生了错误！' + err.message)
  res.send('Error：' + err.message)
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

Express内置的中间件

 自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验： 

① express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性） 

② express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用） 

③ express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json())
// 通过 express.urlencoded() 这个中间件，来解析 表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false }))
app.post('/user', (req, res) => {
  // 在服务器，可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})
app.post('/book', (req, res) => {
  // 在服务器端，可以通过 req,body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
  console.log(req.body)
  res.send('ok')
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

第三方的中间件 

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置 第三方中间件，从而提高项目的开发效率。 

例如：在 express@4.16.0 之前的版本中，经常使用 body-parser这个第三方中间件,来解析请求体数据。使用步骤如下：

 ① 运行 npm install body-parser 安装中间件

 ② 使用 require 导入中间件

 ③ 调用 app.use() 注册并使用中间件 注意：Express 内置的express.urlencoded中间件，就是基于body-parser这个第三方中间件进一步封装出来的。

### 使用Express写接口

#### 基本使用

创建基本的服务器

```javascript
// 导入 express
const express = require('express')
// 创建服务器实例
const app = express()
//导入路由模块
const router=require('./apiRouter')
// app.use({})
//把路由模块注册到app上
app.use('/api',router)
// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

```javascript
// 创建 API 路由模块  apiRouter
const express = require('express')
const router = express.Router()
// 在这里挂载对应的路由
router.get('/get', (req, res) => {
  // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
  const query = req.query
  // 调用 res.send() 方法，向客户端响应处理的结果
  res.send({
    status: 0, // 0 表示处理成功，1 表示处理失败
    msg: 'GET 请求成功！', // 状态的描述
    data: query, // 需要响应给客户端的数据
  })
})

// 定义 POST 接口
router.post('/post', (req, res) => {
  // 通过 req.body 获取请求体中包含的 url-encoded 格式的数据
  const body = req.body
  // 调用 res.send() 方法，向客户端响应结果
  res.send({
    status: 0,
    msg: 'POST 请求成功！',
    data: body,
  })
})
// 定义 DELETE 接口
router.delete('/delete', (req, res) => {
  res.send({
    status: 0,
    msg: 'DELETE请求成功',
  })
})
module.exports = router
```

#### CORS 跨域资源共享

1、接口的跨域问题 

刚才编写的 GET 和 POST接口，存在一个很严重的问题：不支持跨域请求。

 解决接口跨域问题的方案主要有两种： 

① CORS（主流的解决方案，推荐使用） 

② JSONP（有缺陷的解决方案：只支持 GET 请求）

2、使用 cors 中间件解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。 使用步骤分为如下 3 步： 

① 运行 npm install cors 安装中间件 

② 使用 const cors = require('cors') 导入中间件 

③ 在路由之前调用 app.use(cors()) 配置中间件

#### JSONP 接口

## 4.数据库与身份认证

### 数据库的基本操作

### 在node.js中操作数据库

#### 配置mysql模块

 安装 mysql 模块

```javascript
npm install mysql
```

配置mysql模块

```javascript
//引入mysql模块
const mysql = require('mysql')
//配置数据库相关的信息
const db = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: 'root',
    database: 'dormitory'
})
```

测试 mysql 模块能否正常工作

调用 db.query() 函数，指定要执行的 SQL 语句，通过回调函数拿到执行的结果：

```javascript
db.query('select * from student where name="小明"', (err, results) => {
  if (err) {
   return console.log(err.message)
  }
  else {
    console.log(results)
  }
})
```

#### 使用 mysql 模块操作 MySQL 数据库

查询 users 表中所有的数据

```javascript
const sqlStr = 'select * from users'
db.query(sqlStr, (err, results) => {
  // 查询数据失败
  if (err) return console.log(err.message)
  // 查询数据成功
  // 注意：如果执行的是 select 查询语句，则执行的结果是数组
  console.log(results)
}) 
```

向 users 表中，新增一条数据，其中 username 的值为 Spider-Man，password 的值为 pcc123

```javascript
const user = { username: 'Spider-Man', password: 'pcc123' }
// 定义待执行的 SQL 语句
const sqlStr = 'insert into users (username, password) values (?, ?)'
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password], (err, results) => {
  // 执行 SQL 语句失败了
  if (err) return console.log(err.message)
  // 成功了
  // 注意：如果执行的是 insert into 插入语句，则 results 是一个对象
  // 可以通过 affectedRows 属性，来判断是否插入数据成功
  if (results.affectedRows === 1) {
    console.log('插入数据成功!')
  }
}) 
```

插入数据的便捷方式

```javascript
 const user = { username: 'Spider-Man2', password: 'pcc4321' }
// 定义待执行的 SQL 语句
const sqlStr = 'insert into users set ?'
// 执行 SQL 语句
db.query(sqlStr, user, (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('插入数据成功')
  }
}) 
```

更新用户的信息

```javascript
 const user = { id: 6, username: 'aaa', password: '000' }
// 定义 SQL 语句
const sqlStr = 'update users set username=?, password=? where id=?'
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
  if (err) return console.log(err.message)
  // 注意：执行了 update 语句之后，执行的结果，也是一个对象，可以通过 affectedRows 判断是否更新成功
  if (results.affectedRows === 1) {
    console.log('更新成功')
  }
}) 
```

更新数据的便捷方式

```javascript
 const user = { id: 6, username: 'aaaa', password: '0000' }
// 定义 SQL 语句
const sqlStr = 'update users set ? where id=?'
// 执行 SQL 语句
db.query(sqlStr, [user, user.id], (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('更新数据成功')
  }
}) 
```

 删除 id 为 5 的用户

```javascript
 const sqlStr = 'delete from users where id=?'
db.query(sqlStr, 5, (err, results) => {
  if (err) return console.log(err.message)
  // 注意：执行 delete 语句之后，结果也是一个对象，也会包含 affectedRows 属性
  if (results.affectedRows === 1) {
    console.log('删除数据成功')
  }
})
```

标记删除

```javascript
const sqlStr = 'update users set status=? where id=?'
db.query(sqlStr, [1, 6], (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('标记删除成功')
}
```

### 前后端的身份认证

#### Web 开发模式

 目前主流的 Web 开发模式有两种，分别是： 

​		① 基于服务端渲染的传统 Web 开发模式 

​		② 基于前后端分离的新型 Web 开发模式

服务端渲染的优缺点 

优点： 

​		① 前端耗时少。因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤		其是移动端，更省电。 

​		② 有利于SEO。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信		息，更有利于 SEO。 

缺点： 

​		① 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造		成一定的访问压力。 

​		② 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端		复杂度高的项目，不利于 项目高效开发。

前后端分离的优缺点 

优点： 

​		① 开发体验好。前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。 

​		② 用户体验好。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷		新。 

​		③ 减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。 

缺点： 

​		① 不利于 SEO。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面		的有效信息。（解决方案：利用 Vue、React 等前端框架的 SSR （server side render）技术能		够很好的解决 SEO 问题！）

#### 身份认证

身份认证（Authentication）又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。

不同开发模式下的身份认证 

对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案： 

​		① 服务端渲染推荐使用 Session 认证机制 

​		② 前后端分离推荐使用 JWT 认证机制

Session 认证机制

Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用 于控制 Cookie 有效期、安全性、使用范围的可选属性组成。 不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器。 

Cookie的几大特性： 

​		① 自动发送 

​		② 域名独立 

​		③ 过期时限 

​		④ 4KB 限制

Cookie 不具有安全性 

由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全 性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

**注意：千万不要使用 Cookie 存储重要且隐私的数据！比如用户的身份信息、密码等**

#### 在 Express 中使用 Session 认证

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// TODO_01：请配置 Session 中间件
const session = require('express-session')
//express-session 中间件安装成功后，需要通过 app.use() 来注册 session 中间件
app.use(
  session({
    secret: 'itheima',
    resave: false,
    saveUninitialized: true,
  })
)
// 托管静态页面
app.use(express.static('./pages'))
// 解析 POST 提交过来的表单数据
app.use(express.urlencoded({ extended: false }))

// 登录的 API 接口
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' })
  }
  // TODO_02：请将登录成功后的用户信息，保存到 Session 中
  // 注意：只有成功配置了 express-session 这个中间件之后，才能够通过 req 点出来 session 这个属性
  req.session.user = req.body // 用户的信息
  req.session.islogin = true // 用户的登录状态
  res.send({ status: 0, msg: '登录成功' })
})
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
  // TODO_03：请从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    return res.send({ status: 1, msg: 'fail' })
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  })
})

// 退出登录的接口
app.post('/api/logout', (req, res) => {
  // TODO_04：清空 Session 信息
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1:80')
})
```

#### JWT 认证机制

了解 Session 认证的局限性 

Session 认证机制需要配合 Cookie 才能实现。由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接 口的时候，需要做很多额外的配置，才能实现跨域 Session 认证。 

注意： 

​		当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。 

​		当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证		机制。

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案。

用户的信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份

JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效荷载）、Signature（签名）。

​	**Payload 部分才是真正的用户信息**，它是用户信息经过加密之后生成的字符串。 

​	 Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')

// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }))

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
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
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
```


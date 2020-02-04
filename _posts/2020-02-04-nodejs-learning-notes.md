---
layout: post
title: "Node.js Learning Notes"
subtitle: 
date: 2020-02-04 11:59:57
catalog: true
tags: 
header-img: http://ww1.sinaimg.cn/large/007dh5vlly1g5bcln7dflj30kb06u74a.jpg
post_copyright: true
author: Jerry
---


<center>Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。</center> 
<center>Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。</center>
# Node.js适用场景

 Node.js 擅长处理 I/O，不善于计算（单线程的缺点），因此 Node.js 适用于：当应用程序需要处理大量并发的 I/O，而在向客户端发出响应之前，应用程序内部并不需要进行非常复杂的处理的时候，Node.js 也非常适合与 web socket 配合，开发长连接的实时交互应用程序。
 比如：聊天室，博客系统，考试系统等。

# 全局对象

在 JavaScript 中全局对象通常是 window，而在 Node.js 中全局对象是 globa，所有全局变量（除了 global 本身以外）都是 global 对象的属性，我们可以直接访问到 global 的属性

## 全局变量

按照 ECMAScript 的定义，满足以下条 件的变量是全局变量：

+ 在最外层定义的变量

+ 全局对象的属性

+ 隐式定义的变量（未定义直接赋值的变量）

>当你定义一个全局变量的时候，这个变量同时也会成为全局对象的属性，反之亦然。在 Node.js 中你不可能在最外层定义变量，因为所有用户代码都是属于当前模块的，而模块本身不是最外层上下文。定义变量一定要使用 var 关键字，因为全局变量会污染命名空间。

### 常见全局变量和全局函数

- __filename 表示当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。如果在模块中，返回的值是模块文件的路径。
- __dirname，表示当前执行脚本所在的目录。
- setTimeout(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb),只执行一次函数。
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5bvhqxm8rg30y20b8mxu.gif)

# require方法--创建hello world

Node中的JavaScript可以具备文件操作能力，得益于丰富的API。

引入核心模块`fs`，调用相应的API即可实现


```js
var fs = require('fs')//用require方法创建实例
fs.writeFile('./hello.md','写入一段文本')

var http = require('http')
var server = http.createServer()
server.on('request',function(request,response){
    console.log('收到请求:'+request.url)
    response.write('hello')
    response.end()
})
server.listen(3000,function(){
    console.log('启动咯')
})
```


```js
var http = require('http');
http.createServer(function(request,response){
    response.writeHead(200,{'Content-Type':'text/plain'});
    response.end('hello world');
}).listen(8080);
console.log('开启咯')
```


`http.createServer([requestListener])`
其中`requestListener 请求函数`是一个自动添加到 'request' 事件的函数。函数传递有两个参数：request 请求对象 和 response 响应对象。

**response 对象**常用的方法有：

- response.writeHead(statusCode[, statusMessage][, headers])。表示向请求发送响应头。
- response.write() 发送一块响应主体，也就是说用来给客户端发送响应数据。可以直接写文本信息，也可以写我们的 html 代码，注意要设置 Content-Type 的值 。write 可以使用多次，但是最后一定要使用 end 来结束响应，否则客户端会一直等待。

- response.end() 此方法向服务器发出信号，表示已发送所有响应头和主体，该服务器应该视为此消息完成。必须在每个响应上调用方法 response.end()。

**request**对象的常用方法：

- request.url 获取请求路径，获取到的是端口号之后的那一部分路径,也就是说所有的 url 都是以 / 开头的，判断路径处理响应。

- request.socket.localAddress 获取 ip 地址。

- request.socket.remotePort 获取源端口。

# Node.js包

用于管理多个模块及其依赖关系，可以对多个模块进行封装，包的根目录必须包含 package.json 文件，package.json 文件是 CommonJS 规范用于描述包的文件，符合 CommonJS 规范的 package.json 文件一般包含以下字段：

1. name：包名。包名是唯一的，只能包含小写字母、数字和下划线。
2. version：包版本号。
3. description：包说明。
4. keywords：关键字数组，用于搜索。
5. homepage：项目主页。
6. bugs：提交 bug 的地址。
7. license：许可证。
8. maintainers：维护者数组。
9. contributors：贡献者数组。
10. repositories：项目仓库托管地址数组。
11. dependencies：包依赖。这个属性十分重要，NPM会通过这个属性，帮你自动加载依赖的包

>packae.json包示例
```json
{
    "name": "shiyanlou",
    "description": "Shiyanlou test package.",
    "version": "0.1.0",
    "keywords": [
        "shiyanlou",
        "nodejs"
     ],
    "maintainers": [{
        "name": "test",
        "email": "test@shiyanlou.com"
    }],
    "contributors": [{
        "name": "test",
        "web": "http://www.shiyanlou.com/"
    }],
    "bugs": {
        "mail": "test@shiyanlou.com",
        "web": "http://www.shiyanlou.com/"
    },
    "licenses": [{
        "type": "Apache License v2",
        "url": "http://www.apache.org/licenses/apache2.html"
    }],
    "repositories": [{
        "type": "git",
        "url": "http://github.com/test/test.git"
    }],
    "dependencies": { 
        "webkit": "1.2",
        "ssl": { 
            "gnutls": ["1.0", "2.0"],
            "openssl": "0.9.8"
        }
    }
}
```
>注：
>package.json 文件可以自己手动编辑，还可以通过 npm init 命令进行生成。你可以自己尝试在终端中输入 npm init 命令来生成一个包含 package.json 文件的包。直接输入 npm init --yes 跳过回答问题步骤，直接生成默认值的 package.json 文件。

==安装包==
`npm install express`

==更新包==
`npm update express`

==删除包==
`npm uninstall express`

# Node.js模块

在 JavaScript 中，我们通常把 JavaScript 代码分为几个 js 文件，然后在浏览器中将这些 js 文件合并运行，但是在 Node.js 中，是通过以模块为单位来划分所有功能的，每一个模块为一个 js 文件，每一个模块中定义的全局变量和函数的作用范围也被限定在这个模块之内，只有使用 **exports 对象**才能传递到外部使用。

▶1.js
```javascript
function foo(){
    console.log('hello');
}
module.exports.foo = foo;//用module.exports导出,也可以直接exports导出
```
▶2.js
```javascript
var hello = require('./1.js');
hello.foo();
```

>**require 加载模块**，以'/' 为前缀的模块是文件的绝对路径。'./' 为前缀的模块是相对于调用 require() 的文件的，上面的例子中 index.js 和 myModule.js 是在同一个目录下（project 目录）。当没有以 '/'、'./' 或 '../' 开头来表示文件时，这个模块必须是一个核心模块或加载自 node_modules 目录。

<div class="tip inlineBlock important">module.exports 和 exports 的区别</div>

每次导出接口成员的时候都通过 module.exports.xxx = xxx 的方式很麻烦。所以，Node.js 为了简化你的操作，专门提供了一个变量：exports 等于 module.exports。也就是说在模块中还有这么一句代码：
`var exports = module.exports;`

让我们看一下它们
```javascript
a = {
    b:3
}
console.log(a);
console.log(module.exports);
console.log(exports == module.exports)
console.log(exports === module.exports)
```
运行结果：
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5c5b4u4rgj30k502mt8l.jpg)

```javascript
exports = {
    b:3
}
console.log(exports);
console.log(module.exports);
console.log(exports == module.exports)
console.log(exports === module.exports)
```
运行结果：
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5c5cylve6j30i002ldfq.jpg)

也就是说给 exports 赋值会断开和 module.exports 之间的引用，同样的给 module.exports 重新赋值也会断开它们之间的引用。但是最终导出的是 module.exports。而如果给其他变量赋值则没有对exports 和 module.exports之间的引用造成改变。即module.exports才是真正的接口，exports只不过是它的一个辅助工具。最终返回给调用的是module.exports而不是exports

**总结：**
require 得到的是 module.exports 导出的值，导出多个成员可以用 module.exports 和 exports,导出单个成员只能用 module.exports。

# Node.js函数

在 JavaScript 中，一个函数可以作为另一个函数的参数。我们可以先定义一个函数，然后把函数作为变量在另一个函数中传递，也可以在传递参数的地方直接定义函数。

```javascript
function sayHi(value){
    console.log(value);
}
function execute(someFunction,value){
    someFunction(value);
}
execute(sayHi,'hi');
```
## 匿名函数

```javascript
var fun = function(){

}
```
### 箭头函数
```javascript
(参数1, 参数2, …, 参数N) => { 函数声明 }

//相当于：(参数1, 参数2, …, 参数N) =>{ return 表达式; }
(参数1, 参数2, …, 参数N) => 表达式（单一）

// 当只有一个参数时，圆括号是可选的
(单一参数) => {函数声明}
单一参数 => {函数声明}

// 没有参数的函数应该写成一对圆括号。
() => {函数声明}
```
示例：
```javascript
var fun = function(){
    console.log('hello syl');
}
//上面的匿名函数可以用箭头函数改写为下面的
var fun = () => console.log('hello syl');
```


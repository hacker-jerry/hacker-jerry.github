---
layout: post
title: "Node.js Learning Notes 2"
subtitle: 学习Node.js
date: 2020-02-04 12:11:09
catalog: true
tags: 
header-img: http://blog.img.hackerjerry.top/FvTXExGq7_Blv_6f1KX8bfa_KdF8
post_copyright: true
author: Jerry
---
# Node.js 异步编程

Node.js 异步编程的直接体现就是**回调**。回调函数在完成任务后就会被调用，Node.js 使用了大量的回调函数，Node.js 所有 API 都支持回调函数。回调函数一般作为函数的最后一个参数出现。

## 阻塞代码

```javascript
var fs = require('fs');
var data = fs.readFileSync('1.txt');
console.log(data.toString());
console.log('end')
```
运行结果：
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5c6kgip3yj30mm01iq2t.jpg)

## 非阻塞代码

```javascript
var fs = require('fs');
fs.readFile('1.txt',function (err,data){
    if(err) return console.error(err);
    console.log(data.toString());
});
console.log('end');
```
运行结果：
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5c6p84k91j30mr01l3ye.jpg)

第一个实例在文件读取完后才执行完程序。 第二个实例我们不需要等待文件读取完，这样就可以在读取文件时同时执行接下来的代码，大大提高了程序的性能。

## 异步打开文件

`fs.open(path, flags[, mode], callback)`

参数说明：

- path:文件的路径

- flags：文件打开的行为。

- mode：设置文件模式(权限)，文件创建默认权限为 0o666（可读写）。mode 设置文件模式（权限和粘滞位），但仅限于创建文件的情况。在 Windows 上，只能操作写权限。

- callback：回调函数，带有两个参数如：callback(err, fd)。

- flags 参数可以是以下值：

> 'a' - 打开文件用于追加。如果文件不存在，则创建该文件。
>
> 'ax' - 与 'a' 相似，但如果路径存在则失败。
>
> 'a+' - 打开文件用于读取和追加。如果文件不存在，则创建该文件。
>
> 'ax+' - 与 'a+' 相似，但如果路径存在则失败。
>
> 'as' - 以同步模式打开文件用于追加。如果文件不存在，则创建该文件。
>
> 'as+' - 以同步模式打开文件用于读取和追加。如果文件不存在，则创建该文件。
>
> 'r' - 打开文件用于读取。如果文件不存在，则会发生异常。
>
> 'r+' - 打开文件用于读取和写入。如果文件不存在，则会发生异常。
>
> 'rs+' - 以同步模式打开文件用于读取和写入。指示操作系统绕开本地文件系统缓存。这对于在 NFS 挂载上打开文件非常有用，因为它允许跳过可能过时的本地缓存。 它对 I/O 性能有非常实际的影响，因此除非需要，否则不建议使用此标志。这不会将 fs.open() 或 fsPromises.open() 转换为同步的阻塞调用。 如果需要同步操作，则应使用 fs.openSync() 之类的操作。
>
> 'w' - 打开文件用于写入。创建文件（如果它不存在）或截断文件（如果存在）。
>
> 'wx' - 与 'w' 相似，但如果路径存在则失败。
>
> 'w+' - 打开文件用于读取和写入。创建文件（如果它不存在）或截断文件（如果存在）。
>
> 'wx+' - 与 'w+' 相似，但如果路径存在则失败。

## 异步关闭文件

`fs.close(fd, callback)`
参数说明：

- fd：通过 fs.open() 方法返回的文件描述符。

- callback：回调函数，除了可能的异常，完成回调没有其他参数。
  
```javascript
var fs = require("fs");
// 异步打开文件
fs.open('test.txt', 'r+', function(err, fd) {
   if (err) {
       return console.error(err);
   }
   console.log("文件打开成功！");
      //异步关闭文件
      fs.close(fd, function(err){//特别注意：fs.close是包在fs.open中参数之一的回调函数中的，而且它们的参数形式不同。 fs.open是文件路径名,fs.close是传入的回调函数的fd参数。
         if (err){
            console.log(err);
         }
         console.log("文件关闭成功");
      });
});
```

## 读写文件

**异步读取文件的语法格式为：

`fs.read(fd, buffer, offset, length, position, callback)`

参数说明：

- fd: 通过 fs.open() 方法返回的文件描述符。//不能变成路径！

- buffer:是数据写入的缓冲区。 
>通常用var buf= Buffer.alloc(1024)创建1024字节的缓冲区然后传参

- offset:是缓冲区中开始写入的偏移量。一般它的值我们写为 0。

- length:是一个整数，指定要读取的字节数。

- position:指定从文件中开始读取的位置。 如果 position 为 null，则从当前文件位置读取数据，并更新文件位置。

- callback:回调函数，有三个参数 err, bytesRead, buffer。err 为错误信息， bytesRead 表示读取的字节数，buffer 为缓冲区对象。
**示例：**
```javascript
var fs = require("fs");
// 异步打开文件
fs.open('test.txt', 'r+', function(err, fd) {
    if(err) {
        return console.error(err);
    }
    console.log("文件打开成功！");
    console.log("准备读取文件：");
    // 创建一个大小为 1024 字节的缓存区
    var buf = Buffer.alloc(1024);
    // 异步读取文件
    fs.read(fd, buf, 0, buf.length, 0, function(err, bytes, buf) {
        if(err) {
            console.log(err);
        }
        console.log(bytes + "字节被读取");
        // 仅输出读取的字节
        if(bytes > 0) {
            console.log(buf.slice(0, bytes).toString());
        }
        // 异步关闭文件
        fs.close(fd, function(err) {
            if(err) {
                console.log(err);
            }
            console.log("文件关闭成功");
        });
    });
});
```
**异步写入文件的语法格式为：**

`fs.write(fd, buffer, offset, length, position, callback)`

参数说明：

- fd：从指定的文件写入数据。

- buffer：是数据写入的缓冲区。

- offset：指定要写入的 buffer 部分。

- length：是一个整数，指定要写入的字节数。

- position 指定应该写入此数据的文件开头的偏移量。 如果 typeof position !== 'number'，则从当前位置写入数据。

- callback：回调有三个参数 (err, bytesWritten, buffer)，其中 bytesWritten 指定从 buffer 写入的字节数。
```javascript
var fs = require('fs');
// 异步打开文件
fs.open('./test.txt', 'a', function(err, fd) {
    if(err) {
        return console.error(err);
    }
    console.log("文件打开成功！");
    console.log("准备写入文件：");
    //新写入内容为 hello world
    var buffer = Buffer.from(new String(' hello world'));
    // 异步写入文件
    fs.write(fd, buffer, 0, 12, 0, function(err, bytes, buffer) {//0，12这两个参数 一个是buffer字符串位于开头的偏移量 一个是总共要写入的字符数 它们的和 不能超过buffer的总长度
        if (err) {
            throw err;
        }
        console.log('写入成功');
        // 打印出buffer中存入的数据
        console.log(bytes + "字节被写入");
        console.log(buffer.slice(0, bytes).toString());
        // 异步关闭文件
        fs.close(fd, function(err) {
            if(err) {
                console.log(err);
            }
            console.log("文件关闭成功");
        });
    });
});
```
或
`fs.write(fd, string[, position[, encoding]], callback)`
参数说明：

- fd：从指定的文件写入数据。

- string:写入的数据，如果不是字符串，则该值将被强制转换为字符串。

- position 指定应该写入此数据的文件开头的偏移量。 如果 typeof position !== 'number'，则从当前位置写入数据。

- encoding：指定字符串的编码，默认为 'utf8'。

- callback：回调有三个参数 (err, written, string)，其中 written 指定字符串中已写入文件的字节数。 写入的字节数与字符串的字符数是不同的。
```javascript
var fs = require('fs')
fs.open('./1.txt','a',function(err,fd){
    if(err)
        console.error(err)
    var data = 'hello'
    fs.write(fd,data,0,'utf-8',function(err,bytes,Buffer){
        if(err)
        console.error(err)
        console.log(Buffer)
    })
    fs.close(fd,function(err){
        if(err)
        console.error(err)
    })
})
```
以上方法都是基于`fs.open()函数`的，那么有没有简单粗暴点的函数呢？
Yeap！
`fs.readFile(path,[options], callback)`闪亮登场
法一：
```javascript
var fs = require('fs')
fs.readFile('./1.txt',function(err,data){
    if(err)
    console.log(err)
    console.log(data.toString())
})
```
法二：
```javascript
var fs = require('fs');
fs.readFile('./test.txt', 'utf-8', function(err, data) {//加上编码方式
    if (err) {
        throw err;
    }
    console.log(data);
});
```
`fs.writeFile(file, data,[options], callback)`
参数说明：

- file：文件名或文件描述符。
- data：要写入文件的数据，可以是 String(字符串) 或 Buffer(缓冲) 对象。
- options：该参数是一个对象，包含 {encoding, mode, flag}。encoding 默认值为：'utf8', mode 默认值为 0o666 ，flag 默认为 'w'。
- callback：回调函数。
示例：
```javascript
var fs = require('fs');
// 传递了追加参数 { 'flag': 'a' }
fs.writeFile('./test.txt', '我是新加的内容', { 'flag': 'a' }, function(err) {
    if (err) {
        throw err;
    }
    console.log('Saved.');
    // 写入成功后读取测试
    fs.readFile('./test.txt', 'utf-8', function(err, data) {
        if (err) {
            throw err;
        }
        console.log(data);
    });
});
```
专门的异步追加函数`fs.appendFile(path, data[, options], callback)`

```javascript
fs.appendFile('message.txt', '追加的数据', (err) => {
  if (err) throw err;
  console.log('数据已追加到文件');
});
```
如果 options 是字符串，则它指定字符编码：
`fs.appendFile('message.txt', '追加的数据', 'utf8', callback);`

## 截取文件（将文件只保留前n个字节）
`fs.ftruncate(fd[, len], callback)`
参数说明：

- fd：通过 fs.open() 方法返回的文件描述符。

- len：文件内容截取的长度，默认为 0。

- callback：除了可能的异常，完成回调没有其他参数。
```javascript
var fs = require('fs')
fs.open('./1.txt','r+',function(err,fd){//注意这里必须是r+属性，否则无法截取
        if(err)
        throw err
        fs.ftruncate(fd,3,function(err){

            fs.readFile('./1.txt',function(err,data){
                console.log(data.toString())
            })
        })
})
```

## 删除文件
`fs.unlink(path, callback)`
参数说明：

- path:文件路径。

- callback: 除了可能的异常，完成回调没有其他参数。
  
## 修改文件名
`fs.rename(oldPath, newPath, callback)`
参数说明：

- oldPath:原来的文件名字。

- newPath：新的文件名字。

- callback：回调函数，除了可能的异常，完成回调没有其他参数。


## 目录操作
### 新建目录
`fs.mkdir(path[, options], callback)`
参数说明：

- path：文件路径(名)。

- options：有两个参数。recursive 表示是否以递归的方式创建目录，默认为 false。mode 设置目录权限，Windows 上不支持。默认为 0o777。

- callback：回调函数，除了可能的异常，完成回调没有其他参数。

### 读取目录
`fs.readdir(path[, options], callback)`
参数说明：

- path：文件路径。

- options：有两个参数 encoding，withFileTypes。encoding 默认值为 'utf8'，withFileTypes 默认值为 false。

- callback - 回调函数，回调函数带有两个参数 err, files。err 为错误信息，files 为目录下的文件数组列表。
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5ea0oeoe1j30rb0g8761.jpg)

### 删除目录
`fs.rmdir(path, callback)`

# Node.js事件

大多数 Node.js 核心 API 构建于惯用的异步事件驱动架构，其中某些类型的对象（又称触发器，Emitter）会触发命名事件来调用函数（又称监听器，Listener）。比如：fs.readStream 打开文件时会发出一个事件。可以通过 require("events"); 获得 event 模块。通常，事件名采用“驼峰式”(即单词首字母大写，其他字母小写)命名方式。

## EventEmitter
所有能触发事件的对象都是 EventEmitter 类的实例。这些对象有一个 eventEmitter.on() 函数，用于将一个或多个函数绑定到命名事件上。当 EventEmitter 对象触发一个事件时，所有绑定在该事件上的函数都会被同步地调用。
** EventEmitter类获取**
```javascript
// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();
```
### 添加监听器
`emitter.on(eventName, listener)`
使用 emitter.on(eventName, listener) 方法为指定事件注册一个监听器。添加 listener 函数到名为 eventName 的事件的监听器数组的末尾。
>别名   emitter.addListener(eventName, listener) 

注意，**这种注册监听器的方法将监听器一直保留在内存中**
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5dkupxxjfj30z70h6ac3.jpg)

**参数说明：**
- eventName：事件名称，string 类型。
- listener：回调函数。
**示例**
```javascript
//引入 events 模块
var events = require('events');
// 创建 emitter 对象
var emitter = new events.EventEmitter();
//为 connection 事件注册一个监听器
emitter.on('connection', function() {
  console.log('已连接');
});
//一秒后调用监听器
setTimeout(function() {
    emitter.emit('connection');
}, 1000);
```
运行结果：
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5c8b4xxweg30y20gw0u0.gif)

其原理是`emitter`对象给`connection`事件注册了监听器，用**setTimeout**函数1000毫秒后向`emitter`对象发送事件`connection`，此时调用它的监听器。`emit`方法就是发送事件的。
使用` emitter.emit(eventName[, ...args]) `按照监听器注册的顺序，同步地调用每个注册到名为` eventName `的事件的监听器，并传入提供的参数。如果事件有注册监听返回 **true**，否则返回 **false**。

参数说明：

- eventName ：事件名称
- args：传递的参数，多个，类型为任意。

默认情况下，事件监听器会按照添加的顺序依次调用。`emitter.prependListener()` 方法可用于将事件监听器添加到监听器数组的开头。

例如在`setTimeout`前添加，`emitter.prependListener('connection',() =>console.log('hh'));`，将会先打印**hh**,再打印**已连接**。

-----------------------------------------------------------
` eventEmitter.once(eventName, listener) `

此可以注册最多可调用一次的监听器。 当事件被触发时，监听器会被注销，然后再调用。
![](http://ww1.sinaimg.cn/large/007dh5vlly1g5dky9oqukj30vg0d0wg2.jpg)
而`emitter.prependOnceListener()` 方法可用于将事件监听器添加到监听器数组的开头。

### 移除监听器

`emitter.removeListener(eventName, listener)`
参数说明：

- eventName 事件名称
- listener 监听器也就是回调函数名称。

>注：removeListener() 最多只会从监听器数组中移除一个监听器。我们可以多次调用 removeListener() 的方式来一个个的移除我们需要移除掉的监听器。

>emitter.off(eventName, listener)是emitter.removeListener()的别名

`emitter.removeAllListeners([eventName])`
使用 emitter.removeAllListeners([eventName]) 移除全部监听器或指定的 eventName 事件的监听器。

### 设置监听器最大绑定数

`emitter.setMaxListeners(n)`
默认情况下，如果为特定事件添加了超过 10 个监听器，则 EventEmitter 会打印一个警告，这有助于我们发现内存泄露。显然实际编码中并不是所有的事件都要限制 10 个监听器。 emitter.setMaxListeners() 方法可以为指定的 EventEmitter 实例修改限制。当值设为 Infinity（或 0）表示不限制监听器的数量。

### 查看事件绑定的监听器个数

`emitter.listenerCount(eventName)`

## error事件

当 EventEmitter 实例出错时，应该触发 'error' 事件。

如果没有为 'error' 事件注册监听器，则当 'error' 事件触发时，会抛出错误、打印堆栈跟踪、并退出 Node.js 进程。

通常我们要为会触发 error 事件的对象设置监听器，避免遇到错误后整个程序崩溃。

```javascript
var events = require('events');
var emitter = new events.EventEmitter();
emitter.on('error',(err)=>{
	console.error('错误');
});
emitter.emit('error');
```

# Node.js框架---Express框架

可以通过 Express 可以快速地搭建一个完整功能的网站。使用框架的目的就是让我们更加专注于业务，而不是底层细节。
**第一个示例**
```javascript
var express = require('express');
var app = express();

app.get('/', function (req, res) {
   res.send('Hello World');
});

app.listen(3000, function () {
  console.log("服务器启动了");
});
```
## 路由
`app.method(path, handler)`
路由**用于**确定应用程序如何响应客户端请求，包含一个 URI（路径）和一个特定的 HTTP 请求方法（GET、POST 等）。
>注：app 是 express 的实例，method 是指 HTTP 请求方法（GET、POST 等），path 是指服务器上的路径，handler 是指路由匹配时执行的函数。

栗子
```javascript
var express = require('express');
var app = express();

// GET 请求
app.get('/', function (req, res) {
   console.log("GET 请求");
   res.send('Hello，我是GET请求');
})

// POST 请求
app.post('/', function (req, res) {
   console.log("POST 请求");
   res.send('Hello，我是 POST 请求');
})

// /index 响应index页面 GET 请求
app.get('/index', function (req, res) {
   console.log("/响应index页面 GET 请求");
   res.send('Hello，我是 index 页面 GET 请求');
})
```
## 静态文件
公开`public`目录，然后访问其中的资源
`app.use('/public/', express.static('./public/'))`
或者
```javascript
var express = require('express');
var app = express();

app.use(express.static('public'));

app.get('/', function (req, res) {
  res.send('Hello World');
})

app.listen(8080, function () {
  console.log("服务器启动了");
});
```
## Express 框架处理POST请求

<!-- tab 1.js -->
```js
var express = require('express')
var app = express()
var bodyParser = require('body-parser')
  //创建 application/x-www-form-urlencoded 解析
var urlencodedParser = bodyParser.urlencoded({extended: false})
app.get('/', function (req, res) {
    //传送指定路径的文件 -会自动根据文件extension设定Content-Type
    //也可以用前面的 art-template 模板引擎
    //必须有
   res.sendFile( __dirname + "/" + "1.html" );
})
//获取 URL编码的请求体
app.post('/post_test',urlencodedParser,function(req,res){
    var response = {
        "stuNum":req.body.stuNum,
        "stuNam":req.body.stuNam
    }
    console.log(response)
    res.end(JSON.stringify(response))
})
app.listen('8080',function(){
    console.log('start')
})
```
<!-- endtab -->
<!-- tab 1.html -->
```html
<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    
    <body>
        <form action="/post_test" method="POST">
            学号: <input type="text" name="stuNum"><br />
            姓名: <input type="text" name="stuNam">
            <input type="submit" value="提交">
        </form>
    </body>

</html>
```
<!-- endtab -->


这里用到了`body-parser`这个HTTP**请求体解析中间件**，用这个模块可以解析JSON、Raw、文本、URL-encoded格式的请求体

1. bodyParser.json(options): 解析json数据
2. bodyParser.raw(options): 解析二进制格式(Buffer流数据)
3. bodyParser.text(options): 解析文本数据
4. bodyParser.urlencoded(options): 解析UTF-8的编码的数据。

option可选对象:

<!-- tab bodyParser.json()-->

1. inflate - 设置为true时，deflate压缩数据会被解压缩；设置为true时，deflate压缩数据会被拒绝。默认为true。
2. limit - 设置请求的最大数据量。默认为'100kb'
3. reviver - 传递给JSON.parse()方法的第二个参数，详见JSON.parse()
4. strict - 设置为true时，仅会解析Array和Object两种格式；设置为false会解析所有JSON.parse支持的格式。默认为true
5. type - 该选项用于设置为指定MIME类型的数据使用当前解析中间件。这个选项可以是一个函数或是字符串，当是字符串是会使用type-is来查找MIMI类型；当为函数是，中间件会通过fn(req)来获取实际值。默认为application/json。
6. verify - 这个选项仅在verify(req, res, buf, encoding)时受支持
<!-- endtab -->
<!-- tab bodyParser.raw()-->
1. inflate - 设置为true时，deflate压缩数据会被解压缩；设置为true时，deflate压缩数据会被拒绝。默认为true。
2. limit - 设置请求的最大数据量。默认为'100kb'
3. type - 该选项用于设置为指定MIME类型的数据使用当前解析中间件。这个选项可以是一个函数或是字符串，当是字符串是会使用type-is来查找MIMI类型；当为函数是，中间件会通过fn(req)来获取实际值。默认为application/octet-stream。
4. verify - 这个选项仅在verify(req, res, buf, encoding)时受支持
<!-- endtab -->
<!-- tab bodyParser.text()-->
1. defaultCharset - 如果Content-Type后没有指定编码时，使用此编码。默认为'utf-8'
2. inflate - 设置为true时，deflate压缩数据会被解压缩；设置为true时，deflate压缩数据会被拒绝。默认为true。
3. limit - 设置请求的最大数据量。默认为'100kb'
4. type - 该选项用于设置为指定MIME类型的数据使用当前解析中间件。这个选项可以是一个函数或是字符串，当是字符串是会使用type-is来查找MIMI类型；当为函数是，中间件会通过fn(req)来获取实际值。默认为application/octet-stream。
5. verify - 这个选项仅在verify(req, res, buf, encoding)时受支持
<!-- endtab -->
<!-- tab bodyParser.urlencoded()-->
1. extended - 当设置为false时，会使用querystring库解析URL编码的数据；当设置为true时，会使用qs库解析URL编码的数据。后没有指定编码时，使用此编码。默认为true
2. inflate - 设置为true时，deflate压缩数据会被解压缩；设置为true时，deflate压缩数据会被拒绝。默认为true。
3. limit - 设置请求的最大数据量。默认为'100kb'
4. parameterLimit - 用于设置URL编码值的最大数据。默认为1000
5. type - 该选项用于设置为指定MIME类型的数据使用当前解析中间件。这个选项可以是一个函数或是字符串，当是字符串是会使用type-is来查找MIMI类型；当为函数是，中间件会通过fn(req)来获取实际值。默认为application/octet-stream。
6. verify - 这个选项仅在verify(req, res, buf, encoding)时受支持
<!-- endtab -->
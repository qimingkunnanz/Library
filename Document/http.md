## 服务器

#### 1. B/S交互模型 服务器 --HTTP-->浏览器 

#### 2. HTTP协议:请求 - 处理 - 响应

> - ==请求==:客户
> - 处理:服务器
> - ==响应==:服务器将处理完的结果通过网络返回发送给客户

静态资源:不需要处理

动态资源:服务器上没有的资源,需要动态生成的

#### 3.  node.js提供HTTP模块 可以自己搭建服务器(有c++实现 性能可靠)

### 1. 创建服务器

```js
// 1.导入模块
const http = require('http');
// 2.调用方法
const server = http.createServer();
// 3.绑定事件
// rep:请求
// res:响应
server.on('request', function(rep, res) {
  // 防止中文乱码
  res.writeHeader(200, {
    'Content-Type': 'text/plain;charset=utf-8'
  });
  // res.end('hello world');
  res.end('你好');
});
// 4.启动服务器
// '127.0.0.1':不写就默认127.0.0.1 回调函数也可以不写
server.listen(500, '127.0.0.1', function() {
  console.log('server http://127.0.0.1:500');
});
```

### 2. 根据不同url地址返回不同的页面

```js
const http = require('http')

const server = http.createServer()

server.on('request', function (req, res) {
  // 打印客户端请求的 URL 地址
  // console.log(req.url)
  const url = req.url

  // 防止中文乱码
  res.writeHeader(200, {
    //  text/plain  和  text/html 的区别： plain 表示普通的文本字符串；  html 表示以 HTMl 标签的形式去解析服务器返回的内容
    // image/jpg     image/gif     image/png
    'Content-Type': 'text/html; charset=utf-8'
  })

  if (url === '/' || url === '/index.html') {
    res.end('<h3>首页</h3>')
  } else if (url === '/movie.html') {
    res.end('<h3>电影</h3>')
  } else if (url === '/about.html') {
    res.end('<h3>关于</h3>')
  } else {
    res.end('<h3>请求的内容不存在！</h3>')
  }
})

server.listen(3000, function () {
  console.log('server running at http://127.0.0.1:3000')
})
```

### 3.最终页面

```js
const http = require('http');
const path = require('path');
const fs = require('fs');
const server = http.createServer();
// req:服务器 
server.on('request', (req, res) => {
  let url = req.url;
  if (url == '/') {
    url = './views/index.html';
  }
  fs.readFile(path.join(__dirname, url), (err, data) => {
    if (err) return new Error('文件读取失败');
    res.end(data);
  })
});
server.listen(500);
```

MIME

## URL 统一资源定位符

URL：Uniform Resource Locator统一资源定位符

　　用于定位网络上我们需要访问的资源

组成：协议名称+域名+路径+资源的名称。如:https://img13.360img.com/da/jfs/t15031/162/1989680528/5a.gif

其中：5a.gif是文件名

　　da/jfs/t15031/162/1989680528是服务器上存储gif文件的路径

　　img13.360img.com是域名

　　https是协议名

## 报错信息

pending:(后台)路径找不到

客户端的请求服务器没有(监听)处理就无法响应

href 和 src(会自己发送请求)由HTML发送请求
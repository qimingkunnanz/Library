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





1. HTTP 协议（HyperText Transfer Protocol，超文本传输协议）
2. HTTPS 协议（HyperText Transfer Protocol over Secure Socket Layer）：可以理解为HTTP+SSL/TLS
3. SSL（Secure Socket Layer，安全套接字层）；SSL 协议位于 TCP/IP 协议与各种应用层协议之间，为数据通讯提供安全支持
4. TLS（Transport Layer Security，传输层安全）：其前身是 SSL；目前使用最广泛的是TLS 1.1、TLS 1.2。
5. 加密算法：
   1. 对称加密：加密和解密都是使用的同一个密钥
   2. 非对称加密：加密使用的密钥和解密使用的密钥是不相同的，分别称为：公钥、私钥；公钥和算法都是公开的，私钥是保密的；  常见的非对称加密的算法 RSA
   3. 哈希算法：将任意长度的信息转换为较短的固定长度的值,算法不可逆;MD5、SHA-1、SHA-2、SHA-256 等
   4. 数字签名: 签名就是在信息的后面再加上一段内容（信息经过hash后的值）



### tcp三次握手四次挥手

1. http是建立在 TCP/IP 协议之上的应用层规范， 
2. tcp/ip 是传输层和网络层的协议
3. http的请求和响应
   1. 输入网址www.baidu.com；先解析DNS，就是将域名转换为127.0.0.1之类的ip地址，然后加上端口，默认是80，建立socket套接字 (建立了连接)
   2. 发送请求类型： socket建立好之后，客户端向服务器发送请求命令 get/post 之类
   3. 发送请求头： 
   4. 回传状态行： 服务器响应的第一步，发送对应的状态码 200 404 500之类
   5. 回传响应头： 类似于Content-Type之类的信息
   6. 回传响应体： 类似于在浏览器的xhr的result里面
   7. 关闭连接， 如果是keep-alive 则TCP连接不关闭
4. TCP通信过程包括三个步骤：建立TCP连接通道，传输数据，断开TCP连接通道
   1. **第一次握手：**客户端发送syn包(seq=x)到服务器，并进入SYN_SEND状态，等待服务器确认 (客户端发送x)
   2. **第二次握手：**服务器收到syn包，必须确认客户的SYN(ack=x+1)，同时自己也发送一个SYN包(seq=y)，即SYN+ACK包，此时服务器进入SYN_RECV状态; (服务器发送x+1, 和y)
   3. **第三次握手：**客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=y+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。 (客户端发送y+1)



### http向https演化的过程

1. 防止传输的信息被黑客获取到后修改了，采用了一个办法；对传输的信息进行加密； 客户端和服务端用对应的 对称秘钥 加密和解密；  缺点：客户端/服务器数量庞大，要维护的秘钥太多不方便； 以及秘钥容易泄露
2. 客户端使用公钥加密，服务器使用私钥解密； 或者服务器使用公钥加密，客户端使用私钥解密； 这个中间黑客也有公钥(解密)，截取到信息后可以进行解密
3. 对称加密和非对称加密结合起来； 遇到的问题？ 怎么获取公钥， 怎么确定服务器是真实的而不是黑客？
   1. 获取公钥？ SSL证书(cert)； 客户端在请求服务器后，服务器发送了一个SSL证书给客户端， 里面有CA(证书的发布机构)，有效期，公钥，签名等
   2. 客户端解析证书； 客户端的TLS来完成，检测证书是否有问题，没问题就会生成一个随机值，然后用证书对该随机值进行加密，值为A
   3. 传送加密信息； 传送的是用证书(公钥)加密后的随机值，让服务端得到以后，后面服务端和客户端都通过这个随机值来进行加密解密。
   4. 服务端解密； 服务端用私钥解密后，得到客户端传递过来的随机值(私钥)；然后将信息和私钥通过算法混合在一起(对称加密)。  后面的都是用对称加密，传递的是S作为秘钥对信息进行一次对称机密就好
   5. 传输加密后的信息： 这部分信息是服务端用私钥加密后的信息，可以在客户端被还原
   6. 客户端解密； 客户端用之前生成的私钥解密服务端传递过来的信息，这样就可以获取解密后的内容



### Content-Type 

1. [详解](https://www.cnblogs.com/tugenhua0707/p/8975121.html)

2. Content-Type是指http/https发送信息至服务器时的内容编码类型；contentType用于表明发送数据流的类型，服务器根据编码类型使用特定的解析方式，获取数据流中的数据。

3. 在网络请求中，常用的Content-Type有：

   ```
   text/html, text/plain, text/css, text/javascript, image/jpeg, image/png, image/gif, 
   application/x-www-form-urlencoded, multipart/form-data, application/json, application/xml 等
   ```

4. 常用的属性值如下：application/x-www-form-unlencoded： 在发送前编码所有字符(默认情况下)； multipart/form-data, 不对字符编码。在使用文件上传时候，使用该值。

5. application/x-www-form-urlencoded 是最常用的一种请求编码方式，支持GET/POST等方法，所有数据变成键值对的形式 key1=value1&key2=value2的形式，并且特殊字符需要转义成utf-8编号，如空格会变成 %20;

6. 使用表单上传文件时，必须指定表单的 enctype属性值为 multipart/form-data. 请求体被分割成多部分，每部分使用 --boundary分割；

7. 在使用ajax跨域请求时，如果设置Header的ContentType为 application/json，它会发两次请求，第一次先发Method为OPTIONS的请求到服务器，这个请求会询问服务器支持那些请求方法(比如GET,POST)等。如果这个请求支持跨域的话，就会发送第二个请求，否则的话在控制台会报错，第二个请求不会请求。如果成功，提交的数据会显示 Request Payload;

8. ```
   Content-Type的值仅限于下列三者之一：
   - `text/plain`
   - `multipart/form-data`
   - `application/x-www-form-urlencoded`
   ```





### HTTP协议 和websocket协议

> `webpack`的热更新实现原理？

1. 在最新版本的`webpack-dev-server`中，热更新机制已经从`EventSource`切换到了`WebSocket`。
2. `WebSocket`是基于TCP的全双工通讯的协议，`EventSource` 基于HTTP协议
3. 传统的和服务器的信息保持一致的手段一般是**轮询**，就是每隔多长时间就给服务器发送一个请求，来和服务器的数据保持同步，效率差
   1. 传统的通过`ajax`轮训获取服务器信息的技术方案已经过时，我们迫切需要一个高效的节省资源的方式去获取服务器信息，一旦服务器资源有更新，能够及时地通知到客户端，从而实时地反馈到用户界面上。`EventSource`就是这样的技术，**它本质上还是HTTP，通过response流实时推送服务器信息到客户端**。
4. HTTP协议
   1. HTTP是不支持持久连接的，HTTP的生命周期通过Request来界定，也就是一个Request 一个Response
   2. 在HTTP1.0中，每个http请求响应后都会关闭tcp连接。
   3. 在HTTP1.1中进行了改进，可以在请求头和响应头中增加字段connection: keep-alive ，多个http 请求共用同一个 tcp 连接，这样可以减少相邻多次 http请求导致的 tcp连接建立和关闭的资源消耗
   4. 不管怎么，都是客户端主动发送，服务器被动接收请求，对于一些高并发和用户实时响应的web应用，(如金融证券的实时信息、Web导航应用中的地理位置获取、社交网络的实时消息推送等)； 一般采用的是长轮询机制
5. 轮询
   1. 轮询的原理非常简单，让浏览器隔个几秒就发送一次请求，询问服务器是否有新信息
      1. 缺点是消息交互的实时性较低，当客户端按固定频率向服务器发起请求，数据可能并没有更新，浪费服务器资源
   2. long polling指的是客户端发起连接后，如果有数据，立刻响应请求；如果没有数据 客户端像传统轮询一样从服务端请求数据，服务端会阻塞请求不会立刻返回，直到有数据或超时才返回给客户端，然后关闭连接，客户端处理完响应信息后再向服务器发送新的请求
      1. server 没有数据到达时，http连接会停留一段时间，这会造成服务器资源浪费。(因为连接的时间长，增大了并发压力)
      2. 都是在不断地建立HTTP连接，然后等待服务端处理
      3. HTTP协议的一个特点，被动性。不管是长轮询还是短轮询，都不太适用于客户端数量太多的情况，因为每个服务器所能承载的TCP连接数是有上限的，这种轮询很容易把连接数顶满。
6. websock协议
   1. 只需要经过一次HTTP请求，就可以做到源源不断的信息传送了；WebSocket只需要一次TCP握手，所以说整个通讯过程是建立在一次连接/状态中














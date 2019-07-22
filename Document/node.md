# npm是包管理工具

## cmd 创建自定义包

1. 先新创建一个`node_modules`文件 将所有的包都放在里面

2. 在`node_modules`里打开`cmd`文件输入`npm init` 直接回车回车 最后 `yes` 直接创建了一个文件里面包含`package.json`文件(没有package.json就不是包)



==require的运行原理==

## 自定义包包含文件

1. package.json必须有 
2. 创建一个存放`js`的文件夹
   - 必须包含`index.js`文件 在index.js将所有的文件暴露出去 就不用单个单个的暴露了

## 包的使用

```js
// 向外暴露成员，使用 module.exports
module.exports = b;
// 自定义模块 引入使用的是文件路径
const selfModule = require('./my.js')
```



# npm工具包

## 一. 安装卸载

> (默认安装最新版本 工具名+@+版本号指定安装版本)

### 1) 全局 (-g :全局 工具包)

#### 安装:

npm install 工具名 -g

#### 卸载:

npm uninstall 工具名 -g

### 2) 本地(当前目录文件夹)

#### 安装:

npm install 工具名 

#### 卸载:

npm uninstall 工具名

### 3) 安装package.json 中所有需要的包

npm init

### 4) 清除缓存

npm cache clear --force

## 二. 工具使用

### i5ting_toc (将md文档转为HTML文件)

`i5ting_toc -f md文件名`

### nodemon (保存项目即可重启web服务器)

`npm install nodemon -g`

### Express基于 [Node.js](https://nodejs.org/en/) 平台，快速、开放、极简的 Web 开发框架

1. 进一步封装HTTP模块 , 扩展了方法 , 原生的方法一直存在
2. 没有覆盖原生HTTP模块中的方法 , 而是基于原生方法之上
3. ==创建网站项目==

==`--save`安装到当前依赖==

`npm install express --save`  (==局部==)

###  sql(数据库模块)

`npm install mysql --save`

### body-parser(解析中间件模块)

`npm install body-parser --save`

### axios api(通过相关配置发送请求)

`npm install axios --save`

#### app.get() 监听客户端的请求

- 参数:

  - url地址
  - 处理函数
    - 参数:
      1. req : 浏览器(请求对象) 包含触发事件的HTTP请求信息对象
      2. res : 服务器(响应对象)

- 方法
  - res.send()
    1. 传输的是字符串,文字,对象或数组 会转为json格式
    2. 传输二进制 会当文件进行下载
  - res.sendFile() 发送文件
    - 参数:
      1. 相对路径
      2. 绝对路径
    - 返回值:
      1. 静态页面
  - app.use() 
    - 注册**中间件** 
        - 参数:
            1. 回调函数
      - 静态资源目录
        - 参数:
              1. 虚拟目录
  - express.static('目录') 快速托管为静态资源夹(使文件更安全)
  - app.set() 设置模板引擎
  
  ```js
  // 1. 使用 app.set('view engine', '模板引擎的名称')
  app.set('view engine', 'ejs')
  // 2. 设置模板页面的默认存放路径 app.set('views', '模板页面的具体存放路径')
  app.set('views', './ejs_pages')
  ```
  
  - res.render() 渲染页面
    - 参数:
        1. 目标文件
        2. 模板引擎需要的数据
  
  ```js
  // 可以在托管静态资源文件的时候，指定要挂载的虚拟路径；
  app.use('/page', express.static('./views'))
  ```
  
  - express.Router() 创建路由对象

### bootstrap

1. 默认bootstrap是 4.3.1的版本，比较新；

   ```
   先卸载旧版本  npm uninstall boostrap --save
   安装指定版本  npm install bootstrap@3 --save
   ```

2. bugs

   ```
   Refused to apply style from 'http://127.0.0.1:3000/public/semantic.min.css' because its MIME type ('text/html') is not a supported stylesheet MIME type, and strict MIME checking is enabled.
   //表示我们的文件引入路径出错了，注意服务器的静态资源目录，那个目录相当于服务器已经看见了，我们就不用再加上这层文件夹了
   ```

   

### 自定义模板引擎

`npm install art-template express-art-template`

```js
// 1. 使用 app.engine() 方法自定义模板引擎
app.engine('html', require('express-art-template'))
// 2. 使用 app.set('view engine', '指定模板引擎名称') 来配置项目中用到的模板引擎
app.set('view engine', 'html')
// 3. 配置模板页面的存放路径
app.set('views', './art_page')

app.get('/', (req, res) => {
  res.render('index.html', { name: 'zs', age: 22, hobby: ['玩游戏', '唱歌'] })
})

app.listen(3000, () => {
  console.log('server running at http://127.0.0.1:3000')
})
```

### 路由模块(一种对应关系,没有对应的关系会出现404)

路由:路径地址对应的页面

```js
// 这是定义了一个路由模块，专门负责创建路由对象，并挂载路由规则
const express = require('express')

// 调用 express.Router() 方法，创建路由对象
const router = express.Router()

router.get('/', (req, res) => {
  res.sendFile('./views/home.html', { root: __dirname })
})

router.get('/movie', (req, res) => {
  res.sendFile('./views/movie.html', { root: __dirname })
})

router.get('/about', (req, res) => {
  res.sendFile('./views/about.html', { root: __dirname })
})

// 最后，一定要把路由对象导出，供外界使用
module.exports = router
```

> 多个小文件,精简页面 使项目看起来更方便(一个文件一个功能)

### ==use()中间件==

> 本质上是有个处理函数 , 有一个中间处理的过程叫中间件
>
> 对用户的请求进行处理

#### 处理程序之前，在中间件中对传入的请求体进行解析

`body-parser` 提供四种解析器
[JSON body parser](https://github.com/expressjs/body-parser#bodyparserjsonoptions)

#### JSON解析器

```json
app.post('/login.do', jsonParser, (req, res) => {
    res.end();
})
```

Postman 以raw 方式发送JSON 数据，执行结果：

> ```js
> { name: 'wang', password: '123456' }
> ```

[Raw body parser](https://github.com/expressjs/body-parser#bodyparserrawoptions)

#### urlencoded解析器

```js
app.post('/login.do', urlencodedParser, (req, res) => {
    console.log('********************')
    console.log(req.body)

    res.end();
})
```

[Text body parser](https://github.com/expressjs/body-parser#bodyparsertextoptions)

[URL-encoded form body parser](https://github.com/expressjs/body-parser#bodyparserurlencodedoptions)

#### 加载到没有挂载路径的中间件

```js
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())
```

`app.use(bodyParser.json())`

#### 公用参数:

1. req:请求对象(浏览器)
2. res:响应对象(服务器)
3. ==next==:调用下一个中间件的方法(必须有,没有不会向下执行)

#### 1)应用级中间件

绑定到app对象上 app.get()

#### 2)路由级中间件

绑定到路由( router)对象上 router .get()

#### 3)错误处理中间件

- 参数:
  1. err
  2. req
  3. res
  4. next

#### 4)内置中间件

express.static()

#### 5)第三方中间件

需要先安装才能在使用

## express获取数据

### 1) 获取url地址中查询参数

`req.query`获取用户提交到服务器查询的数据

### 2) 获取url地址中的路径

> url规则中的`:`是请求项

`req.params`获取动态路由参数

### 3) 从post获取表单数据

- 借助于`body-parser`(中间件)来解析表单数据
- **安装：**`npm i body-parser -S`
- **导入：**`const bodyParser = require('body-parser')`
- **注册中间件：**`app.use(bodyParser.urlencoded({ extended: false }))`
- **使用解析的数据：** `req.body` 来访问解析出来的数据

gulp:前端工程库(通过工具打开项目)

chunk:数据块

jsonp:只支持get请求

cors:支持post(后台)

一页代码不能超过100行





------


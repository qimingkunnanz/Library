# 获取a标签href属性中的值

```js
var a= document.getElementsByTagName("a")[0].href
var a= $('a')[0].href;
```

## var a= $('a')



## 找到init(1)对象的0元素 其中herf元素保存的是所需要的值



## 所以可以得到值



## 最后拆分字符串可以得到id

> substr(0,a.length-1):去掉最后一个字符

> split('='):截取第一个符合条件的字符

```js
var c=a.substr(0,a.length-1).split('=')
```

## 返回数组



## 找到下标为1的字符 就得到最终想要的结果

```js
console.log(c[1]);
```


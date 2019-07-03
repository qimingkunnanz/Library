> template.js 一款 JavaScript 模板引擎，简单，好用。提供一套模板语法

# 语法

## 引入文件

```js
<script src="template.js"></script> 
```

## 表达式

```js
{{template模板语句}}
```

## 条件表达式

```js
{{if admin}} 
 <p>admin</p> 
{{else if code > 0}} 
 <p>master</p> 
{{else}} 
 <p>error!</p> 
{{/if}}
```

## 遍历表达式

```js
{{each list as value index}} 
 <li>{{index}} - {{value.user}}</li> 
{{/each}}
```

## 简写

```js
{{each list}} 
 <li>{{$index}} - {{$value.user}}</li> 
{{/each}} 
```

## 模板包含表达式

> 用于嵌入子模板(子模板默认共享当前数据)

```js
{{include 'template_name'}}
```

## 辅助方法

> 使用template.helper(name, callback)注册公用辅助方法

```js
template.helper('dateFormat', function (date, format) { 
 // .. 
 return value; 
});
```

## 模板中使用的方式

```js
{{time | dateFormat:'yyyy-MM-dd hh:mm:ss'}}
```

## 支持传入参数与嵌套使用

```js
 {{time | say:'cd' | ubb | link}}
```


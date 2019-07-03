#### DOM 文档对象模型

1. **获取查询dom元素(五种方法)**
   1. getElementById, getElementsByTagName,getElementsClassName,
   2. 常用： querySelector, querySelectorAll
2. **修改元素相关**
   1. 可读写元素属性： src,href,title
   2. 可读写普通元素内容： innerHTML、innerText
   3. 可读写表单元素： value, type, disabled
   4. 可读写元素样式： style, className
3. **属性操作**
   1. setAttribute，getAttribute， removeAttribute
4. **创建元素**
   1. document.write()
   2. innerHTML
   3. createElement
5. **添加元素**
   1. appenChild
   2. insertBefore
6. **删除元素**
   1. removeChild
7. **事件操作**
   1. 鼠标相关onclick, onmouseover,onmouseout,onfocus,onblur, onmousemove, onmouseup,onmousedown



#### jQuery选择器

```
// jquery重要思想  隐式迭代，链式编程


$('ul li.current')
$('ul>li')

$('ul').eq(2)
$('ul').parent();
$('ul').children('li'); // 相当于 ul>li  最近一级，亲儿子 
$('ul').find('li');  // 相当于ul li 所有的后代元素
$('ul li').siblings('li');  // 查找除了自身以外的兄弟节点
```



#### jQuery属性操作

1. prop,attr

   ```javascript
   // 都是可读写属性
   // prop使用场景
   $("a").prop("href")
   $(this).prop("checked")
   
   // attr属性 一般用来获取或添加自定义属性
   $("div").attr("index")
   $("div").attr("data-index", 5)
   ```

#### jQuery文本属性值

1. 三种方法 html,text,val  都是可读写的， 类比着原生的三种方式来学习，时刻记住jquery是一个库，封装了我们的原生js

   ```javascript
   $("div").html()
   $("div").html('可识别<br>html的标签')
   
   $("div").text()
   $("div").text('不能识别<br>html的标签')
   
   // 表单元素要用单独的 方法
   $("input").val()
   $("input").val('123')
   
   // 元素的方法复习
   var divDom = document.querySelector('div');
   divDom.innerHTML = 'XXX';
   divDom.innerText = 'xxx';
   divDom.value = "xxx";
   ```

   

#### jQuery元素操作

1. 返回祖先元素

   ```javascript
   // parent 没有加s  表示返回第一个父亲，亲爸爸
   $(".current").parent().parent().parent();
   
   // 返回所有的父亲， 祖先都会遍历出来
   $(".four").parents()
   // 返回类名 含有one的祖先
   $(".four").parents(".one")
   
   // 原生的节点操作  父子
   div.parentNode
   div.children
   ```

2. 创建、添加、删除 元素

   ```javascript
   //1. jquery方式 先创建 再添加
   var li = $("<li></li>");
   // 这样添加的是父子关系
   $("ul").append(li);
   $("ul").prepend(li);
   // 2.这样添加的是 兄弟关系
   var div = $("<div>我是后妈生的</div>");
   // $(".test").after(div);
   $(".test").before(div);
   ```
   ```javascript
   // 3. 删除元素
   $("ul").remove(); // 删除匹配的元素，包括自己
   $("ul").empty(); // 删除匹配元素里面的 子元素
   $("ul").html(""); // 也是删除里面的子元素
   ```
   ```javascript
   //原生js的方式
   var ul = document.querySelector('ul');
   var li = document.createElement('li');
   ul.appendChild(li);
   ul.insertBefore(li, ul.children[0])
   ```










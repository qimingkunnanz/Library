# ES6

## 一 . 变量&常量

### 1) **let** 声明变量(块级作用域 未来替代var)

1. 允许声明一个**块级作用域**(被限制**块级**中的**变量** , 语句 , 表达式)
2. 只能是**全局作用域**或**函数作用域**

3. 不会再**局部作用域**中创建**全局变量**
4. 暂存死区(定义被执行时才会执行 , 再声明之前使用会报错)

### 扩展:

-  在 `let `语句块内使用 var 声明的变量，它的作用域与在 let 语句块之外声明没有区别；这样的变量仍然具有函数作用域。在使用 `let` 语句块时，必须使用花括号，否则会导致语法错误

```js
var x = 5;
var y = 0;

let (x = x + 10, y = 12) {
  console.log(x + y); // 27
}

console.log(x + y); // 5
```

- **let表达式** 可以将变量的作用域仅作用于一条语句

```js
var a = 5;
let(a = 6) console.log(a); // 6
console.log(a); // 5
```

### 2) const 声明常量(块级作用域与let很像)

1. 声明必须赋值
2. 赋值后不能改变 (复杂数据类型的值可以改变)
3. 不能重新声明
4. 声明创建的是一个只读引用 , 只有变量标识符不能重新被赋值

## 二  . 数据类型

### 1.基本数据类型(7种)

undefined,null,boolean,number,string,object

symbol:es6新增语法 表示独一无二的值类似于id的作用,一般用来定义对象的唯一属性名(你需要对外操作和访问的属性)



## 三. 解构赋值

1. 对数组或对象进行模拟匹配，然后对其变量进行赋值操作
2. 方便复杂对象中数据字段的获取
3. 左边是目标，右边是解构源

### 1）数组解构

之前变量赋值

```js
let a = 1;
let b = 2;
```

ES6允许变量赋值

```js
// a = 1 b = 2 可忽略的解构
let [a, b, c] = [1, 2, 3];
```

[^]: 本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值

```js
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]
// 如果解构不成功，变量的值就等于undefined
let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```

另一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功

```js
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```

### 2）对象函数

1. 对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值
2. 等号左右的格式必须一样

```js
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"
```

[^解构失败，变量的值等于undefined]: 

```js
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"
foo // error: foo is not defined
```

[^真正被赋值的是变量而不是foo模式]: 属性名: 属性值  必须有同名的属性名才能拿到相应的值

#### 默认值

对象的解构也可以指定默认值 --->属性值必须等于**undefined**

### 3) 字符串的解构赋值

> 字符串被转换成了一个类似数组的对象 属性名于字符串下标一一对应

```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

### 4) 数值和布尔值的解构赋值 

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于`undefined`和`null`无法转为对象，所以对它们进行解构赋值，都会报错

```js
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true

let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```

### 5) 函数参数的解构赋值 

将参数解构赋值 undefined会触发函数参数默认值

```js
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

### 6) 圆括号问题 ()

解构赋值虽然很方便，但是解析起来并不容易。对于编译器来说，一个式子到底是模式，还是表达式，没有办法从一开始就知道，必须解析到（或解析不到）等号才能知道。

由此带来的问题是，如果模式中出现圆括号怎么处理。ES6 的规则是，只要有可能导致解构的歧义，就不得使用圆括号。

但是，这条规则实际上不那么容易辨别，处理起来相当麻烦。因此，建议只要有可能，就不要在模式中放置圆括号。

### 7) 不能使用圆括号的情况

1. 变量声明语句
2. 函数参数
3. 赋值语句的模式

### 8) 可以使用圆括号的情况

1. 赋值语句的非模式部分，可以使用圆括号

```js
[(b)] = [3]; // 正确
({ p: (d) } = {}); // 正确
[(parseInt.prop)] = [3]; // 正确
```

### 9) ==用途==

1. 交换两个变量的值

   ```js
   let x = 1;
   let y = 2;
   
   [x, y] = [y, x];
   ```

2. 从函数返回多个值

   ```js
   // 返回一个数组
   
   function example() {
     return [1, 2, 3];
   }
   let [a, b, c] = example();
   
   // 返回一个对象
   
   function example() {
     return {
       foo: 1,
       bar: 2
     };
   }
   let { foo, bar } = example();
   ```

3. 函数参数的定义

   解构赋值可以方便地将一组参数与变量名对应起来。

   ```javascript
   // 参数是一组有次序的值
   function f([x, y, z]) { ... }
   f([1, 2, 3]);
   
   // 参数是一组无次序的值
   function f({x, y, z}) { ... }
   f({z: 3, y: 2, x: 1});
   ```

4. 提取 JSON 数据

   解构赋值对提取 JSON 对象中的数据，尤其有用。

    ```javascript
   let jsonData = {
       id: 42,
       status: "OK",
       data: [867, 5309]
   };

   let { id, status, data: number } = jsonData;

   console.log(id, status, number);
   // 42, "OK", [867, 5309]
    ```

​	上面代码可以快速提取 JSON 数据的值。

5. 函数参数的默认值

    ```javascript
    jQuery.ajax = function (url, {
      async = true,
      beforeSend = function () {},
      cache = true,
      complete = function () {},
      crossDomain = false,
      global = true,
      // ... more config
    } = {}) {
      // ... do stuff
    };
    
    ```
    
    指定参数的默认值，就避免了在函数体内部再写`var foo = config.foo || 'default foo';`这样的语句。
    
6. 遍历 Map 结构

   任何部署了 Iterator 接口的对象，都可以用`for...of`循环遍历。Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便。

    ```javascript
    const map = new Map();
    map.set('first', 'hello');
    map.set('second', 'world');
    for (let [key, value] of map) {
      console.log(key + " is " + value);
    }
    // first is hello
    // second is world
    ```

   如果只想获取键名，或者只想获取键值，可以写成下面这样。
   
   ```js
   javascript
   // 获取键名
   for (let [key] of map) {
   // ...
   }
   // 获取键值
   for (let [,value] of map) {
   // ...
   }
   ```

7. 输入模块的指定方法

   加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。

    ```javascript
    const { SourceMapConsumer, SourceNode } = require("source-map");
    ```

## 四. 字符串

### 1) 字符串的遍历接口

ES6为字符串添加了遍历接口,是的字符串可以被 `for of` 循环遍历

```javascript
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```

这个遍历器最大的优点是可以识别大于`0xFFFF`的码点

```js
let text = String.fromCodePoint(0x20BB7);

for (let i = 0; i < text.length; i++) {
  console.log(text[i]);
}
// " "
// " "

for (let i of text) {
  console.log(i);
}
// "𠮷"
```

### 2) JSON.stringify() 的改造

根据标准，JSON 数据必须是 UTF-8 编码。但是，现在的`JSON.stringify()`方法有可能返回不符合 UTF-8 标准的字符串。

具体来说，UTF-8 标准规定，`0xD800`到`0xDFFF`之间的码点，不能单独使用，必须配对使用。比如，`\uD834\uDF06`是两个码点，但是必须放在一起配对使用，代表字符`𝌆`。这是为了表示码点大于`0xFFFF`的字符的一种变通方法。单独使用`\uD834`和`\uDFO6`这两个码点是不合法的，或者颠倒顺序也不行，因为`\uDF06\uD834`并没有对应的字符。

`JSON.stringify()`的问题在于，它可能返回`0xD800`到`0xDFFF`之间的单个码点。

```javascript
JSON.stringify('\u{D834}') // "\u{D834}"
```

为了确保返回的是合法的 UTF-8 字符，[ES2019](https://github.com/tc39/proposal-well-formed-stringify) 改变了`JSON.stringify()`的行为。如果遇到`0xD800`到`0xDFFF`之间的单个码点，或者不存在的配对形式，它会返回转义字符串，留给应用自己决定下一步的处理。

```javascript
JSON.stringify('\u{D834}') // ""\\uD834""
JSON.stringify('\uDF06\uD834') // ""\\udf06\\ud834""
```

### 3) 模板字符串

> 为解决传统拼接字符串繁琐

```js
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```

模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量

```js
let name = 'add'
let str = `hello 
${name}
 world`
console.log(str);
```

如果在模板字符串中需要使用反引号，则前面要用反斜杠转义

```js
let greeting = `\`Yo\` World!`
// `Yo` World!
```

使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中, 比如`<ul>`标签前面会有一个换行。如果你不想要这个换行，可以使用`trim`方法消除它

```js
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`.trim());
```

大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性

```js
let x = 1;
let y = 2;

`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

`${x} + ${y * 2} = ${x + y * 2}`
// "1 + 4 = 5"

let obj = {x: 1, y: 2};
`${obj.x + obj.y}`
// "3"
```

模板字符串之中还能调用函数。

```javascript
function fn() {
  return "Hello World";
}

`foo ${fn()} bar`
// foo Hello World bar
```

### 4) 标签模板

> 模板字符串的功能，不仅仅是上面这些。它可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串。这被称为“标签模板”功能（tagged template）

```javascript
alert`123`
// 等同于
alert(123)
```

标签模板其实不是模板，而是函数调用的一种特殊形式。“标签”指的就是函数，紧跟在后面的模板字符串就是它的参数。

但是，如果模板字符里面有变量，就不是简单的调用了，而是会将模板字符串先处理成多个参数，再调用函数

```javascript
let a = 5;
let b = 10;

tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```

模板字符串前面有一个标识名`tag`，它是一个函数。整个表达式的返回值，就是`tag`函数处理模板字符串后的返回值。函数`tag`依次会接收到多个参数

## 五. 箭头函数

箭头函数是匿名函数 this的指向外层this

```js
() =>{

}
```

1. 只有一个参数时()可以简写

```js
x =>{
	console.log(x);
}
```

2. 只有一条执行语句时{}可以简写

```js
(x) => console.log(x);
```

3. 只有一个参数和一条执行语句时(){}都可以简写

```js
x => console.log(x);
```

## 六. 三个点号

1. 放在形参或者等号左边为 rest运算符； 表示把逗号隔开的值序列 组合成一个数组

   ```javascript
   //使用场景   1. 用于不定参数的问题， 可以不再使用arguments对象，使用...arg
   const sum = (...args) => {  // (x,y,z)  [x,y,z]
   	let total = 0;
   	args.forEach(item => total += item);
   	return total;
   };
   
   console.log(sum(10, 20));
   console.log(sum(10, 20, 30));
   
   // 2. 剩余运算符 的解构赋值
   let [a, ...b] = [1, 2, 3]; // a=1, b=[2,3]   这个叫不完全解构
   let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};
   ```

2. 放在实参或者等号右边的为 扩展运算符(spread)；  可以将数组拆分成以逗号分隔的参数序列

   ```js
   // 1. 当做函数的实参
   var foo = function (a, b, c) {
     console.log(a);
     console.log(b);
     console.log(c);
   }
   var arr = [1, 2, 3];
   //传统写法
   // foo(arr[0], arr[1], arr[2]);
   //使用扩展运算符
   foo(...arr); // foo(...arr)  1,2,3
   
   
   // 2. 合并数组， 数组的拷贝,
   let ary1 = [1, 2, 3]; // let newArr = [...arr1]
   let ary2 = [4, 5, 6];
   let ary3 = [...ary1, ...ary2];
   // 或者这样写 arr1.push(...arr2)
   
   // 3. 字符串转数组
   var str = 'hello';
   var arr5 = [...str];  // str.split('')
   
   // 4. 将伪数组转换为真正的数组
   var oDivs = document.getElementsByTagName('div');
   console.log(oDivs)
   var ary = [...oDivs];
   ary.push('a');
   console.log(ary);
   ```

   





## 模块

> 是一种约定，规范

模块作用域

1. 每一个js文件都是独立的模块
2. 默认在 Node 中，每一个 JS 文件中定义的 方法、变量，都是属于 模块作用域的

### 1）引入模块

```js
// 引入核心模块
const fs = require('fs')
// 引入第三方模块
const a = require('名称标识符')
// 引入自定义模块
const a = require('路径标识符')
```

### 2）自己写入模块 将外暴露私有成员

```js
module.exports = {
	a,
    b
}; // 当属性名和变量名相同时可以简写
```

### 3) export命令

模块功能主要由两个命令构成：`export`和`import`。`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能

#### 对外暴露变量

> 使用 export default 和 export 向外暴露成员
>
> 在一个模块中，export default 只允许向外暴露1次
>
> 在一个模块中，可以同时使用 export default 和 export 向外暴露成员

```js
// 脚本尾部
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export { firstName, lastName, year };
```

`export`命令除了输出变量，还可以输出函数或类（class）。

```javascript
export function multiply(x, y) {
  return x * y;
};
```

通常情况下，`export`输出的变量就是本来的名字，但是可以使用`as`关键字重命名。

```javascript
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

上面代码使用`as`关键字，重命名了函数`v1`和`v2`的对外接口。重命名后，`v2`可以用不同的名字输出两次。
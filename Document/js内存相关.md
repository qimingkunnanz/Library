### 1.基本数据类型

> 基本数据类型的值是不可变的
>
> 基本数据类型的比较，仅仅是值的比较； 复杂数据类型是值和地址的比较
>
> 基本数据类型存储在 栈； 栈空间包括了变量的标识符和变量的值

```javascript
var name = "change";
name = "change1";
console.log(name)//change1
// 注意： 这里的name值看起来被改变了，但是其实是 "change"字符串这个基本类型不可以改变，name只是一个指针，指针的指向可以改变，所以name="change1"， 这里的解释是name指向了"change1".  注意一点name是一个变量，可以改变， "change"字符串不可改变
```



### 2. 引用数据类型

> 引用数据类型的值是可以修改的
>
> 引用类型的赋值其实是对象保存在栈内存 地址指针的一个赋值，赋值操作后两个变量都保存了同一个对象的地址，
>
> 引用类型的比较 是引用(地址)的比较
>
> 引用类型是同事保存在栈(放地址的引用)和堆(放具体的值)里面的



```javascript
var a = {};
var b= a;
a.name = "change";
console.log(a.name)//change;
console.log(b.name)//change
b.age = 29;
console.log(a.age)//29
console.log(b.age)//29

var obj1 = {};
var obj2 = {};
console.log(obj1 == obj2); //false
// 对象的比较  就是地址的比较，obj1,obj2 它们在的值{}在堆里面有连个值
```



### 3. 基本包装类型

> ECMAScript还提供了三个特殊的引用类型Boolean,String,Number.我们称这三个特殊的引用类型为基本包装类型，也叫包装对象

```javascript
var s1 = "helloworld";
var s2 = s1.substr(4);

// js内部的实际处理过程
创建String类型的一个实例；// var s1 = new String("helloworld");
在实例上调用指定方法；// var s2 = s1.substr(4);
销毁这个实例；// s1 = null;

基本装包类型和引用类型主要区别：对象的生存期.使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都是一直保存在内存中.而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁
```





### 4.栈(stack)  和  堆(heap)

> 基本数据类型 Number， String， Boolean, Undefined, Null 都保存在栈内存中
>
> 复杂数据类型 Object   它们的值不固定，保存在堆内存中； 但是他们的内存地址存储在 堆内存中； 我们平时在操作对象时，都是操作的对象的引用而不是实际的对象

```javascript
//举个栗子
var num = 1;
var num2 = num;
// 栈内存中 数据的复制  系统为 开辟一个新的内存空间，让后赋值给它
num2 = 5;
console.log(num, num2);

var obj1 = {name: 'abc', age: 24};
// 变量obj1 存在占中， {name:'abc', age:24}作为对象存在于堆内存中
// 变量obj1 实际的值 0x0012ff7d
var obj2 = obj1;
obj2.name="def";
obj2.age = 99
console.log(obj1, obj2)

// 总结： 简单数据类型 ，拷贝的是值，新建了一个地址，
//       复杂数据类型， 拷贝的是地址， 同一个地址， 堆空间里面的值只有一份
//       JS里面给变量重新赋值，将会新开辟一块存储空间，而没有销毁原来的空间

//JavaScript 的变量可以存储直接量也可以存储指针
```



### 5.值传递 和 引用传递

```javascript
var a = 10;
var x = a;
// 这是使用 = 号，  将对应的a的值拷贝了一份 并赋值非新的变量x， 这个过程我们成为值传递

var obj = {age: 24}
var obj2 = obj1;
//这里是 将obj1对象 地址赋值给 obj2；  他们的值都是存在堆内存里面的一个引用

var arr1 = [1,2,3];
var arr2 = [1,2,3];
console.log(arr1 == arr2); //false
console.log(arr1 === arr2); //false
// 只要地址不想等， 各种条件都不等

// 所有函数的参数都是按值传递的，因为 如果存在引用传递的话，那么函数内的变量将是全局变量，在外部也可以访问。但这明显是不可能的。
```


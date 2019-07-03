1. 普通函数 this 指向window
    ```js
    function str() {

    	consols.log('普通函数' + this);

    }

    str(); // 返回window
    ```
2. 对象的方法 this指向的是对象 o
    ```js
    var arr = {

    Hi: function() {

      consols.log('对象的方法' + this);

      }

    }

    arr.Hi(); // 返回实例对象
    ```
3. 构造函数 this 指向 ldh 这个实例对象 原型对象里面的this 指向的也是 ldh这个实例对象
    ```js
    function Str() {

    	consols.log('构造函数' + this);

    }

    new Str(); // 返回实例对象 
    ```
4. 绑定事件函数 this 指向的是函数的调用者 btn这个按钮对象
    ```js
    var button = document.querySelector('button');

    button.onclick = function() {

    	consols.log('绑定事件函数' + this);

    }; // 返回实例对象 
    ```
5. 定时器函数 this 指向的也是window
    ```js
    setTimeout(function() {

    	consols.log('定时器函数' + this);

    }, 1000); // 返回window
    ```
6. 立即执行函数 this还是指向window
    ```js
    (function() {

    	consols.log('立即执行函数' + this);

    })() // 返回window
    ```
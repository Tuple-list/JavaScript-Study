# 使用自调用匿名函数创建块级作用域  
  > 摘要：使用自调用匿名函数创建块级作用域，并通过括号、加减号等转换函数声明为表达式。  

> ## 代码与说明  
  JavaScript中没有块级作用域（私有作用域）的概念，但可以使用自调用的匿名函数来模拟块级作用域。  
  用作块级作用域的常见代码如下：  
  ```
  (function(){
      //内部代码，外部无法访问这里定义的变量
  })();
  ```
  
  带参数时：  
```
(function($){
    //封装jQuery插件的代码
})(jQuery);
```

  为什么可以写成这种形式呢？  看一个普通的函数调用：  
  ```
  //定义一个函数
  var greet = function(name){
      alert("Hello " + name);
  }

  //调用函数
  greet("Sky");
  ```
  
  在调用函数时，使用的是变量greet，显然我们可以用该变量的值（即函数体）来替代变量，这是等价的：  
  ```
  function(name){
      alert("Hello " + name);
  }("Sky");
  ```
  然而这段代码会报错：  
  > SyntaxError: function statement requires a name  
  这是因为JavaScript把function关键字当作一个函数声明的开始，而函数声明之后不能直接跟括号。  
  但JavaScript允许一个表达式之后跟括号，故我们需要将上面的函数声明语句转变为一个表达式。最常见的做法即是给函数声明加上圆括号：  
  ```
  (function(name){
      alert("Hello " + name);
  })("Sky");
  ```  
> ## 其它写法  
  其实，任何能够将函数声明转为表达式的方式都是可以的，而不限于圆括号，比如：  
  加号（+）  
  ```
  +function(){
      //内部代码，外部无法访问这里定义的变量
  }();
  ```
  
  减号（-）  
  ```
  -function(){
      //内部代码，外部无法访问
  }();
  ```
  
  感叹号（!）
  ```
  !function(){
      //内部代码，外部无法访问
  }();
  ```   
  
  外层圆括号  
  ```
  (function(){
      //内部代码，外部无法访问
  }());
  ```
  
  其中加号（+）和减号（-）的性能较好，且无须像括号那样关注前后匹配，bootstrap.js插件使用的就是加号；  
  括号的优点是更易于理解。  
  
  
---
                                              【END】
---

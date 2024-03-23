---
title: 箭头函数
date: 2023-01-09 20:40:00 +0800
categories: [小知识]
tags: [JavaScript]
pin: false
toc: true
typora-root-url: ../../farmud.github.io
---

# 箭头函数

**箭头函数表达式**的语法比[函数表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/function)更简洁，并且没有自己的[`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)，[`arguments`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)，[`super`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/super)或[`new.target`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new.target)。箭头函数表达式更适用于那些本来需要**匿名函数**的地方，并且它不能用作构造函数。

箭头函数本质上同lambda表达式是一件事，区别在于箭头函数在JavaScript中为`=>` ，而在Java中的lambda表达式为`->`。同时，还有与JavaScript弱类型的特点，JavaScript中的箭头函数比Java中的更为简洁（少了参数类型说明）。



## 语法

> ### 基础语法
>
> ```javascript
> //无返回值:
> (a1,a2,...,an)=>{statements;}
> //实质是：
> var f = function(a1,a2,...an){
>     statements;
> }
> 
> 
> (a1,a2,...,an)=>expression
> //等价于:
> (a1,a2,...,an)=>{return expression};
> 
> 
> //仅有一个参数时，()是可选的
> a1=>expression
> 
> 
> //无参数时
> ()=>{statements}
> ```

> ### 高级语法
>
> ```javascript
> //加括号的函数体返回对象字面量表达式：
> id => ({id:id,name:"Tom"})
> 
> 
> //支持剩余参数和默认参数
> (param1, param2, ...rest) => { statements }
> (param1 = defaultValue1, param2, …, paramN = defaultValueN) => {
> statements }
> 
> 
> //同样支持参数列表解构
> let f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
> f();  // 6
> 
> ```



**留待解决：什么是参数列表结构？**



## 注意事项

箭头函数没有自己的`this` ，他只会从自己的作用域链的上一层继承`this` 。

```javascript
//不利用箭头函数：
function Person() {
  var that = this;
  that.age = 0;

  setInterval(function growUp() {
    // 回调引用的是`that`变量，其值是预期的对象。
    that.age++;
  }, 1000);
}
```

```javascript
//利用箭头函数的处理方式：
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| 正确地指向 p 实例
  }, 1000);
}

var p = new Person();

```



---

详细参见[箭头函数 - JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arrow_functions#语法) ，本文只是简单总结箭头函数的用法及注意事项。


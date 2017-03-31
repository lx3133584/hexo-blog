---
title: JavaScript中的变量提升
tags: 
- JavaScript
- 原生JS语法
categories: JavaScript
comments: true
---
最近在准备面试，看网上的一些面试题，发现了很多自己基础知识不足的地方，其中有一道题很有意思，看似很简单，其实涉及到了JavaScript中作用域和变量提升的问题。

这道题是这样的：求下面alter弹出的结果
``` javascript
var a = 1;  
function b() {  
    a = 10;  
    return;  
    function a() {}  
}  
b();  
alert(a);  
```
如果是像我一样的初学者肯定以为结果是10吧，然而结果是1。

这就是因为JavaScript的变量提升：

>函数声明和变量声明总是会被解释器悄悄地被“提升”到方法体的最顶部。

例如：
``` javascript
function foo() {  
    bar();  
    var x = 1;  
}  
```
实际上会被解释成：
``` javascript
function foo() {  
    var x;  
    bar();  
    x = 1;  
} 
```
请注意，变量赋值并没有被提升，只是声明被提升了。

但是，函数的声明有点不一样，函数体也会一同被提升。但是请注意，函数的声明有两种方式：
``` javascript
function test() {  
    foo(); // TypeError "foo is not a function"  
    bar(); // "this will run!"  
    var foo = function () { // 变量指向函数表达式  
        alert("this won't run!");  
    }  
    function bar() { // 函数声明 函数名为bar  
        alert("this will run!");  
    }  
}  
test();  
```
这个例子里面，只有函数式的声明才会连同函数体一起被提升。foo的声明会被提升，但是它指向的函数体只会在执行的时候才被赋值。

>还有：函数的声明比变量的声明具有高的优先级。

但是函数有一个方法可以解决声明提升的问题，那就是**命名函数**

你可以给一个函数一个名字。如果这样的话，它就不是一个函数声明，同时，函数体定义里面的指定的函数名(如果有的话,如下面的spam)将不会被提升,而是被忽略。

这里一些代码帮助你理解：
``` javascript
foo(); // TypeError "foo is not a function"  
bar(); // valid  
baz(); // TypeError "baz is not a function"  
spam(); // ReferenceError "spam is not defined"  
  
var foo = function () {}; // foo指向匿名函数  
function bar() {}; // 函数声明  
var baz = function spam() {}; // 命名函数，只有baz被提升，spam不会被提升。  
  
foo(); // valid  
bar(); // valid  
baz(); // valid  
spam(); // ReferenceError "spam is not defined"  
```
现在再来看上面的面试题就明白怎么回事了吧，如果还没明白，这里贴上一份代码帮助理解这道题：
``` javascript
//代码1：结果是function number 10 1  
var a = 1;      
function b() {      
    alert(typeof a);    
    a = 10;      
    alert(typeof a);    
    alert(a);    
    return;      
    function a() {}     
}      
b();      
alert(a);     
  
//代码2：结果是number number 10 10  
var a = 1;      
function b() {      
    alert(typeof a);    
    a = 10;      
    alert(typeof a);    
    alert(a);    
    return;      
}      
b();      
alert(a);  
```
        

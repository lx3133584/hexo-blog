---
title: JS中批量修改CSS--cssText
tags:
  - JavaScript
  - CSS
comments: true
date: 2017-04-06 13:07:46
updated:
categories: JavaScript
---

平常编写代码，更改一个元素样式的时候，自己都是用:

``` javascript
obj.style.width = "200px";
obj.style.position = "absolute";
obj.style.left = "100px";
```
之类的代码进行设置，这样的话如果更改样式很多的时候，就要写很多代码，难道不能像Jquery那样使用`$(obj).css(……);`这样进行设置么？

于是自己搜了下使用Javascript批量修改样式的方法。于是看到[这篇文章](http://www.css88.com/archives/1849)，原来是有一个 `cssText` 属性的，看来自己的基础知识掌握的还并不充分呐。

在w3school中查询了下用法:

>它是一组样式属性及其值的文本表示。这个文本格式化为一个 CSS 样式表，去掉了包围属性和值的元素选择器的花括号。

将这一属性设置为非法的值将会抛出一个代码为 SYNTAX_ERR 的 DOMException 异常。当 CSS2Properties 对象是只读的时候，试图设置这一属性将会抛出一个代码为 NO_MODIFICATION_ALLOWED_ERR 的DOMException 异常。

**cssText的使用方法**

``` javascript
obj.cssText = "width:200px;position:absolute;left:100px;";
```

正如那篇文章所提cssText会清除之前元素含有的样式，所以得使用`+=`号

``` javascript
obj.cssText += "width:200px;position:absolute;left:100px;";
```

但是在IE中的最后一个分号会被删除，所以在css表达式前面加一个分号`;`

``` javascript
obj.cssText += ";width:200px;position:absolute;left:100px;";
```

现在可以批量修改CSS了。



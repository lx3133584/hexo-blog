---
title: 对IE浏览器不同事件机制的兼容性处理
tags:
  - JavaScript
  - 兼容IE
  - event
comments: true
date: 2017-04-06 13:30:45
updated: 2017-04-06 13:56:45
categories: JavaScript
---

## 1.添加事件监听句柄

IE浏览器的事件处理程序和其他的浏览器不同，在IE浏览器中，使用`attachEvent()`这个方法设置事件监听，而在其他的浏览器中，使用`addEventListener()`进行处理。

##### 兼容性处理代码：

``` javascript
function addHandler(element,type,handler) {
      if(element.addEventListener){//大多数浏览器
          element.addEventListener(type,handler,false);
      }else if(element.attachEvent){//IE浏览器
          element.attachEvent('on'+type,handler);
      }else{                        //其它老版浏览器
          element['on'+type] = handler;
      }
}  
```
***
## 2.event对象的方法和属性

兼容DOM的浏览器会将一个`event`对象传入到事件处理程序中，其中每个事件包含的属性和方法都不同，但是有些属性和方法是所有的事件共有的：

* `bubbles`:表明事件是否可以冒泡
* `cancelable`:表示是否可以取消事件的默认行为
* `preventDefault()`:取消事件默认行为，但是需要cancelable是true
* `stopPropagation()`:取消事件的进一步冒泡或者捕获,需要bubbles是true
* `stopImmediatePropagation()`:取消事件的进一步冒泡或者捕获，同时阻止任何事件处理程序被调用
* `target`:事件的目标，指向触发的元素

IE中的事件对象有一些不同：

* `srcElement`:等同target
* `returnValue`:默认true，设施false等同preventDefault()
* `cancelBubble`:默认值为false,设置为true就可以取消事件冒泡，等同stopPropagation()

##### 兼容性处理代码：

获取事件的目标，指向触发的元素

``` javascript
function getTarget(event) {
    return event.target || event.srcElement;
}
```

取消事件默认行为

``` javascript
function preventDefault(event) {
    if(event.preventDefault){
        event.preventDefault()
    }else{
        vent.returnValue = false;
    }
}
```

取消事件的进一步冒泡或者捕获

``` javascript
function stopPropagation() {
    if(event.stopPropagation){
        event.stopPropagation();
    }else{
        event.cancelBubble = true;
    }
}
```

---
title: 使用_this = this区分作用域
tags: 
- JavaScript
- 原生JS
categories: JavaScript
comments: true
---
在看别人的代码的时候看到过好几次有人用到：`var _this = this`;。在网上找到了这么用的原因，觉得用的很巧妙。

下面举一个例子：
``` javascript
$("#btn").click(function(){
    var _this = this;//这里this和_this都代表了"#btn"这个对象
    $(".tr").each(function(){
          this;//在这里this代表的是每个遍历到的".tr"对象
          _this;//仍代表"#btn"对象
    })
})
```
这种情况就是在一个代码片段里this有可能代表不同的对象。通过使用 `var _this = this`; 把最初的对象赋值给_this。之后就可以使用_this一直指向最初的对象了。
---
title: JS实现二叉树的遍历
tags: 
- JavaScript
- 算法
categories: JavaScript
comments: true
---
二叉树的遍历指的是按照某种顺序，依次访问二叉树的每个节点，有且访问一次。

### 二叉树的遍历有以下三种

1. 前序遍历，从根节点，到左子树，再到右子树，简称根左右。
2. 中序遍历，从左节点，到根节点，再到右子树，简称左根右。
3. 后序遍历，从左子树，到右子树，再到根节点，简称左右根。

DEMO代码（[完整代码](https://github.com/lx3133584/baidu-IEF/blob/master/%E4%BB%BB%E5%8A%A1%E4%B8%83%EF%BC%9AJavaScript%E5%92%8C%E6%A0%91%EF%BC%88%E4%B8%80%EF%BC%89/index.html)）：

``` javascript
//二叉树的遍历的三种方式
//(1)前序遍历（DLR
function preOrder(node){
    if(node){
        arr.push(node);
        preOrder(node.firstElementChild);
        preOrder(node.lastElementChild);
    }
}
//(2)中序遍历（LDR）
function inOrder(node){
    if(node){
        inOrder(node.firstElementChild);
        arr.push(node);
        inOrder(node.lastElementChild);
    }
}
//(3)后序遍历（LRD）
function postOrder(node){
    if(node){
        postOrder(node.firstElementChild);
        postOrder(node.lastElementChild);
        arr.push(node);
    }
}
```
注：在完成代码过程中出现一个小tips：showWay函数内设置延时器后，回调函数异步运行，读取不出arr的值，可以使用闭包传递参数，以下为代码：
``` javascript
setTimeout(function(arguments){
	return function(){
		//需要运行的代码
	}
}(arguments),500)
```
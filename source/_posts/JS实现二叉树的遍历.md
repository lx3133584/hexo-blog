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
``` html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>JS实现二叉树的遍历</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .wrap{
            display: flex;
            border:1px solid #000;
            width: 600px;
            margin:0 auto;
            height: 150px;
            align-items: center;
            justify-content:center;
        }
        .wrap div{
            display: flex;
            height: 70%;
            width: 44%; 
            margin:0 3%;
            border:1px solid #000;
            justify-content:center;
            align-items: center;   
            background: #fff;         
        }
        .btn-wrap{
            text-align: center;
            padding-top: 20px;
        }
        .btn-wrap button{
            display: inline-block;
            padding:4px 10px;
        }
        
    </style>
</head>
<body>
    <div class="wrap">
        <div>
            <div>
                <div>
                    <div></div>
                    <div></div>
                </div>
                <div>
                    <div></div>
                    <div></div>
                </div>
            </div>
            <div>
                <div>
                    <div></div>
                    <div></div>
                </div>
                <div>
                    <div></div>
                    <div></div>
                </div>
            </div>
        </div>
        <div>
            <div>
                <div>
                    <div></div>
                    <div></div>
                </div>
                <div>
                    <div></div>
                    <div></div>
                </div>
            </div>
            <div>
                <div>
                    <div></div>
                    <div></div>
                </div>
                <div>
                    <div></div>
                    <div></div>
                </div>
            </div>            
        </div>
    </div>
    <div class="btn-wrap"> 
        <button>前序</button>
        <button>中序</button>
        <button>后序</button>
    </div>
    <script>
        var wrap = document.querySelector(".wrap");
        var btn_wrap = document.querySelector(".btn-wrap");
        var btn1 = btn_wrap.querySelectorAll("button")[0];
        var btn2 = btn_wrap.querySelectorAll("button")[1];
        var btn3 = btn_wrap.querySelectorAll("button")[2];
        var arr = [];
        var last;
        var toggle = false;
        //给按钮绑定事件
        btn1.onclick = function(){
            if(!toggle){
                toggle = true;
                reset();
                preOrder(wrap);
                showWay();
            }
        }
        btn2.onclick = function(){
            if(!toggle){
                toggle = true;
                reset();
                inOrder(wrap);
                showWay();
            }
        }
        btn3.onclick = function(){
            if(!toggle){
                toggle = true;
                reset();
                postOrder(wrap);
                showWay();
            }
        }
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
        //显示遍历的过程
        function showWay(){
            for(var i=0; i<arr.length; i++){
                setTimeout(function(i){
                    return function(){
                        if(i == arr.length-1){
                            toggle = false;
                        }
                        if(last){
                            last.style.background = "white";
                        }
                        arr[i].style.background = "red";
                        last = arr[i];
                    }
                }(i),i*1000)
            }
        }
        //初始化
        function reset(){
            arr = [];
            if(last){
                last.style.background = "white";
            }
        }
    </script>
</body>
</html>
```
注：在完成代码过程中出现一个小tips：showWay函数内设置延时器后，回调函数异步运行，读取不出arr的值，可以使用闭包传递参数，以下为代码：
``` javascript
setTimeout(function(arguments){
	return function(){
		//需要运行的代码
	}
}(arguments),500)
```
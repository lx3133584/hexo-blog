---
title: JS页面间传值
tags: 
- JavaScript
categories: JavaScript
comments: true
---
# 一：JavaScript静态页面值传递之URL篇
能过URL进行传值，把要传递的信息接在URL上。

例子：

参数传出页面Post.htm—>
``` html
<input type="text"name="username">
<input type="text" name="sex">
<input type="button"value="Post">
<script language="javascript" >
    function Post(){
　　    //单个值 Read.htm?username=baobao;
　　    //多全值 Read.htm?username=baobao&sex=male;
　　    url= "Read.htm?username="+escape(document.all.username.value);
　　    url+= "&sex=" + escape(document.all.sex.value);
　　    location.href=url;
    }
</script>
```
参数接收页面Read.htm—>
``` javascript
<script language="javascript" >

/*
*--------------- Read.htm -----------------
* Request[key]
* 功能:实现ASP的取得URL字符串,Request("AAA")
* 参数:key,字符串.
* 实例:alert(Request["AAA"])
*--------------- Request.htm -----------------
*/
var url = location.search;
var Request = new Object();
if (url.indexOf("?") != -1) {
    varstr = url.substr(1)　//去掉?号
    　　strs = str.split("&");
    　　for (vari = 0; i < strs.length; i++) 　　{
        Request[strs[i].split("=")[0]] = unescape(strs[i].split("=")[1]);
    }
}
alert(Request["username"])
alert(Request["sex"])

function Request(strName) {
    var strHref = "www.abc.com/index.htm?a=1&b=1&c=测试测试";
    var intPos = strHref.indexOf("?");
    var strRight = strHref.substr(intPos + 1);
    var arrTmp = strRight.split("&");
    for (var i = 0; i < arrTmp.length; i++) {
        var arrTemp = arrTmp[i].split("=");
        if (arrTemp[0].toUpperCase() == strName.toUpperCase()) return arrTemp[1];
    }
    return "";
}
alert(Request("a"));
alert(Request("b"));
alert(Request("c"));

String.prototype.getQuery = function (name) {
    varreg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    varr = this.substr(this.indexOf("?") + 1).match(reg);
    　　if (r != null) return unescape(r[2]); return null;
}
var str = "www.abc.com/index.htm?a=1&b=1&c=测试测试";
alert(str.getQuery("a"));
alert(str.getQuery("b"));
alert(str.getQuery("c"));

</script>
```
优点:取值方便,可以跨域.

缺点:值长度有限制.
# 二：JavaScript静态页面值传递之Cookie篇
Cookie是浏览器存储少量命名数据，它与某个特定的网页或网站关联在一起。还用来给浏览器提供内存,以便脚本和服务器程序可以在一个页面中使用另一个页面的输入数据

参数传出页面Post.htm—>
``` javascript
<inputtype="text" name="txt1">
<inputtype="button" value="Post">

functionsetCookie(name,value){
/*
*---------------setCookie(name,value) -----------------
*setCookie(name,value)
* 功能:设置得变量name的值
* 参数:name,字符串;value,字符串.
* 实例:setCookie('username','baobao')
*---------------setCookie(name,value) -----------------
*/
　　var Days = 30; //此 cookie 将被保存 30 天
　　var exp　= new Date();
　　exp.setTime(exp.getTime() +Days*24*60*60*1000);
　　document.cookie = name +"="+ escape (value) + ";expires=" + exp.toGMTString();
　　location.href = "Read.htm";//接收页面.
}
```
参数接收页面Read.htm—>
``` javascript
function getCookie(name) {
    /*
    *---------------getCookie(name) -----------------
    *getCookie(name)
    * 功能:取得变量name的值
    * 参数:name,字符串.
    * 实例:alert(getCookie("baobao"));
    *---------------getCookie(name) -----------------
    */
    var arr = document.cookie.match(new RegExp("(^|)" + name + "=([^;]*)(;|$)"));
    if (arr != null) returnunescape(arr[2]); return null;
}
alert(getCookie("baobao"));
```
优点:可以在同源内的任意网页内访问，生命期可以设置。

缺点:值长度有限制。
# 三：JavaScript静态页面值传递之Window.open篇
这两窗口之间存在着关系:父窗口parent.htm打开子窗口son.htm

子窗口可以通过window.opener指向父窗口，这样可以访问父窗口的对象。
``` javascript
<input type='text' name='maintext'>
<input type='button' value="Open">
Read.htm

//window.open打开的窗口.
//利用opener指向父窗口.
varparentText = window.opener.document.all.maintext.value;
alert(parentText);
```
优点:取值方便。只要window.opener指向父窗口，就可以访问所有对象。不仅可以访问值，还可以访问父窗口的方法。值长度无限制。

缺点:两窗口要存在着关系，就是利用window.open打开的窗口。不能跨域。


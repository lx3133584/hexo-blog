---
title: meta标签的总结
tags:
  - meta
comments: true
date: 2017-05-05 21:37:30
updated:
categories: HTML
---

***

meta元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。meta标签位于文档的头部，不包含任何内容。meta标签的属性定义了与文档相关联的名称/值对。

# 属性

在HTML5中，不再支持scheme属性。主要关注的是http-equiv和name属性。

name用来描叙网页，对应于content（网页内容）； http-equiv属性看名字就知道了，是用来在HTML文档中模拟HTTP协议的响应头报文的东西。

charset定义字符集，可以为：ISO-8859-1、BIG5、utf-8、shift-Jis、Euc、Koi8-2等！一句代码搞定。

```
<meta charset="utf-8">

```

| 属性       | 值                        | 描述                                         |
|------------|--------------------------|----------------------------------------------|
| charset    | _character encoding_     | 定义文档的字符编码。                           |
| content    | some_text                | 定义与 http-equiv 或 name 属性相关的元信息。   |
| http-equiv |   content-type           | 把 content 属性关联到 HTTP 头部。              |
|            |     expires              |                                               |
|            |     refresh              |                                               |
|            |     set-cookie           |                                               | 
| name       |     author               | 把 content 属性关联到一个名称。                |
|            |     description          |                                               |
|            |     keywords             |                                               |
|            |     generator            |                                               |
|            |     revised              |                                               |
|            |     others               |                                               |
| scheme     | some_text                | 定义用于翻译 content 属性值的格式。不支持。     |


# SEO优化(name相关）

## generator 生成工具

用以说明生成工具（如Microsoft FrontPage 4.0）等。

```
<meta name="generator" content="">

```

## keywords 页面关键词

每个网页应具有描述该网页内容的一组唯一的关键字。

使用人们可能会搜索，并准确描述网页上所提供信息的描述性和代表性关键字及短语。标记内容太短，则搜索引擎可能不会认为这些内容相关。另外标记不应超过874个字符。

```
<meta name="keywords" content="your tags" />

```

## author 作者

告诉搜索引擎你的站点的制作的作者。

```
<meta name="author" content="author name" />

```

## description 页面描述

告诉搜索引擎你的站点的主要内容，每个网页都应有一个不超过150个字符且能准确反映网页内容的描述标签。

```
<meta name="description" content="150 words" />

```

## robots 搜索引擎索引方式

robotterms是一组使用逗号(,)分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。确保正确使用nofollow和noindex属性值。

```
<meta name="robots" content="index,follow" />

```

*   all：文件将被检索，且页面上的链接可以被查询；
*   none：文件将不被检索，且页面上的链接不可以被查询；
*   index：文件将被检索；
*   follow：页面上的链接可以被查询；
*   noindex：文件将不被检索，但页面上的链接可以被查询；
*   nofollow：页面上的链接不可以被查询。

## 其他

```
<meta name="google" content="index,follow" />

<meta name="googlebot" content="index,follow" />

<meta name="verify" content="index,follow" />

```

# http-equiv属性

## Content-Type & Content-Language

```
<meta http-equiv="Content-Type" content="text/html";charset=gb_2312-80">
<meta http-equiv="Content-Language" content="zh-CN">

```

用以说明主页制作所使用的文字以及语言。**如开头所言，这句直接换H5标准的charset标签即可。** 　　

## refresh 页面重定向和刷新

content内的数字代表时间（秒），既多少时间后刷新。如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。

```
<meta http-equiv="refresh" content="0;url=" />

```

## Expires 网页的到期时间

可以用于设定网页的到期时间，一旦过期则必须到服务器上重新调用。需要注意的是必须使用GMT时间格式。

```
<meta http-equiv="Expires" content="Mon,12 May 2001 00:20:00 GMT">

```

## Pragma 禁止缓存

是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出。

```
<meta http-equiv="Pragma" content="no-cache">

```

**一溜好meta，禁止缓存，调试非常方便！**

```
<meta http-equiv="Expires" CONTENT="0">
<meta http-equiv="Cache-Control" CONTENT="no-cache">
<meta http-equiv="Pragma" CONTENT="no-cache"> 

```

## set-cookie cookie设定

cookie设定，如果网页过期，存盘的cookie将被删除。需要注意的也是必须使用GMT时间格式。

```
<meta http-equiv="set-cookie" content="Mon,12 May 2001 00:20:00 GMT">

```

## Pics-label 网页等级评定

网页等级评定，在IE的internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级别就是通过meta属性来设置的。

```
<meta http-equiv="Pics-label" content="">

```

## windows-Target

强制页面在当前窗口中以独立页面显示，可以防止自己的网页被别人当作一个frame页调用。

```
<meta http-equiv="windows-Target" content="_top">

```

## Page-Enter & Page-Exit

设定进入和离开页面时的特殊效果，这个功能即FrontPage中的“格式/网页过渡”，不过所加的页面不能够是一个frame页面。

```
<meta http-equiv="Page-Enter" content="revealTrans(duration=10,transtion=50)"＞和＜meta http-equiv="Page-Exit" contect="revealTrans(duration=20，transtion=6)">

```

# 移动设备

## [viewport](http://www.ttwshell.com/article/Mobile-phone-Webpage-adaptive.html "http://www.ttwshell.com/article/Mobile-phone-Webpage-adaptive.html")

viewport 详情请点击以上链接！

## WebApp全屏模式

伪装app，离线应用。

```
<meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->

```

## 隐藏状态栏/设置状态栏颜色

只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent 。

```
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />

```

## 添加到主屏后的标题

```
<meta name="apple-mobile-web-app-title" content="标题">

```

## 忽略数字自动识别为电话号码

```
<meta content="telephone=no" name="format-detection" /> 

```

## 忽略识别邮箱

```
<meta content="email=no" name="format-detection" />

```

## 添加智能App广告条

Smart App Banner：告诉浏览器这个网站对应的app，并在页面上显示下载banner。

```
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"> 

```

---
title: 解决各种IE兼容
date: 2017-01-03 10:09:21
tags:
---
可以让用户的IE浏览器外不变，但用户在浏览网页时，实际上使用的是Google Chrome浏览器内核，而且支持IE6、7、8等多个版本的IE浏览器。

<!-- more -->

```
Google Chrome Frame也可以让IE用上Chrome的引擎:

<meta http-equiv=“X-UA-Compatible” content=“chrome=1″ />

<meta http-equiv=”X-UA-Compatible” content=”IE=edge,chrome=1″ />
创建html5时发现这么一句话，百度如下：
这样写可以达到的效果是如果安装了GCF，则使用GCF来渲染页面，如果没安装GCF，则使用最高版本的IE内核进行渲染。
Google Chrome Frame（谷歌内嵌浏览器框架GCF）。
可以让用户的IE浏览器外不变，但用户在浏览网页时，实际上使用的是Google Chrome浏览器内核，而且支持IE6、7、8等多个版本的IE浏览器。
```


---
layout: post
title: 兼容ie6半透明效果的css代码及如何用js改变透明度
category: "note"
tags: ["css"]
---

以下是兼容ie6半透明效果的css代码：

	.coming{ filter:alpha(opacity=60); -moz-opacity:0.6; opacity: 0.6;}

或者：

	.coming{ filter:alpha(opacity=60); opacity: 0.6;}

样式名为 coming 的标签内实现了兼容ie6的半透明效果。  
`filter`用于只支持ie的滤镜效果；  
`-moz-opacity`用于firefox早期旧版的透明效果，较新的版本已经不支持，基本上可以去掉这句了；  
`opacity`是标准css半透明属性，用于符合css标准的浏览器，包括现在最新的firefox；

(完)
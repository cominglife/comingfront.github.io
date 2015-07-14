---
layout: post
title: 最简单的用正则表达式读取页面链接参数的js
category: "code"
tags: ["JavaScript"]
---

近期在做一个用js读取页面链接上的参数的功能，上网查了几个都觉得比较复杂或者代码比较多。所以自己做了一个，目前用得还可以，但不知道能否经得起日后的不断使用与验证，先把代码帖出来：

	function getPara(name) {
		var para = window.location.toString().replace(new RegExp(".*[?&]" + name + "=(.*?)(&.*|$)","i"),"$1");
		if(para != window.location.toString() ) {return para}else{return '';}
	}
	alert(getPara("abc"));//调用，这里返回名称为“abc”的参数值

getPara 函数接收一个参数：name，函数第一行用于匹配本页面链接里参数名为变量 name 的值。本来可以一句完成，直接返回 para 的，但使用过程发现当匹配不到参数的时候它是返回本页面链接，这个返回值判断起来比较麻烦。所以在函数里加多第二句：用于判断匹配的值是否等于本页面链接，不等的话返回匹配的值，相等的话则返回空值，这里可以根据页面实际情况设置返回什么值。
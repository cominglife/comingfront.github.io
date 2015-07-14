---
layout: post
title: 跟随页面滚动的浮层实例
category: "code"
tags: ["JavaScript"]
---

最近学习了跟随页面滚动的浮层的效果，而且可以根据滚动到一定的位置才开始跟随，虽然逻辑比较简单，但为了方便提高代码速度，在这里做一下备忘，以后的项目要是再遇到类似效果就可以直接调用了。

html部分：

	<div id="标记位置box的id" style="height:0;line-height:0;font-size:0;overflow:hidden;visibility:hidden"></div>//指定开始滚动的位置，注意不要被任何层包裹，不然容易出问题
	<div id="滚动层id" class="原有css名">

css部分：

	html{_background:url(auto.txt) fixed}　　//修正IE6振动bug，会强制页面在重画之前先处理CSS，auto.txt并不存在
	.原有css名{}
	.跟随滚动css名{position:fixed;top:0;_position:absolute;_top:expression(documentElement.scrollTop);z-index:999;}　　//前面两句支持除ie6以外的浏览器，ie6不支持"fixed"，但支持expression，下划线只有ie6支持

javascript部分：

	<script>
	$$ = function(id){return document.getElementById(id)}
	function addClass(o,cn){var re = new RegExp("(\\s*|^)"+cn+"\\b","g");o.className +=o.className?(re.test(o.className)?"":" "+ cn):cn}
	function removeClass(o,cn){var re = new RegExp("(\\s*|^)"+cn+"\\b","g");var sName = o.className;o.className = sName.replace(re,"")}
	window.onscroll=window.onresize=function(){
		var scrTop = document.documentElement.scrollTop,offTop = $$("标记位置box的id").offsetTop;
		scrTop>offTop?addClass($$("滚动层id"),"跟随滚动css名"):removeClass($$("滚动层id"),"跟随滚动css名");
	}
	</script>

如果是要固定在底部，则：

	.跟随滚动css名{position:fixed;bottom:0;_position:absolute;_top:expression(documentElement.scrollTop+documentElement.clientHeight-this.offsetHeight);z-index:999;}

Chrome 对`document.documentElement.scrollTop`不识别，可获取高度时使用`document.documentElement.scrollTop+document.body.scrollTop`，或者：`Math.max(document.documentElement.scrollTop,document.body.scrollTop)`，经测试，代码在IE、Firefox、Chrome下都能显示正常了。




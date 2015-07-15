---
layout: post
title: document.referrer的用法：计数器
category: "note"
tags: ["JavaScript"]
---

大家都知道，在计数器中有一个很重要的参数：网站流量来源。这个参数的重要性我就不多说了，下面列出它的用法及注意事项：

举例：

coming1.html：

	<body>
		<a href="coming2.html">source link</a>
	</body>

coming2.html（获取页面来源）：

	<body>
		<a href="javascript:alertLink();">alert link</a>
		<script type="text/javascript">
		function alertLink() {
		  alert('本面来源： '+document.referrer);
		}
		</script>
	</body>

上面的例子很清楚的说明了document.referrer的用法了，但需要注意的是有很多特殊情况：  
1、用window.location去跳转页面  
2、用window.open 方式打开新窗口  
3、鼠标拖拽打开新窗口  
4、点击Flash内部链接  
5、HTTPS跳转到HTTP  
以上几种情况在一些浏览器（主要是ie）会丢失document.referrer信息

然后要注意的是，来源地址是包含了链接上问号形式的参数，但不会包含书签形式（#）的参数。

(完)
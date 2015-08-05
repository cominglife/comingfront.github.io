---
layout: post
title: 关于js打开新窗口是否会被浏览器拦截
category: "note"
tags: ["JavaScript"]
---

通过 js 新开窗口打开页面的方法，主要有一下几种：

第1种：window.open(url) 执行 window.open('test.php')，将会打开心新的指定页面，当前页面不变。该方法大部分情况下会被浏览拦截；

第2种：form表单'<form action="drag.html" method="get" id="form" target="_blank"/></form>'，通过新窗口提交表单，target='target' 使表单信息提交至新打开的指定页面，否则当前页面跳转到指定页面；

第3种：模拟超链接(<a>)被点击，用jquery的写法如下，注意最后 openLink[0] 是模拟的原生DOM对象被点击的（使用 Jquery 对象的话没反应）：

	var openLink = $("");
	openLink.attr('href', 'URL地址');
	openLink[0].click();

第4种：利用浏览器的冒泡事件，这种方法稍微有点复杂：

	clickOpenWin: function(f){
	    var dataKey = "clickOpenWin.dataKey"
	    var me = $(this);
	    var A = me.data(dataKey);
	    var returnData = null;
	    if(!A){
	        A = $("");
	        me.data(dataKey, A);
	        A.click(function(e){
	            if(returnData){
	                A.attr("href", returnData);
	            }else {
	                A.before(me);
	                e.stop();
	            }
	        });
	    }
	    me.mouseover(function(){$(this).before(A).appendTo(A);});
	    me.mouseout(function(){A.before($(this));});
	    me.click(function(){
	        A.attr("href", "#|");
	        returnData = f.apply(this, arguments);
	    });
	}

首先，说一下最终的效果，是实现用 “A” 包含你要触发弹窗的元素，原来的click事件要返回弹窗的URL 对应这一句 returnData = f.apply(this, arguments)；然后就要说到弹窗拦截的策略了，具体我就不说了，反正 策略里是不会拦截 “A” 本身吧；最后就是合成了，用A包含后，因为事件会冒泡，所以利用正常的点击，生成动态的链接地址给 A，触发 A 的原始点击事件，就完成了。

浏览器对于用户点击行为直接打开的页面一般不会拦截，比如不通过JS直接点击 a、提交 form 表单，浏览器是不会阻止其跳转页面或者打开新页面行为的。但是对于JS打开新页面浏览器会好好审核的，如下面的例子，很多浏览器回去拦截。

	<form action="test.php" method="get" id="form" target="_blank"/>
		<input type="hidden" name="name" value="ck">
		<input type="hidden"id="pwd"  name="id" value="123456">
		<input type="submit" style="display:none;"  value="提交"> 
	</form>
	<button id="btnSubmitForm">点击我提交表单</button>
	<button id="btnAjaxSubmitForm">点击我发送ajax提交表单</button>
	<script src="js/jquery.js"></script>
	<script>
		$("#btnSubmitForm").on('click,function() {
			window.open(url);
			$("#form").submit();
		})
		//下面这种代码是系统自动执行的默认会被拦截。
		window.open(url);
		$("#form").submit();
		$("#btnSubmitForm").trigger('click');

		$.post(url,json,function(){
			//下面两种也会被浏览器当成广告给拦截掉。浏览器认为ajax发送之后执行的以下事件等同于系统自动触发的都会去阻止。
			window.open(url);
			$("#form").submit();
			$("#btnSubmitForm").trigger('click');
		})
	</script>

如何避免避免这种被拦截情况呢，很简单，我们可以通过以下方法：

	<form action="test.php" method="get" id="form" target="_blank"/>
		<input type="hidden" name="name" value="ck">
		<input type="hidden"id="pwd"  name="id" value="123456">
		<input type="submit" style="display:none;"  value="提交"> 
	</form>
	<button id="btnSubmitForm">点击我提交表单</button>
	<button id="btnAjaxSubmitForm">点击我发送ajax提交表单</button>
	<script src="js/jquery.js"></script>
	<script>
		//第1种方法点击直接触发window.open()或者$(form).submit();
		$("#btnSubmitForm").on('click,function(){
			window.open(url);
			$("#form").submit();
		})
		//第2种方法 若是点击发送 ajax 触发方法，这里要强调一下不管是自动发送 ajax 还是手动发送 ajax 成功之后调用的方法内部用 Window.open() 或者 $(form).submit() 都可能会被认为是广告。下面我的解决方法是，手动同步发送ajax，之后
		将ajax的值赋予变量，再在ajax方法之后调用 Window.open() 或者 $(form).submit() 就可以避免这种问题。
		$("#btnAjaxSubmitForm").on('click,function(){
			$.ajax({
				url: "test.php",
				async: false,
				success:function(){}
			})
			Window.open()或者$(form).submit();
		})
	</script>

这个同步的意思是当JS代码加载到当前AJAX的时候会把页面里所有的代码停止加载，页面出去假死状态，当这个AJAX执行完毕后才会继续运行其他代码页面假死状态解除，用户体验不佳。

以下测试用异步的方式发出ajax请求：

	<form action="test.php" method="get" id="form" target="_blank"/>
		<input type="hidden" name="name" value="ck">
		<input type="hidden"id="pwd"  name="id" value="123456">
		<input type="submit" style="display:none;"  value="提交"> 
	</form>
	<button id="btnSubmitForm">点击我提交表单</button>
	<button id="btnAjaxSubmitForm">点击我发送ajax提交表单</button>
	<script src="js/jquery.js"></script>
	<script>
		$("#btnAjaxSubmitForm").on('click,function(){
			$.ajax({
				url: "test.php",
				async: true,
				success:function(){}
			});
			Window.open()或者$(form).submit();
		})
	</script>

(完)











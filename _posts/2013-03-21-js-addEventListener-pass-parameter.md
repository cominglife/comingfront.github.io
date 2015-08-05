---
layout: post
title: 兼容各浏览器的事件绑定和解绑定并传参
category: "note"
tags: ["JavaScript"]
---

之前在好多项目里遇到这个问题都是使用全局变量去传递参数这个笨办法去解决的，现在有更好的方法了，记录下来备忘：

	<!doctype html>
	<html>
	<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<title>hscm</title>
	<meta name="keywords" content="" />
	<meta name="description" content="" />
	<link type="text/css" rel="stylesheet" href="css/style.css" />
	</head>
	<body>

	<div id="clickDiv">click me xx</div>

	<script>
	    /*addEvent 绑定事件方法
	    **removeEvent 移除绑定方法
	    **obj 添加事件的对象
	    **type 要添加的事件类型如：'click'、‘mouseover’等
	    **fn 要添加的事件，function
	    **para 要传入的参数，调用时使用 e.para
	    */
	    function addEvent(obj, type, fn, para) {
	        obj['e' + type + fn] = obj['e' + type + fn] || null;
	        if (!obj['e' + type + fn]) {
	            obj['e' + type + fn] = function (event) {
	                var event = event || window.event;
	                event.para = para || {};
	                fn.call(obj, event);
	            };
	        }
	        if (obj.addEventListener) {//W3C
	            obj.addEventListener(type, obj['e' + type + fn], false);
	        } else if (obj.attachEvent) {
	            obj.attachEvent('on' + type, obj['e' + type + fn]);
	        }
	    }

	    function removeEvent(obj, type, fn) {//删除事件这个在上面的基础上就比较容易点了
	        if (typeof obj.removeEventListener != 'undefined') {
	            obj.removeEventListener(type, obj['e' + type + fn], false);
	        } else if (typeof obj.detachEvent != 'undefined') {
	            /*这段代码来自网上，但是用ietester测试不行，不知道原生行不行，改成了下面那句ietester测试没问题
	            if(obj.events) {
	                for(var i in obj.events[type]) {
	                    if (obj.events[type][i] == fn) {
	                        delete obj.events[type][i];
	                    }
	                }
	            }
	            */
	           obj.detachEvent("on" + type, obj['e' + type + fn]);
	        }
	    }


	    var oTd = document.getElementById("clickDiv");
	    
	    function onDivClick(e){
	        var xPos;
	        if(e.pageX) {         
	            xPos=e.pageX;
	        }else{
	            xPos=e.clientX+document.body.scrollLeft -document.body.clientLeft;
	            yPos=e.clientY+document.body.scrollTop-document.body.clientTop;
	        }
	        alert(xPos);
	        alert(e.para);
	    }
	    addEvent(oTd, "click", onDivClick, "123");

	    function onDivMouseover(e){
	        var xPos;
	        if(e.pageX) {         
	            xPos=e.pageX;
	        }else{
	            xPos=e.clientX+document.body.scrollLeft -document.body.clientLeft;
	            yPos=e.clientY+document.body.scrollTop-document.body.clientTop;
	        }
	        alert(xPos);
	        alert(e.para);
	        removeEvent(oTd,"mouseover",onDivMouseover);
	    }
	    addEvent(oTd, "mouseover", onDivMouseover, "223");

	</script>
	</body>
	</html>

(完)



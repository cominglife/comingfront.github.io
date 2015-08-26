---
layout: post
title: canvas基础教程
category: "note"
tags: ["canvas"]
---

canvas元素绘制图像的时候有两种方法，分别是，填充：`context.fill()` 和 绘制边框：`context.stroke()`；而在进行图形绘制前，要设置好绘图的样式，填充的样式：`context.fillStyle`、边框样式：`context.strokeStyle`、图形边框宽度：`context.lineWidth`。

demo1：绘制矩形：`context.fillRect(x,y,width,height)`、`context.strokeRect(x,y,width,height)`。  
x:矩形起点横坐标  
y:矩形起点纵坐标  
width:矩形长度  
height:矩形高度


	<html>
	<head>
	<title>矩形</title>
	<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
	<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo1" width="500" height="800"></canvas>
		<script>
			(function(){
			    var canvas = document.getElementById("demo1");  
			    var context = canvas.getContext("2d");  
			    
				//默认black
			    context.fillRect(0, 0, 100, 100);
			    context.strokeRect(120, 0, 100, 100);
			 
			    //设置纯色
			    context.fillStyle = "red";
			    context.strokeStyle = "blue";
			    context.fillRect(0, 120, 100, 100);
			    context.strokeRect(120, 120, 100, 100);
			 
			    //0<透明度值<1，值越低越透明，值>=1时为纯色，值<=0时为完全透明
			    context.fillStyle = "rgba(255,0,0,0.2)";
			    context.strokeStyle = "rgba(255,0,0,0.2)";
			    context.fillRect(0,240 , 100, 100);
			    context.strokeRect(120, 240, 100, 100);
			})();
		</script>
	</body>
	</html>

运行结果：

<canvas id="demo1" width="500" height="800"></canvas>
<script>
	(function(){
	    var canvas = document.getElementById("demo1");  
	    var context = canvas.getContext("2d");  
	    
		//默认black
	    context.fillRect(0, 0, 100, 100);
	    context.strokeRect(120, 0, 100, 100);
	 
	    //设置纯色
	    context.fillStyle = "red";
	    context.strokeStyle = "blue";
	    context.fillRect(0, 120, 100, 100);
	    context.strokeRect(120, 120, 100, 100);
	 
	    //0<透明度值<1，值越低越透明，值>=1时为纯色，值<=0时为完全透明
	    context.fillStyle = "rgba(255,0,0,0.2)";
	    context.strokeStyle = "rgba(255,0,0,0.2)";
	    context.fillRect(0,240 , 100, 100);
	    context.strokeRect(120, 240, 100, 100);
	})();
</script>



(完)











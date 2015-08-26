---
layout: post
title: canvas基础教程
category: "note"
tags: ["canvas"]
---

canvas元素绘制图像的时候有两种方法，分别是，填充：`context.fill()` 和 绘制边框：`context.stroke()`；而在进行图形绘制前，要设置好绘图的样式，填充的样式：`context.fillStyle`、边框样式：`context.strokeStyle`、图形边框宽度：`context.lineWidth`。

demo1：  
绘制矩形：`context.fillRect(x,y,width,height)`、`context.strokeRect(x,y,width,height)`。  
x：矩形起点横坐标  
y：矩形起点纵坐标  
width：矩形长度  
height：矩形高度


	<html>
	<head>
	<title>矩形</title>
	<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
	<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo1" width="400" height="220"></canvas>
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

<canvas id="demo1" width="400" height="220"></canvas>
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

demo2：绘制圆弧  
`context.arc(x, y, radius, starAngle, endAngle, anticlockwise)`  
x：圆心的x坐标  
y：圆心的y坐标  
radius：圆的半径
straAngle：开始角度  
endAngle：结束角度  
anticlockwise：是否逆时针，true为逆时针，false为顺时针

	<html>
	<head>
	<title>圆弧</title>
	<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
	<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo2" width="400" height="400"></canvas>
		<script>
			function() {
			    var canvas =document.getElementById("demo2");  
			    var context =canvas.getContext("2d");  

			    context.beginPath();
			    context.arc(100, 100, 40, 0, Math.PI * 2, true);
			    //不关闭路径路径会一直保留下去，当然也可以利用这个特点做出意想不到的效果
			    context.closePath();
			    context.fillStyle = 'rgba(153,0,255,0.25)';
			    context.fill();

			    context.beginPath();
			    context.arc(200, 100, 40, 0, Math.PI * 3/4, true);
			    context.closePath();
			    context.fillStyle = 'rgba(153,0,255,0.25)';
			    context.fill();

			    context.beginPath();
			    context.arc(100, 200, 40, 0, Math.PI * 3/4, true);
			    context.closePath();
			    context.strokeStyle = 'rgba(153,0,255,0.25)';
			    context.stroke();

			    context.beginPath();
			    context.arc(200, 200, 40, 0, Math.PI * 3/4, true);
			    
			    context.strokeStyle = 'rgba(153,0,255,0.25)';
			    context.stroke();

			    /*
			    1、系统默认在绘制第一个路径的开始点为beginPath
			    2、如果画完前面的路径没有重新指定beginPath，那么画第其他路径的时候会将前面最近指定的beginPath后的全部路径重新绘制
			    3、每次调用context.fill（）的时候会自动把当次绘制的路径的开始点和结束点相连，接着填充封闭的部分
			    */
			    context.beginPath();
			    context.moveTo(100,300);
			    context.arc(100,300,40,0,Math.PI *3/4,true);
			    context.lineTo(100,300);
			    context.closePath();
			    context.strokeStyle = 'rgba(153,0,255,1)';
			    context.stroke();

			    context.beginPath();
			    context.moveTo(200,300);
			    context.arc(200,300,40,0,Math.PI *3/4,true);
			    context.lineTo(200,300);
			    context.closePath();
			    context.fillStyle = 'rgba(153,0,255,1)';
			    context.fill();
			})();
		</script>
	</body>
	</html>

<canvas id="demo2" width="400" height="400"></canvas>
<script>
	function() {
	    var canvas =document.getElementById("demo2");  
	    var context =canvas.getContext("2d");  

	    context.beginPath();
	    context.arc(100, 100, 40, 0, Math.PI * 2, true);
	    //不关闭路径路径会一直保留下去，当然也可以利用这个特点做出意想不到的效果
	    context.closePath();
	    context.fillStyle = 'rgba(153,0,255,0.25)';
	    context.fill();

	    context.beginPath();
	    context.arc(200, 100, 40, 0, Math.PI * 3/4, true);
	    context.closePath();
	    context.fillStyle = 'rgba(153,0,255,0.25)';
	    context.fill();

	    context.beginPath();
	    context.arc(100, 200, 40, 0, Math.PI * 3/4, true);
	    context.closePath();
	    context.strokeStyle = 'rgba(153,0,255,0.25)';
	    context.stroke();

	    context.beginPath();
	    context.arc(200, 200, 40, 0, Math.PI * 3/4, true);
	    
	    context.strokeStyle = 'rgba(153,0,255,0.25)';
	    context.stroke();

	    /*
	    1、系统默认在绘制第一个路径的开始点为beginPath
	    2、如果画完前面的路径没有重新指定beginPath，那么画第其他路径的时候会将前面最近指定的beginPath后的全部路径重新绘制
	    3、每次调用context.fill（）的时候会自动把当次绘制的路径的开始点和结束点相连，接着填充封闭的部分
	    */
	    context.beginPath();
	    context.moveTo(100,300);
	    context.arc(100,300,40,0,Math.PI *3/4,true);
	    context.lineTo(100,300);
	    context.closePath();
	    context.strokeStyle = 'rgba(153,0,255,1)';
	    context.stroke();

	    context.beginPath();
	    context.moveTo(200,300);
	    context.arc(200,300,40,0,Math.PI *3/4,true);
	    context.lineTo(200,300);
	    context.closePath();
	    context.fillStyle = 'rgba(153,0,255,1)';
	    context.fill();
	})();
</script>






(完)











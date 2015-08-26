---
layout: post
title: canvas基础教程
category: "note"
tags: ["canvas"]
---

canvas元素绘制图像的时候有两种方法，分别是，填充：`context.fill()` 和 绘制边框：`context.stroke()`；而在进行图形绘制前，要设置好绘图的样式，填充的样式：`context.fillStyle`、边框样式：`context.strokeStyle`、图形边框宽度：`context.lineWidth`。
  
绘制矩形：`context.fillRect(x,y,width,height)`、`context.strokeRect(x,y,width,height)`。  
x：矩形起点横坐标  
y：矩形起点纵坐标  
width：矩形长度  
height：矩形高度

demo1：

	<!DOCTYPE html>
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

绘制圆弧  
`context.arc(x, y, radius, starAngle, endAngle, anticlockwise)`  
x：圆心的x坐标  
y：圆心的y坐标  
radius：圆的半径
straAngle：开始角度  
endAngle：结束角度  
anticlockwise：是否逆时针，true为逆时针，false为顺时针

demo2：

	<!DOCTYPE html>
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

运行结果：

<canvas id="demo2" width="400" height="400"></canvas>
<script>
	(function() {
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

绘制线段  
`context.moveTo(x,y)`  
`context.lineTo(x,y)`  
x：x坐标  
y：y坐标

绘制贝塞尔曲线（贝济埃、bezier）
`context.bezierCurveTo(cp1x,cp1y,cp2x,cp2y,x,y)`  
cp1x：第一个控制点x坐标  
cp1y：第一个控制点y坐标  
cp2x：第二个控制点x坐标  
cp2y：第二个控制点y坐标  
x：终点x坐标  
y：终点y坐标


绘制二次样条曲线  
`context.quadraticCurveTo(qcpx,qcpy,qx,qy)`  
qcpx：二次样条曲线控制点x坐标  
qcpy：二次样条曲线控制点y坐标  
qx：二次样条曲线终点x坐标  
qy：二次样条曲线终点y坐标

demo3：

	<!DOCTYPE html>
	<html>
	<head>
	<title>贝塞尔</title>
	<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
	<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo3" width="400" height="450"></canvas>
		<script>
			(function init(){
			    var canvas =document.getElementById("demo3");  
			    var context =canvas.getContext("2d");

			    context.strokeStyle = 'rgba(0,0,0,1)';
			    context.moveTo(50, 50);
			    context.lineTo(150, 50);
			    context.lineTo(150, 150);
			    context.stroke();
			    //贝塞尔曲线
			    context.beginPath();
			    context.strokeStyle = 'rgba(153,0,255,1)';
			    context.moveTo(50, 50);
			    context.bezierCurveTo(50, 50,150, 50, 150, 150);
			    context.stroke();

			    context.strokeStyle = 'rgba(0,0,0,1)';
			    context.moveTo(50, 200);
			    context.lineTo(150, 200);
			    context.lineTo(150, 300);
			    context.lineTo(150, 400);
			    context.lineTo(250, 400);
			    context.stroke();
			    //绘制二次样条曲线
			    context.beginPath();
			    context.moveTo(50, 200);
			    context.bezierCurveTo(50, 200, 150, 200, 150, 300);
			    context.quadraticCurveTo(150, 400, 250, 400);
			    context.strokeStyle = 'rgba(153,0,255,1)';
			    context.stroke();
			})();
		</script>
	</body>
	</html>

运行结果：

<canvas id="demo3" width="400" height="450"></canvas>
<script>
	(function init(){
	    var canvas =document.getElementById("myCanvas");  
	    var context =canvas.getContext("2d");

	    context.strokeStyle = 'rgba(0,0,0,1)';
	    context.moveTo(50, 50);
	    context.lineTo(150, 50);
	    context.lineTo(150, 150);
	    context.stroke();
	    //贝塞尔曲线
	    context.beginPath();
	    context.strokeStyle = 'rgba(153,0,255,1)';
	    context.moveTo(50, 50);
	    context.bezierCurveTo(50, 50,150, 50, 150, 150);
	    context.stroke();

	    context.strokeStyle = 'rgba(0,0,0,1)';
	    context.moveTo(50, 200);
	    context.lineTo(150, 200);
	    context.lineTo(150, 300);
	    context.lineTo(150, 400);
	    context.lineTo(250, 400);
	    context.stroke();
	    //绘制二次样条曲线
	    context.beginPath();
	    context.moveTo(50, 200);
	    context.bezierCurveTo(50, 200, 150, 200, 150, 300);
	    context.quadraticCurveTo(150, 400, 250, 400);
	    context.strokeStyle = 'rgba(153,0,255,1)';
	    context.stroke();
	})();
</script>

线性渐变  
`Object createLinearGradient(x1, y1, x2, y2);`  
//创建一个从(x1, y1)点到(x2, y2)点的线性渐变对象。

径向渐变  
`Object createRadialGradient(x1, y1, r1, x2, y2, r2);`  
//创建一个从以(x1, y1)点为圆心、r1为半径的圆到以(x2, y2)点为圆心、r2为半径的圆的径向渐变对象。

渐变对象创建完成之后必须使用它的addColorStop()方法来添加颜色，该方法的原型如下：

	void addColorStop(position, color);
	position：介于 0.0 与 1.0 之间的值，表示渐变中开始与结束之间的位置。
	color：颜色

demo4：

	<!DOCTYPE html>
	<html>
	<head>
		<title>渐变</title>
		<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
		<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo4" width="400" height="400"></canvas>
		<script>
			(function init(){
				var myCanvas =document.getElementById("demo4");  
				var myContext =myCanvas.getContext("2d");  

				var canvasWidth = myCanvas.width;
				var canvasHeight = myCanvas.height;

				var lg = myContext.createLinearGradient(0,0, canvasWidth / 2, canvasHeight / 2);  
				lg.addColorStop(0, '#004073');  
				lg.addColorStop(0.4, '#CC66FF'); 
				lg.addColorStop(1, '#FF6699');  
				myContext.fillStyle = lg;  
				myContext.fillRect(0, 0, canvasWidth / 2, canvasHeight / 2);  

				var rg = myContext.createRadialGradient(canvasWidth / 4 - 50 , canvasHeight * 3 / 4, 20, canvasWidth / 4, canvasHeight * 3 / 4, 100);  
				rg.addColorStop(0, '#FF6699'); 
				rg.addColorStop(0.5, '#FFFFFF');  
				rg.addColorStop(0.7, '#000000'); 
				rg.addColorStop(1, '#004073'); 
				myContext.fillStyle = rg;  
				myContext.fillRect(0, 200, 200, 200);  
			})();
		</script>
	</body>
	</html>

运行结果：

<canvas id="demo4" width="400" height="400"></canvas>
<script>
	(function init(){
		var myCanvas =document.getElementById("demo4");  
		var myContext =myCanvas.getContext("2d");  

		var canvasWidth = myCanvas.width;
		var canvasHeight = myCanvas.height;

		var lg = myContext.createLinearGradient(0,0, canvasWidth / 2, canvasHeight / 2);  
		lg.addColorStop(0, '#004073');  
		lg.addColorStop(0.4, '#CC66FF'); 
		lg.addColorStop(1, '#FF6699');  
		myContext.fillStyle = lg;  
		myContext.fillRect(0, 0, canvasWidth / 2, canvasHeight / 2);  

		var rg = myContext.createRadialGradient(canvasWidth / 4 - 50 , canvasHeight * 3 / 4, 20, canvasWidth / 4, canvasHeight * 3 / 4, 100);  
		rg.addColorStop(0, '#FF6699'); 
		rg.addColorStop(0.5, '#FFFFFF');  
		rg.addColorStop(0.7, '#000000'); 
		rg.addColorStop(1, '#004073'); 
		myContext.fillStyle = rg;  
		myContext.fillRect(0, 200, 200, 200);  
	})();
</script>

globalCompositeOperation 属性  
设置或返回如何将一个源（新的）图像绘制到目标（已有）的图像上。  
Ps：源图像 = 您打算放置到画布上的绘图。目标图像 = 您已经放置在画布上的绘图。  
JavaScript语法：context.globalCompositeOperation="source-in";

	值	描述
	source-over	默认。在目标图像上显示源图像。
	source-atop	在目标图像顶部显示源图像。源图像位于目标图像之外的部分是不可见的。
	source-in	在目标图像中显示源图像。只有目标图像内的源图像部分会显示，目标图像是透明的。
	source-out	在目标图像之外显示源图像。只会显示目标图像之外源图像部分，目标图像是透明的。
	destination-over	在源图像上方显示目标图像。
	destination-atop	在源图像顶部显示目标图像。源图像之外的目标图像部分不会被显示。
	destination-in	在源图像中显示目标图像。只有源图像内的目标图像部分会被显示，源图像是透明的。
	destination-out	在源图像外显示目标图像。只有源图像外的目标图像部分会被显示，源图像是透明的。
	lighter	显示源图像 + 目标图像。
	copy	显示源图像。忽略目标图像。
	source-over	使用异或操作对源图像与目标图像进行组合。

demo5：

	<!DOCTYPE html>
	<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
		<title>globalCompositeOperation 属性</title>
	</head>
	<body>
		<div>
			<strong>红色矩形是源图像，蓝色矩形是目标图像</strong>
		</div>
		<script>
			(function() {
				var gco=new Array();
				gco.push("source-over");
				gco.push("source-atop");
				gco.push("source-in");
				gco.push("source-out");
				gco.push("destination-over");
				gco.push("destination-atop");
				gco.push("destination-in");
				gco.push("destination-out");
				gco.push("lighter");
				gco.push("copy");
				gco.push("xor");
				for (n=0; n<gco.length; n++) {
					document.write("<div id='demo5_" + n + "' style='width:120px; height:100px; float:left; margin:0 5px 5px 0'>" + gco[n] + ":<br>");
					var c=document.createElement("canvas");
					c.width=120;
					c.height=100;
					document.getElementById("demo5_" + n).appendChild(c);
					var ctx=c.getContext("2d");    
					ctx.fillStyle="blue";
					ctx.fillRect(10,10,50,50);
					ctx.globalCompositeOperation=gco[n];
					ctx.beginPath();
					ctx.fillStyle="red";
					ctx.arc(50,50,30,0,2*Math.PI);
					ctx.fill();
					document.write("</div>");	
				}
			}) ();
		</script>
	</body>
	</html>

运行结果：

<div>
	<strong>红色矩形是源图像，蓝色矩形是目标图像</strong>
</div>
<script>
	(function() {
		var gco=new Array();
		gco.push("source-over");
		gco.push("source-atop");
		gco.push("source-in");
		gco.push("source-out");
		gco.push("destination-over");
		gco.push("destination-atop");
		gco.push("destination-in");
		gco.push("destination-out");
		gco.push("lighter");
		gco.push("copy");
		gco.push("xor");
		for (n=0; n<gco.length; n++) {
			document.write('<div class="cf"><div id="demo5_' + n + '" style="width:150px; height:100px; float:left; margin:0 10px 10px 0">' + gco[n] + ':<br>');
			var c=document.createElement("canvas");
			c.width=120;
			c.height=100;
			document.getElementById("demo5_" + n).appendChild(c);
			var ctx=c.getContext("2d");    
			ctx.fillStyle="blue";
			ctx.fillRect(10,10,50,50);
			ctx.globalCompositeOperation=gco[n];
			ctx.beginPath();
			ctx.fillStyle="red";
			ctx.arc(50,50,30,0,2*Math.PI);
			ctx.fill();
			document.write('</div></div>');
		}
	}) ();
</script>

demo6：通过数学计算做的动画

	<!DOCTYPE html>
	<html>
	<head>
		<title>数学之美</title>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	</head>
	<body>
		<div id="demo6"><div>
		<script>
			var xmin=-8, xmax=8, ymin=-8, ymax=8;
			var sx = -250, sy=-100;
			var c=document.createElement("canvas");
			c.width=500;
			c.height=250;
			document.getElementById("demo6").appendChild(c);
			var ctx=c.getContext("2d");
			ctx.fillStyle = "rgba(0, 0, 0, 0.5)";
			var x,y,x0,y0,x1,y1,px,py,a,b,m,k;

			update();
			function update(){
				qiangwei();
				huaban();
				setTimeout(update,20);
			}
			function qiangwei(){
				if(a<=k*Math.PI){
					a+=Math.PI/(30.0*m);
					x1=px+b*Math.sin(m*a)*Math.cos(a);
					y1=py+b*Math.sin(m*a)*Math.sin(a);
					dda(x0,y0,x1,y1);
					x0=x1;
					y0=y1;
				}else{
					ctx.clearRect(0, 0, c.width, c.height);
					a=b=100;
					x0=y0=120;
					px = py = 120;
					m = 10;k = 2;
					a=Math.PI/(30.0*m);
				}
			}
			function dda(x0,y0,x1,y1){
				var dx,dy,e,x,y;
				dx=x1-x0;
				dy=y1-y0;
				e=(Math.abs(dx)>Math.abs(dy)) ? Math.abs(dx) : Math.abs(dy);
				dx=dx/e;
				dy=dy/e;
				x=x0;
				y=y0;
				for(var i=1;i<=e;i++){
					ctx.fillRect(Math.floor(x+0.5),Math.floor(y+0.5),1,1);
					x=x+dx;
					y=y+dy;
				 }
			}
			function huaban(){
				for(var xx=-Math.PI;xx<=Math.PI;xx+=0.01){
					ctx.fillStyle = "rgba(0, 0, 0, 0.5)";
					var yy = Math.sin(xx);
					ctx.fillRect(sx+xwtov(xx), sy + ywtov(yy),1,1);
			  		ctx.fillRect(sx+xwtov(xx), sy + ywtov(-yy),1,1);
			  		ctx.fillRect(sx+xwtov(yy), sy + ywtov(xx),1,1);
			  		ctx.fillRect(sx+xwtov(yy), sy + ywtov(-xx),1,1);
			  		
				}
			}
			function xwtov(x){
				return Math.floor(500+350*(x-xmin)/(xmax-xmin));
			} 
			function ywtov(y){
				return Math.floor(400-350*(y-ymin)/(ymax-ymin));
			}
		</script>
	</body>
	</html>

运行结果：

<div id="demo6"><div>
<script>
	var xmin=-8, xmax=8, ymin=-8, ymax=8;
	var sx = -250, sy=-100;
	var c=document.createElement("canvas");
	c.width=500;
	c.height=250;
	document.getElementById("demo6").appendChild(c);
	var ctx=c.getContext("2d");
	ctx.fillStyle = "rgba(0, 0, 0, 0.5)";
	var x,y,x0,y0,x1,y1,px,py,a,b,m,k;

	update();
	function update(){
		qiangwei();
		huaban();
		setTimeout(update,20);
	}
	function qiangwei(){
		if(a<=k*Math.PI){
			a+=Math.PI/(30.0*m);
			x1=px+b*Math.sin(m*a)*Math.cos(a);
			y1=py+b*Math.sin(m*a)*Math.sin(a);
			dda(x0,y0,x1,y1);
			x0=x1;
			y0=y1;
		}else{
			ctx.clearRect(0, 0, c.width, c.height);
			a=b=100;
			x0=y0=120;
			px = py = 120;
			m = 10;k = 2;
			a=Math.PI/(30.0*m);
		}
	}
	function dda(x0,y0,x1,y1){
		var dx,dy,e,x,y;
		dx=x1-x0;
		dy=y1-y0;
		e=(Math.abs(dx)>Math.abs(dy)) ? Math.abs(dx) : Math.abs(dy);
		dx=dx/e;
		dy=dy/e;
		x=x0;
		y=y0;
		for(var i=1;i<=e;i++){
			ctx.fillRect(Math.floor(x+0.5),Math.floor(y+0.5),1,1);
			x=x+dx;
			y=y+dy;
		 }
	}
	function huaban(){
		for(var xx=-Math.PI;xx<=Math.PI;xx+=0.01){
			ctx.fillStyle = "rgba(0, 0, 0, 0.5)";
			var yy = Math.sin(xx);
			ctx.fillRect(sx+xwtov(xx), sy + ywtov(yy),1,1);
	  		ctx.fillRect(sx+xwtov(xx), sy + ywtov(-yy),1,1);
	  		ctx.fillRect(sx+xwtov(yy), sy + ywtov(xx),1,1);
	  		ctx.fillRect(sx+xwtov(yy), sy + ywtov(-xx),1,1);
	  		
		}
	}
	function xwtov(x){
		return Math.floor(500+350*(x-xmin)/(xmax-xmin));
	} 
	function ywtov(y){
		return Math.floor(400-350*(y-ymin)/(ymax-ymin));
	}
</script>

demo7：星空效果

	<!DOCTYPE html>
	<html>
	<head>
		<title>星空效果</title>
		<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
		<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo7" width="800" height="600"></canvas>
		<script>
			(function() {
				var canvasWidth,canvasHeight;
				var startSize = 3;
				var startSpeed = 1;
				var startNum = 100;
				var BGCOLOR = "black";
				var myContext;
				var starsArr = [];

				function init() {
					var myCanvas = document.getElementById('demo7');
					myContext = myCanvas.getContext("2d");
					canvasWidth = myCanvas.width;
					canvasHeight = myCanvas.height;

					for(var i=0;i < startNum;i++){
						var s = new Star();
						starsArr.push(s);
					}
					setInterval(update, 33);
				}
				function Star() {
					this.reset = function(){
						this.x = 0;
						this.y = Math.floor(Math.random() * canvasHeight);
						this.size = Math.ceil(Math.random() * startSize);
						this.vx = startSpeed * this.size / startSize;
						this.vy = 0;
						this.color = "rgba("+Math.floor(Math.random() * 255)+", "+Math.floor(Math.random() * 255)+", "+Math.floor(Math.random() * 255)+", 0.5)";
					}
					this.reset();
					this.x = Math.floor(Math.random() * canvasWidth);
				}
				Star.prototype.reset = function() {}

				function update() {
					myContext.globalCompositeOperation = "source-over";
					myContext.fillStyle = "rgba(0, 0, 0, 0.2)";
					myContext.fillRect(0, 0, canvasWidth, canvasHeight);
					myContext.globalCompositeOperation = "lighter";

					for(var i = 0; i < startNum; i++){
						var str = starsArr[i];
						myContext.beginPath();
						var lg = myContext.createRadialGradient(str.x, str.y, 0, str.x, str.y, str.size);
						lg.addColorStop(0, "white");
						lg.addColorStop(0.4, str.color);
						lg.addColorStop(1, "black");
						myContext.fillStyle = lg;
						myContext.arc(str.x, str.y, str.size, Math.PI*2, false);
						myContext.fill();
						str.x += str.vx;
						str.y += str.vy;
						if(str.x<=0 || str.x>=canvasWidth || str.y<=0 || str.y>=canvasHeight){
							str.reset();
						}
					}
				}
				init();
			}) ();
		</script>
	</body>
	</html>

运行结果：

<canvas id="demo7" width="800" height="600"></canvas>
<script>
	(function() {
		var canvasWidth,canvasHeight;
		var startSize = 3;
		var startSpeed = 1;
		var startNum = 100;
		var BGCOLOR = "black";
		var myContext;
		var starsArr = [];

		function init() {
			var myCanvas = document.getElementById('demo7');
			myContext = myCanvas.getContext("2d");
			canvasWidth = myCanvas.width;
			canvasHeight = myCanvas.height;

			for(var i=0;i < startNum;i++){
				var s = new Star();
				starsArr.push(s);
			}
			setInterval(update, 33);
		}
		function Star() {
			this.reset = function(){
				this.x = 0;
				this.y = Math.floor(Math.random() * canvasHeight);
				this.size = Math.ceil(Math.random() * startSize);
				this.vx = startSpeed * this.size / startSize;
				this.vy = 0;
				this.color = "rgba("+Math.floor(Math.random() * 255)+", "+Math.floor(Math.random() * 255)+", "+Math.floor(Math.random() * 255)+", 0.5)";
			}
			this.reset();
			this.x = Math.floor(Math.random() * canvasWidth);
		}
		Star.prototype.reset = function() {}

		function update() {
			myContext.globalCompositeOperation = "source-over";
			myContext.fillStyle = "rgba(0, 0, 0, 0.2)";
			myContext.fillRect(0, 0, canvasWidth, canvasHeight);
			myContext.globalCompositeOperation = "lighter";

			for(var i = 0; i < startNum; i++){
				var str = starsArr[i];
				myContext.beginPath();
				var lg = myContext.createRadialGradient(str.x, str.y, 0, str.x, str.y, str.size);
				lg.addColorStop(0, "white");
				lg.addColorStop(0.4, str.color);
				lg.addColorStop(1, "black");
				myContext.fillStyle = lg;
				myContext.arc(str.x, str.y, str.size, Math.PI*2, false);
				myContext.fill();
				str.x += str.vx;
				str.y += str.vy;
				if(str.x<=0 || str.x>=canvasWidth || str.y<=0 || str.y>=canvasHeight){
					str.reset();
				}
			}
		}
		init();
	}) ();
</script>

demo8：雨水效果

	<!DOCTYPE html>
	<html>
	<head>
		<title>雨水效果</title>
		<META http-equiv="X-UA-Compatible" content="IE=edge"></META>
		<META http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	</head>
	<body>
		<canvas id="demo8" width="600" height="400"></canvas>
		<script>
			(function() {
				var canvasWidth,canvasHeight;

				var dripSpeed = 1;
				var dripNum = 100;
				var BGCOLOR = "black";
				var myContext;
				var gravity = 0.01;
				var dripArr = [];

				function init(){
					var myCanvas = document.getElementById('demo8');
					myContext = myCanvas.getContext("2d");
					canvasWidth = myCanvas.width;
					canvasHeight = myCanvas.height;

					for(var i=0;i < dripNum;i++) {
						var s = new Drip();
						dripArr.push(s);
					}
					setInterval(update, 10);
				}
				function Drip(){
					this.reset = function(){
						this.x = Math.floor(Math.random() * canvasWidth)
						this.y = 0;
						this.vx = 0;
						this.vy = dripSpeed ;
						this.color = "rgba(0, 153, 255, 0.7)";
					}
					this.reset();
					this.y = Math.floor(Math.random() * canvasHeight);
				}

				function rand( min, max ) {
					return Math.random() * ( max - min ) + min;
				}

				function update(){
					myContext.globalCompositeOperation = "source-over";
					myContext.fillStyle = "rgba(0, 0, 0, 0.1)";
					myContext.fillRect(0, 0, canvasWidth, canvasHeight);
					myContext.globalCompositeOperation = "lighter";
					for(var i = 0; i < dripNum; i++){
						var drip = dripArr[i];
						myContext.beginPath();
						var lg  = myContext.createLinearGradient(drip.x, drip.y, drip.x,drip.y+2);
						lg.addColorStop(0, "white");
						lg.addColorStop(1, drip.color);
						myContext.fillStyle = lg;
						myContext.rect(drip.x, drip.y, 1,2); 
						myContext.fill();
						drip.vy += gravity;
						drip.x += drip.vx;
						drip.y += drip.vy;
						if(drip.x<=0 || drip.x>=canvasWidth || drip.y<=0 || drip.y>=canvasHeight){
							drip.reset();
						}
					}
				}
				init();
			}) ();
		</script>
	</body>
	</html>

运行结果：

<canvas id="demo8" width="600" height="400"></canvas>
<script>
	(function() {
		var canvasWidth,canvasHeight;

		var dripSpeed = 1;
		var dripNum = 100;
		var BGCOLOR = "black";
		var myContext;
		var gravity = 0.01;
		var dripArr = [];

		function init(){
			var myCanvas = document.getElementById('demo8');
			myContext = myCanvas.getContext("2d");
			canvasWidth = myCanvas.width;
			canvasHeight = myCanvas.height;

			for(var i=0;i < dripNum;i++) {
				var s = new Drip();
				dripArr.push(s);
			}
			setInterval(update, 10);
		}
		function Drip(){
			this.reset = function(){
				this.x = Math.floor(Math.random() * canvasWidth)
				this.y = 0;
				this.vx = 0;
				this.vy = dripSpeed ;
				this.color = "rgba(0, 153, 255, 0.7)";
			}
			this.reset();
			this.y = Math.floor(Math.random() * canvasHeight);
		}

		function rand( min, max ) {
			return Math.random() * ( max - min ) + min;
		}

		function update(){
			myContext.globalCompositeOperation = "source-over";
			myContext.fillStyle = "rgba(0, 0, 0, 0.1)";
			myContext.fillRect(0, 0, canvasWidth, canvasHeight);
			myContext.globalCompositeOperation = "lighter";
			for(var i = 0; i < dripNum; i++){
				var drip = dripArr[i];
				myContext.beginPath();
				var lg  = myContext.createLinearGradient(drip.x, drip.y, drip.x,drip.y+2);
				lg.addColorStop(0, "white");
				lg.addColorStop(1, drip.color);
				myContext.fillStyle = lg;
				myContext.rect(drip.x, drip.y, 1,2); 
				myContext.fill();
				drip.vy += gravity;
				drip.x += drip.vx;
				drip.y += drip.vy;
				if(drip.x<=0 || drip.x>=canvasWidth || drip.y<=0 || drip.y>=canvasHeight){
					drip.reset();
				}
			}
		}
		init();
	}) ();
</script>

(完)











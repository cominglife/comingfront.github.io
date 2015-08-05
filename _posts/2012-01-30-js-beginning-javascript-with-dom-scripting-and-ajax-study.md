---
layout: post
title: 深入浅出JavaScript学习笔记
category: "note"
tags: ["JavaScript"]
---

__一、变量：__

以一个字母或一个下划线开始，其它部分可以由数字、字母、美元符和下划线构成。  
变量区分大小写，一般使用骆驼命名法(camel['kAmEl] notation)。  
--notation:[nEu'teiFEn]n. 符号(表示法);标志(法);记号[法];【数】记数法,计数[算]制。  
--chemical notation：化学符号；binary notation：二进位符号, 二进(位计数)法。

__二、基本数据类型：__

1、保存信息的3种基本数据类型，只保存单个值；  
(1)字符串(String)；  
(2)数字(number)；  
(3)布尔值(boolean)；

2、其它2种基本数据类型，不保存信息，用来对特定情况给出警告；  
(1)空值(null)：表示没有数据。  
(2)未定义(undefined)：表示没有定义也没有赋值。

__三、复合数据类型，对象(object)、数组(array)：__

1、对象(object)：javascript提供的对象：String、Date、Math；  
(1)String：可以显式或隐式地创建；  
(2)Date：只能显式地创建；  
a、创建包含当前日期和时间的Date对象：`var todayDate=new Date();`  
b、创建特定日期或时间的Date对象：`var newMillennium=new Date("1 jan 2000 10:24:00");`  
c、如月份是简写，可任意顺序创建：`var someDate=new Date("10 jan 2000");var someDate=new Date("jan 10 2000");`  
d、Date对象可以拥有很多参数：  
`var someDate=new Date(aYear,aMonth,aDate,anHour,aMinute,aSecond,aMillisecond);`  
必须按顺序使用，如：`var someDate=new Date(2003,9,22,17);`正确，  
但`var someDate=new Date(2003,9,,17);`错误。  
注意：javascript从0开始计算月份，因此月份8表示9月；  
(3)Math：不能显示创建，直接使用即可，不存储数据；  
模拟掷骰子事件：`var diceThrow=Math.round(Math.random()*5)+1;`

2、数组(array)：  
(1)创建：

	var preInitArray=new Array("first item","second item","third item");
	var preInitArray=new Array(3);
	var preInitArray=new Array();
	var preInitArray=[1,2,3];

__四、判定__

1、String对象之间的比较要注意：

	<script type="text/javascript">
		var string1=new String("Apple");
		var string2=new String("Apple");
		document.wirte(string1==string2);
	</script>

结果是false，因为他们是不同的对象，如果确实要比较两个对象的值，可以这样：

	document.wirte(string1.valueOf()==string2.valueOf());

结果为true。

2、条件语句：

	if(expression) {
		......
	}else if(expression) {
		......
	}else{
		......
	}

3、switch语句：

	switch(expression) {
		case someValue:
			code to execute if expression==someValue;
		break;
		......
		default:
			code to execute if no value matched;
	}

__注意点：__

1、函数内通过var关键字定义局部变量，不会影响函数外的同名全局变量，不用`var`的话，会覆盖全局变量。

2、可以定义一个新的对象，将函数作为这个对象的方法使用(与Date、Math、String等javascript对象的工作原理一样)

	<script type="text/javascript">
	myscript=new Object();
	myscript.init=function(){
		some code
	};
	myscript.validate=function(){
		some code
	};
	</script>

注意：这时调用`init()`和`validate()`会出错，因为它们根本不存在，要用：  
`myscript.init()`和`myscript.validate()`。

3、定义对象的方法仍然有点笨拙，因为不得不不断重复对象的名称，更简单的方法是叫作对象字面量(Object literal)：

	<script type="text/javascript">
	var dynamicLinks={
		linksInit:function() {
			if(!document.getElementById||!document.createTextNode) {return;}
			var openLink = dynamicLinks.createLink("#","open");
			dynamicLinks.appendLink(openLink);
			var closeLink = dynamicLinks.createLink("closed.html","close");
			dynamicLinks.appendLink(closeLink);
		},
		createLink:function(linkTarget,linkName) {
			if(linkTarget == null) {linkTarget="#";}
			if(linkName == null) {linkTarget="dummy";}
			var tempLink = document.createElement("a");
			tempLink.setAttribute("href",linkTarget);
			tempLink.appendChild(document.creatTextNote(linkName) );
			return tempLink;
		},
		appendLink:founction(sourceLink,elementId) {
			var element = false;
			if(elementId == null || !document.getElementById(elementId) ) {element=document.body;}
			if(!element) {element = document.getElementById(elementId);}
			element.appendChild(sourceLink);
		}
	}
	</script>

如果想使用可被某对象内部所有方法访问的变量，可通过下面的语法实现：

	var myObject={
		objMainVar:'preset',
		objSecondaryVar:0,
		objArray:['one','two','three'],
		init:function(){},
		creatLink:function(){},
		appendLink:function(){}
	}

__五、HTML与javascript__

1、在网页中使用javascript提供反馈信息：老的方式

	<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/html4/strict.dtd">
	<html dir="ltr" lang="en">
	<head>
	<meta http-equiv="content-type" content="text/html; charset=utf-8" />
	<title>Date example</title>
	<script type="text/javascript">
	function checkDate() {
		if(!document.getElementById || !document.createTextNode) {return;}
		if(!document.getElementById("date") ) {return;}
		//define a regular expression to check the date format
		var checkPattern = new RegExp("\\d{2}/\\d{2}/\\d{4}");
		//Get the value of the date entry field
		var dateValue = document.getElementById("date").value;
		//If thres is no date entered,don't sned the form
		if(dateValue=="") {
			alert("Please enter a date");
			return false;
		}
		else{
			//tell the user to change the date syntax either until she presses Cancle or entered the right syntax
			while(!checkPattern.test(dateValue) && dateValue!=null) {
				dateValue = prompt("your date was not in the right format. Please enter it as DD/MM/YYYY.",dateValue);
		}
		document.getElementById("date").value=dateValue;
		return dateValue!=null;
		}
	}
	</script>
	</head>
	<body>
		<h1>Events search</h1>
		<form action="eventssearch.php" method="post" onsubmit="return checkDate();">
		<p>
			<lable for="date">Date in the format DD/MM/YYYY:</lable><br />
			<input type="text" id="date" name="date" />
			<input type="submit" value="Check" />
			<br />(excemple 06/04/1975)
		</p>
		</form>
	</body>
	</html>

2、通过DOM访问文档

(1)访问文档中元素：

A、`document.getElementById("id")`：获取给定id的元素，并将其作为对象；

B、document.getElementsByTagName("tagname")：获取所有标签名为tagname的元素，并把它保存在一个类似数组的列表中；例：

	document.getElementsByTagName("p");
	document.getElementsByTagName("p")[0];
	document.getElementsByTagName("ul")[3].document.getElementsByTagName("li")[2];
	document.getElementsByTagId("id").document.getElementsByTagName("li")[2];

(2)读取元素的属性、节点值及其它节点数据：

A、`node.getAttribute("attribute")`：获取属性名为attribute的值；

B、`node.setAttribute("attribute","value")`：设置属性名为attribute的值为value；

C、`node.nodeType`：读取节点类型（1=元素，3=文本节点）；

D、`node.nodeName`：读取节点名称（元素名字或#textNode）；

E、`node.nodeValue`：读取或设置节点的值（文本节点的情况下则为文本内容）；

	document.getElementByTagName("p")[0].nodeValue="Hello World";//错误
	document.getElementByTagName("p")[0].firstChild.nodeValue="Hello World";//正确

(3)节点之间操作

A、`node.previousSibling`：获取上一个兄弟节点，并将它保存为一个对象；

B、`node.nextSibling`：获取下一个兄弟节点，并将它保存为一个对象；

C、`node.childNodes`：获取对象的所有子节点(注意，只获取一级子节点，不包括子节点的子节点)，交把它储存到一个列表中，该方法在IE与firefox之间有区别，其它浏览器如firefox将元素之间的换行符作为文本节点也计算在内了：

HTML：

	<ul id="eventsList">
		<li>list 1</li>
		<li>list 1</li>
		<li><a href="www.google.com.hk">link list item</a></li>
		<li>list 1</li>
	</ul>

JS：

	function myDOMinspector() {
		var DOMstring = "";
		if(!document.getElementById || !document.createTextNode) {
			alert("!document.getElementById || !document.createTextNode");
		}
		var demoList = document.getElementById("eventsList");
		if(!demoList) {alert("!demoList");}
		if(demoList.hasChildNodes() ) {
			var ch=demoList.childNodes;
			for(var i=0;i<ch.length;i++) {
				DOMstring+=ch[i].nodeName+"\n";
			}
			alert(DOMstring);
		}
	}
	window.onload=myDOMinspector;

D、`node.firstChild`：获取对象的第一个子节点，并把它储存到一个对象中；

E、`node.lastChild`：获取对象的最后一个子节点，并把它储存到一个对象中；

F、`node.parentNode`：获取包含node的节点；

(4)创建新节点

A、`document.createElement(element)`：创建一个名字为element的新元素，需要提供一个字符串形式的元素名

B、`document.createTextNode(string)`：创建一个节点值为string的文本节点

C、`newNode=node.cloneNode(bool)`：创建newNode节点作为node的副本（克隆），如果bool值为true，这个克隆将包含原节点的所有子节点和属性的克隆；

D、`node.appendChild(newNode)`：将newNode作为子节点，添加到node所在的子节点之后；

E、`node.insertBefore(newNode,oldNode)`：在node节点的子节点oldNode之前插入newNode；

F、`node.removeChild(oldNode)`：移除node节点的子节点oldNode；

G、`node.replaceChild(newNode,oldNode)`：使用节点newNode替换node节点的子节点oldNode；

H、`element.innerHTML`：读写给定element的HTML内容，它是一个字符串，包括所有字节点及它们的属性和文本内容；

3、页面加载完成后执行函数

	function func(){
		......
	}
	window.onload=func;









(未完，待续)











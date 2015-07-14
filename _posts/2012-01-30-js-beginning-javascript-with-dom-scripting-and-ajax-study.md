---
layout: post
title: 深入浅出JavaScript学习笔记
category: "note"
tags: ["css"]
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
d、Date对象可以拥有很多参数：`var someDate=new Date(aYear,aMonth,aDate,anHour,aMinute,aSecond,aMillisecond);`必须按顺序使用，如：`var someDate=new Date(2003,9,22,17);`正确，但`var someDate=new Date(2003,9,,17);`错误。  
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

（完）











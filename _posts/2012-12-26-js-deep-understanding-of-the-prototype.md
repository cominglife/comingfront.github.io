---
layout: post
title: 深入理解javascript 之 prototype 属性
category: "note"
tags: ["JavaScript"]
---

看着这个题目，其实要清楚地整理出 javascript 的 prototype 属性是一件比较难的事情。之前对 javascript 的学习都是断断续续，对这个复杂的属性的理解比较模糊。这段时间在看 [Javascript 设计模式] 这本书，发现如果我不梳理一下之前学习的 js 知识是很难看懂这本书的。所以现在首先来详细了解一下 prototype 这个属性吧，以下内容是根据自己在书本、网络里学习总结而出。

首先要清晰的一个知识点：Javascript 的方法分三类：(1)类方法、(2)对象方法、(3)原型方法。以下为例子：

	<script>
	function Coming() {
		//对象方法
		this.methodA = function() {alert("This is a method of object!");}
	}
	//类方法
	Coming.methodA = function() {alert("This is a method of class!");}
	//原型方法
	Coming.prototype.methodB = function() {alert("This is a method of prototype!");}

	//test:
	var coming1=new Coming();
	coming1.methodA();
	Coming.methodA();
	coming1.method1B();
	</script>

明白了js的方法分类后，即可通过以下代码实例去理解prototype属性：

1、prototype 的定义：JavaScript 中对象的prototype 属性，可以返回对象类型原型的引用。对象的类（Class）和对象实例（Instance）之间是一种“创建”关系，因此我们把“类”看作是对象特征的模型化，而对象看作是类特征的具体化，或者说，类（Class）是对象的一个类型(Type)。以下例子演示了通常的在 Javascript 中定义一个类型的方法

	<script>
	function Coming() {
		this.propertyA = "coming";
		this.methodA = function() {
			alert("life");
		}
	}
	var Coming1 = new Coming();
	alert(Coming1.propertyA); //outputs "coming"
	Coming1.methodA(); //outputs "life"
	</script>

2、可以在类型（构造函数）上使用 proptotype 来为类型添加行为。这些行为只能在类型的实例（对象）上体现。JS中允许的类型有Array, Boolean, Date, Enumerator, Error, Function, Number, Object, RegExp, String；

	<script>
	Object.prototype.propertyA = "coming";
	Object.prototype.methodA = function() {alert("life");}
	var obj = new Object();
	alert(obj.propertyA); //outputs "coming"
	obj.methodA(); //outputs "life"
	</script>

3、在实例上不能使用 prototype，否则会出现编译错误；

	<script>
	var obj = new Object();
	obj.prototype.propertyA = "coming"; //Error
	obj.prototype.methodA = function() {alert("life");} //Error
	</script>

4、可以给类型定义“静态”的属性和方法，直接在类型上调用即可；

	<script>
	Object.propertyA = "coming";
	Object.methodA = function() {alert("life");}
	alert(Object.propertyA); //outputs "coming"
	Object.methodA(); //outputs "life"
	</script>

5、实例不能调用类型的静态属性或方法，否则会出现对象未定义的错误；

	<script>
	Object.propertyA = "coming";
	Object.methodA = function() {alert("life");}
	var obj = new Object();
	alert(obj.propertyA); //Error
	obj.methodA(); //Error
	</script>

6、可以在外部使用prototype为自定义的类型添加属性和方法；

	<script>
	function Coming() {
		this.propertyA = "coming";
		this.methodA = function() {alert("life");}
	}
	Coming.prototype.propertyB = "coming 2";
	Coming.prototype.methodB = function {alert("life 2");}
	var coming1 = new Coming();
	alert(coming1.propertyB);
	coming1.methodB();
	</script>

7、在外部不能通过prototype改变自定义类型的属性或方法。该例子可以看到：调用的属性和方法仍是最初定义的结果。

	<script>
	function Coming() {
		this.propertyA = "coming";
		this.methodA = function() {alert("life");}
	}
	Coming.prototype.propertyA = "coming 2";
	Coming.prototype.methodA = function {alert("life 2");}
	var coming1 = new Coming();
	alert(coming1.propertyA);
	coming1.methodA();
	</script>

8、可以在对象上改变属性，也可以在对象上改变方法。（和普遍的面向对象的概念不同）；

	<script>
	function Coming() {
		this.propertyA = "coming";
		this.methodA = function() {alert("life");}
	}
	var coming1 = new Coming();
	coming1.propertyA = "coming 2";
	coming1.methodA = function() {alert("life 2");}
	alert(coming1.propertyA);
	coming1.methodA();
	</script>

9、可以在对象上增加属性或方法；

	<script>
	function Coming() {
		this.propertyA = "coming";
		this.methodA = function() {alert("life");}
	}
	var coming1 = new Coming();
	coming1.propertyB = "coming 2";
	coming1.methodB = function() {alert("life 2");}
	alert(coming1.propertyB);
	coming1.methodB();
	</script>

10、这个例子说明了一个类型如何从另一个类型继承；

	<script>
	function ComingA() {
		this.propertyA = "coming 1";
		this.methodA = function() {alert("life 1");}
	}
	function ComingB() {
		this.propertyB = "coming 2";
		this.methodB = function() {alert("life 2");}
	}
	ComingB.prototype = new ComingA();
	var comingB1 = new ComingB();
	alert(comingB1.propertyA);
	comingB1.methodA();
	alert(comingB1.propertyB);
	comingB1.methodB();
	</script>

11、这个例子说明了子类如何重写父类的属性或方法；

	<script>
	function ComingA() {
		this.propertyA = "coming 1";
		this.methodA = function() {alert("life 1");}
	}
	function ComingB() {
		this.propertyB = "coming 2";
		this.methodB = function() {alert("life 2");}
	}
	ComingB.prototype = new ComingA();
	ComingB.prototype.propertyA = "coming 3";
	ComingB.prototype.methodA = function() {alert("life 3");}
	var comingB1 = new ComingB();
	alert(comingB1.propertyA); //outputs "coming 3"
	comingB1.methodA(); //outputs "life 3"
	</script>

12、注意：在类型外部重写父类的属性或方法时，要写在类型继承之后，如果写在前面会在继承之前清除掉；

	<script>
	function ComingA() {
		this.propertyA = "coming 1";
		this.methodA = function() {alert("life 1");}
	}
	function ComingB() {
		this.propertyB = "coming 2";
		this.methodB = function() {alert("life 2");}
	}
	ComingB.prototype.propertyA = "coming 3";
	ComingB.prototype.methodA = function() {alert("life 3");}
	ComingB.prototype = new ComingA();
	var comingB1 = new ComingB();
	alert(comingB1.propertyA); //outputs "coming 1"
	comingB1.methodA(); //outputs "coming 1"
	</script>

13、注意：在类型内部有与父类同名的属性或方法时，在类型继承之后会覆盖父类的属性或方法；

	<script>
	function ComingA() {
		this.propertyA = "coming 1";
		this.methodA = function() {alert("life 1");}
	}
	function ComingB() {
		this.propertyB = "coming 2";
		this.methodB = function() {alert("life 2");}
		ComingB.prototype.propertyA = "coming 3";
		ComingB.prototype.methodA = function() {alert("life 3");}
	}
	ComingB.prototype = new ComingA();
	var comingB1 = new ComingB();
	alert(comingB1.propertyA); //outputs "coming 3"
	comingB1.methodA(); //outputs "life 3"
	</script>

那么子类的一个实例如何调用父类的实例的方法呢？答案是可以使用call，obj1.func.call(obj)方法意思是将obj看成obj1,调用func方法；

	<script>
	function ComingA() {
		this.propertyA = "coming 1";
		this.methodA = function() {alert("life 1");}
	}
	function ComingB() {
		this.propertyA = "coming 2";
		this.methodA = function() {alert("life 2");}
	}
	ComingB.prototype = new ComingA();
	var comingB1 = new ComingB();
	var comingA1 = new ComingA();
	comingA1.methodA.call(comingB1); //outputs "life 1"
	comingA1.methodA(); //outputs "life 1"
	</script>

至此，本人了解的 prototype 属性的知识都列出来了，以后有相关的知识点都会在这里列出来。

(完)











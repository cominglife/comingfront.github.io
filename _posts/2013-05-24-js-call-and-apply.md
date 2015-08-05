---
layout: post
title: call与apply方法详解
category: "note"
tags: ["JavaScript"]
---

2014.12.5.补充：

通过 call 去实现继承的，子类是不能把父类的 prototype 也继承下来的，需要把父类的 prototype 也继承的可以用：Son.prototype = new Father();

	//例1，call 不能实现父类的 prototype 继承：
	function Father() {
		this.name = "FatherName";
	}
	Father.prototype = {
		age:"FatherAge",
	}
	function Son() {
		Father.call(this);
	}
	var oSon = new Son();
	console.log(oSon.name);  //"FatherName"
	console.log(oSon.age);  //undefined
	var oFather = new Father();
	console.log(oFather.name);  //"FatherName"
	console.log(oFather.age);  //"FatherAge"

	//例2，把父类的prototype也继承下来：
	function Father() {
		this.name = "Father";
		this.showName = function() {alert(this.name);}
	}
	Father.prototype = {
		age:10,
		showAge:function() {
			alert(this.age);
		}
	}
	function Son() {
		console.log(this.name);
	}
	Son.prototype = new Father();
	var oSon = new Son();
	console.log(oSon.name);  //"FatherName"
	console.log(oSon.age);  //"FatherAge"
	var oFather = new Father();
	console.log(oFather.name);  //"FatherName"
	console.log(oFather.age);  //"FatherAge"

<i class="article_hr"></i>

原文：

call([thisObj[,arg1[, arg2[, [,.argN]]]]])  
参数：  
thisObj：可选项，将被用作当前对象的对象。  
arg1, arg2, ..., argN：可选项。将被传递方法参数序列。  
说明： 
call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。

	//例1：
	function add(a,b) {
		alert(a+b);
	}
	function sub(a,b) {
		alert(a-b);
	}
	add.call(sub,3,1);  //alert(4)

这个例子中的意思就是用 add 来替换 sub，add.call(sub,3,1) == add(3,1)，所以运行结果为：alert(4)；注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。

	//例2：
	function Class1() {
		this.name = "class1";
		this.showNam = function() {
			alert(this.name);
		}
	}  
	function Class2() { 
		this.name = "class2";
	}  
	var c1 = new Class1();
	var c2 = new Class2();
	c1.showNam.call(c2);

注意，call 的意思是把 c1 的方法放到 c2 上执行，原来 c2 是没有 showNam() 方法的，现在是把c1 的 showNam() 方法放到 c2 上来执行，所以 this.name 应该是 class2，执行的结果就是：alert("class2")；

	//例3，用call实现继承：
	function Class1() {
		this.showTxt = function(txt) {
			alert(txt);
		}
	}
	function Class2() {
		Class1.call(this);
	}
	var c2 = new Class2();
	c2.showTxt("cc");

Class2 继承了 Class1，Class1.call(this) 的意思是使用 Class1 对象代替 this 对象，那么 Class2 就有了 Class1 的所有属性和方法，c2 对象就能够直接调用 Class1 的方法以及属性，执行结果就是：alert("cc");

	//例4，多重继承：
	function Class10() {
		this.showSub = function(a,b) {
			alert(a-b);
		}
	}
	function Class11() {
		this.showAdd = function(a,b) {
			alert(a+b);
		}
	}
	function Class2() {
		Class10.call(this); Class11.call(this); 
	}

使用多个 call 就实现多重继承。

apply 与 call 这两个方法基本上是一样的，区别在于 call 的第二个参数可以是任意类型，而apply的第二个参数必须是数组，也可以是arguments。

	//例5，apply示例：
    function Person(name,age) {  /*定义一个人类*/
        this.name=name;
        this.age=age;
    }
    function Student(name,age,grade) {  /*定义一个学生类*/
        Person.apply(this,arguments);
        this.grade=grade;
    }
    var student=new Student("qian",21,"一年级");  //创建一个学生类
    //测试：
    alert("name:"+student.name+"\n"+"age:"+student.age+"\n"+"grade:"+student.grade); //name:qian  age:21  grade:一年级

apply的一些其他巧妙用法：  
调用apply方法的时候，第一个参数是对象(this), 第二个参数是一个数组集合, 它可以将一个数组默认的转换为一个参数列表([param1,param2,param3] 转换为 param1,param2,param3)，这个如果让我们用程序来实现将数组的每一个项，来装换为参数的列表，可能都得费一会功夫，借助apply的这点特性可以有以下高效率的方法:
 
(1) Math.max 可以实现得到数组中最大的一项  
因为 Math.max 参数里面不支持 Math.max([param1,param2]) 也就是数组，但是它支持 Math.max(param1,param2,param3…)，所以可以根据刚才apply的那个特点来解决：var max = Math.max.apply(null,array)，这样轻易的可以得到一个数组中最大的一项(apply会将一个数组装换为一个参数接一个参数的传递给方法)。  
这块在调用的时候第一个参数给了一个null，这个是因为没有对象去调用这个方法，我只需要用这个方法帮我运算，得到返回的结果就行，所以直接传递了一个null过去。

(2) Math.min 可以实现得到数组中最小的一项：  
同样和 max 是一个思想 var min = Math.min.apply(null,array);

(3) Array.prototype.push 可以实现两个数组合并：  
同样push方法没有提供 push 一个数组，但是它提供了 push(param1,param,…paramN)，所以同样也可以通过apply来装换一下这个数组,即:

	//例6：
	var arr1=new Array("1","2","3");
	var arr2=new Array("4","5","6");
	Array.prototype.push.apply(arr1,arr2);

通常在什么情况下,可以使用apply类似Math.min等之类的特殊用法：  
一般在目标函数只需要n个参数列表，而不接收一个数组的形式（[param1[,param2[,…[,paramN]]]]），可以通过apply的方式巧妙地解决这个问题。

(完)











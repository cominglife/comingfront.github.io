---
layout: post
title: javascript高级程序设计 读书笔记二
category: "note"
tags: ["JavaScript"]
---

__第3章、对象基础__

ECMA-262 把对象(object)定义为：属性的无序集合，每个属性存放一个原始值、对象或函数；  
可以把类看作对象的配方，类不仅要定义对象的接口(interface)，还要定义对象的内部工作；  
程序使用类创建对象时，生成的对象叫做类的实例(instance)，由类创建对象实例的过程叫做实例化(instantiation)；  
ECMAScript 并没有正式的类，对象定义实际上是对象自身；  
对象定义存放在一个函数-构造函数中，构造函数不是一种特殊函数，是用于创建对象的常规函数。

3.1.1、面向对象语言的要求：  
封装：把相关的信息(无论数据或方法)存储在对象中的能力；  
聚焦：把一个对象存储在另一个对象内的能力；  
继承：由另一个类(或多个类)得来类的属性和方法的能力；  
多态：编写能以多种方法运行的函数或方法的能力。

3.1.2、对象的构成：由特性(attribute)构成，可以是原始值，也可以是引用值，如果特性存放的是函数，它被看作对象的方法(method)，否则被看作属性(property)；

3.2、对象应用：

3.2.1、声明和实例化：

对象是用关键字 new 后跟要实例化的类的名字创建：

	var oObject = now Object();
	var oStringObject = new String();

如果构造函数无参数，括号则不是必需的。

3.2.2、对象的引用：在 ECMAScript 中不能访问对象的物理表示，只能访问对象的引用，每次创建对象，存储在变量中的都是该对象的引用，而不是对象的本身。

3.2.3、对象废除：

ECMAScript 有无用存储单元收集程序，当再没有对对象的引用时，称该对象被废除(dereference)了；

把对象的所有引用都设置为 null，可以强制性的废除对象：

	var oObject = new Object;
	//do something with the object here
	oObject = null;

如果一个对象有两个或更多引用，则要正确废除该对象必须将其所有的引用都设置为 null。

3.2.4、早绑定和晚绑定：

绑定：即把对象的接口与对象实例结合在一起的方法；  
早绑定：指在实例化对象之前定义它的特性和方法，ECMAScript 不是强类型语言，不支持早绑定；  
晚绑定：指编译器或解释程序在运行前，不知道对象的类型，无需检查对象的类型，只需要检查对象是否支持特性和方法即可，ECMAScript 中的所有变量都采用晚绑定方法，允许执行大量的对象操作，而无任何惩罚。

3.3、对象的类型：在 ECMAScript 中，所有对象并非同等创建的，可以创建并使用的对象有三种

3.3.1、本地对象

本地对象指 ECMA-262 定义的类(引用类型)，它们包括：
Object Function Array String  
Boolean Number Date RegExp  
Error EvalError RangeError ReferenceError  
SyntaxError TypeErrors URIError

1、Array 类

	//创建：
	var aValues = new Array();
	var aValues = new Array(20);//如果预告知道数组中项的个数，可以用参数传递数组的大小
	var aColor = new Array("red","green","blue");
	var aColor = ["red","green","blue"];

数组最多可存放 4294967295 项，应该可满足大多数程序设计需要，如果添加更多项则会发生异常；

Array 对象覆盖了 toString() 和 valueOf() 方法，join() 方法也能实现类似的功能：

	var aColor = ["red","green","blue"];
	alert(aColor.toString());//outputs "red,green,blue"
	alert(aColor.valueOf());//outputs "red,green,blue"
	alert(aColor.join(","));//outputs "red,green,blue"
	alert(aColor.join("--"));//outputs "red--green--blue"

split() 方法能把 String 转换成数组：

	var sColor = "red,green,blue";
	var aColor = sColor.split(",");
	var sColor = "red";
	var aColor = sColor.split(",");
	alert(aColor.toString());//outputs "r,e,d"

concat() 和 slice() 方法，与 String 类具有的方法类似：

	var aColors = ["red","green","blue"];
	var aColor2 = aColors.concat("yellow","purple");
	alert(aColor2.toString());//outputs ""red,green,blue,yellow,purple"
	alert(aColors.toString());//outputs ""red,green,blue"
	var aColor3 = aColor2.slice(1);
	var aColor4 = aColor2.slice(1,4);
	alert(aColor3.toString());//outputs "green,blue,yellow,purple"
	alert(aColor4.toString());//outputs "green,blue,yellow"

push() 和 pop() 方法，用于在 Array 结尾添加或者删除项；

	var stack = new Array;
	stack.push("red");
	stack.push("green");
	stack.push("yellow");
	alert(stack.toString());//outputs "red,green,yellow"
	var vItem = stack.pop();
	alert(vItem);//outputs "yellow"
	alert(stack);//outputs "red,green"

shift() 方法将删除数组中第一个项，unshift() 方法把一个项放在数组的第一个位置；

	var aColors = ["red","green","yellow"];
	var vItem = aColors.shift();
	alert(vItem);//outputs "red"
	alert(aColors.toString);//outputs "green,yellow"
	aColors.unshift("black");
	alert(aColors.toString());//outputs "black,green,yellow"

reverse() 方法用于颠倒数组的顺序，sort() 方法将根据数组项的值按升序排序

	var aColors = ["green","red","blue"];
	aColor.reverse();
	alert(aColors.toString());//outputs "blue,red,green"
	aColor.sort();
	alert(aColors.toString());//outputs "blue,green,red"

splice() 方法是把数据项插入数组的中部，但变体却大有用途：  
删除：声明两个参数可删除第一项的位置和要删除的第二项的个数，如：arr.splice(0,2) 将删除 arr 中的前两项；  
替换而不删除：声明三个参数可把数据插入指定位置，如：arr.splice(2,0,"red","green") 将在位置2处插入"red"和"green"；  
替换并删除：如:arr.splice(2,1,"red","green") 将删除数组中位置 2 处的项，并在位置 2 处插入"red"和"green"。

2、Date 类

创建：`var d = new Date();`

有两种方式设置日期和时间的值：

(1)var d = new Date(0);//声明距离 1970年1月1日凌晨12点的毫秒数  
还有 parse() 和 UTC() 两种方法，都是返回日期值（即毫秒表示），parse() 方法接受字符串为参数，格式由地点特定；UTC() 方法的参数是日期中的年、月、日、小时、分、秒和毫秒，必须声明年和月，其他参数可选；

	var d = new Date(Date.parse("May 25,2004"));
	var d = new Date(Date.UTC(2004,1,5));//这里的 1 表示二月，即第二个月

(2)直接声明 UTC() 方法接受的参数

	var d = new Date(2004,1,5);//除了年和月外，它们不必都出现

Date 类的 valueOf() 方法返回日期的毫秒表示，toString() 方法返回地区特定的字符串；

Date 在的其余方法：

	getTime()：返回日期的毫秒表示
	getTime(milliseconds)：设置日期的毫秒表示
	getFullYear()：返回用四位数表示的日期的年份
	getUTCFullYear()：返回用四位数表示的 UTC 日期的年份
	setFullYear(year)：设置日期的年份，参数必须是四位数的年份值
	setUTCFullYear(year)：设置 UTC 日期的年份，参数必须是四位数的年份值
	getMonth()：返回日期的月份值，由数字 0(1月)到 11(12月)表示
	getUTCMonth()：返回 UTC 日期的月份值，由数字 0(1月)到 11(12月)表示
	setMonth(month)：设置日期的月份为大于等于 0 数字，对于大于 11 的数字开始累计年数
	setUTCMonth(month)：设置 UTC 日期的月份为大于等于 0 数字，对于大于 11 的数字开始累计年数
	getDate()：返回该日期该月中的某天
	getUTCDate()：返回该 UTC 日期该月中的某天
	setDate(date)：设置该日期该月中的某天
	setUTCDate(date)：设置该 UTC 日期该月中的某天
	getDay()：返回该日期为星期几
	getUTCDay()：返回该 UTC 日期为星期几
	setDay(day)：设置该日期为星期几
	setUTCDay(day)：设置该 UTC 日期为星期几
	getHours()：返回日期中的小时值
	getUTCHours()：返回 UTC 日期中的小时值
	setHours(hours)：设置日期中的小时值
	setUTCHours(hours)：设置 UTC 日期中的小时值
	getMinutes()：返回日期中的分钟值
	getUTCMinutes()：返回 UTC 日期中的分钟值
	setMinutes(minutes)：设置日期中的分钟值
	setUTCMinutes(minutes)：设置 UTC 日期中的分钟值
	getSeconds()：返回日期中的秒值
	getUTCSeconds()：返回 UTC 日期中的秒值
	setSeconds(seconds)：设置日期中的秒值
	setUTCSeconds(seconds)：设置 UTC 日期中的秒值
	getMilliseconds()：返回日期中的毫秒值，注意，是当前时间中的毫秒值
	getUTCMilliseconds()：返回 UTC 日期中的毫秒值
	setMilliseconds(milliseconds)：设置日期中的毫秒值
	setUTCMilliseconds(milliseconds)：设置 UTC 日期中的毫秒值

3.3.2、内置对象(built-in object)：

ECMA-262 只定义了两个内置对象，即 Global 各 Math，它们也是本地对象，每个内置对象都是本地对象

Global 对象：特殊对象，实际上不存在，所有函数都是某个对象的方法，如 isNaN()、isFinite()、parseInt()等都是 Global 对象的方法；

encodeURI() 和 encodeURIComponent() 方法用于编码传递给浏览器的 URI(统一资源标识符)，区别是前者不对 URI 中的特殊字符进行编码，如冒号、斜杠，而后者则对所有非标准字符进行编码；

decodeURI() 和 decodeURIComponent() 方法用于解码编码过的 URI；

这些 URI 方法代替了 BOM 的 escape() 和 unescape() 方法，URI 方法更可取，因为它们会对所有 Unicode 符号编码，而 BOM 方法只能对 ASCII 符号正确编码，尽量避免使用 escape() 和 unescape() 方法；

eval() 方法：可能是 ECMAScript 中最强大的方法，接受一个即可执行的 ECMAScript 字符串参数，把参数解释为真正的 ECMAScript 语句，使用时要极度小心，尤其在给它传递用户输入的数据时，恶意用户可能会插入对站点或应用的安全性有危害的值（即代码注入）；

Global 对象的属性：

	//属性：说明
	undefined：Undefined 类型的字面量
	NaN：非数的专用数值
	Infinity：无穷大值的专用数值
	Object：Object 的构造函数
	Array：Array 的构造函数
	Function：Function 的构造函数
	Boolean：Boolean 的构造函数
	String：String 的构造函数
	Number：Number 的构造函数
	Date：Date 的构造函数
	RegExp：RegExp 的构造函数
	Error：Error 的构造函数
	EvalError：EvalError 的构造函数
	RangeError：RangeError 的构造函数
	ReferenceError：ReferenceError 的构造函数
	SyntaxError：SyntaxError 的构造函数
	TypeError：TypeError 的构造函数
	URIError：URIError 的构造函数

Math 对象：

	//属性：说明
	E：值 e，自然对数的底
	LN10：10 的自然对数
	LN2：2 的自然对数
	LOG2E：以 2 为底 E 的对数
	LOG10E：以 10 为底 E 的对数
	PI：值π
	SQRT1_2：1/2 的平方根
	SQRT2：2 的平方根

min() 和 max() 方法用于判断一组数中最大和最小值，可接受任意多个参数

	var iMax = Math.max(3,54,32,16);
	alert(iMax);//outputs "54"

abs() 方法返回数字的绝对值：var iNegOne = Math.abs(-1);

ceil()、floor()、round() 方法用于把小数舍入成整数，ceil() 表示向上舍入函数，floor() 表示向下舍入函数，round() 表示标准的舍入函数；

	alert(Math.ceil(25.2));//outputs "26"
	alert(Math.floor(25.6));//outputs "25"
	alert(Math.round(25.5));//outputs "26"，四舍五入

exp() 方法用于把 Math.E 升到指定的幂；log() 方法用于返回特定数字的自然对数；pow() 方法用于把指定的数字升到指定的幂；sqrt() 方法用于返回指定数字的平方根

Math 对象的三角函数方法：

	//方法：说明
	acos(x)：返回 x 的反余弦值
	asin(x)：返回 x 的反正弦值
	atan(x)：返回 x 的反正切值
	atan2(y,x)：返回 y/x 的反余弦值
	cos(x)：返回 x 的余弦值
	sin(x)：返回 x 的正弦值
	tan(x)：返回 x 的正切值

random() 方法返回一个 0 到 1 之间的随机数，不包括 0 和 1

	var iNum = Math.floor(Math.random() * 10 + 1); //返回一个 1 到 10 之间的数
	var iNum = Math.floor(Math.random() * 9 + 2); //返回一个 2 到 10 之间的数
	function selectForm(iFirstValue,iLastValue) {
		var iChoices = iLastValue - iFirstValue + 1;
		return Math.floor(Math.random() * iChoices + iFirstValue);
	}
	var iNum = selectForm(2,10); //返回一个 2 到 10 之间的数

3.3.3、宿主对象：所有非本地对象都是宿主对象（host object），即由 ECMAScript 实现的宿主环境提供的对象（所有 BOM 和 DOM 对象都是宿主对象）

3.4、作用域：即某些变量的适用范围；

3.4.1、公用作用域、私有作用域、受保护作用域

公用作用域中的对象属性可以从对象外部访问，即开发者创建对象的实例后就可使用它的公用属性；  
私有作用域中的属性只能在对象内部访问，即对外部来说这些属性并不存在，意味着如果类定义了私有属性和方法，则它的子类也不能访问；  
受保护作用域用于定义私有的属性和方法，只是这些属性和方法还能被其子类访问；  
ECMAScript 中只存在一种作用域：公用作用域；  
开发者们制定了规约，在属性名前后加下划线作为私有的，或单用前下划线表示私有，这些下划线并不改变这些属性是公用属性的事实，只是为了告诉其他开发者应该把该属性看作私有的：

	obj._color_ = "red";
	obj._color = "red";

3.4.2、静态作用域并非静态的

静态作用域定义的属性和方法任何时候都能从同一个位置访问，如 Java 中的 java.net.URLEncoder 类，它的函数 encode() 即静态方法；
ECMAScript 并没有静态作用域，但可以给构造函数提供属性和方法，构造函数只是函数，函数是对象，对象可以有属性和方法；

	function sayHi() {
		alert("hi");
	}
	sayHi.alternate = function() {
		alert("holo")
	}

这里方法 alternate() 是函数 sayHi 的方法，可像调用常规函数一样调用 sayHi() 输出"hi"，也可以调用 sayHi.alternate() 输出"hola"，即使如此，alternate() 也是 sayHi() 公用作用域中的方法，而不是静态方法。

3.4.3、关键字 this：关键字 this 总是指向调用该方法的对象

为什么使用 this：因为在实例化对象时，不能确定开发者会使用什么样的变量名，使用 this 即可在任意多个地方重用同一个函数；  
引用对象的属性时，必须使用 this 关键字，否则 ECMAScript 会把它看作局部变量或全局变量，但是会找不到，该函数将在警告中显示"null"。

3.5、定义类或对象：使用预定义对象的能力只是面向对象语言的能力的一部分，它真正强大之处在于能够创建自己专用的类和对象；

3.5.1、工厂方式：能创建并返回特定类型的对象的工厂函数（factory function）；

	function showColor() {
		alert(this.color);
	}
	function createCar(sColor,iDoors,iMpg) {
		var oTempCar = new Object;
		oTempCar.color = sColor;
		oTempCar.doors = iDoors;
		oTempCar.mpg = iMpg;
		oTempCar.showColor = showColor;
		return oTempCar;
	}
	var oCar1 = createCar("red",4,23);
	oCar1.showColor();//outputs "red"

3.5.2、构造函数方式：和工厂方式类似，但在构造函数内部无创建对象，而是使用 this 关键字；

	function showColor() {
		alert(this.color);
	}
	function Car(sColor,iDoors,iMpg) {
		this.color = sColor;
		this.doors = iDoors;
		this.mpg = iMpg;
		this.showColor = showColor;
	}
	var oCar1 = new Car("red",4,23);
	oCar1.showColor();//outputs "red"

构造函数与工厂方式都可以用外部函数重写构造函数，这么做语义上无任何意义

3.5.3、原型方式：利用对象的 prototype 属性，可把它看成创建新对象所依赖的原型；

	function Car() {}
	Car.prototype.coler = "red";
	Car.prototype.doors = 4;
	Car.prototype.mpg = 23;
	Car.prototype.showColor = function() {
		alert(this.color);
	}
	var oCar1 = new Car("red",4,23);
	oCar1.showColor();//outputs "red"

用 instanceof 运算符检查给定变量指向的对象的类型：

	alert(oCar1 instanceof Car);//outputs "true"

该方法在调用 new Car() 时，原型的所有属性都被立即赋予要创建的对象，意味着所有 Car 实例存放的都是指向 showColor() 函数的指针，从语义上讲所有属性看起来都属于一个对象，解决了前两种方式存在的问题；  
该方法的问题：构造函数没有参数，不能通过给构造函数传参初始化属性，意味着必须在对象创建后才能改变属性的默认值，另外真正的问题出现在属性指向的是对象，而不是函数时，函数共享不会造成问题，但对象却很少被多个实例共享的。

3.5.4、混合的构造函数/原型方式：即用构造函数定义对象的所有非函数属性，用原型方式定义对象的函数属性

	function Car(sColor,iDoors,iMpg) {
		this.color = sColor;
		this.doors = iBoors;
		this.mpg = iMpg;
		this.drivers = new Array("Mike","Sue");
	}
	Car.prototype.showColor = function() {
		alert(this.color);
	}
	var oCar1 = new Car("red",4,23);
	var oCar2 = new Car("blue",3,25);
	oCar1.driver.push("Matt");
	alert(oCar1.drivers);//outputs "Mike,Sue,Matt"
	alert(oCar2.drivers);//outputs "Mike,Sue"

这种方法是 ECMAScript 采用的主要方法，它具有其他方式的特性，却没有它们的副作用。

3.5.5、动态原型方法：基本想法与混合方式相同，唯一区别是赋予对象方法的位置：

	function Car(sColor,iDoors,iMpg) {
		this.color = sColor;
		this.doors = iDoors;
		this.mpg = iMpg;
		this.drivers = new Array("Mike","Sue");
		if(typeof Car._initialized == "undefined") {
			car.prototype.showColor = function() {
				alert(this.color);
			}
			Car._initialized = true;
		}
	}

该方法使用标志（_initialized）来判断是否已给原型赋予了任何方法，该方法只创建并赋值一次，这段代码看起来更便其他语言中的类定义了。

3.5.6、混合工厂方式：创建假构造函数，只返回另一种对象的新实例，与工厂函数非常相似；

	function Car() {
		var oTempCar = new Object;
		oTempCar.color = "red";
		oTempCar.doors = 4;
		oTempCar.mpg = 23;
		oTempCar.showColor = funtiong() {
			alert(this.color);
		}
		return oTempCar;
	}
	var oCar = new Car();

除非万不得已，还是避免使用这种方式

3.5.7、采用哪种方式：目前使用最广泛的是混合的构造函数/原型方式，此外动态原型方法也很流行，可采用这两种方式中的任何一种。

3.5.8、实例

字符串连接用加号（+）比用 Array 对象存储字符串，然后用 join() 方法创建最后的字符串消耗更多性能，可用类打包功能：

	function StringBuffer() {
		this._strings_ = new Array;
	}
	StringBuffer.prototype.append = function(str) {
		this._strings_.push(str);
	}
	StringBuffer.prototype.toString = function() {
		return this._strings_.join("");
	}

可用以下代码测试 StringBuffer 对象和传统的字符串连接方法的性能：

	var d1 = new Date();
	var str = "";
	for(var i=0; i < 10000; i++) {
		str += "text";
	}
	var d2 = new Date();
	document.write("Concatenation with plus: " + (d2.getTime() - d1.getTime()) + "milliseconds");

	var oBuffer = new StringBuffer();
	d1 = new Date();
	for(var i=0; i < 10000; i++) {
		oBuffer.append("text");
	}
	var sResult = oBuffer.toString();
	d2 = new Date();
	document.write("<br />Concatenation with Array: " + (d2.getTime() - d1.getTime()) + "milliseconds");

结果应该说明使用 StringBuffer 类比使用加号节省了 50-60% 的时间

这里笔者测试后发现只有 ie6 与 ie7 下如书中所说，但其他更高级的浏览器则相反，用传统加更快，可能是新的浏览器改变了算法。测试链接：http://www.cominglife.net/demo_1.html

3.6、修改对象：每个本地对象也有个用法与构造函数完全相同的 prototype 属性；

3.6.1、创建新方法

	Array.prototype.indexOf = function(vItem) {
		for(var i=0; i < this.length; i++) {
			if(vItem == this[i]){
				return i;
			}
		}
		return -1;
	};
	var aColors = new Array("red","green","yellow");
	alert(aColors.indexOf("green"));//outputs "1"

如果想给 ECMAScript 中的每个本地对象添加新方法，必须在 Object 对象的 prototype 属性上定义它：

	Object.prototype.showValue = function() {
		alert(this.valueOf());
	};

3.6.2、重定义已有方法

	Function.prototype.originalToString = Function.prototype.toString;

	Function.prototype.toString = function() {
		if(this.originalToString().length > 100) {
			return "Function too long to display.";
		}else{
			retuen this.ogiginalToString();
		}
	}

3.6.3、极晚绑定：从技术上来说，不存在极晚绑定，本书采用该术语描述 ECMAScript 中的一种现象，即能够在对象实例化后再定义它的方法

	var o = new Object;
	Object.prototype.sayHi = function() {
		alert("hi");
	};
	o.sayHi();

不建议使用极晚绑定方法，因为很难对其跟踪和记录。

__第4章、继承__

真正面向对象语言必须支持继承机制，即一个类能够重用（继承）另一个类的方法和属性

4.1、继承机制实例

形状（Shape）是椭圆开（Ellipse）和多边形（Polygon）的基类（base class），圆形（Circle）继承了椭圆形，圆形是椭圆开的子类（subclass），椭圆开是圆形的超类（superclass）。三角形（Triangle）、矩形（Rectangle）和五边形（Pentagon）都是多边形的子类，多边形是它们的超类，正方形（Square）继承了矩形

4.2、继承机制的实现

所有开发者定义的类都可作为基类；

出于安全原因，本地类和宿主类不能作为基类，防止公用访问编译过的浏览器级的代码，这些代码可被用于恶意攻击；

ECMAScript 没有严格地定义抽象类，但会创建一些不允许使用的类，称为抽象类；

创建的子类继承超类的所有属性和方法，包括构造函数及方法的实现，所有属性和方法都是公用的，子类可直接访问这些方法，还可添加超类中没有的属性和方法，可也覆盖类中的属性和方法；

4.2.1、继承的方式

(1)对象冒充（object masquerading）：

所有的新属性和新方法都必须在删除了新方法的代码后定义，否则可能会覆盖超类的相关属性和方法；

	function ClassA(sColor) {
		this.color = sColor;
		this.sayColor = function() {
			alert(this.color);
		};
	}

	function ClassB(sColor,sName) {
		this.newMethod = ClassA;
		this.newMethod(sColor);
		delete this.newMethod;
		this.name = sName;
		this.sayName = functiong() {
			alert(this.name);
		};
	}

	var objA = new ClassA("red");
	var objB = new ClassB("blue","Nicholas");
	objA.sayColor();//outputs "red"
	objB.sayColor();//outputs "blue"
	objB.sayName();//outputs "Nicholas"

对象冒充可以支持多重继承：

	function ClassZ() {
		this.newMethod = classX;
		this.newMethod();
		delete this.newMethod;

		this.newMethod = classY;
		this.newMethod();
		delete this.newMethod;
	}

如果 ClassX 和 ClassY 具有同名的属性或方法，ClassY 具有高优先级，因为它从后面的类继承。

(2) call() 方法：与经典的对象冒充方法最相似，第一个参数用作 this 的对象，其他参数都直接传递给函数自身；

	function sayColor(sPrefix,sSuffix) {
		alert(sPrefix + this.color + sSuffix);
	}

	var obj = new Object();
	obj.color = "red";
	sayColor.call(obj,"The color is "," a nice color.");//outputs "The color is red, a nice color."

	function ClassB(sColor,sName) {
		ClassA.call(this,sColor);
		this.neme = sName;
		this.sayName = function() {
			alert(this.name);
		};
	}

(3) apply() 方法：

	function sayColor(sPrefix,sSuffix) {
		alert(sPrefix + this.color + sSuffix);
	}

	var obj = new Object();
	obj.color = "red";
	sayColor.apply(obj,new Array("The color is "," a nice color."));
	//outputs "The color is red, a nice color."

	function ClassB(sColor,sName) {
		ClassA.apply(this,new Array(sColor));
		this.neme = sName;
		this.sayName = function() {
			alert(this.name);
		};
	}

可以把 ClassB 的整个 arguments 对象作为第二个参数传递给 apply() 方法：

	function ClassB(sColor,sName) {
		ClassA.apply(this,arguments);
		this.neme = sName;
		this.sayName = function() {
			alert(this.name);
		};
	}

原型链：

	function ClassA() {}
	ClassA.prototype.color = "red";
	ClassA.prototype.sayColor = function() {
		alert(this.color);
	};
	function ClassB() {}
	ClassB.prototype = new ClassA();
	ClassB.prototype.sayName = function() {
		alert(this.name);
	}

注意：调用 ClassA 的构造函数时，没有给它传递参数，这在原型链中是标准做法，要确保构造函数没有任何参数；  
与对象冒充相似，子类的所有属性和方法都必须出现在 prototype 属性被赋值后，因为在它之前赋值的所有方法都会被删除，因为 prototype 属性被替换成了新对象，添加了新的方法的原始对象将被销毁；  
可通过下面的例子来测试上面这段代码：

	var objA = new ClassA();
	var objB = new ClassB();
	objA.color = "red";
	objB.color = "blue";
	objB.name = "Nicholas";
	objA.sayColor();//outputs "red"
	objB.sayColor();//outputs "blue"
	objB.sayName();//outputs "Nicholas"

此外在原型链中，instanceof 运算符的运行方式也很独特：

	var objB = new ClassB();
	alert(objB instanceof ClassA);//outputs "true"
	alert(objB instanceof ClassB);//outputs "true"

原型链的弊端是不支持多重继承，记住，原型链会用另一类的对象重写类的 prototype 属性。

(4)混合方式

	function ClassA(sColor) {
		this.color = sColor;
	}
	ClassA.prototype.sayColor = functiong() {
		alert(this.color);
	};
	functiong ClassB(sColor,sName) {
		classA.call(this,sColor);
		this.name = sName;
	}
	ClassB.prototype = new ClassA();
	ClassB.prototype.sayName = functiong() {
		alert(this.name);
	};

这种混合方式使用了原型链，所以 instanceof 运算符仍能正确运动。

4.2.2、一个更实际的例子：Polygon(多边形)、Triangle(三角形)、Rectangle(矩形)；

Polygon 的属性：边数：sides；计算面积方法：getArea()；

	function Polygon(iSides) {
		this.sides = iSides;
	}
	Polygon.prototype.getArea = function() {
		return 0;
	};

Triangle 的属性：底长度：base；高度：height；面积公式：1/2 * 底 * 高；

	function Triangle(iBase,iHeight) {
		Polygon.call(this,3);
		this.base = iBase;
		this.height = iHeight;
	}
	Triangle.prototype = new Polygon();
	Triangle.prototype.getArea = function() {
		return 0.5 * this.base * this.height;
	};

Rectangle 类似于 Triangle：

	function Rectangle(iLength,iWidth) {
		Polygon.call(this,3);
		this.length = iLength;
		this.width = iWidth;
	}
	Rectangle.prototype = new Polygon();
	Rectangle.prototype.getArea = function() {
		return this.length * this.width;
	};

测试代码：

	var triangle = new Triangle(12,4);
	var rectangle = new Rectangle(22,10);

	alert(triangle.sides);//outputs "3"
	alert(triangle.getArea());//outputs "24"

	alert(rectangle.sides);//outputs "4"
	alert(rectangle.getArea());//outputs "220"

注意：继承机制不能使用动态原型方法

4.3、其它继承方式

4.3.1、zlnherit 库

4.3.2、xbObjects 工具

__第五章、浏览器中的 JavaScript__

5.1、HTML 中的 JavaScript

5.1.1、<script/> 标签：language 特性声明要使用的脚本语言，src 特性是可选的，声明要加入页面的外部 JavaScript 文件；

5.1.2、外部文件格式：外部 JavaScript 是只包含 JavaScript 代码的纯文本文件；

5.1.3、内嵌代码和外部文件：大量的 JavaScript 代码不应该内嵌在 HTML 中，原因：安全性、代码维护、缓存；

5.1.4、标签放置：JavaScript 是从上到下载入的；

5.1.5、隐藏还是不隐藏

对于旧浏览器隐藏 JavaScript 代码的格式：

	<script language="JavaScript"><!-- hide from loder browsers
	function sayHi() {
	alert("Hi");
	}
	//-->
	</script>

5.1.6、<noscript/> 标签

	<noscript><p>Your browser doesn't support JavaScript.</p></noscrip>

5.1.7、XHTML 中的改变

用 type 特性声明内嵌代码或要加入的外部文件的 mime 类型，JavaScript 的 mime 类型是“text/javascript”；  
使用 CDATA 段，用于声明不应被解析为标签的文本，为避免 CDATA 的问题，最好还是用外部文件引用 JavaScript 代码；

	<script type="text/javascript">
	//<![CDATA[
	JavaScript code
	......
	//]]>
	</script>

5.2、SVG 中的 JavaScript：这块不兼容低极浏览器，不考虑浏览器兼容性的话 html5 会更好，所以跳过

5.3、BOM（浏览器对象模型）

基本的 BOM 体系结构（图1）


5.3.1、window 对象：表示整个浏览器窗口；

frames（框架）集合：

	<frameset rows="100,*">
		<frame src="frame.html" name="topFrame" />
		<frameset cols="50%,50%">
			<frame src="anotherframe.html" name="leftFrame" />
			<frame src="yetanotherframe.html" name="rightFrame">
		</frameset>
	</frameset>

这里可以用 window.frames[0] 或 window.frames["topFrame"] 引用框架，也可以用 top 对象代替 window 对象，如：top.frames[0]，也可以直接用框架名，如：window.leftFrame；  
top 对象指向最项层（最外层）框架，即浏览器窗口自身；  
由于 window 对象是整个 BOM 的中心，可省略掉；  
parent 对象指向当前框架的父级框架；  
self 对象总是等于 window，如果页面上没有框架，window 和 self 就等于 top，frames 集合长度为 0；  
还可连锁引用 window，如：parent.parent.frames["topFrame"]。

窗口操作

moveBy(dx,dy)：把浏览器相对当前位置水平移动 dx 个像素，垂直移动 dy 个像素，dx 为负时向左移，dy 为负时向上移；  
moveTo(x,y)：移动浏览器窗口，使它的左上角位于用户屏幕的（x,y）处，用负数会把窗口移出屏幕的可视区域；  
resizeBy(dw,dh)：相对于浏览器窗口的当前大小，把它的宽度调整 dw 个像素，高度调整 dy 个像素，负数为缩小；  
resizeTo(w,h)：把窗口宽度调整为 w，高度调整为 h，不能使用负数；

IE 提供了 window.screenLeft 和 window.screenTop 对象来判断窗口的位置，未提供判断窗口大小的方法，用 document.body.offsetWidth 和 document.body.offsetHeight 属性可以获取视口的大小；  
Mozilla 提供 window.screenX 和 window.screenY 属性判断窗口的位置，提供 window.innerWidth 和 window.innerHeight 属性来判断视口大小，window.outerWidth 和 window.outerHeight 属性判断浏览器窗口自身大小；

导航和打开新窗口





(未完，待续)











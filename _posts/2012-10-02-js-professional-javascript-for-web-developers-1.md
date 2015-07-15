---
layout: post
title: [javascript高级程序设计] 读书笔记
category: "note"
tags: ["JavaScript"]
---

__前言：__

[javascript高级程序设计] 这本书对于做前端开发工作的朋友来说一定不会陌生，在业界这是一本很著名的书。其具体介绍我就不多说了，搜索引擎一下就有一大堆。对于好书个人认为看一次是远远不够的，每多看一次都会有新的收获。所以把我之前的看书笔记列出来，用于以后复习重温。

__第1章、JavaScript是什么：__

1.1、历史简述：ECMAScript(标签定义) -> JavaScript；

1.2、JavaScript实现：一个完成的JavaScript由以下3部分组成：核心(ECMAScript)、文档对象模型(DOM)、浏览器对象模型(BOM)；

1.2.1、ECMAScript(Javascript的核心)：  
ECMAScript描述了以下内容：语法、类型、语句、关键字、保留字、运算符、对象；

1.2.2、DOM：  
DOM(文档对象模型)是HTML与XML的应用程序接口(API)，描述了处理网页内容的方法和接口；  
(1)DOM视图：描述跟踪文档的各种视图(即css样式化之前与之后的文档)的接口；  
(2)DOM事件：描述事件的接口；  
(3)DOM样式：描述处理基于css样式的接口；  
(4)DOM遍历和范围：描述遍历和操作文档树的接口；  
等等......

1.2.3、BOM：  
BOM(浏览器对象模型)可以对浏览器窗口进行访问和操作，描述了与浏览器进行交互的方法与接口；  
(1)弹出新的浏览器窗口；  
(2)移动、关闭浏览器窗口以及调整窗口大小；  
(3)提供Web浏览器详细信息的导航对象；  
(4)提供装载到浏览器中页面的详细信息的定位对象；  
(5)提供用户屏幕分辨率详细信息的屏幕对象；  
(6)对cookie的支持；  
(7)IE扩展了BOM，加入了ActiveXObject类，可通过JavaScript实例化ActiveX对象；

__第2章、ECMAScript基础：__

2.1、语法

ECMAScript的基础概念如下：  
(1)区分大小写；  
(2)变量是弱类型的：定义变量时只用 var 运算符，可将它初始化为任意的值；  
(3)每行结尾的分号可有可无；  
(4)注释与Java、C、PHP语言的注释相同：单行(//)、多行(/* ... */)；  
(5)括号表明代码块；

2.2、变量

遵守以下两条规则：  
(1)第一个字母必须是字母、下划线或美元符号($)；  
(2)余下的字符可以是下划线、美元符号或任何字母或数字字符；

匈牙利类型标记法：  
类型｜前缀｜示例  
数组｜a｜aValues  
布尔型｜b｜bFound  
浮点型(数字)｜f｜fValue  
函数｜fn｜fnMethod  
整型(数字)｜i｜iValue  
对象｜o｜oType  
正则表达式｜re｜rePattren  
字符串｜s｜sValue  
变型(可以是任何类型)｜v｜vValue

注意：ECMAScript一个有趣的方面，也是与大多数程序设计的主要区别，是在使用变量之前不必声明，其解释程序遇到未声明变量时会将其作为全局变量，这是便利和是危险，最好总是声明所有变量。

2.3、关键字

2.4、保留字

关键字与保留字都不能作为变量名或函数名

2.5、原始值和引用值：

在ECMAScript中，变量可存放两种类型的值，即原始值与引用值：  
(1)原始值(primitive value)是存储在栈(stack)中的简单数据段，即它们的值直接存储在变量访问的位置；  
(2)引用值(reference value)是存储在堆(heap)中的对象，即存储在变量处的值是一个指针(point)，指向存储对象的内存处。

注意：在许多语言中，字符串都是被看作引用类型，而非原始类型，因为字符串的长度是可变的，ECMAScript打破了这一传统。

2.6、原始类型

ECMAScript有5种原始类型(prmitive type)：Undefined、Null、Boolean、Number、String；  
ECMAScript提供了 typeof 运算符来判断一个值是否在某种类型的范围内，可用这个运算符判断一个值是否表示一种原始类型，如果它是原始类型，还可以判断它表示哪种原始类型。

2.6.1、typeof 运算符

typeof 运算符有一个参数，即要检查的变量或值，如：

	var sTemp = "test string";
	alert(typeof sTemp);//outputs "string"
	alert(typeof 95);//outputs "number"

对变量或值调用 typeof 运算符返回下列值之一：  
"undefined"，如果变量是 Undefined 型的；  
"boolean"，如果变量是 Boolean 型的；  
"number"，如果变量是 Number 型的；  
"string"，如果变量是 String 型的；  
"object"，如果变量是一种引用类型或 Null 型的。

2.6.2、Undefined 类型

Undefined 类型只有一个值：undefined，当声明的变量未初始化时，该变量默认值为 undefined；  
值 undefined 并不同于未定义的值，但 typeof 运算符并不真正区分这两种值；  
typeof 可用于未声明的变量，但其它运算符只能用于已声明的变量上，不然会出错；  
当函数无明确返回值时，返回的值也是 undefined；

2.6.3、Null 类型：

另一种只有一个值的类型是 Null，它只有一个专用值 null，即它的字面量；  
值 undefined 是坐值 null 派生来的，因此它们是相等的：`alert(null == undefined);//outputs "true"`；  
但它们的含义不同，undefined 是声明了变量但未对其初始化时赋予该变量的值，null 则用于表示尚未存在的对象，如果函数或方法要返回的是对象，那么找不到该对象时，返回的通常是 null。

2.6.4、Boolean 类型：

Boolean 类型有两个值`true`和`false`(即两个 Boolean 字面量)，即使`false`不等于 0，0 也可以在必要时被转换成`false`，这样在 Boolean 语句中使用两者都是安全的

2.6.5、Number 类型：

既可以表示 32 位的整数，还可以表示 64 位的浮点数，直接输入的任何数字都被看作 Number 型的字面量；  
八进制字面量的首数字必须是 0，其后的数字可以是任何八进制数字( 0 - 7 )，如：

	var iNum = 070;//070 is equal to 56 in decimal

十六进制字面量的首数字必须是 0，其后接字母 x，然后是任意十六进制数字( 0 - 9 和 A 到 F )，这些字母可大写也可小写，如：

	var iNum = 0x1f;//ox1f if equal to 31 in decimal
	var iNum2 = 0xAB;//oxAB if equal to 171 in decimal

尽管所有整数都可以表示为八进制或十六进制的字面量，但所有数学运算返回的都是十进制结果；  
要定义浮点值，必须包括小数点和小数点后的一位数字(如：用 1.0 而不是 1 )，浮点字面量用它进行计算前，真正存储的是字符串；  
科学计数法：如：var fNum = 3.125e7(表示 3.1257 乘以 10 的 7 次方)，又如：3-e17(这里 10 被升到 -17 次幂)；  
也可用 64 位 IEEE 754 形式存储浮点数，这意味着十进制值最多可有17个十进制位，超过将被截去，从而造成数学误差。

注意：几个特殊值也被定义为 Number 类型：  
(1)`Number.MAX_VALUE`和`Number.NIN_VALUE`，所有数都必须在这两个值之间，但计算的结果可以不落在这两个数之间；  
(2)当计数值大于`Number.MAX_VALUE`时，它被赋予值`Number.POSITIVE_INFINITY`，即不再有数字值，小于`Number.MIN_VALUE`的计算也会赋予值`Number.NEGATIVE_INFINITY`，如果返回的是无穷大值，那么生成的结果不能再用于其他计算，事实上有专门的值表示无穷大，即`Infinity`，`Number.POSITIVE_INFINITY`的值为`Infinity`，`Number.NEGATIVE_INFINITY`的值为`-Infinity`，由于无穷大可正也可负，可用一个方法判断一个数是否有穷的：`ifFinit()`，以确保该数不是无穷大(如：`if(ifFinit(iResult) alert"Number if finite";`)；  
(3)`NaN`表示非数(Not a Number)，这种情况一般发生在类型(String、Boolean 等)转换失败，`NaN`也不能用于计算，另外它与自身是不相等的(如：`alert(NaN == NaN);//outputs "false"`)，出于这种情况不推荐使用`NaN`值本身，函数 `isNaN()`会做得相当好(如：`alert(isNaN("123"));//outputs "false"`)。

2.6.6、String 类型

唯一没有固定大小的原始类型，可以用字符串存储 0 或更多的 Unicode 字符，由16位整数表示，字符串中的最后一个字符位置一定是字符串的长度减 1，字符串字面量是由双引号(")或单引号(')声明的(Java是用双引号声明字符串，用单引号声明字符，ECMAScript 没有字符类型)。

String 类型还包括几种字符字面量：  
字面量　：　含义  
\n　：　换行  
\t　：　制表符  
\b　：　空格  
\r　：　回车  
\f　：　换页符  
\\　：　反斜杠  
\'　：　单引号  
\"　：　双引号  
\0nnn　：　八进制代码 nnn (n 是 0 - 7 中的一个八进制数字)表示的字符  
\xnn　：　十六进制代码 nn (n 是 0 - f 中的一个十六进制数字)表示的字符  
\unnnn　：　十六进制代码 nnnn (n 是 0 - f 中的一个十六进制数字)表示的 Unicode 字符

2.7、转换；

ECMAScript 的 Boolean 值、数字和字符串的原始值都是伪对象，即它们都具有属性和方法，如：

	var sColor = "ComingLife";
	alrt(sColor.length);//outputs "10";

Boolean 型的 toString() 方法只输出 "true" 或 "false"；

Number 类型的 toString() 方法有默认模式与基模式：

(1)默认模式中无论最初采用什么表示法声明数字，其方法返回的都是十进制数字：

	var fNum = 10.0;alert(fNum.toString());//outputs "10"

(2)基模式可用不同的基输出数字，基只是要转换成的基数的另一种叫法而已，它是 toString() 方法的参数：

	var iNum = 10;
	alert(iNum.toString(2));//outputs "1010"
	alert(iNum.toString(8));//outputs "12"
	alert(iNum.toString(16));//outputs "A"

(3)HTML 采用十六进制数标示每种颜色，在 HTML 中处理数字时这种功能非常有用，对数字调用`toString(10)`与调用`toString()`相同，返回的都是该数字的十进制形式；

2.7.2、转换成数字；

parseInt() 方法：先检查位置 0 处字符，如不是有效数字将返回 NaN，但如果是，则将查看 1 处字符，持续到发现非数字为止，把非数字之前的字符串转换成数字并返回，以下是注意点：  
1、小数点是无效字符；  
2、有基模式，如果十进制数包含前导 0，则要采用基数 10，才不会意外得到八进制值；

	var iNum1 = parseInt("123.5Coming");//return 123
	var iNum2 = parseInt("0xA");//return 10
	var iNum2 = parseInt("010");//return 8
	var iNum3 = parseInt(".123");//return NaN
	var iNum4 = parseInet("af",16);//return 175

parseFloat() 方法：与parseInt() 方法的处理方式相似，以下是注意点：  
(1)第一个出现的小数点是有效字符，第二个小数点将被看作无效；  
(2)字符串必须以十进制形式表示浮点数，没有基模式；

	var fNum1 = parstFloat(".23.4Coming");//return 0.23
	var fNum2 = parstFloat("0xa");//return NaN
	var fNum3 = parstFloat("0908");//return 908

2.7.3、强制类型转换；

Boolean(value)：把值转换成 Boolean 型；

	var b1 = Boolean("");//false: empty string
	var b2 = Boolean("hi");//true: non-empty string
	var b3 = Boolean(100);//true: non-zero number
	var b4 = Boolean(null);//false: null
	var b5 = Boolean(0);//false: zero
	var b6 = Boolean(new Object());//true: object

Number(value)：把值转换成数字(可以是整数或浮点数)，与 parseInt 和 parseFloat() 处理方式相似，只是转换的是整个值，如果字符串能被完整地转换，它将判断是调用 parseInt() 还是 parseFloat()：

	Number(false)//return 0
	Number(true)//return 1
	Number(undefined)//return NaN
	Number(null)//return 0
	Number("5.6.7")//return NaN
	Number(new Object())//return NaN
	Number("100")//return 100

String(value)：把值转换成字符串，另外还有 toString() 方法，区别是强制转换对 null 或 undefined 值强制类型转换可生成字符串而不会引发错误：

	var s1 = String(null);//return "null"
	var oNull = null;
	var s2 = oNull.toString();//won't work,couses an error

在处理 ECMAScript 这样的弱类型语言时，强制类型转换非常有用，但应确保使用值的正确。

2.8、引用类型；

引用类型通常叫作类(calss)，即遇到引用值时，所处理的就是对象，在传统意义上，ECMAScript 并不真正具有类，它定义了 "对象定义"，逻辑上等价于其他语言中的类；  
对象由 new 运算符加上要实例化的类的名字创建，如果没有参数可省略括号，但为了避免混乱，尽量使用括号，如：

	var o = new Object();//var o = new Object;

2.8.1、object类：

与 Java 中的 java.lang.object 相似，所有类都由这个类继承而来，Object 类中所有属性和方法都会在其他类中

属性：  
(1)Constructor：对创建对象的函数的引用(指针)，对于 Object 类，该指针指向原始的 object() 函数；  
(2)prototype：对该对象的对象原型的引用，对于所有类它默认返回 object 对象的一个实例；

方法：  
(1)HasOwnPrototype(property)：判断对象是否有某个特定的属性(如：o.hasOwnPrototype("name");)；  
(2)IsPrototypeOf(object)：判断该对象是否为另一个对象的原型；  
(3)PropertyIsEnumerable(property)：判断给定的属性是否可用 for ... in 语句进行枚举；  
(4)toString()：返回对象的原始字符串表示，不同的 ECMAScript 实现具有不同的值；  
(5)ValueOf()：返回最适合该对象的原始值，对于许多类该方法返回的值都与 toString() 的返回值相同。

2.8.2、Boolean 类；

Boolean 类是 Boolean 原始类型的引用类型，要创建只需传送 Boolean 值作为参数：

	var oBooleanObject = new Boolean(true);

Boolean 对象将覆盖 object 类的 valueOf() 方法，返回原始值，即 true 或 false；  
toString() 方法也会被覆盖，返回字符串 "true" 或 "false"；
在 ECMAScript 中很少使用 Boolean 对象，也不易理解，所以最好还是使用 Boolena 原始值，如：

	var oFalseObject = new Boolean(false);
	var bResult = oFalseObject && true;//outputs true

在这段代码中，用 false 值创建 Boolean 对象，然后与原始值 true 进行 AND 操作，在 Boolean 运算中，false 和 true 进行 AND 操作的结果是 false。不过在这里计算的是 oFalseObject，而不是它的值 false。在 Boolean 表达式中，所有对象都会被自动转换为 true，所以 oFalseObject 的值是 true。

2.8.3、Number 类：Number 原始类型的引用类型；

创建：`var oNumberObject = new Number(55);`；
所有特殊值都是 Number 类的静态属性，如：`Number.MAX_VALUE`；
得到数字对象的 Number 原始值：`var iNumber = oNumberObject.valueOf();`；
当然 Number 类也有`toString()`方法；
`toFixed()`方法返回的是具有指定倍数小数的数字的字符串表示，其参数能表示具有0-20位小数的数字，超出会引发错误；

	var oNumberObject = new Number(99);
	alert(oNumberObject.toFixed(2));//outputs "99.00"

`toExponential()`方法返回用科学计数法表示的数字的字符串形式，其参数表示指定要输出的小数的位数；

	var oNumberObject = new Number(99);
	alert(oNumberObject.toExponential(1));//outputs "9.9e+1"

`toPrecision()`方法根据最有意义的形式来返回数字的预定义形式或指数形式，其参加表示数的数字总数(不包括指数)；

	var oNumberObject = new Number(99);
	alert(oNumberObject.toPrecision(1));//outputs "1e+2"
	alert(oNumberObject.toPrecision(２));//outputs "99"
	alert(oNumberObject.toPrecision(3));//outputs "99.0"

以上3种方法都会进行舍入操作，以便用正确的小数位数表示一个数，与 Boolean 对象相似，Number 对象也很重要但应该少用这种对象，以避免发生潜在问题，只要可能都应该使用数字的原始表示法。

2.8.4、String 类：String 原始类型的引用类型

创建：`var oStringObject = new String("hello world");`

String 对象的 valueOf() 和 toString() 方法都会返回 String 型的原始值

	alert(oStringObject.valueOf() == oStringObject.toString());//outputs "true"

String 类具有属性 lenght，它是字符串的字符个数，注意，即使字符串包含双字节的字符，每个字符也只算一个字符；

	var oStringObject = new String("hello world");
	alert(oStringObjcet.length);//outputs "11"

charAt() 方法返回的是包含指定位置处的字符的字符串，charCodeAt() 方法则返回字符代码；

	var oStringObject = new String("hello world");
	alert(oStringObject.charAt(1));//outputs "e"
	alert(oStringObject.charCodeAt(1));//outputs "101"

concat() 方法用于把一个或多个字符串链接到 String 对象的原始值上，返回 String 原始值，保持原始的 String 对象不变，与加号(+)链接字符串功能一样；

	var oStringObject("hello ");
	var sResult = oStringObject.concat("world");
	alert(sResult);//outputs "hello world"
	alert(oStringObject);//outputs "hello"
	var sResult = oStringObject + "world";
	alert(sResult);//outputs "hello world"
	alert(oStringObject);//outputs "hello"

indexOf() 和 lastIndexOf() 方法返回的都是指定子串在另一个字符串的位置，不同之处是前者从头开始检索子串，后者从结尾开始检索，如果没有找到则返回 -1；

	var oStringObjcet = new String("hello world");
	alert(oStringObject.indexOf("o"));//outputs "4"
	alert(oStringObject.lastIndexOf("o"));//outputs "7"

localeCompare() 方法对字符串进行排序，如果 String 对象按照字母顺序在参数中的字符串之前，返回负数(一般为 -1)，反之则返回正数(一般为 1)，相等则返回 0，先从第一字符相比较，相等则比较第二个字符，该方向不周区域实现方法可能会不同；

slice() 和 substring() 方法返回要处理的字符串的子串，都接受一个或二个参数，第一个参数是获取子串的起始位置，第二个参数是获取子串终止前的位置(即不包括终止位置的字符)，如果无第二个参数则终止位就默认为字符串的长度，不改变 String 对象自身的值，返回原始的 String 值，两者区别为：对于负数参数，slice() 方法会用字符串的长度加上参数，substring() 方法则将其作为 0 处理，而且它总是把较小的数字作为起始位；

	var oStringObject = new String("hello world");
	alert(oStringObject.slice(3,-4));//outputs "lo w"
	alert(oStringObject.subString(3,-4));//outputs "hel"

大小写转换方法：toLowerCase()、toLocaleLowerCase()、toUpperCase()、toLocaleUpperCase()，前两种用于把字符串换成全小写，后两种换成全大写，1、3是原始的，2、4是基于特定的区域实现的，与 localeCompare() 的用法相同；

String 类的所有属性和方法都可应用于 String 原始值上，因为它们是伪对象；

2.8.5、instanceof 运算符；

typeof 运算符无论引用的是什么类型的对象，它都返回"object"，instanceof 运算符与它相似，不同的是它要求开发者明确地确认对象为某特定类型：

	var oStringObject = new String("hello world");
	alert(oStringObject instanceof String);//outputs "true"

2.9、运算符

2.9.1、一元运算符

`delete`：删除对以前定义的对象属性或方法的引用，但它不能删除未定义的属性和方法，也不能删除 ECMAScript 的原始方法，如 toString；

	var o = new Object;
	o.name = "Nicholas";
	alert(o.name);//outputs "Nicholas"
	delete o.name;
	alert(o.name);//outputs "undefined"

`void`：对任何值都返回 undefined，用于避免输出不应该输出的值

前增量/前减量运算符：

	var iNum1 = 2;
	var iNum2 = 20;
	var iNum3 = --iNum1 + ++iNum2;//equals 22
	var iNum4 = iNum1 + iNum2;//equals 22

后增量/后减量运算符：与前缀式运算符不同的是，后缀式运算符是在计算过包含它们的表达式后才进行增量或减量运算的；

	var iNum1 = 2;
	var iNum2 = 20;
	var iNum3 = iNum1-- + iNum2--;//equals 22
	var iNum4 = iNum1 + iNum2;//equals 20

一元加法和一元减法：与普通数学中学到的用法相同，另外它会把字符串转换成数字，只对"0x"开头的字符串转换成十进制的值；

	var sNum = "25";
	alert(typeof sNum);//outputs "string"
	var iNum = +sNum;
	alert(typeof iNum);//outputs "number"
	var sNum1 = "25abc";
	var iNum1 = +sNum1;
	alert(iNum1);//outputs "NaN"
	alert(typeof iNum1);//outputs "number"
	var sNum2 = "0xb";
	alert(+sNum2);//outputs "11"
	var sNum3 = "010";
	alert(+sNum2);//outputs "10"

2.9.2、位运算符；

重温整数：  
(1)ECMAScript 有两种类型整数，即有符号整数(允许用正数和负数)和无符号整数(只允许用正数)；  
(2)有符号整数用前 31 位表示整数的数值，用第 32 位表示整数的符号，0 表示正数，1 表示负数，数值范围从 -2147483648 到 2147483647；  
(3)负数也存储为二进制代码，但形式是二进制补码，计算步骤：确定非负版本的二进制表示-求得二进制反码，即把 0 换为 1，把 1 换为 0，在二进制反码上加 1；  
(4)把负整数转换成二进制字符串后，ECMAScript 并不以二进制补码形式显示，而是用数字绝对值的标准二进制代码前加负号的形式输出；  
(5)无符号整数的数值范围为 0 到 4294967295；  
(6)所有整数字面量都默认存储为有符号整数，只有用 ECMAScript 的位运算符才能创建无符号整数；

位运算 NOT：  
(1)位运算 NOT 由否定号(~)表示，其三步处理过程为：把运算转换成 32 位数字，把二进制形式转换成它的进制反码，把二进制反码转换成浮点数：

	var iNum1 = 25;//25 is equal to 00000000000000000000000000011001
	var iNum2 = ~iNum1;//convert to 11111111111111111111111111100110
	alert(iNum2);//outputs "-26"

(2)位运算 NOT 实质上是对数字求负然后减 1：

	var iNum1 = 25;
	var iNum2 = -iNum1 - 1;
	alert(iNum2);//outputs "-26"

位运算 AND：由和号(&)表示，把每个数字中的数位对齐，然后用以下规则对同一位置的两个数进行 AND 运算：  
第一个数字中的数位 | 第二个数字中的数位 | 结果  
1 | 1 | 1  
1 | 0 | 0  
0 | 1 | 0  
0 | 0 | 0  
如：

	var iResult = 25 & 3;
	alert(iResult);//outputs "1"

位运算 OR：由符号(|)表示，在计算每个位时，OR 采用以下规则：  
第一个数字中的数位 | 第二个数字中的数位 | 结果  
1 | 1 | 1  
1 | 0 | 1  
0 | 1 | 1  
0 | 0 | 0  
如：

	var iResult = 25 | 3;
	alert(iResult);//outputs "27"

位运算 XOR：由符号(^)表示，采用以下规则：  
第一个数字中的数位 | 第二个数字中的数位 | 结果  
1 | 1 | 0  
1 | 0 | 1  
0 | 1 | 1  
0 | 0 | 0  
如：

	var iResult = 25 ^ 3;
	alert(iResult);//outputs "26"

左移运算：由两个小于号表示(<<)，把数字中的所有数位向左移动指定的数量，注意，在左移数位时数字右边多出的空位会用0填充，而且保留数字原来的符号位；

有符号右移运算：由两个大于号表示(>>)，把 32 位数字中的所有数位整体右移，同时保留该数的符号，与左移运算相反；

无符号右移运算：由三个大于号表示(>>>)，把无符号 32 位数中的所有数位整体右移，对于正数，无符号右移与有符号右移一运算一样，对于负数情况就不同了，无符号右移用 0 填充所有空位，包括符号位，负数被作为正数处理；

	var iUnsigne64 = -64 >>> 0;
	alert(iUnsigne64.toString(2));
	//outputs "11111111111111111111111111000000",equals "4294967232"

2.9.3、Boolean 运算符；

逻辑 NOT：由感叹号表示(!)，其返回的一定是 Boolean 值，其行为如下：  
(1)如运算数是对象，返回 false；  
(2)如运算数是数字 0，返回 true；  
(3)如运算数是 0 以外的任何数字，返回 false；  
(4)如运算数是 null，返回 true；  
(5)如运算数是 NaN，返回 true；  
(6)如运算数是 undefined，发生错误；  
判断 ECMAScript 变量本身的 Boolean 值时，可以在一行代码中使用两个逻辑 NOT 运算符。

	var bFalse = false;
	alert(!!bFalse);//outputs "false"

逻辑 AND 运算符：由双和号(&&)表示，以下真值表描述了它的行为：  
运算数1 | 运算数2 | 结果  
true | true | true  
true | false | false  
false | true | false  
false | false | false  

AND 是简便运算，即如果第一个运算数决定了结果，它就不再计算第二个运算数；

	var bTrue = true;
	var bResult = (bTrue && bUnknown);//error occurs here
	alert(bResult);//this line never executes
	var bTrue = false;
	var bResult = (bTrue && bUnknown);
	alert(bResult);//outputs "false"

其运算数不止 Boolean 值，并不一定返回 Boolean 值：  
(1)如果一个运算数是对象，另一个是 Boolean 值，返回该对象；  
(2)如果两个运算数都是对象，返回第二个对象；  
(3)如果某个运算数是 null，返回 null；  
(4)如果某个运算数是 NaN，返回 NaN；  
(5)如果某个运算数是 undefined，发生错误。

2.9.4、乘性运算符，注意：其除了普通运算功能外还具有一些自动的类型转换功能；

乘法运算符：由星号(*)表示，在处理特殊值时还有一些特殊行为：  
(1)除常规乘法运算外，如果结果太大或太小，那么生成的结果是 Indinify 或 -Indinify；  
(2)如果某个运算数是 NaN，结果为 NaN；  
(3)Infinify 乘以 0，结果为 NaN；  
(4)Infinify 乘以 0 以外的任何数字，结果为 Infinity 或 -Infinity，由第二个运算数的符号决定；  
(5)Infinify 乘以 Infinify，结果为 Infinity；

除法运算符：由斜线(/)表示，在处理特殊值时还有一些特殊行为：  
(1)除常规除法运算外，如果结果太大或太小，那么生成的结果是 Indinify 或 -Indinify；  
(2)如果某个运算数是 NaN，结果为 NaN；  
(3)Infinify 被 Infinify 除，结果为 NaN；  
(4)Infinify 被任何数除，结果为 Infinity；  
(5)0 除一个非无穷大的数字，结果为 NaN；  
(6)Infinify 被 0 以外的任何数字除，结果为 Infinity 或 -Infinity，由第二个运算数的符号决定；

取模(余数)运算符：由百分号(%)表示，在处理特殊值时也有一些特殊行为：  
(1)如果被除数是 Infinity，或者除数是 0，结果为 NaN；  
(2)Infinity 被 Infinity 除，结果为 NaN；  
(3)如果除数是无穷大的数，结果为被除数；  
(4)如果被除数为 0，结果为 0；

2.9.5、加性运算符

加法运算符(+)，特殊行为：  
(1)某个运算数是 NaN，结果为 NaN；  
(2)Infinity 加 Infinity，结果为 Infinity；  
(3)-Infinity 加 -Infinity，结果为 -Infinity；  
(4)Infinity 加 -Infinity，结果为 NaN；  
(5)+0 加 +0，结果为 +0；  
(6)-0 加 -0，结果为 -0；  
(7)+0 加 -0，结果为 +0；  
(8)如果两个运算数都是字符串，把第二个字符串连接到第一个字符串上；  
(9)如果只有一个运算数是字符串，则把运算数转换成字符串后再连接起来；

	var result = 5 + 5;//two numbers
	alert(result);//outputs "10"
	var result = 5 + "5";//a number and a string
	alert(result);//outputs "55"

注意：为避免 JavaScript 中的一种常见错误，在使用加法运算符时，一定要仔细检查运算数的数据类型。

减法运算符(-)，特殊行为：  
(1)某个运算数是 NaN，结果为 NaN；  
(2)Infinity 减 Infinity，结果为 NaN；  
(3)-Infinity 减 -Infinity，结果为 NaN；  
(4)Infinity 减 -Infinity，结果为 Infinity；  
(5)-Infinity 减 Infinity，结果为 -Infinity；  
(6)+0 减 +0，结果为 +0；  
(7)-0 减 -0，结果为 -0；  
(8)-0 减 -0，结果为 +0；  
(9)某个运算数不是数字，结果为 NaN；

2.9.6、关系运算符：小于(<)、大于(>)、小于等于(<=)、大于等于(>=)，执行的是两个数的比较运算；

对两个字符串用关系运算符，是按首个字母的字符代码进行比较，但大写字母的代码都小于小写字母，可把两个运算数转换成相同的大小写形式后再进行比较；

	var bResult = "Brick" < "alphabet";//return "true";
	var bResult = "Brick".toLowerCase() < "alphabet".toLowerCase();//return false

当比较两个字符串形式的数字时，也是比较首个数字的字符代码；

	var bResult = "23" > "3";//return "false"

当一个运算数是字符串式的数字，一个运算数是数字时，字符串会被调用 Number() 方法后再进行比较；

	var bResult = "23" > 3;//return "true"

当一个运算数是数字，另一个运算数不能用 Number() 方法转换成数字，则任何包含 NaN 的关系运算都要返回 false；

	var bResult = "23abc" > 3;//return "false"
	var bResult = "23abc" < 3;//return "false"

2.9.7、等性运算符：等号与非等号用于处理原始值，全等号和非全等号用于处理对象；

等号和非等号：等号由双等号表示(==)，非等号是感叹号加等号(!=)，都会进行类型转换；  
(1)如果运算数是 Boolean 值，会先把它转换成数字值，false 转换成 0，true 转换成 1；  
(2)如果一个运算数是字符串，另一个是数字，会先尝试把字符串转换成数字；  
(3)如果一个运算数是对象，另一个是字符串，会先尝试把对象转换成字符串(调用 toString() 方法)；  
(4)如果一个运算数是对象，另一个是数字，会先尝试把对象转换成数字；  
规则：  
(1)值 null 和 undefined 相等；  
(2)在检查相等性时，不能把 null 和 undefined 转换成其他值；  
(3)如果某个或者两个运算数是 NaN，等号将返回 false，非等号将返回 true，因为 NaN 不等于 NaN；  
(4)如果两个运算数都是对象，则比较的是它们的引用值，如果两个运算数指向同一个对象，返回 true，否则返回 false；

	null == undefined //return true
	NaN == NaN //return false
	NaN != NaN //return true
	false == 0 //return true
	true == 1 //return true
	undefined ==0 //return false
	"5" == 5 //return true

全等号和非全等号：全等号(===)，非全等号(!==)，它们在检查相等性前，不执行类型转换；

	var sNum = "55";
	var iNum = 55;
	alert(sNum === iNum);//outputs "false"
	alert(sNum !== iNum);//outputs "true"

2.9.8、条件运算符：`variable = boolean_expression ? true_value : false_value;`如：

	var iMax = (iNum1 > iNum2) ? iNum1 : iNum2;

2.9.9、赋值运算符，由等号(=)实现；

	var iNum = 10;
	iNum = iNum + 10;
	//可以用一个复合赋值运算符改写第二行代码：
	var iNum = 10;
	iNum += 10;

每种主要的算术运算以及其他几个运算都有复合赋值运算符
(1)乘法/赋值(*=)；  
(2)除法/赋值(/=)；  
(3)取模/赋值(%=)；  
(4)加法/赋值(+=)；  
(5)减法/赋值(-=)；  
(6)左移/赋值(<<=)；  
(7)有符号右移/赋值(>>=)；  
(8)无符号右移/赋值(>>>=)；

2.9.10、逗号运算符：用于在一条语句中执行多个运算，最常用于变量声明中；

	var iNum1 = 1, iNum2 = 2, iNum3 = 3;

2.10、语句；

2.10.1、if 语句：

语法：`if (condition) statement1 else statement2;`
也可以是：`if (condition1) statement1 else if (condition2) statement2 else statement3;`
condition 可以是任何表达式，结果甚至不必是真正的 Boolean 值，ECMAScript 会把它转换成 Boolean 值。

2.10.2、迭代语句，又叫循环语句

do-while 语句：计算表达式之前至少会循环主体一次；

	var i = 0;
	do{
		i += 2;
	}while(i<10);

while 语句：循环主体可能根本不被执行；

	var i = 0;
	while(i < 10) {
		i += 2;
	}

for 语句，能够初始化变量，交定义循环后要执行的代码；

	for (var i = 0; i < iCount; i++) {
		alert(i);
	}

for-in 语句，是严格的迭代语句，用于枚举对象的属性；

	for (sProp in window) {
		alert(sProp);
	}

2.10.4、break 语句和 continue 语句；  
break 语句可以立即退出循环，阻止再次反复执行任何代码，而 continue 语句只是退出当前循环，继续进行下一次循环；

2.10.5、with 语句：用于设置代码在特定对象中的作用域；

	var sMessage = "hello world";
	with(sMessage) {
		alert(toUpperCase());//outputs "HTLLO WORLD"
	}

这段代码中 with 语句用于字符串，解释程序将检查该方法是否本地函数，如果不是，它将检查伪对象 sMessage，看它是否为该对象的方法，然后输出"HELLO WORLD"，因为解释程序找到了了字符串"hello world"的 toUppperCase() 方法；  
with 语句是运行缓慢代码段，最好避免使用它。

2.10.6、switch 语句：在 ECMAScript 中，switch 语句可以用于字符串，而且能用不是常量的值说明情况：

	var BLUE = "blue", RED = "red", GREEN = "green";
	switch (sColor) {
		case BLUE: alert("Blue");
		break;
		case RED: alert("Red");
		break;
		case GREEN: alert("Green");
		break;
		default: alert("Other");
	}

2.11、函数：ECMAScript 的核心；

函数可以 return 返回值，也可以直接调用 return 退出函数，那么它真正返回的值是 undefined；  
函数在执行过 return 语句后会停止执行代码，函数中可以通过 if 语句有多个 return 语句。

2.11.1、无重载：ECMAScript 中的函数不能重载，虽然两个同名函数不会引发错误，但最后一个会覆盖前面的。

2.11.2、arguments 对象；  
无需明确指出参数名，即可在函数代码中使用 arguments 对象，用 arguments[0] 可以访问第一个参数值；  
用 arguments.lenght 即可检测传递给函数的参数个数；  
ECMAScript 不会验证传递给函数的参数个数是否等于函数定义的参数个数；  
用 arguments 对象判断传递给函数的参数个数或值，即可模拟函数重载；

2.11.3、Function 类：函数实际是上功能完整的对象，Function 类可以表示开发者定义的任何函数，语法如下：

	var function_name = new Function(argument1,argument2,...,argumentN,function_body);

Function 定义函数比用传统方式要慢得多，最好不要使用它，但所有函数都应看作是 Function 类的实例；  
ECMAScript 定义的属性 length 声明了函数期望的参数个数，ECMAScript 可以接受任意多个参数，最多 25 个。

2.11.4、闭包：指词法表示包括不必计算的变量的函数，即函数能使用函数外定义的变量。

第3章、对象基础

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

第4章、继承

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

第五章、浏览器中的 JavaScript

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











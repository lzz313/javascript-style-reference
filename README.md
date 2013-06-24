# Javascript代码及注释规范 2013/6/24 #

----------
## 声明 ##

- 变量声明必须加var关键字，严格控制作用域；
- 使用驼峰式命名变量和函数，如：functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis,namespaceNamesLikeThis；
- 函数可选参数命名以opt_开头；
- 全局变量，私有成员变量和方法命名以下划线开头，如：var _this；
- 常量定义单词全部大写，以下划线连接，但不要用const关键字来声明，如：SOME_CONSTANTS；
- 禁止在代码块中声明函数，错误的范例：if (true) {function foo() {}}；
- 禁止用new来实例化基本类型，错误的范例：var x = new Boolean(false)；
- 直接定义数组或对象，而不使用new关键字声明，错误的范例：var a = new Array();var o = new Object()；
- 使用单引号来定义字符串；
- 文件名必须全部用小写；

## 分号 ##

一个语句必须用分号结束，下面是错误的范例：

    myMethod = function() {
      return 42;
    }    
    (function() {
      // 一个匿名函数，在这里会被错误解析当作参数调用导致报错
    })();

## 异常 ##

由于无法完美的控制都不出现异常，所以尽量在可能但不确定出现异常的地方用try-catch(e)来抛出异常，这样有利于规模较大的项目中排查错误。如果可以，使用自定义异常抛出错误信息，更有利于错误信息阅读，且更加通用，因为不同浏览器抛出的信息不一样，可能完全无法定位到问题所在位置。

## 标准化代码编写 ##

为获取最大化的可移植性和兼容性，代码中尽量同标准中支持的方式来书写代码，例如：使用string.charAt(3)而不是string[3]，虽然浏览器支持但不在规范中，你无法保证你将来会不会遇到兼容其他浏览器的情况，如果这个浏览器完全或部分特性只按规范实现。

## 面向对象编程 ##

- 类中的成员变量使用构造函数来初始化；
- 除非是必须移除类的成员，否则析构函数中对成员的销毁应通过将其设置为null，而不是用delete，因为重新赋值方式性能比用delete好；
- 避免通过prototype方式污染内置对象原型链；

## 安全 ##

- 慎用eval，仅用于反序列化数据，禁止对用户输入数据进行eval；
- 审查用户输入，如需要从URL获取参数信息之类的操作；
- 慎用可回调的iframe跨域调用；

## 作用域相关 ##

- 不使用with关键字，容易造成作用域混乱；
- this仅用于类成员函数或对象中；
- 通用全局函数，特别是通用组件代码应将业务逻辑放入闭包中，并通过“命名空间”将其引入；

## 杂项 ##

- 多行字符串书写不要用\加换行的方式，应使用+运算连接字符串；
- 不使用关联数组，而用JSON代替；
- 避免使用IE条件注释；

## 格式化代码 ##

没有强制要求代码需格式化成什么样子，但尽量使代码具有较高的可读性。下面给出一些建议的代码风格：
	
	// 花括号起始位置与语句开始在同一行
	if (something) {
	  // ...
	} else {
	  // ...
	};

	// 数组和对象书写
	var arr = [1, 2, 3];  // [之后，]之前没有空格
	var obj = {a: 1, b: 2, c: 3};  // {之后，}之前没有空格

	// 多行数组和对象书写
	var a = [
	  'huangrongrong',
	  'chenying',
	  'small grey grey',
	  'shenshunlin'
	];

	var pos = {
	  top: 10,
	  right: 20,
	  bottom: 15,
	  left: 12
	};
	
	// 将业务逻辑相关的代码写一起，不相关的以空行分隔
	doSomethingTo(x);
	doSomethingElseTo(x);
	andThen(x);
	
	nowDoSomethingWith(y);
	
	andNowWith(z);

	var x = a ? b : c;  // 一行能写完
	
	// 写不完可以换行加缩进
	var y = a ?
	    longButSimpleOperandB : longButSimpleOperandC;
	
	// 或者这样
	var z = a ?
	        moreComplicatedB :
	        moreComplicatedC;


## 类型转换 ##

对于代码中需要进行逻辑判断的变量，建议进行强制类型转换或使用===进行判断。

下列值在布尔表达式中结果为false：

- null
- undefined
- '' //空字符串
- 0 //数字

而下面的为true：

- '0' //字符串
- [] //空数组
- {} //空对象

还有一些难以区分的表达式：

	Boolean('0') == true
	'0' != true
	0 != null
	0 == []
	0 == false

	Boolean(null) == false
	null != true
	null != false

	Boolean(undefined) == false
	undefined != true
	undefined != false

	Boolean([]) == true
	[] != true
	[] == false

	Boolean({}) == true
	{} != true
	{} != false


## 注释规范 ##

文档注释遵循YUIDoc规范（[http://yui.github.io/yuidoc/syntax/](http://yui.github.io/yuidoc/syntax/)），所有的文件、类、方法和属性都应该用合适的标记和类型进行注释。

- YUIDoc要求文档中至少要有一个Class定义；
- YUIDoc中注释块必须至少以/**（两个星号）开头；
- 方法、参数和返回值等需要有简单的说明；
- 单行注释使用//；
- 对于代码中特殊用途的变量、存在临界值、函数中使用的hack、使用了某种算法或思路等需要进行注释描述；


下面给出代码注释实例作为参考，更多标记和类型定义请参考YUIDoc官方文档。

	/**
	这是一个UELib类
	
	@class UELib
	@constructor
	**/
	function UELib = function(){};
	
	/**
	My method description.  Like other pieces of your comment blocks, 
	this can span multiple lines.
	
	@method css
	@param prop {String} set/get a css property
	@param [value] {String} A value you want to set to a css property
	@example
	   ele.css('width', '100%');
	@return {Boolean} Returns true on success
	**/
	UELib.prototype.css = function(prop,value){
	
	};

## 代码发布 ##

待定
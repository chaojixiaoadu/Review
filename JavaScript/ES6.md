### ES6
严格模式：‘use strict’

let：块变量； 不能重复声明。
减少使用全局变量，优化代码。
### 类型转换

	var myVar = "3.14159";
	string: ''+myVar;
	Number: +myVar;
	Inter: ~~myVar;
	floor: 1 * myVar;

> num.toFixed(2):保留两位小数。
> 
>NaN != NaN;true
>
>undefined == null;true
>
>undefined === null;fasle


### 扩展运算符

	var arr = [1,2,3,4];
	function fun(a,b,c){
		console.log(a,b,c);
	};
	// 传统写法
	fun(arr[0],arr[1],arr[2]);
	// 使用扩展运算符（...）
	fun(...arr);
	

> “...” 扩展运算符

##### Math扩展
	
	var num = -123.008;
	console.log(Math.floor(num));//-124
	console.log(Math.trunc(num));//-123
	console.log(~~num)//-123

## 数组
	
	let item in arr;
> in 下标

	let item of arr;
> of 内容

    Object.keys() 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和使用 for...in 循环遍历该对象时返回的顺序一致 （两者的主要区别是 一个 for-in 循环还会枚举其原型链上的属性）。

- Array.from(arr);用于将伪数组转换为真数组。

### 箭头操作符

* “=>”	

		function add(a,b,callback){
		let c = a + b;
		callback(c);
		}
		//调用
		add(10,20,(res) => {
		console.log(res);
		}
		//() => {}  等于  function () {}
		// (a) || a => {}  等于  function (a) {}
		// (a,b) => {}  等于  function(a,b) {}


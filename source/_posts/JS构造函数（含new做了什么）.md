---
title: JS构造函数（含new做了什么）
date: 2018-09-28 16:56:05
tags: （JH）JS构造函数、new做了什么
---

## 一、构造函数和普通函数的区别
	
1. 构造函数名一般第一个字母大写：`Function/Number/String`，普通函数为驼峰式名命：`puTongHanShu`

2. 构造函数由new调用：`new String('abc')`, （abc不要忘了引号）

3. 构造函数中可以使用this，普通函数一般不使用

3. 构造函数一般默认不return

4. 原型指向： 

		//只写个形式表达意思
		function FF(){//...}
		let ff = new FF()

		//那么，这个生成实例的__proto__指向构造它的函数的prototype
		ff.__proto__ === FF.prototype		//true
		FF.__proto__ === Function.prototype	//true	


## 使用new时到底做了什么
构造函数可由new调用，那么new到底做了什么：

1. 创建临时对象，并将this指向这个临时对象

2. 将临时对象的\_\_proto\_\_指向构造函数的prototype（并将构造函数Fn的prototype.constructor=Fn）

3. 执行构造函数中的代码

4. 返回这个临时对象

代码举例：

		function F1(x){
			this.name = 'xiao'
			console.log(x*100)
		}
		let f1 = new F1()	 //NaN 执行了打印代码
		let f2 = new F1(5)	 //500

		//返回对象，f1是对象
		f1(5)	    //报错： f1 is not a function
		f1		    //F1 {name: "xiao"}
		f1.name		//"xiao"

		//指定对象原型
		f1.__proto__ === F1.prototype	 //true
		f1.constructor === F1		     //true
		
		//另外
		F1.constructor === F1			 //false
		F1.constructor === Function		 //true



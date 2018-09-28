---
title: JS中的this指向
date: 2018-09-28 11:17:25
tags: （JH）JS-this指向
---
# 使用call的情况

要知道什么是call的实质：JavaScript模仿Java（抱大腿），所以也要弄一个this，JS之父就把**call第一个参数**作为this。

	function fn(){console.log(this)}
	fn()			 //window
	fn.call(1)		 //Number{1}
	fn.call('abc')	 //String {"abc"}

call把第一个参数作为this，后面的参数作为函数的参数。
	
	function fn(x,y){console.log(x,y)}
	fn(1,2)			//3
	fn.call(undefined,1,2)	//3，this是undefined，1，2作为参数

正是因为this实质上是call第一个参数，那么我们想确定this，看各种API源码是最靠谱的。


既然知道this是call第一个参数，那么关于this的问题就简单了，接下来看：通过改写为call调用的方式确定this


# 一般分类（注意：以下都是不使用call强行改this的情况，或者说默认call的情况）

## 一、
全局作用域中调用this，那么this指向window

## 二、

1. 在全局的函数中（两种情况）

		//第一种:window
		function f1(){
			console.log(this)
		}	
		f1()    //window对象
		
		//第二种：严格模式是undefined
		function f2(){
			'use strict'
			console.log(this)
		}
		f2()    //undefined

转换为call：
	
	f1.call()	||  f2.call()
	
	//这里的call没有传第一个参数，也就是this为undefined，为什么是window呢
	
	//浏览器规定context为null或undefined，

	//那么context就是window对象，严格模式是undefined

## 三、对象调用

之前看到有人说：“要搞懂this只需理解：函数中this在定义时是不能确定的，只有在执行时才知道，因为函数this永远指向最后调用这个函数的对象”，这呢，正是因为源是把这个调用对象作为call第一个参数啊！

	let o1 = {
		a: 1,
		f3: function f3(){
			console.log(this)
		}
	}
	
	//1、用o1调用
	o1.f3()   //{a: 1, f3: ƒ}  this指向o1
	//即
	o1.f3.call(o1)
	
	//2、不用o1
	let f4 = o1.f3
	f4()	  //window对象   this指向window
	//即
	f4.call()

## 四、构造函数: 指向构造出的实例
一、正常情况：指向构造出的实例，这是因为new源码中就是把this指向新生成的实例。

	function F(){
		this.b = 2
	}
	let f5 = new F()
	console.log(f5.b)	//2, 所以f5上是有属性 b 的，也就是构造时this指向f5

二、非常情况（如果在构造函数有return）

1. return 一个对象，那么构造实例就为这个对象，也就得不到正常结果，无所谓this指向了。

		//return 对象
		function F(){
			this.b = 2
			let o2 = {name:'xiao'}	//xiao不加引号错误！
			return o2	
		}
		let f5 = new F()

		console.log(f5)			//{name: "xiao"}
		console.log(f5.b)		//undefined

2. return 非对象，包括null，虽然 typeof(null) === 'object'，那么新构造的实例还是正常的。

	
		function F(){
			this.b = 2
			return null	//或者return 1/undefined/"abc"
		}
		let f6 = new F()

		console.log(f6)   //{b:2}

到这里，我发现这些非常情况似乎已经不是this指向问题了，而是new的返回问题了。

所以记住，**构造函数的this指向构造实例** 就OK

[关于new的博客]()


## 五、箭头函数
箭头函数不改变this，箭头函数里面的this就是它外面的this，可以理解为**将当前的this作为call第一个参数**。

	let o3 = {
		name: 'ooo3',
		f7: ()=>{console.log(this)}
	}
	
	o3.f7()		//window对象
	//按照上面‘对象调用’的说法，改为call似乎应该是
	o3.f7.call(o3)

	//但是箭头函数不改变this，所以应该是：
	o3.f7.call(this)
	//当前this就是window对象


## 最后总结，this就是call第一个参数，call调用才是正常的模式，不使用call调用的，想要确定this都只能看底层调用源码怎么写了。

this就是call第一个参数，写完这篇文章，成功洗脑 √
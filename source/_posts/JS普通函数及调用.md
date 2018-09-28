---
title: JS普通函数及调用
date: 2018-09-28 13:00:35
tags: （JH）JS普通函数及调用
---
想想还是决定把普通函数、构造函数分两篇总结。

## 一、声明（包括函数名情况）
### 方法一：具名函数
	
	function f1(x){
		console.log(x)
	}
		
	//函数名
	f1.name === 'f1'	//true
	f1.name === 'f1'	//true
	f1.name === 'f1'	//true
	
### 方法二：匿名函数

	let f2
	f2 = function(x){
		console.log(x)
	}

	//函数名
	f2.name === 'f2'	//true
	f2.name === 'f2'	//true
	f2.name === 'f2'	//true
	
### 方法三：具名函数赋值
	
	let f3 = function f4(){
		console.log('f3')
	}
	
	//函数名
	f3.name === 'f4'	//true
	f3.name === 'f4'	//true
	f3.name === 'f4'	//true

	//注意 
	f4.name		//报错：f4 is not defined
	f4.name		//报错：f4 is not defined
	f4.name		//报错：f4 is not defined


### 方法四：使用window.Function

	let f5 = new Function('x','y','return x+y')
	f5(1,2)		//3
	
	//函数名
	f5.name		//'annoymous'  匿名的
	f5.name		//'annoymous'  匿名的
	f5.name		//'annoymous'  匿名的


### 方法五：箭头函数

	(x)=>{console.log(x)}
	
	let f6 = (x)=>{console.log(x)}
	
	//箭头函数只有一句返回时，可以省略大括号和return
	let f6 = (x,y)=>{return x + y}
	let f6 = (x,y)=> x + y

	//箭头函数只有一个参数时，可以省略小括号
	let f6 = (x)=>{return x*2}
	let f6 = x => x*2
	

## 二、函数返回

+ 函数需要return；
+ 没有return 就默认 return undefined。

## 三、函数调用

1. 使用 `fn(x1,x2)`

2. 作为对象方法 `obj.xx.fn(x,y)`

3. call()
 
	 	fn.call(asThis,x1,x2,...)

		//call第一个参数是this，后面的做真正的参数。

		function ff(x,y,z){return x+y+z}
		ff.call(1,2,2,2)	//6

4. apply()

		fn.apply(asThis,[x1,x2,...])
	
		//apply区别与call就是它第二个参数接受数组，
		//我们需要把剩下的参数作为一个数组传递。
	
		function ff(x,y,z){return x+y+z}
		ff.apply(1,[2,2,2])	//6


5.  bind()（绑定不调用）
	
		fn.bind(asThis,[x1,x2,...])

		//bind方法不会调用函数，而是生成一个绑定函数(而且已经传好参数，不可改)
		//它的参数同call一致
			
		function ff(x,y,z){return x+y+z}
		let mm = ff.bind(1,2,2,2)
		mm()	//6	
		mm(1,1,1)	//6，没有变
		mm.call(1,3,3,3)	//6，新传的参数不起作用
	
	
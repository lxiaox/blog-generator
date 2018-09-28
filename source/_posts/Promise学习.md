---
title: Promise学习
date: 2018-09-07 19:40:44
tags: （J）Promise
---
# 什么是 Promise？
Promise作为ES6最重要的特性之一，它本身是一个构造函数，并拥有`resolve`、 `reject`、 `all`、 `race` 等方法。

![打印Promise](http://p8rplhkt6.bkt.clouddn.com/18-9-8/100325.jpg)

##### Promise 对象用于表示一个异步操作的最终状态（完成或失败），以及其返回的值。

### 语法:
`new Promimse( function(resolve, reject) {} )`

Promise构造函数接受一个函数，这个函数的参数为`resolve`和`reject`，`resolve`将`Promise`状态改为`fulfilled`,`reject`将其状态改为`rejected`，promise会根据不同状态执行不同操作。

### 一个Promise有以下几种状态：
+ `pending`：初始状态，不成功也没失败
+ `fulfilled`：表示操作成功完成
+ `rejected`：表示操作失败
+ `settled`：完成状态，fulfilled和rejected的统称

`pending`状态的Promise可能触发`fulfilled`状态，并传递一个值给成功之后的操作；也可能触发`rejected`状态，并传递失败信息或失败原因给失败之后的操作。

# 改变状态之后的操作：
打印Promise对象可以看到，它的原型方法`then()`、`catch()`、`finally()`，这些方法会表明Promise操作完成之后要做的事情。

### 1、Promise.prototype.then(onFulfilled, onRejected)
 then()方法最多接受两个参数，即成功之后调用的回调函数，和失败之后调用的回调函数，同时它返回一个Promise对象，使得Promise().then().then()这样的链式操作得以实现。

		promise.then(
		    function(value){
		        //如果成功...
		    },
		    function(reason){
		        //失败...
		    }
		)
`then()`方法也可只接受成功的回调函数，那么失败情况就会由`catch()`方法处理。

### 2、Promise.prototype.catch(onRejected)
 `catch()`方法处理拒绝也就是失败的情况，同时返回一个Promise对象。

		promise.catch(
		    function(reason){
		        //失败...
		    }
		)

### 3、Promise.prototype.finally()
 `finall()`也返回一个Promise对象，then()和catch()执行之后都会执行finally()，可以避免重复书写同样的代码。

		promise.finally(
		    function(){
		        //成功和失败都会执行...
		    }
		)

要注意，就算是失败的Promise经过`then()`、`catch()`处理，返回的新的Promise状态是**成功**的，除非再次处理（`then`、`catch`）失败。

同时形如`promise.then().then().then().catch()`，所有的失败情况都由最后的`catch()`处理，一旦某个地方失败，就会顺着操作链寻找到失败的回调函数。

## 那么现在就可以写一个Promise了
先封装一个函数：

	function test(num){
	    var p = new Promise(function(resolve, reject){
	        //设置延时，进行异步操作
	        setTimeout(function(){
	           if(num === 66){
	               console.log('顺利完成')
	               resolve('66大顺，成功') //resolve将状态改为fulfilled，完成
	           }else{
	               console.log('失败')
	               reject('不顺利，失败了')  //reject将状态改为rejected，拒绝
	           }
	        }, 3000)
	    })
	    return p
	}
在上述代码中，我们封装了一个函数，这个函数返回一个promise对象。我们定义了一个异步操作，就是判断数值是否为66，等于成功，不等于就失败。

为什么要封装函数？因为在new一个Promise对象时，传进去的函数会执行，封装函数之后我们就可以在调用函数时再执行它。

接下来就可以调用函数，进行下一步操作：

		//成功的情况：
		test(66).then(function(value){
		    console.log('成功信息：')
		    console.log(value)
		}).catch(function(reason){
		    console.log('失败信息：')
		    console.log(reason)
		})
成功结果截图，3s之后输出：

![成功结果](http://p8rplhkt6.bkt.clouddn.com/18-9-8/35816019.jpg)

		//失败的情况：
		test(55).then(function(value){
		    console.log('成功信息：')
		    console.log(value)
		}).catch(function(reason){
		    console.log('失败信息：')
		    console.log(reason)
		})
失败结果截图，3s之后输出：

![失败结果](http://p8rplhkt6.bkt.clouddn.com/18-9-8/48159739.jpg)

# 更多用法

### 1、Promise.resolve(value)
`resolve()`方法返回一个给定值解析之后的Promise对象。其中又分为几种情况：

1、如果传入的值本身是一个Promise对象，那么就返回这个Promise对象

![传入Promise对象](http://p8rplhkt6.bkt.clouddn.com/18-9-8/58265184.jpg)

如图传入Promise对象为：test(55)，它的状态是失败，resolve()的返回值就是这个失败状态的promise，因此会调用失败的回调输出failed。

2、如果传入的值是个thenable对象，即带有then方法，那么返回的是then之后最终状态的promise。

![传入thenable](http://p8rplhkt6.bkt.clouddn.com/18-9-8/84989719.jpg)

如图传入`test(55).then().catch()`，虽然`test(55)`是失败的，但是它经过`catch()`处理，最后返回的状态是成功，所以`resolve()`最后的`then()`会输出`success`。

3、如果传入的是其他值，那么就以成功状态返回Promise。

![传入其他值](http://p8rplhkt6.bkt.clouddn.com/18-9-8/24130485.jpg)

如图传入`‘abcde’`，最终状态是成功，输出`success`。

### 2、Promise.reject(reason)
`reject()`方法返回一个带有拒绝原因参数的Promise对象。

![reject1](http://p8rplhkt6.bkt.clouddn.com/18-9-8/43684756.jpg)

从上图可以看出这里的拒绝原因就是字符串‘abcde’本身。

![reject2](http://p8rplhkt6.bkt.clouddn.com/18-9-8/47409228.jpg)

这里的原因是Error: failed。

### 3、Promise.all(iterable)
`all()`方法返回一个Pomise对象，它传入的参数（iterable译为可迭代的）是promise的数组，即多个promise，只有所有的Promise对象都为成功状态，`all()`才会返回成功状态的Promise对象。如果有一个失败，那么`all()`返回失败promise，且失败原因就是第一个失败promise的失败原因。

	var promise1 = Promise.resolve(66)
	var promise2 = Promise.reject(55)
	var promise3 = 'abcde'
	var promise4 = new Promise(function(resolve, reject) {
	    setTimeout(()=>{resolve('success')}, 300)
	})
	var promise5 = new Promise(function(resolve, reject) {
	    setTimeout(()=>{reject('failed')}, 300)
	})
	//promise4和promise5被创建的时候，传入的函数就开始执行，我验证时是直接在控制台粘贴本段所有代码再执行，影响不大，但最好封装成一个函数，将时间延迟增长至3s:
	var promise4 =function() {
	    return new Promise(function (resolve, reject) {
	        setTimeout(() => {
	            resolve('success')
	        }, 3000)
	    })
	}
	var promise5 =function() {
	    return new Promise(function (resolve, reject) {
	        setTimeout(() => {
	            reject('failed')
	        }, 3000)
	    })
	}
	
	function onFulfilled(value) {
		console.log('成功：')
	    console.log(value)
	}
	function onRejected(reason){
	    console.log('失败：' + reason)
	}

	//开始测试：
	Promise.all([promise1, promise2, promise3]).then(onFulfilled,onRejected)
		//输出“失败：55”，因为promise1成功，promise2失败

	Promise.all([promise5(), promise2, promise3]).then(onFulfilled,onRejected)
		//输出“失败：55”，因为promise2比promise5先处理完成，这里是看处理时间
		//promise5设置了延时，这里要注意本人之前犯的错误：setTimeout(resolve('success'),300)
		//resolve('success')没有包在函数里，导致代码直接执行（原因同eval()）没有延迟，最终输出为“失败：failed”，得出错误的结论

	Promise.all([promise1, promise3, promise4()]).then(onFulfilled,onRejected)
		//过3s输出：Array [66, "abcde", "success"]，因为promise4有延时，等全部promise为成功状态时就会将值组成数组一起输出


### 3、Promise.race(iterable)
`race()`方法返回一个Promise对象，它与`all()`不同之处在于一旦迭代器中某个proise完成或拒绝，那么就返回完成或拒绝的Promise对象。
	
	//沿用上面的代码
	Promise.race([promise1, promise2, promise3])
		.then(onFulfilled,onRejected)
	//输出“成功：66”，第一个成功就返回成功值66。

	Promise.race([promise5(), promise2, promise3])
		.then(onFulfilled,onRejected)
	//输出“失败：55”，因为promise5有延时，所以promise2最先处理完。

---
title: JS实现继承的几种方法
date: 2018-10-05 20:45:37
tags: （J）继承
---

1. 类式继承（单纯的原型链继承）
2. 构造继承
3. 组合继承 （1，2组合）
4. 寄生组合继承（3的优化）
5. extends


### 类式继承
形如：

	function A(){this.a = ...}
	A.prototype.aa = ...
	function B(){}
	B.prototype = new A()	//标记代码
	//效果是 B.prototype.__proto__ = A.prototype

如此，子类B就拥有了父类A的原型（方法、属性）。

但是它的缺点之二是：

1. 来自原型的所有属性要被所有实例共享
2. 无法在新建子类实例时，向父类构造函数传参，（只能在标记代码处传），那由B衍生的后代，这些属性值就是统一的。

### 构造函数继承
形如：

	function A(){this.a = ...}
	A.prototype.aa = ...
	function B(){
		A.call(this,...)	//改变作用域，使得A属性方法都赋给B（this）
	}
	//B无法获得A原型（上的aa），只能获得A上的属性方法（a）

### 组合继承
很显然，上面两种各有所长，互相弥补，结合他们就得到了更好地方法--组合继承。

	function A(){this.a = ...}
	A.prototype.aa = ...
	function B(){
		A.call(this,...)	//构造函数
	}
	B.prototype = new A()		//类式（原型链）

	//缺点是调用了两次A()

	B.prototype.constructor = B	//本来的constructor被覆盖，重写一下

### 寄生组合继承
弥补组合继承的劣势，将类式继承改一下，如：

	//写法一
	let C = function(){}
	C.prototype = A.prototype
	B.prototype = new C()

	//C()什么也不干，要优秀一点

	//写法二
	B.prototype = Object.create(A.prototype)	
	//b = Object.create(a)的作用就是使 b.__proto__ = a


### extends继承
ES6的class实现继承，形如：

	class A{
		constructor(a){
			this.a = a
		}
	}
	A.prototype.aa = ...

	class B extends A{
		constructor(a){
			super(a)	//子类没有this，为了继承父类的this对象
			this.a = a
		}
	}
	
	//B自动地继承A的原型

---
title: 实现一个jQuery的API
date: 2018-07-04 22:20:26
tags: （J）自己实现-jQuery API
---
通过自己动手写 API 来学习 jQuery！
### 第1个API：addClass
功能：通过节点或选择器给元素添加一个类

### 第2个API：setText
功能：设置元素的文本内容

代码：

 html：

	<body>
	  <div>hello</div>
	  <div>hello</div>
	  <div>hello</div>
	  <div>hello</div>
	  <div>hello</div>
	</body>

 css： 

	div{
	  border:1px solid red;
	  width: 150px;
	  height: 25px;
	  margin-top: 10px;
	}
	.blue{  color:blue; }
	.high{  height:50px; }
	.narrow{  width:60px; }
此时效果为：

![原始结果](http://p8rplhkt6.bkt.clouddn.com/18-7-4/94812649.jpg)

 js：

	//jQuery就是一个函数，传进一个节点或选择器nodeOrSelector，返回一个对象nodes。
	window.jQuery = function(nodeOrSelector){
	  let nodes = {}
	  if(typeof nodeOrSelector === 'string'){
		//如果参数为字符串类型，也就是代表一个选择器，就获取到选择的所有元素存入nodes。
	    let temp = document.querySelectorAll(nodeOrSelector)
	    for(let i = 0; i<temp.length; i++){
	       nodes[i] = temp[i]
	    }
	    nodes.length = temp.length
	  }else if( nodeOrSelector instanceof Node){
	        //如果参数是一个节点，那就只存一个节点；为了返回结果的一致性，仍将其存为伪数组。
			nodes = {
	          0: nodeOrSelector,
	          length: 1
	        }
	  }
	  
	  //API1 添加一个类
	  nodes.addClass = function(class1){
	      for(let i = 0; i<nodes.length; i++){
	        nodes[i].classList.add(class1)
	      }
	    
	  }

	    //添加多个类
		//     nodes.addClass = function(classes){
		//       classes.forEach( (value)=>{
		//         for(let i = 0; i<nodes.length; i++){
		//           nodes[i].classList.add(value)
		//         }
		//       })
		    
		//     }

	  //API2 设置文本内容
	  nodes.setText = function(text){
	    for(let i = 0; i<nodes.length; i++){
	     nodes[i].textContent = text 
	    }
	
	  }
	  //nodes的key为0，1，2，...，length，addClass，setText等
	  return nodes  
	}
	
	window.$ = jQuery	//$为代替jQuery的缩写符,同时，在变量前加上$，可以区分jQuery与Dom的变量
	var $div = $('div')	//传入了选择器'div',$div即返回的对象nodes
	$div.addClass('blue')
	//$div.addClass(['blue','high','narrow'])//添加多个类
	$div.setText('hi') 


添加'blue'类的效果：

![结果1](http://p8rplhkt6.bkt.clouddn.com/18-7-4/73660343.jpg)

添加多个类的效果：

![结果2](http://p8rplhkt6.bkt.clouddn.com/18-7-4/88773623.jpg)
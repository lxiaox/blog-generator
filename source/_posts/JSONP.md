---
title: JSONP
date: 2018-08-17 10:22:50
tags: （W）jsonp
---

JSONP（全称是 JSON with Padding）是JSON的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。JSONP通过GET请求向服务器请求数据。

## 浏览器发送请求的历史

在了解JSONP之前，先来看看在JSONP之前浏览器是怎么向服务器发送请求的，前端程序员经过长时间的探索，曾先后使用过form、img等标签发请求，然而

+ form（可以发送post、get等请求）表单会刷新页面，在新的页面中显示成功或失败，这个时候可以将新页面展示在iframe中，但这专门用来防止刷新的iframe无疑是碍眼的；
+ img标签（发送get请求）只知道成功、失败，无法获取更多的数据；
+ a标签（发送get请求）同样会刷新页面；
+ link（发送get请求）只能以css、favcon的形式展示；

## SRC

那有什么办法能够更好的发送请求并得到数据呢？程序员发现script标签很好地实现了这种需求，并将这种解决策略称为**SRC**（Server Rendered JavaScript）即服务器返回JS。顾名思义，在这种方法中，浏览器向服务器请求script，服务器则进行相关操作，并返回一段JS数据告诉客户端也就是浏览器页面进行局部刷新。

接下来看客户端的代码：

	<body>
	    <p style="color:red;">您的余额是<span id=amount>&&&amount&&&</span></p>
	    <button id=button>付款</button>
	    <script>
	        $('#button').on('click',function(){
			   //首先新建一个scrippt标签，路径为/pay
	           let script=document.createElement('script') 
	           script.src='pay' 
	           document.body.appendChild(script)
			   //加载成功后删除这个script，节省内存
	           script.onload=function(e){
	                e.currentTarget.remove()
	            }
			   //script加载失败通知用户
	           script.onerror=function(e){
	                alert('fail'); 
	                e.currentTarget.remove()
	            }
	        })
	    </script>
	</body>

服务端代码：

	if(path === '/'){
	    let string=fs.readFileSync('./index.html','utf8')
	    let amount=fs.readFileSync('./db','utf8')
		//这里的db为自建的文件充当数据库
	    string=string.replace('&&&amount&&&',amount)
	    response.statusCode = 200
		//写响应头
	    response.setHeader('Content-Type', 'text/html;charset=utf-8')
		//响应体，即返回给浏览器的内容
	    response.write(string)
	    response.end()
	} else if (path === '/pay'){
	    let amount=fs.readFileSync('./db','utf8')
	    amount--	//付款1元，余额减1
		//新的余额写进数据库
	    fs.writeFileSync('./db',amount)  
	    response.statusCode = 200
	    response.setHeader('Content-Type', 'application/javascript;charset=utf-8')
		//这里是返回给客户端的JS代码
	    response.write(`
	      amount.innerText--
	    `) 
	    response.end()
	}

这就是SRC的流程，然而这段代码中还存在着一个问题，不难看出，这里是由后端代码返回操作页面的JS代码，这就要求后端程序员掌握前端代码写法，并且必须对页面内容非常地熟悉，我们把这种代码杂糅称为代码的耦合，那么，为了解决这个问题，就说到了今天的重头戏--JSONP。

## JSONP

上面说到了解决代码耦合，方法就是将上述后端写的前端代码，先封装为一个函数写在js中，发送script请求时，同时将这个函数作为请求参数传给服务器，这样后端就不需要写这些代码，只需要调用这个函数就行了。
代码修改如下：
	
	//1、客户端加上请求参数
	//注意，为了统一，请求参数的名字规定叫做callback，以便所有人使用
	script.src='/pay?callback=函数名'
	//2、封装函数，注意这里的函数名一般都加上随机以免造成变量名冲突。
	//例如: let 函数名 = 'xxx' + parseInt(Math.random()*10000,10)
	window.函数名=function(result){
            amount.innerText = result.left
    }

	//3、服务器，修改原来的请求头数据格式javascript为json
	response.setHeader('Content-Type', 'application/json;charset=utf-8')
	//4、修改响应第四部分，调用请求参数callback即我们传入的 函数
	response.write(`
	    ${query.callback}.call(undefined,{
	        "success":true,
	        "left":${amount}
	    })
	`)

在上面的服务器代码响应第四部分中，给函数传入了参数：

	${query.callback}.call(undefined,{
		"success":true,
		"left":${amount}
	})


这个参数包含了执行结果（成功）以及返回的数据（新的余额），这个参数的数据格式就是JSON对象，它左右的内容 `${query.callback}.call(undefined,` 与 `)`  分别是 左padding 和 右padding，这就是 `Json with Padding` 名字的由来。

当然，理论上这里的参数实际上并不一定需要JSON对象，只是对象能表示更多的数据，并且JSON对象能被JS解析，如果你想学习JSON，[点击去JSON官网](https://www.json.org/ "这里是JSON官网")。

## JSONP与跨域
上述讲了浏览器是怎么通过 JSONP 发送请求得到数据的，似乎还没提到怎么实现跨域。

>先来了解一下跨域：只有 **协议、域名、端口** 完全一样才被浏览器认为是同一个域，在一个网站中浏览器不能跨域执行另一个网站的脚本，这就是浏览器的 **同源策略**，也就是说你可以跨域发送请求，但是请求到的非同源数据会被拦截。浏览器的同源策略保护了数据的安全，但同时也造成了一些问题，比如一个公司有不同的子域需要互相访问，或者调用外部API，因此有时候我们就有了跨域的需求。

那么JSONP是怎么跨域的呢？我们已经知道了是 JSONP 通过 script 发送GET请求，事实上，**script 请求是不受同源策略限制的，请求到的script资源会被立即执行**，JSONP就是利用了这一特性来实现跨域。

## 总结

最后来总结一下 JSONP 的过程：

1. 请求方动态创建一个 script 元素，src 指向响应方，并传递一个 callback=xxx 的参数；
2. 响应方作出形如 callback.call(‘undefined’,‘要的数据’) 或者 callback('要的数据') 的响应；
3. 请求方接到响应，调用 xxx.call(‘undefined’,‘要的数据’)；
4. 这样请求方就得到了他要的数据。

+ 为什么JSONP不能发送POST请求？
答案：因为JONP是通过动态创建script标签实现的，script标签只能发送GET请求。

最后介绍一个jQuery使用JSONP的简单方法。

	$.ajax({
	    url: "http://xxx.com:8002/pay",
	    dataType: "jsonp",
	    success: function( response ) {
	        if(response === 'success'){
	            amount.innerText = amount.innerText - 1
	        }
	    }
	})
虽然名字叫 `ajax`，但是两者并没有任何联系，事实上应该叫做 `jsonp`。
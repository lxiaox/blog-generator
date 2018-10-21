---
title: AJAX
date: 2018-08-23 09:59:51
tags: （W）ajax
---
之前我们介绍了JSONP与跨域，JSONP是一种通过 script 发送请求的跨域技术，但是我们也提到了 jsonp 的缺点：

那就是 jsonp 是通过 script 只能发送 GET 请求，并只能以脚本运行。

那么有没有方式能实现各种请求方式`（get、post、put、delete...）`，并且我们想以什么方式展示都可以呢？

针对这个需求，微软率先做出了突破：

IE 5 在JS中引入了一个 ActiveX 对象，使得 JS 可以直接发起 HTTP 请求，随后 Mozilla、Safari、Opera 等浏览器也引进该对象。

该对象被纳入 [W3C](https://www.w3.org/Consortium/) 规范，取名为 `XMLHttpRequest` 。

## AJAX
使用上述对象  XMLHttpRequest 发送请求的步骤：

1. 使用 XMLHttpRequest 发请求，
2. 服务器返回XML格式的字符串（现在大多使用[JSON](https://www.json.org/)格式），
3. JS 解析 XML ，并更新局部页面。


[Jesse James Garrett](https://zh.wikipedia.org/wiki/%E5%82%91%E8%A5%BF%C2%B7%E8%A9%B9%E5%A7%86%E5%A3%AB%C2%B7%E8%B3%88%E7%91%9E%E7%89%B9) 将以上技术取名为 `AJAX` ，全称是 `Asynchronous JavaScript And XML`，意为异步的 JavaScript 和 [XML](https://zh.wikipedia.org/zh-hans/XML)。

## 用原生JS发 AJAX 请求实例
上文提到使用 AJAX 的基本步骤，现在写一个请求实例。
客户端JS代码：

	//页面中有一个 myButton 按钮，点击它发送请求。
	myButton.addEventListener('click',(e)=>{
	    //创建XMLHttpRequest对象
	    let request = new XMLHttpRequest()
	    //配置请求：动作，协议，域名，路径...
	    request.open('get','http://baidu.com/xyz')
	    //1、发送XML请求
	    request.send()
	    //2、服务器发送XML(JSON)字符串
	    //3、JS解析XML
	    request.onreadystatechange = ()=>{
	        if(request.readyState === 4){
	            if(request.status >= 200 && request.status <300){
	                let string = request.responseText
					//把JSON格式的字符串转换为JS对应值
	                let object = wndow.JSON.parse(string)
	            }else if(request.status >= 400){
        			console.log('说明请求失败') 
     			}
	        }
	    }
	})
服务端部分代码：

	if(path==='/xxx'){
	    response.statusCode = 200
		//设置响应第四部分数据格式为json格式
	    response.setHeader('Content-Type', 'text/json;charset=utf-8')
		//跨域
	    response.setHeader('Access-Control-Allow-Origin', 'http://abcdef.com:8001')
	    response.write(`
	    {
	      "note":{
	        "to": "B同学",
	        "from": "A同学",
	        "heading": "打招呼",
	        "content": "hi"
	      }
	    }
	    `)
	    response.end()

上述代码即使用AJAX发送请求，及服务器返回数据的过程。

其中值得注意的是：
 `response.setHeader('Access-Control-Allow-Origin', 'http://abcdef.com:8001')` 
这一行代码就是为了应对浏览器的同源策略（只有协议+域名+端口完全一致才能获取到请求的数据）的机制，

叫做 `CORS ( Cross-Origin Resource Sharing)`，即跨站资源共享。

代码中 `Access-Control-Allow-Origin` 告诉浏览器，允许后面的网页跨域访问。

## 封装一个 ajax()
为了方便使用AJAX发送请求，我们可以将上面的客户端代码封装成一个函数 ajax()：

	window.jQuery.ajax = function(url,method,body,headers,success, fail){
	    let request = new XMLHttpRequest()
	    request.open(method,url)
		for(let key in headers) {
     		let value = headers[key]
      		request.setRequestHeader(key, value)
    	}
	    request.onreadystatechange = ()=>{
	        if(request.readyState === 4){
	            if(request.status >= 200 && request.status <300){
	                success.call('undefined',request.responseText)
	            }else if(request.status >= 400){
	                fail.call('undefined',request)
	            }
	        }
	    }
	    request.send(body)
	}
这样我们使用的时候只需将： 请求方式，路径，请求体（请求第四部分），成功函数，失败函数 传 给 ajax() 即可。

事实上使用 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 升级这个 ajax() 使其更加方便使用。

	//这里我们可以将参数封装成一个对象（ES6语法,解构赋值）
	window.jQuery.ajax = function({url,method,body,headers}){
	    return new Promise(function(resolve, reject) {
	        let request = new XMLHttpRequest()
	        request.open(method, url)
			for(let key in headers) {
     			let value = headers[key]
      			request.setRequestHeader(key, value)
    		}
	        request.onreadystatechange = () => {
	            if (request.readyState === 4) {
	                if (request.status >= 200 && request.status < 300) {
	                    resolve.call('undefined', request.responseText)
	                } else if (request.status >= 400) {
	                    reject.call('undefined', request)
	                }
	            }
	        }
	        request.send(body)
	    })
	}

	//按以下方式调用
	jQuery.ajax({
	    url: '/xxx',
	    method: 'get'
	}).then(success, fail)

## AJAX 的功能
+ 客户端的 JS 发送请求
+ 服务端的 JS 发送响应

一、客户端 JS 设置请求各部分：

1. 第一部分 `request.open('get', '/xxx')`
2. 第二部分 `request.setHeader('content-type','x-www-form-urlencoded')`
3. 第四部分 `request.send('a=1&b=2')`

二、客户端 JS 获取响应各部分

1. 第一部分 `request.status（响应码） / request.statusText（响应码解释）`
2. 第二部分 `request.getResponseHeader() / request.getAllResponseHeaders()（一个或所有响应头）`
3. 第四部分 `request.responseText`

三、服务端 JS 获取请求各部分

1. 第一部分 `request.method，request.url`
2. 第二部分 `request.header`
3. 第四部分 `request.body`

四、服务端 JS 设置响应各部分：

1. 第一部分 `response.statusCode = 200`
2. 第二部分 `response.setHeader('Content-Type', 'text/html;charset=utf-8')`
3. 第四部分 `response.write('hi...')`
4. 响应结束 `response.end()`

### AJAX优缺点
1.优点：

+ 无刷新更新数据：以前是响应传回一个新的html文件，而Ajax无需传输不需要的未改变的数据，减少响应时间，提高用户体验
+ 异步执行：允许用户继续其他操作
+ 降低服务器负担：一些简单的判断操作可在客户端执行
+ 基于标准被广泛支持
+ 数据与页面分离

2.缺点：

+ 增加客户端负担
+ 不支持浏览器back按钮和history事件，即破坏浏览器机制
+ 破环了程序出错处理机制
+ 带来了安全漏洞
+ 其他：对搜索哦引擎支持弱，移动设备支持弱等

另：本文中使用了

+ [解构赋值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
+ [promise语法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
+ [回调函数](https://www.cnblogs.com/moltboy/archive/2013/04/24/3040213.html)
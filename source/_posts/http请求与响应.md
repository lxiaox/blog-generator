---
title: HTTP协议请求与响应
date: 2018-04-21 18:33:33
tags: （W）HTTP（入门）
---
## 1.协议概述
HTTP（英文全称：HyperText Transfer Protocol，中文：超文本传输协议）是一个客户端和服务器端之间请求和应答的标准。通常，由客户端发起一个HTTP**请求**到服务器上的指定端口（默认80端口），服务器则在端口接收客户端请求并作出**响应**。
   
   
## 2.请求部分
HTTP请求信息包括以下几点：
1. 请求行（动作 路径 协议/版本）
2. 请求头
3. 空行
4. 其他信息体（要上传的数据，可以为空）

+ 1中的动词为HTTP/1.1协议中定义的用来操作指定资源的方法，有GET、HEAD、POST、PUT、DELETE、TRACE、OPTIONS、CONNECT等。
+ 请求行格式为：key+英文:+空格+value（key: value)，可以有多行。
+ 路径不写时默认为/。
+ 请求的1、2、3部分必须包括，4部分可以为空。

### 请求举例
    GET / HTTP/1.1
    HOST: www.baidu.com
       
+ 第二行header作用为指定主机
+ 末尾加空行

   
## 3.响应部分
HTTP响应信息包括以下几点:
1. 状态行（协议/版本 状态码 状态路径）
2. 响应头（key: value)
3. 空行
4. 其他信息体（要下载的内容）

+ 状态码由3位数字组成，第一个数字代表当前应的类型
+ 1xx----请求已被服务器接受，继续处理
+ 2xx----请求成功
+ 3xx----重定向，文件暂时或永久地搬走了
+ 4xx----请求错误，无法被执行
+ 5xx----服务器发生错误
具体参见 [HTTP状态码](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)

### 响应举例
    HTTP/1.1 200 OK
    Content-Length: 0
    Content-Type: image/gif
        
+ Content-Type表示的是响应信息第4部分的格式
+ 末尾加空行
 
 
## 4.使用Chrome开发者工具查看 HTTP 内容
1. 打开 Network（在Chrome中点击鼠标右键→选择检查→点击Network）；
2. 在地址栏输入网址（eg：www.baidu.com）；
3. 点击第一个request；
4. 查看 Request Headers，点击 view source 即可看到上述**请求**信息；
5. 查看 Response Headers，点击 view source 即可看到上述**响应**信息；
6. 如果有第4部分，那么在 FormData 或 Payload 里面可以看到。

![](https://ws1.sinaimg.cn/large/d826ea31ly1fx9qrrros5j20n20bkq6j.jpg)	
 
 
## 5.使用curl命令发起请求
cURL是一个利用URL规则在**命令行**下工作的文件传输工具。

### 请求示例1
    curl -s -v -H "xxx: yyy" -- "https://www.baidu.com"
请求内容为：

    GET / HTTP/1.1
    Host: www.baidu.com
    User-Agent: curl/7.55.0
    Accept: */*
    xxx:yyy


响应内容为：

    HTTP/1.1 200 OK
    Accept-Ranges: bytes
    Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
    Connection: Keep-Alive
    Content-Length: 2443
    Content-Type: text/html
    Date: Sat, 21 Apr 2018 08:31:17 GMT
    Etag: "58860411-98b"
    Last-Modified: Mon, 23 Jan 2017 13:24:33 GMT
    Pragma: no-cache
    Server: bfe/1.0.8.18
    Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/
       

### 请求示例2
    curl -X POST -d "hello" -s -v -H "xxx: yyy" -- "https://www.baidu.com"
请求内容为：

    POST / HTTP/1.1
    Host: www.baidu.com
    User-Agent: curl/7.55.0
    Accept: */*
    xxx: yyy
    Content-Length: 5
    Content-Type: application/x-www-form-urlencoded
       

响应内容为：

    HTTP/1.1 302 Found
    Connection: Keep-Alive
    Content-Length: 17931
    Content-Type: text/html
    Date: Sat, 21 Apr 2018 08:36:38 GMT
    Etag: "54d9748e-460b"
    Server: bfe/1.0.8.18
       

* 举例中-X -d -s -v -H等均为curl参数，可根据需要改变。
* -X----指定什么命令
* -d----使用POST方式提交数据
* -s----silent静音模式，不输出任何东西
* -v----verbose详细，显示请求及响应
* -H----header，自定义头信息传给浏览器


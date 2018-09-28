---
title: Session学习
date: 2018-08-28 11:25:38
tags: （W）Session
---

上次学习了[登录注册与Cookie](https://lxiaox.github.io/2018/08/26/%E7%99%BB%E5%BD%95%E6%B3%A8%E5%86%8C%E4%B8%8Ecookie/)，Cookie用于保存用户登录信息。

Cookie过程如下：

1. 服务器服务器通过 Set-Cookie 头给客户端一串字符串
2. 客户端每次访问相同域名的网页时都带上这段字符串，也就是Cookie
3. 服务器通过Cookie读取用户id等，填充并返回相应页面
4. 客户端在一段时间内保存Cookie，Cookie默认网页关闭后失效，但后台可以设置过期时间。


但是Cookie存在一个问题，那就是用户是可以篡改Cookie信息的。`打开控制台->Application->Cookies`，我们就可以看到Cookie，改变它的值，如果我们把id改为别的id，那就可以直接登录别人的账户，这是非常不合理的。

![控制台Cookies](http://p8rplhkt6.bkt.clouddn.com/18-9-11/59114318.jpg)

所以我们用到另外一种技术：
### Session

如果把Cookie理解为公园的一张门票，上面记录了你的姓名，性别等信息，那么Session就像是一张保密的门票，它只记录你的‘入场号’，而你的信息则存在与公园内部的记录册中，所以当你把门票出示给工作人员时，他仍可以根据入场号搜索到你的姓名，并说欢迎您，xxx。

Session的工作原理正是如此：

1. 当用户登录后，服务器就会给用户生成相应的随机数，SessionID
2. 将SessionID**通过Cookie**返回给客户端
3. 客户端再次访问这个服务器的时候，带上这段Cookie
4. 事实上服务器上有hash表存储了所有的Session，当服务器读取到了SesssionID，就可以找到对应的Session
5. 最终得到用户的隐私信息，如id，邮箱。

#### Cookie、Session存储位置
Cookie是保存在客户端的，每次都随着请求发送给服务器。

而Session是存储在服务器端的，每次通过Cookie将SessionID发送到服务器。

Seesion缺点：所有用户的Sessioon都存储在服务器，这是很占内存的。


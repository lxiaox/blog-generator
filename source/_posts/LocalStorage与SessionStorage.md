---
title: LocalStorage与SessionStorage
date: 2018-08-30:11:18
tags: （W）Web Storage
---
### 在学习LocalStorage前先来看一下，JS中变量有什么问题：

	<script>
	    var age = 18
	    console.log('age = ' + age)
		//结果输出 age = 18
	</script>

在页面中改变变量 age 的值：

![age](http://p8rplhkt6.bkt.clouddn.com/18-9-11/55819352.jpg)

现在的 age = 19

但是，刷新页面之后呢？

![age](http://p8rplhkt6.bkt.clouddn.com/18-9-11/16450453.jpg)

可以看到刷新之后页面中的age值已经又变回了 18，这就是问题所在。

### 有什么办法可以使一个变量一直存在页面中或者从一个页面跳到另一个页面时值不变呢？答案就是 将变量保存在 LocalStorage里。

LocalStorage是不存储在页面中的，它存储在C盘（windows）的一个文件中。 

使用localStorage存变量：

	<script>
	    let age = localStorage.getItem('age') //读取名为age的变量值
	    if(! age) {
	        age = 18
	    }else {
	        age = (+age) + 1 //（+age）将age变成数字，同 parseInt(age, 10)
	    }
	    console.log('age = ' + age)
	    localStorage.setItem('age', age) //将age存进localStorage
	</script>

这样每次刷新都会将age加1，不会覆盖之前作的改变。

打开控制台->Application->Local Storage，可以看到：

![图0](https://ws1.sinaimg.cn/large/d826ea31ly1fx9r4zw6osj20ki06xt8x.jpg)

可以看到当前的age值为 27，可以拉动下面的框，出现 key-value

![图1](http://p8rplhkt6.bkt.clouddn.com/18-9-11/13943624.jpg)

控制台打印：

![图2](https://ws1.sinaimg.cn/large/d826ea31ly1fx9r2960l0j208y0490sl.jpg)

### localStorage典型应用：记录是否提示过用户
代码如下：

	let prompted = localStorage.getItem('是否提示')
    if(!prompted){
        alert('这里是提示内容...')
        localStorage.setItem('是否提示',true)
    }
只有第一次进去页面会有此提示：

![图5](https://ws1.sinaimg.cn/large/d826ea31ly1fx9r68yhbwj20cm03zt8l.jpg)

点击确定会看到localStorage增加了一项 `是否提示：true` ：

![图6](https://ws1.sinaimg.cn/large/d826ea31ly1fx9r28qtbjj20kc04waa4.jpg)


### localStorage接口

1、增加一个数据项: 

	localStorage.setItem('name', 'xiaoxiao')

2、读取一个localStorage项：

	localStorage.getItem('name')    //xiaoxiao
	localStorage.name    //xiaoxiao

3、读取所有localStorage项：

	localStorage.valueOf()    //Storage {age: "33", name: "xiaoxiao", length: 2}

4、读取第i项变量名：

	localStorage.key(i)    //length不算在里面

5、读取localStorage项数：

	localStorage.length    //2，只有age和name

6、移除一个localStorage项：

	localStorage.remove('name')

7、移除所有localStorage项：

	localStorage.clear()

8、检查localStorage里是否保存某个变量：

	localStorage.hasOwnProperty('name') //true

9、将数组转为字符串：

	localStorage.array = [1,2,3,4]  //[]
	localStorage.array.toLocaleString()   //"1,2,3,4"

10、存储JSON对象为字符串：

	let sisters = {
        xiaoxiao: {
            name: "xiaoxiao",
            age: 10
        },
        xiaolu: {
            name: "xiaolu",
            age: 8
        }
    }
	localStorage.sisters = window.JSON.stringify(sisters)
	//	"{"xiaoxiao":{"name":"xiaoxiao","age":10},"xiaolu":{"name":"xiaolu","age":8}}"

	window.JSON.parse(localStorage.sisters) //可将字符串还原为对象

### SessionStorage与localStorage比较

SessionStorage作用与用法LocalStorage基本相同，不同的是，localStorage是永久有效的，除非用户清理缓存，但是sessionStorage会在页面会话后就清除。

**页面会话**：在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。

要注意的是：localStorage和sessionStorage都是仅限于页面的协议，虽然没有同源策略那么严格，但也只有相同域名的页面才能互相读取。

#### sessionStorage用法与localStorage差不多，简单介绍：

	// 保存数据到sessionStorage
	sessionStorage.setItem('key', 'value');
	
	// 从sessionStorage获取数据
	var data = sessionStorage.getItem('key');
	
	// 从sessionStorage删除保存的数据
	sessionStorage.removeItem('key');
	
	// 从sessionStorage删除所有保存的数据
	sessionStorage.clear();

### localStorage与cookie比较

事实上，localStorage是一个新的对象，为了使前端能够存储数据创建，以前都是由cookie完成，但是cookie要上传到服务器，使得页面加载非常地慢速，所以现在不推荐使用cookie，他们两者主要区别是：

+ cookie需发送到服务器，localStorage与HTTP请求无关。
+ cookie最大存储量在4kb左右，localStorage在5Mb左右（不同的浏览器各不相同）。
+ cookie默认在页面关闭后清除（后端可以设置清除时间），LocalStorage理论上永久有效，除非用户清理缓存。

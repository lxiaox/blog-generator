---
title: canvas的使用
date: 2018-09-1 14:11:49
tags: （H）canvas的使用
---
## 一、canvas的作用

canvas是一个HTML元素，可以使用脚本（如JS）绘制图形，制作照片，动画，甚至实时视频处理渲染。

## 二、属性
canvas和img元素很像，但是没有src和alt属性，只有width和height两个属性（默认300px，150px）

## 三、替代内容
跟audio/vedio等标签很像，直接将替代内容写在标签里面。比较老的不支持canvas的浏览器会展示替代内容，支持的会忽略替代内容。

	<canvas id="canvas" width="150" height="150">  
		//这里写替代内容，文字或图片等等。
	</canvas>

## 四、标签不可省
不同于img标签，canvas需要闭合。

`</canvas>结束标签`没有时，后面的内容都将作为替代内容。

## 五、JS使用
canvas创造了一块空白大小的空白画布（渲染上下文（名词）），它有一个 getContext()方法，可以获取到渲染上下文和绘画功能，它有一个参数，比如2D图形：

	var canvas = document.getElementById('canvas')
	var ctx = canvas.getContext('2d')
	//or
	var ctx = document.getElementById('canvas').getContext('2d')


也可以检查浏览器是否支持canvas，代码改为

	if (canvas.getContext){
  		var ctx = canvas.getContext('2d');
	}else{}

## 六、绘制图形
首先要了解：如[100px*100px]的canvas画布的坐标空间，在左上角坐标为(0,0)，向右延申为x轴，向下为y轴，右下角坐标为(100,100)。

### 1、三个画矩形的方法

1. fillRect(x,y,width,height): 实心矩形。
2. strokeRect(x,y,width,height)：空心矩形，即矩形边框。
3. clearRect(x,y,width,height)：清除该矩形区域。

### 2、路径/画线

1. beginPath()：新建一条路径
2. closePath()：关闭一条路径（非必需），（将笔触从当前移动到起始位置，可能会画一条直线）
3. fill()：填充路径内容（会自动关闭路径）
4. stroke()：路径描边
5. moveTo(x,y)：移动笔触
6. lineTo(x,y)：从当前位置画线到(x,y)

code:

	//画一个三角形
	ctx.beginPath()
	ctx.moveTo(100,100)
	ctx.lineTo(150,50)
	ctx.lineTo(150,150)
    ctx.fill()	//不写fill或stroke不会显示东西

	//不管画什么都要写ctx.fill()/stroke()
	//不管画什么都要写ctx.fill()/stroke()
	//不管画什么都要写ctx.fill()/stroke()

### 3、圆/圆弧

+ arcTo(x1, y1, x2, y2, radius)：不可靠不作介绍


+ arc(x, y, radius, 起始弧度, 结束弧度, 方向)：

	1. 弧度的计算：180°为Π（Math.PI），公式：角度/180*Math.PI = 弧度。
	2. 弧度为零：圆心的水平向右方向。
	3. 方向：true逆时针，false/不写 顺时针
	
举例

	//画圆
	ctx.arc(100,100,50,0,Math.PI*2)
	//圆弧
	ctx.arc(100,100,50,0.3,6,true)
	//填充圆（弧）
	ctx.fill()
	//描边
	ctx.stroke()

### 3、二次/三次 贝塞尔曲线

1. quadraticCurveTo(x0,y0,x1,y1): 二次，起点（控制点）（x0,y0），终点（x1,y1）
2. dezierCurveTo(x0,y0,x1,y1,x2,y2)：三次，控制点1/2：(x0,y0)/(x1,y1)，结束点：(x2,y2)

虽然不熟悉贝塞尔曲线，但通过多次绘制它可以用来绘制有用的图形：
	
	//二次
	 ctx.beginPath();
	 ctx.moveTo(75,25);
	 ctx.quadraticCurveTo(25,25,25,62.5);
	 ctx.quadraticCurveTo(25,100,50,100);
	 ctx.quadraticCurveTo(50,120,30,125);
	 ctx.quadraticCurveTo(60,120,65,100);
	 ctx.quadraticCurveTo(125,100,125,62.5);
	 ctx.quadraticCurveTo(125,25,75,25);
	 ctx.stroke();

结果图：

![对话框](http://p8rplhkt6.bkt.clouddn.com/18-9-26/124307.jpg)

还可以用三次贝塞尔曲线画心型等等。


### 4、Path2D
可以把创建的图形存为path2D对象，再引用它们。

code:
	
	ctx.strokeStyle = "red"
	ctx.fillStyle = "#00eeee"
	//存对象
    var rectangle = new Path2D()
    rectangle.rect(10, 10, 50, 50)

    var circle = new Path2D();
    circle.arc(100, 35, 25, 0, 2 * Math.PI)
	//用对象
    ctx.stroke(rectangle);
    ctx.fill(circle);	

结果：

![path2d](http://p8rplhkt6.bkt.clouddn.com/18-9-26/97079506.jpg)

### 5、使用SVG paths
获取路径时以svg或canvavs方式重用：

	var p = new Path2D("M 80 20 h 20 v 80 h -80 Z");
	ctx.fill(p)
	//M 80 20 这条路径先移动到点（80，20），
	//h 20 向右移20
	//v 80 向下移80
	//h -80 向左移80
	//z  回到起点

结果图：

![svg](http://p8rplhkt6.bkt.clouddn.com/18-9-26/13245959.jpg)

## 七、指定颜色
如：

	ctx.fillStyle = "red"	//指定填充颜色为红色
	ctx.strokeStyle = "green"   //指定描边为绿色

## 八、指定透明度
如：

	ctx.fillStyle = "rgba(0,0,0,0.5)"

### 所有图形的透明度

	ctx.globalAlpha =  0.2
	//透明度取值为0.0(完全透明)-1.0(完全不透明)

## 九、线条样式

1. lineWidth=：线条宽度
2. lineCap=：线条末端
	+ （butt 默认，不加）
	+ （round 加半圆半径为线条宽度一半）
	+ （square 加方形）
3. lineJoin=：线条连接处
	+ （miter 默认，尖角）
	+ （bevel 平）
	+ （round 圆弧）
4. miterLimit=：连接处最大长度（内角顶点~外角顶点）
5. setLineDash()：虚线样式，接受一个数组，指定线段与间隙交替
6. getLineDash()：返回含虚线样式的数组
7. lineDashOffsest=：设置虚线偏移量。通过循环改变偏移量，有虚线在动的效果，通过延时函数控制速度。

虚线例子：
	
	  ctx.setLineDash([4, 2])
	  ctx.lineDashOffset = 10
	  ctx.strokeRect(100,20, 100, 100)
结果：

![虚线](http://p8rplhkt6.bkt.clouddn.com/18-9-26/25096540.jpg)

## 九、渐变Gradient

1. 创建Gradient对象（并定义渐变位置）
	+ createLInearGradient(x1,y1,x2,y2)：线性的渐变，参数为起点和终点。
	+ createRadiusGradient(x1,y1,r1,x2,y2,r2)：圆形，参数为两个圆圆心和半径。
	
2. 渐变颜色
	+ gradient.addColorStop(position,color)：参数为欸位置（0.0~1.0）和颜色。

3. 把gradient对象赋给fillStyle/strokeStyle

举例：

	//1.创建对象，定义位置
    var gradient = ctx.createLinearGradient(0,0,0,150)
	//2、定义颜色
	//0-0.5：蓝-绿
	//0.5-1：红-白-黑
    gradient.addColorStop(0, '#0000ff')
    gradient.addColorStop(0.5, '#00ff00')
  	gradient.addColorStop(0.5, '#ff0000')
    gradient.addColorStop(0.75, '#fff')
  	gradient.addColorStop(1, '#000')

  	// 3、将 渐变对象 赋给fillStyle
  	ctx.fillStyle = gradient
	ctx.strokeStyle = gradient

  	// 4、画图
  	ctx.fillRect(10,10,100,130)
    ctx.strokeRect(130,10,100,130);

结果图：

![渐变](http://p8rplhkt6.bkt.clouddn.com/18-9-26/43135778.jpg)

## 十、添加图案 Pattern
将image对象赋给图案，将图案作为填充样式：代码

	//1、创建image对象
	var img = new Image();
  	img.src = '图片路径';
  	img.onload = function(){
	    // 2、用image，创建图案
	    var ptrn = ctx.createPattern(img,'repeat');
		// 3、用图案作填充样式
	    ctx.fillStyle = ptrn;
	    ctx.fillRect(0,0,350,350);
  	}
结果：

![图案](http://p8rplhkt6.bkt.clouddn.com/18-9-26/83555573.jpg)

## 十一、阴影shadows
1. shadowOffsetX = float
shadowOffsetX 和 shadowOffsetY ：向右延申距离
2. shadowOffsetY = float：向下延申距离
3、shadowBlur = float：阴影模糊程度
4、shadowColor = color：阴影颜色

## 十二、绘制文本

1. ctx.fillText('kakami',10,10)：填充文字和位置
2. ctx.strkeText('kakami',10,10)：只描边的文字
3. ctx.font = "48px serif"：设置font
4. ctx.textAlign=start(默认)/end/left/right/center：文字对齐方式
5. textBaseline = top/hanging/middle/bottom/alphabetic(默认)/ideographic：基线对齐方式
6. direction = ltr/rtl/inherit(默认)

## 一些注意事项
1. 画完一个（描边）图形之后，没有再次写ctx.beginPath()就画一个填充图形，那第一个图形也会被填充。
2. 一定要写fill/stroke()
3. 使用封装函数对于减少代码量以及复杂度十分有用，如roundedRect()
4. roundedRect(ctx,10,10,5,5,3)能画圆角矩形。
5. [MDN有关canvas](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Drawing_text)



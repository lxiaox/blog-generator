---
title: css布局
date: 2018-05-27 13:04:48
tags: css布局
---
本文主要介绍以下几点

+ 左右布局
+ 水平居中
+ 垂直居中

***
## 左右布局（两个子元素或以上）
1. **利用浮动**<br>
给所有子元素添加属性`float:left/right`，父元素添加clearfix类，可使子元素从左至右排列，同时添加
`margin`可增加元素间距。但是当宽度大于父元素宽度时，子元素会换行显示。
2. **利用绝对定位**<br>
父元素添加`position:relative`，所有子元素添加`position:absolute`，使子元素脱离文档流，再利用`top: px`使子元
素顶部对齐，同时使用left属性调整左右位置。


## 水平居中
+ **行内元素&类行内元素（文本、链接等）**<br>
	1. 在块级父容器中让行内元素居中，只需在**父元素**中使用`text-align: center;`<br>
这个方法可使`inline`、`inline-block`、`inline-table`、`inline`、`flex`等类型的元素水平居中。
+ **块级元素（确定宽度）**<br>
	1. **法一**：将子元素`margin-left`、`margin-right`均设置为`auto`。(不确定宽度时会拉至与父元素等宽。)<br>
	2. **法二**：利用绝对定位，将子元素`left`设置为父元素宽度的一半，同时`margin-left`设置为子元素宽度一半的**负值**。
+ **块级元素（不确定宽度）**<br>
	1. **法三：**利用绝对定位，并将子元素`top`、`left`、`right`、`bottom`均设置为0，这个方法会将子元素的宽高都拉至与父元素等宽高。<br>
	2. **法四：**利用绝对定位，将子元素`top`、`left`设置为`50%`，并添加`transform: translate(-50%, -50%);` 可使子元素水平且垂直居中。<br>其中`left`、`translateX(-50%)`实现水平居中。<br>
	3. **法五：** flex布局：在**父元素**中添加`display:flex;`、`justify-content:center;//水平居中`、`align-items: center;//垂直居中` 即可使子元素水平且垂直居中。
+ **多个块级元素**<br>
	1. 对所有子元素使用`display:inline-block;`，在父元素上使用`text-align:center;`即可。
	2. 见**法五**。

## 垂直居中
+ **行内元素**<br>
	1. 在**父元素**中使用`display:table-cell;`、`vertical-align:middle;` 即可使子元素垂直居中。
+ **块级元素（确定高度）**<br>
	1. 同理**法二**，利用绝对定位，将子元素`top`设置为父元素宽度的一半，同时`margin-top`设置为子元素宽度一半的 **负值**。
+ **块级元素（不确定高度）**<br>
	1. 见**法三**。
	2. 见**法四**。其中`top`、`translateY(-50%)`实现垂直居中。
	3. 见**法五**。
+ **多个块级元素**<br>
	1. 见**法五**。

## 总结居中
+ **行内元素**
	1. 水平居中：在父元素中使用`text-align: center;`
	2. 垂直居中：在父元素中使用`display:table-cell;`、`vertical-align:middle;`
+ **块级元素(确定宽高)**
	1. 利用`margin:auto`：<br>
		a.水平居中：`margin-left`、`margin-right`均设置为`auto`。<br>
		b.垂直居中不适用。 
	2. 绝对定位 + margin负值。
	3. 绝对定位 + transform
	4. flex布局
+ **块级元素(不确定宽高)**
	1. 绝对定位 + transform
	2. flex布局
+ **多个块级元素**
	1. 对所有子元素使用`display:inline-block;`，在父元素上使用`text-align:center;` (只适用于水平居中)。
	2. flex布局


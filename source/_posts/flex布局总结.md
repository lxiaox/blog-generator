---
title: flex布局总结
date: 2018-09-21 21:47:00
tags: （C）flex布局
---
今天发现flex布局很多没有经常使用的属性，特来总结。

弹性盒子（Flex Box）是CSS3新出的一种布局模式。它主要是将容器内元素进行合理排列、对齐以及分配空白空间。它的优点是响应式布局，使得页面适用于不同设备，不同大小的屏幕。

方法：在父元素上添加样式:

	.parent{
		display: flex;
	}
或者：

	.parent{
		display: inline-flex;
	}
如此使该父容器中的子元素按横向排列（默认）。

[青蛙跳荷叶的游戏网站](http://flexboxfroggy.com/#zh-cn) 帮助学习flex布局各种属性。

### flex-direction 选择子元素排列方向
该属性有四个值：

1. row：横向，从左至右。(父子左对齐，超出在右边）
+ row-reverse：横向：从右至左。(父子右对齐，超出在左边）
+ column：纵向，从上至下。（父子上对齐，超出在下面）
+ column-reverse：纵向，从下至上。（父子下对齐，超出在上面）

另：`body { direction: rtl; }`也可以修改排列方向为从右至左。

### justify-content 子元素沿容器主轴线对齐方向
五个属性值：

1. flex-start: 元素紧挨行头。
+ flex-end: 元素紧挨行尾。 
+ center: 元素靠向容器中间。
+ space-between:元素之间保持相等的距离。
+ space-around:元素周围保持相等的距离。（区别在于多了首尾两边的空白）

这时主轴线可以理解为 `第一个元素` 到 `最后一个元素` 连线（一行）的方向。

根据flex-direction的取值不同，行头行尾随之变化。

比如：row：行头在左边， row-reverse：行头在右边。

总之：行头在第一个元素所在侧，行尾是最后一个元素那侧。

### align-items 子元素沿容器侧轴对齐方向
侧轴与主轴垂直。
属性值如下：

1. flex-start：子元素靠侧轴起始位置。（上或左）
2. flex-end：子元素靠侧轴结束位置。（下或右）
3. center：在侧轴方向居中。（如果溢出是同时向两边溢出）
4. baseline：元素在容器的基线位置显示。
5. stretch: 元素被拉伸以填满整个容器。（也受'min/max-width/height'属性的限制。）

### flex-wrap 属性
各个值解析:

1. nowrap：（默认），子元素在同一行。可能会溢出。
2. wrap: 溢出部分会换行。
3. wrap-reverse：行之间排列反转。比如第一行在最下面。

### flex-flow: 
是flex-direction和flex-wrap的简写

`如：flex-flow: column wrap`

### align-content 属性

1. stretch：（默认）各行将会伸展以占用剩余的空间。
2. flex-start： 各行向容器的起始位置堆叠。
3. flex-end：各行向容器的结束位置堆叠。
4. center：各行向弹性盒容器的中间位置堆叠。
5. space-between：行与行之间保持相等的距离。
6. space-around：行与行周围保持相等的距离。


## 以上都是定义在父元素身上的属性，现在来看子元素：

### order 排列顺序
用整数值表示排列顺序，可以为负数，小的排在前面。
 
 + 当几个元素为同值，他们之间按原顺序。

比如将第三个子元素排在最前面:

 `.child3{ order: -1; } //其他子元素不设置 `

为什么设为 -1 ？

将child3设为order：0 时，它仍排在child1、child2后面。可以猜测默认所有元素 order 值为 0。

### margin: auto

1. 比如某一个子元素设置：`margin-left: auto`,那么所有空白都集中在它左侧。
2. 所有子元素设置为：`margin: auto`,可以实现所有元素居中。

### align-self
值同align-items，区别在于：align-items针对所有子元素，align-selgf只管一个。

1. auto
2. flex-start
3. flex-end
4. center
5. baseline
6. stretch

### flex
flex三个属性：

1. flex-grow：扩展比率。值必须为无单位数。默认为1。负值无效。
2. flex-shrink：收缩比率。值必须为无单位数。默认为1。负值无效。
3. flex-basis：基本宽度/高度。值必须为**各种**有效宽度值（0必须带单位）。默认为0%。

##### 所谓扩展是指子元素伸展占领空白区的比率；收缩也是针对溢出的宽高。

#### 语法：
1、`flex: [flex-grow] [flex-shrink] [flex-basis];`

	.child1{ flex: 1 0 30px; }
	
	//child1可扩展，可收缩，基值30px（一般大于或等于30px）

2、

1. `flex: auto`: 计算值为 1 1 auto
+ `flex: initial`: 计算值为 0 1 auto
+ `flex: none`：计算值为 0 0 auto
+ `flex: inherit`：从父元素继承

#### 单/双值：
1. 三个值按顺序赋给相应属性；
2. flex只有一个数会作为flex-grow；
3. 两个数第一个给flex-grow，第二个给flex-shrink；
4. 一个数一个宽度值：数给flex-grow，宽度给flex-basis。

举例：

	.child1{
		flex: 2; //扩展，将空白部分的2/4分配给child1
	}
	.child2{
		flex: 1; //扩展，将空白部分的1/4分配给child1
	}
	.child3{
		flex: 1; //扩展，将空白部分的1/4分配给child1
	}
	//并不表示child1宽度是child2或child2的两倍。
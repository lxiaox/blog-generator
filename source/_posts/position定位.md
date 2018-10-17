---
title: position定位
date: 2018-8-11 15:29:14
tags: （C）position
---
## 取值（5）：
### static：

+ 元素在文档流中的正常位置
+ top, right, bottom, left 和 z-index 属性无效。
### relative：

+ 对table元素无效
+ 不脱离文档流
+ 相对正常位置进行偏移
+ 元素原位置会留下空白。

### absolute：

+ 脱离文档流，
+ 相对最近非static的祖先元素的定位
+ 设置margin不会与其他元素合并。


### fixed：

+ 固定定位
+ 脱离文档流
+ 相对浏览器视口定位，滚动屏幕，位置固定
+ 元素祖先的transform为 非none时，相对该祖先定位


### sticky：

+ 粘性定位
+ 相对定位relative和固定定位fixed的结合
+ 对table元素无效
+ 指定top、bottom、left、right后粘性定位生效，且不影响后面元素布局。
+ 相对最近的BFC和块级元素祖先定位
+ 举例：#one{position:sticky;top:10px}，元素初始top为50px，滚动屏幕使它top<10px时，粘在top=10px的位置。


### top、bottom、left、right

+ 定位元素（上、下、左、右）外边距边界与其包含块（上、下、左、右）边界之间的偏移
+ 非定位元素设置此属性无效
---
title: JS中的数据类型
date: 2018-06-09 23:07:26
tags: （J）JS-数据类型
---
### js共有七种数据类型：number、string、boolean、symbol（ES6新增）、null、undefined、object
> 通常，数值、字符串、布尔值这三种类型，合称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于undefined和null，一般将它们看成两个特殊值。
## 数值（number）：
>JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。

+ 整数和小数（比如`1`、`1.1`、`.1`)。
+ 也可用 科学记数法 表示: `1.23e2 = 123`。
+ 二进制表示：前缀`0b`。
+ 八进制表示：前缀`0`（后ES5添加`0o`）。
+ 十六进制：前缀`0x`。
+ ES即ECMAScript：标准化JavaScript。
## 字符串（string）：
定义：零或多个排在一起的字符，使用''或""表示。

+ `''`中可以使用`""`或`"`，`""`中可以使用`''`或`'`。
+ 在单(双)引号中使用单(双)引号：`\'` `\"`。

字符串只能写在一行，如果想分多行写，可以:

+ 在每一行尾加 `\`，但`\`后只能接回车换行，尤其注意不能有空格，非常坑，别这样写！
+ 使用连接符`+`，行尾行首均可。
+ 使用反引号包住多行代码，但字符串中会增加`换行`字符。
## 布尔值（boolean）：
只有表示真伪的两个特殊值，即`true`真 和 `false`假。
<table>
<tr><th>会返回布尔值的运算符<td>> 两元逻辑运算符： && (And)，|| (Or)<br>> 前置逻辑运算符： ! (Not)<br>> 相等运算符：===，!==，==，!=<br>> 比较运算符：>，>=，<，<=
<tr><th>会转为false的值<td>undefined、null、false、null、0、NaN、空字符串
<tr><th>会转为true的值<td>除上述的其他。包括[]、{}
</table>
## symbol:
symbol用来生成一个全局唯一的值，但并不是字符串。symbol的名字与值无关。
## undefined：
表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值。一般用于不赋值的**非对象**：`var n`，但不是规定。
## null：
表示空值，即此处的值为空。一般用于不赋值的**对象**。null转为数值时自动转为0，这样不便发现错误，于是JS之父Brendan Eich又设计了undefined，它会转为`NaN`(非数，特殊的数值)。
<br>一个null的特例：`typeof null`值为`Object`,其它数据类型均为自身。
## 对象（object）：
对象是JS核心概念，也是最重要的数据类型。对象就是各种键值对组成的集合`(key-value)`，是以上几种基本类型的**无序**的组合。

+ object中所有`key`均为`string`，**字符串**。全为数字或符合标识符规范的可不加引号。
+ object中所有`value`可以为各种类型和function。类型为string时必须加引号。
+ `Object['key']`，`key`必须加引号，`Object[key]`不加引号时`key`是变量，key全为数字除外，会自动转为字符串。
+ `Object['key']`可以写成`Object.key`，key全为数字除外，会将`.`看成小数点。
+ `Object[表达式]`是正确的，`Objecct['H'+'H']=Object['HH']`，注意数值键不加引号时`Objecct[1+2]=Object[3]`。
+ `delete object['key']`可以删除`key&value`，`object['key'] = undefined`只删除`value`。
+ `for(var key in Object)`可遍历对象所有可以遍历的属性，包括可以遍历的继承属性。
+ `Object.keys()`API可以查看对象所有key。
+ 在行首的`{'x':'y'}`均看作代码块，所以对象要写成({'x':'y'})。
## typeof操作符
`typeof`运算符可以返回一个值的数据类型。
<center>
<table>
<tr><th>各种值<th>typeof 值
<tr><td>string<td>'string'
<tr><td>number<td>'number'
<tr><td>boolean<td>'boolean'
<tr><td>symbol<td>'symbol'
<tr><td>undefined<td>'undefined'
<tr><td>null<th>'object'
<tr><td>object<td>'object'
<tr><td>function<th>'function'
</table>
<center>
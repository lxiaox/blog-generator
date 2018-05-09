# HTML常用标签及简单介绍
本文介绍内容主要分为HTML结构、标题标签、段落标签、图形标签、一些常用标签、制表、表单、框架标签、超链接标签、字符控制、列表控制以及多媒体等。


## HTML结构
<table style="border-collapse:collapse">
<tr><td><th>标签<th>描述
<tr><td><td>DOCTYPE<td>指定文件类型，如html5中:<br>&lt;!DOCTYPE html>
<tr><td><td>html<td>文档的根元素
<tr><td><td>head<td>网页中顶级元素，一般包含浏览器环境设置部分
<tr><th rowspan=5 width=4>head嵌套<td>title<td>
<tr><td>style<td>设置html元素的样式
<tr><td>script<td>定义网页使用哪种脚本语言
<tr><td>meta<td>定义网页元数据，如文档关键字、描述和作者信息
<tr><td>object<td>定义对象
<tr><td><td>body<td>包含显示在浏览器可视区的信息主体，及正文部分
</table>

## 标题标签&lt;h1>~&lt;h6>
<table style="border-collapse:collapse">
<tr><th>标签<th>示例
<tr><td>h1<td><h1>一级标题</h1>
<tr><td>h1<td><h2>二级标题</h2>
<tr><td>h3<td><h3>三级标题</h3>
<tr><td>h4<td><h4>四级标题</h4>
<tr><td>h5<td><h5>五级标题</h5>
<tr><td>h6<td><h6>六级标题</h6>
<tr><th>标题align属性<th>中间对齐方式
<tr><td>left<td>左对齐
<tr><td>right<td>右对齐
<tr><td>center<td>中间对齐
<tr><td>justify<td>两边对齐
</table>

## 段落标签&lt;p>
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td>p<td>用于在网页中显示一个段落
<tr><td colspan=2>align属性对齐方式与&lt;h1>方式一致
</table>

## 图形标签&lt;img>
img是一个空元素，不需要结束元素,一般格式如下：

	&lt;img src="" width="" height="" alt="">
1. src属性为img元素的必选属性，用于指定图形文件的路径，由URL确定，可以是本地资源，也可以是远程资源。
2. width和height属性分别表示图形显示在浏览器中的宽度和高度，为可选属性。
3. alt表示图片不能正常显示时的替换文字。
4. align属性<table style="border-collapse:collapse">
<tr><th>align属性值<th>对齐方式
<tr><td>left<td>把图像和左边界对齐
<tr><td>right<td>把图像和右边界对齐
<tr><td>center<td>把图像居中
<tr><td>middle<td>把图像中部和行的中部对齐
<tr><td>top<td>把图像和同行中的最高部分对齐
<tr><td>bottom<td>把图像的底部和和同行文本的底部对齐
<tr><td>texttop<td>把图像和同行中的最高文本的顶部对齐
<tr><td>absmiddle<td>把图像中部和同行中最大顶的中部对齐
<tr><td>absbottom<td>把图像的底部和同行中的最大顶对齐
<tr><td>baseline<td>把图像的底部和文本的基线对齐
<tr><td colspan=2>**通过设置align属性可以达到图文环绕的效果**
</table>

## 一些常用标签
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td>&lt;!--注释--><td>注释多行内容。<br>快捷方式：选中想注释掉的文本内容，按键盘Ctrl+/。
<tr><td>hr<td>在网页中画一条横线
<tr><td>br<td>另起一行
<tr><td>center<td>使内容居中显示
<tr><td>div<td>定义一个块级容器，用来规划网页
<tr><td>span<td>定义一个行内容器
</table>

## 制表标签
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td>table<td>建立表格的主要元素。含border，bgcolor，bordercolor等属性。
<tr><td rowspan=2>caption<td>用于把一行文本置于表格上方或下方
<tr><td>&lt;caption align="top/bottom">表格标题&lt;/caption> 
<tr><td>thead<td rowspan=3>分别定义表格的表头，表体和底部，书写顺序不影响其先后顺序。
<tr><td>tbody
<tr><td>tfoot
<tr><td>tr<td>定义表格中的一行。属性有align、bgcolor、border、bordercolor、nowrap（禁止浏览器对单元格中的内容产生换行）、valign（设置单元格内容在垂直方向的对齐方式：top、middle、bottom）
<tr><td>th<td>与td用法一致，但内容以粗体显示，可用来设计表格的表头。
<tr><td>td<td>定义一行中的一列，又叫单元格。具有colspan和rowspan属性，即一个单元格所占的列数和行数，可设置单元格合并;可设置宽高width、height，align等。
<tr><td rowspan=2>colgrop<td>设置某一列的width和bgcolor
<tr><td>&lt;colgrop>&lt;col width="" bgcolor="">&lt;colgrop>
</table>

## 表单元素
<table style="border-collapse:collapse">
<tr><td><th>标签<th>描述
<tr><td><td>form<td>建立表单的主要元素。含method属性（与服务器交换信息时使用的方式），一般选择post或<s>get</s>
<tr><td><td>input<td>定义一个用于用户输入的表单控件。由type属性规定其类型；由name属性定义控件名称，按照name/value发送给服务器，没有写那么属性的控件不会发送。
<tr><td rowspan=10>input元素的type属性值<td>text<td>文本框
<tr><td>password<td>密码或口令
<tr><td>radio<td>单选按钮
<tr><td>checkbox<td>复选框，可选，可多选，可不选
<tr><td>file<td>文件按钮
<tr><td>hiddle<td>隐藏按钮
<tr><td>image<td>图像控件
<tr><td>button<td>命令按钮
<tr><td>submit<td>提交按钮，发送表单
<tr><td>reset<td>重置按钮，将表单填写清零
<tr><td rowspan=2><td rowspan=2>select<td>下拉列表选择控件。通常包含若干个option元素。
<tr><td>默认multiple一次只能选择一项；设置multiple size=#，一次可选择#项（按住Ctrl或Shift键单击）
<tr><td><td>option<td>定义select元素的列表选项。属性：selected默认选中该项，disabled不能选择该项。
<tr><td><td>textarea<td>支持多行输入。属性：cols文本框宽度；rows文本框高度；或者使用width、height（准确）
</table>

## 框架标签
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td rowspan=3>frameset<td>定义框架结构，放在body元素外。HTML5不支持。
<tr><td>用法：<br>&lt;frameset rows="#,...,#"><br>&lt;frameset>
<br>&lt;frameset cols="#,...,#"><br>&lt;frameset><br>
＃的个数是将窗口所分区域数，#可以是整数，也可以是百分数。
<tr><td>frameborder属性值为‘0’隐藏边框，‘1’显示边框
<tr><td>frame<td>定义一个区域中的内容，HTML5不支持。
<tr><td>noframes<td>包含框架不能显示时的替换内容，HTML5不支持。
<tr><td>iframe<td>用法：&lt;iframe src="" name="name">
</table>

## 超链接
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td>a<td>用法：&lt;a href="" target="">链接对象&lt;a>
<tr><td rowspan=5>href属性值<td>href属性用于指定超链接的链接对象，可以为相对地址或绝对地址。
<tr><td>http://或ftp://或gopher://等
<tr><td>mailto:...<br>提供一个E-mail地址，启动E-mail默认程序发送信件。
<tr><td>伪协议：javascript:;点击a时不做任何动作
<tr><td>锚点"#"；查询参数"？name="。
<tr><td rowspan=5>target属性值<td>_blank<BR>新打开一个浏览器窗口显示链接对象
<tr><td>_self<br>在原网页所在窗口打开
<tr><td>_top<br>在浏览器整个窗口（祖宗窗口）中显示
<tr><td>_parent<br>在父窗口中显示
<tr><td>框架name<br>在相应框架中显示
<tr><td>图片链接<td>&lt;a href="">&lt;img src="" border=0>&lt;a><br>
</table>

## 字符控制
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td rowspan=2>font<td>控制文字的字体、字号、颜色
<tr><td>用法：&lt;font face="" size="" color="">&lt;font>
<tr><th colspan=2>字体样式标签
<tr><td>small<td>用小一号字体显示文字
<tr><td>strong<td>加粗显示
<tr><td>b<td>加粗显示
<tr><td>big<td>加大一号字体加粗显示
<tr><td>i<td>斜体强调显示
<tr><td>em<td>斜体强调显示
<tr><td>s<td>加上删除线
<tr><td>u<td>加上下划线
</table>

## 列表控制
<table style="border-collapse:collapse">
<tr><th>标签<th>描述
<tr><td>dl<td>定义列表
<tr><td>dt<td>由dd元素定义的对象
<tr><td>dd<td>对dt元素的定义
<tr><td>menu<td>设定菜单或列表的开头
<tr><td>ul<td>无序列表
<tr><td>ol<td>有序列表
<tr><td>li<td>列表项目
<tr><th colspan=2>ul、ol元素的type属性
<tr><td>1<td>以整数作为项目标记符
<tr><td>a<td>以小写字母作为项目标记符
<tr><td>A<td>以大写字母作为项目标记符
<tr><td>i<td>以小写罗马数字作为项目标记符
<tr><td>I<td>以大写罗马数字作为项目标记符
<tr><td>circle<td>以空心圆作为项目标记符
<tr><td>disc<td>以实心圆作为项目标记符
<tr><td>square<td>以方块作为项目标记符
</table>

## 多媒体
<table style="border-collapse:collapse">
<tr><th>技术<th>实现方法
<tr><td>声音与视频<td>使用a标签
<tr><td>背景音乐<td>在head标签中写入：<br>&lt;bgsound src="" loop=""><br>（loop为循环次数）
<tr><td>动态文件<td>使用img元素的dynsrc（引入各种格式的多媒体）、loop、start（值为mouseover等）等IE属性。
<tr><td>动画和视频的插入<td>使用embed元素，用法：<br>&lt;embed src="" width="" height="">
</table>

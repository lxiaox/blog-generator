---
title: HTML5标签列表
date: 2018-04-29 19:35:35
tags: （H）html5-标签
---
##### 以下为所有标准化的、有效的HTML5元素。

## 根元素
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;html>
<td>代表 HTML 或 XHTML 文档的根。其他所有元素必须是这个元素的子节点。
</table>

## 文档元数据
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;head>
<td>代表关于文档元数据的一个集合，包括脚本或样式表的链接或内容。
<tr>
<td>&lt;title>
<td>代表关于文档元数据的一个集合，包括脚本或样式表的链接或内容。
<tr>
<td>&lt;base>
<td>定义页面上相对 URL 的基准 URL。
<tr>
<td>&lt;link>
<td>用于链接外部的 CSS 到该文档。
<tr>
<td>&lt;meta>
<td>定义其他HTML元素无法描述的元数据。
<tr>
<td>&lt;style>
<td>用于内联CSS。
</table>

## 脚本
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;script>
<td>定义一个内联脚本或链接到外部脚本。脚本语言是 JavaScript。
<tr>
<td>&lt;noscript>
<td>定义当浏览器不支持脚本时显示的替代文字。
<tr>
<td>&lt;template>
<td>通过JS在运行时实例化内容的容器。
</table>

## 章节
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;body>
<td>代表 HTML 文档的内容。在文档中只能有一个 &lt;body> 元素。
<tr>
<td>&lt;section>
<td>定义文档中的一个章节。
<tr>
<td>&lt;nav>
<td>定义只包含导航链接的章节。
<tr>
<td>&lt;article>
<td>定义可以独立于其余内容的完整独立内容块。
<tr>
<td>&lt;aside>
<td>定义和页面内容关联度较低的内——如果被删除，剩下的内容依然很合理。
<tr> 
<td>&lt;h1>&lt;h2>&lt;h3><br>&lt;h4>&lt;h5>&lt;h6>
<td>标题元素实现了六层文档标题，&lt;h1> 是最大的标题，&lt;h6> 是最小的标题。标题元素简要地描述章节的主题。
<tr>
<td>&lt;header>
<td>定义页面或章节的头部。它经常包含 logo、页面标题和导航性的目录。
<tr>
<td>&lt;footer>
<td>定义页面或章节的尾部。它经常包含版权信息、法律信息链接和反馈建议用的地址。
<tr>
<td>&lt;address>
<td>定义包含联系信息的一个章节。
<tr>
<td>&lt;main>
<td>定义文档中主要或重要内容。
</table>

## 组织内容
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;p>
<td>定义一个段落。
<tr>
<td>&lt;hr>
<td>代表章节、文章或其他长内容中段落之间的分隔符。
<tr>
<td>&lt;pre>
<td>代表其内容已经预先排版过，格式应当保留 。
<tr>
<td>&lt;blockquote>
<td>代表引用自其他来源的内容。
<tr>
<td>&lt;ol>
<td>定义一个有序列表。
<tr>
<td>&lt;ul>
<td>定义一个无序列表。
<tr>
<td>&lt;li>
<td>定义列表中的一个列表项。
<tr>
<td>&lt;dl>
<td>代表一个定义列表（一系列术语及其定义）。
<tr>
<td>&lt;dt>
<td>代表由下一个&lt;dd>定义的术语。
<tr>
<td>&lt;dd>
<td>对上个术语的定义。
<tr>
<td>&lt;figure>
<td>代表一个和文档有关的图例。
<tr>
<td>&lt;figcaption>
<td>代表一个图例的说明。
<tr>
<td>&lt;div>
<td>代表一个通用容器，没有任何实际含义。
</table>

## 文字形式
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;a>
<td>代表一个链接到其他资源的超链接。
<tr>
<td>&lt;em>
<td>代表强调文字。
<tr>
<td>&lt;strong>
<td>代表特别重要 文字。
<tr>
<td>&lt;amsll>
<td>代表注释 ，如免责声明、版权声明等，对理解文档不重要。
<tr>
<td>&lt;s>
<td>代表不准确或不相关 的内容。
<tr>
<td>&lt;cite>
<td>代表作品标题 。
<tr>
<td>&lt;q>
<td>代表内联的引用 。
<tr>
<td>&lt;dfn>
<td>代表一个术语包含在其最近祖先内容中的定义 。
<tr>
<td>&lt;abbr>
<td>代表省略或缩写 ，其完整内容在 title 属性中。
<tr>
<td>&lt;data>
<td>关联一个内容的机器可读的等价形式 （该元素只在 WHATWG 版本的 HTML 标准中，不在 W3C 版本的 HTML5 标准中）。
<tr>
<td>&lt;time>
<td>代表日期和时间值；机器可读的等价形式通过 datetime 属性指定。
<tr>
<td>&lt;code>
<td>代表计算机代码。
<tr>
<td>&lt;var>
<td>代表代码中的变量。
<tr>
<td>&lt;samp>
<td>代表程序或电脑的输出。
<tr>
<td>&lt;kbd>
<td>代表用户输入，一般从键盘输出，但也可以代表其他输入，如语音输入。
<tr>
<td>&lt;sup>
<td>代表上标。
<tr>
<td>&lt;sub>
<td>代表下标。
<tr>
<td>&lt;i>
<td>代表一段不同性质的文字，如技术术语、外文短语等。
<tr>
<td>&lt;b>
<td>代表一段需要被关注 的文字。
<tr>
<td>&lt;u>
<td>代表一段需要下划线呈现的文本注释，如标记出拼写错误的文字等。
<tr>
<td>&lt;mark>
<td>代表一段需要被高亮的引用文字。
<tr>
<td>&lt;ruby>
<td>代表被ruby 注释标记的文本，如中文汉字和它的拼音。
<tr>
<td>&lt;rt>
<td>代表ruby注释，如中文拼音。
<tr>
<td>&lt;rp>
<td>代表 ruby 注释两边的额外插入文本 ，用于在不支持 ruby 注释显示的浏览器中提供友好的注释显示。
<tr>
<td>&lt;bdi>
<td>代表需要脱离 父元素文本方向的一段文本。它允许嵌入一段不同或未知文本方向格式的文本。
<tr>
<td>&lt;bdo>
<td>指定子元素的文本方向，显示地覆盖默认的文本方向。
<tr>
<td>&lt;span>
<td>代表一段没有特殊含义的文本。当其他语义元素都不适合文本时候可以使用该元素。
<tr>
<td>&lt;br>
<td>换行。
<tr>
<td>&lt;wbr
<td>建议换行 (Word Break Opportunity) ，当文本太长需要换行时将会在此处添加换行符。
</table>

## 编辑
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;ins>
<td>定义增加到文档的内容。
<tr>
<td>&lt;del>
<td>定义从文档中删除的内容。
</table>

## 嵌入内容
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;img>
<td>代表一张图片 。
<tr>
<td>&lt;iframe>
<td>代表一个内联的框架 。
<tr>
<td>&lt;embed>
<td>代表一个嵌入 的外部资源，如应用程序或交互内容。
<tr>
<td>&lt;object>
<td>代表一个外部资源 ，如图片、HTML 子文档、插件等。
<tr>
<td>&lt;param>
<td>代表 <object> 元素所指定的插件的参数 。
<tr>
<td>&lt;video>
<td>代表一段视频 及其视频文件和字幕，并提供了播放视频的用户界面。
<tr>
<td>&lt;audio>
<td>代表一段声音 ，或音频流 。
<tr>
<td>&lt;source>
<td>为 &lt;video> 或 &lt;audio> 这类媒体元素指定媒体源 。
<tr>
<td>&lt;track>
<td>为 &lt;video> 或 &lt;audio> 这类媒体元素指定文本轨道（字幕） 。
<tr>
<td>&lt;canvas>
<td>代表位图区域 ，可以通过脚本在它上面实时呈现图形，如图表、游戏绘图等。
<tr>
<td>&lt;map>
<td>与&lt;area> 元素共同定义图像映射 区域。
<tr>
<td>&lt;area>
<td>与&lt;map> 元素共同定义图像映射 区域。
<tr>
<td>&lt;svg>
<td>定义一个嵌入式矢量图 。
<tr>
<td>&lt;math>
<td>定义一段数学公式 。
</table>

## 表格
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;table>
<td>定义多维数据 。
<tr>
<td>&lt;caption>
<td>代表表格的标题 。
<tr>
<td>&lt;colgroup>
<td>代表表格中一组单列或多列 。
<tr>
<td>&lt;col>
<td>代表表格中的列 。
<tr>
<td>&lt;tbody>
<td>代表表格中一块具体数据 （表格主体）。
<tr>
<td>&lt;thead>
<td>代表表格中一块列标签 （表头）。
<tr>
<td>&lt;tfoot>
<td>代表表格中一块列摘要 （表尾）。
<tr>
<td>&lt;tr>
<td>代表表格中的行 。
<tr>
<td>&lt;td>
<td>代表表格中的单元格 。
<tr>
<td>&lt;th>
<td>代表表格中的头部单元格 。
</table>

## 表单
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;form>
<td>代表一个表单，由控件组成。
<tr>
<td>&lt;fieldset>
<td>代表控件组。
<tr>
<td>&lt;legend>
<td>代表&lt;fieldset>控件组的标题。
<tr>
<td>&lt;label>
<td>代表表单控件的标题。
<tr>
<td>&lt;input>
<td>代表允许用户编辑数据的数据区（文本框、单选框、复选框等）。
<tr>
<td>&lt;button>
<td>代表按钮。
<tr>
<td>&lt;select>
<td>代表下拉框。
<tr>
<td>&lt;datalist>
<td>提供给其他控件的一组预定义选项。
<tr>
<td>&lt;optgroup>
<td>代表一个选项分组。
<tr>
<td>&lt;option>
<td>代表一个&lt;select>元素或&lt;datalist>元素中的一个选项。
<tr>
<td>&lt;textarea>
<td>多欧行文本框。
<tr>
<td>&lt;keygen>
<td>密钥对生成器控件。
<tr>
<td>&lt;output>
<td>计算值。
<tr>
<td>&lt;progress>
<td>代表进度条。
<tr>
<td>&lt;meter>
<td>代表滑动条。
</table>

## 交互元素
<table>
<tr>
<th>Element
<th>Description
<tr>
<td>&lt;details>
<td>用户可以获取额外信息或空间的小部件。
<tr>
<td>&lt;summary>
<td>代表&lt;details>元素的综述或标题。
<tr>
<td>&lt;menuitem>
<td>用户可以点击的菜单项。
<tr>
<td>&lt;menu
<td>代表菜单。
</table>

#### [MDN原文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)
---
title: 'HTML浅解'
date: '2021/5/24'
tags:
- HTML
mainImg: 'https://images.unsplash.com/photo-1446057032654-9d8885db76c6?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MjIzNzk4NTM&ixlib=rb-1.2.1&q=80&w=1080'
coverImg: 'https://images.unsplash.com/photo-1446057032654-9d8885db76c6?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MjIzNzk4NTM&ixlib=rb-1.2.1&q=80&w=400'
intro: '作为一个 web 开发者，我们需要掌握的 HTML 知识到底应该有多少？HTML 真的如此简单吗，我们是否应该给与其更多的重视？'
---

​		作为一个 web 开发者，我们需要掌握的 HTML 知识到底应该有多少？HTML 真的如此简单吗，我们是否应该给与其更多的重视？

​		带着这些疑问，我决定重新学习`HTML`知识，如何学习？本文将带着疑问去学习`HTML`相关的知识，并且做出一定的总结。



## 前言

**HTML**（超文本标记语言），也是万维网的核心标记语言，对于现代浏览器来说，`HTML`已经发展到了第五个版本，在多年的演变和改进之下，许多不合时宜的内容被清除了，同时随着版本更迭也有新的内容添加进来，作为一个 web 开发者，我们需要紧跟技术的发展，保持前瞻性和技术敏感度。

知识无限，时间有限。

忽略掉那些琐碎的片段，我们将从不同的问题开启每一个知识点。

## Q&A

### 1. HTML 和 XML 语法的差别

HTML（超文本标记语言）和 XML（可扩展标记语言）结构类似，但是在语法上具有以下不同之处：

- XML 严格区分大小写
- XML 具有严格的树状结构，禁止省略结束标记
- XML 属性值必须用引号包裹起来，而在 HTML 中则是可选的
- XML 所有属性必须具有值，HTML 则允许无值属性（采用默认值）
- XML 解析器不会像 HTML 这样过滤空格
- XML 没有固定的标记标签，所有标签都是自定义可扩展的

二者在作用上也不同：

- XML 偏向于保存数据，可以被视为持久化结构
- HTML 偏向于描述数据结构

其他方面：

- 在浏览器中，HTML 文件的媒体类型是`text/html`，而 XML 的媒体类型则是`application/xhtml+xml`，不同的`MIME`类型在浏览器中将会以不同的解析器去解析文档。



### 2. 简单快速介绍一下 HTML 的知识

从最简单的一份`html`文档说起：

```html
<!DOCTYPE html>
<html lang="en">
 <head>
  <title>Sample page</title>
 </head>
 <body>
  <h1>Sample page</h1>
  <br />
  <p>This is a <a href="demo.html">simple</a> sample.</p>
  <!-- this is a comment -->
 </body>
</html>
```

如上述示例那样，HTML 文档具有树状结构，每一个节点标签都具备`开始标签`，但是不一定具有结束标签，标签支持`嵌套`。

每个标签都可能有属性和值，举个例子：

```html
<a href="url">somewhere</a>
```

标签具有各自的意义，属性值总是在`开始标签`内，并且如果属性值不包含特殊字符，则可以省略引号，但是更推荐保留引号，让整体结构的描述更准确。

浏览器通过自己的`HTML`解析器去解析`HTML`文档，并且将之转换为`DOM（文档对象模型）`，这种模型将保存在内存中。

![image-20210524205054501](https://i.loli.net/2021/05/24/5e1l7FsB24hyqtR.png)

上图是上述简单文档的`DOM`树状图形式，`DOM`提供了诸多`API`可以让开发者控制和修改`DOM`的结构。

> 我们可以通过：` caniuse.com `对标签和属性的兼容性进行查询

又绕回来说上述代码，最基础的上述结构中，可以继续延伸了解一下大部分标签。

- `<html>` 为根元素，页面唯一
- `<head>` 为头部信息标签，页面唯一，内部常嵌套一些补充信息和标题 
  - `<meta>` 元数据，常用于设置字符集，添加相关名字和描述性内容，常用于提高`SEO`
  - `<script>` 引入 JavaScript 
  - `<title>` 标题设置
  - `<style>` 嵌入 Css
  - `<link>` 外部资源链接
  - `<base>` 定义页面默认超链接的默认地址和打开方式，建议放在 head 的最前面
- `<body>` 页面主体，页面唯一，常用标签全部嵌套在内部。
  - `<h1>~<h6>` 设置标题
  - `<p>` 设置段落文本
  - `<a>` 超链接
  - `<pre>`预格式化
  - `<q>,<blockquete>`长短引用内容
  - `<br />`,`< hr />` 换行标签和水平线标签
  - `<b>` 粗体
  - `<small>`小号字体
  - `<i>`斜体
  - `<rt>` 中文发音注释，顶部显示
  - `<sub>`下标
  - `<sup>` 上标
  - `<iframe>`内联框架，替换`<frame>`
  - `<cite>`标签定义作品（比如书籍、歌曲、电影、电视节目、绘画、雕塑等等）的标题。默认斜体，引用分离，有助于自动摘录参考的功能。
  - `<div>` 通用块元素
  - `<span>` 内联文本元素
  - `<textarea>` 输入区
  - `<input>` 输入框
    - `<datalist>` 输入框可选值列表
  - `<img>` 图像
  - `<map>` 图像区域映射
    - `<area>` 定义区域位置和映射目标地址
  - `<figure>`标记文档中的媒体内容
    - `<figcaption>`媒体的标题，常用于媒体标签的上面或者下面
  - `<button>` 按钮
  - `<from>` 表单
    - `<fieldset>` 表单边框
      - `<legend>`表单边框描述，内容标题
  - `<video>` 视频
  - `<audio>` 音频
    - `<source>` 数据源和媒体类型说明，添加多个备用
  - `<table>` 表格
    - `<col>` 配合 `<colgroup>`为列添加属性
    - `<caption>` 表格标题
    - `<tbody>` 表格主体
    - `<td>`表格单元
    - `<th>` 表头单元格
    - `<tfoot>`表格脚注
    - ...
  - `<address>` 定义作者地址信息
  - `<ul>, <ol>` 有序和无序列表
    - `<li>` 列表项
  - `<dl>` 定义列表，增加列表的灵活性
    - `<dt>` 定义列表标题
    - `<dd>` 定义描述，通常在标题下方，并且具有缩进
  - `<del>` 被删除的文本
  - `<ins>` 默认下划线，定义插入的行内文本
  - `<details>` 默认不展开的内容隐藏
    - `<summary>` details 默认显示的描述信息，不支持`IE`
  - `<header>` 正文中的标题
  - `<nav>`旨在封装一组链接，常用于导航栏
  - `<footer>` 页脚内容
  - `<main>` 正文主体核心内容区域
  - `<article>` 文章容器
  - `<section>` 相关性内容，比如章节、页眉、页脚或文档中的其他部分。
  - `<aside>` 表示与它周围文本没有密切关系的内容，通常的广告区域、搜索、分享链接。
  - `<canvas>` canvas 图像容器
  - `<embed>` 嵌入页面的元素，外部应用，互动插件等等，本意是不属于当前页面的内容，使用时指定外部资源类型。
  - `<diakig>` 对话框，支持性很差
  - `<mark>` 类似`strong`，H5 属性且更为通用
  - `<meter>`给定的数据范围度量，需要制定相关属性
  - `<output>`表示输出结果的行内元素
  - `<time>`标注时间
  - `<datetime>`标注日期
  - `<progress> `进度条
  - `<select>` 下拉列表
    - `<optgroup>` 可选组选项
      - `<option>` 选项

所有`HTML`短语标签如下：

| <em>     | 呈现为被强调的文本。                                         |
| -------- | ------------------------------------------------------------ |
| <strong> | 定义重要的文本。                                             |
| <dfn>    | 定义一个定义项目。                                           |
| <code>   | 定义计算机代码文本。                                         |
| <samp>   | 定义样本文本。                                               |
| <kbd>    | 定义键盘文本。它表示文本是从键盘上键入的。它经常用在与计算机相关的文档或手册中。 |
| <var>    | 定义变量。您可以将此标签与 <pre> 及 <code> 标签配合使用。    |

### 3. HTML 和语义化有何意义

我们知道，`HTML`标签都具有独特的语义，使用合适的标签来组织整体的结构却不是开发者“必须”去做的一件事，在很多情况下，开发者混用不适宜的标签去达到相同的效果屡见不鲜。

清晰的语义能带来良好的页面结构，并且非常有利于搜索引擎和网络爬虫解析页面内容，大大提高页面内容的识别准确性，优化`SEO`让页面得到更好的传播和搜索权重。



### 4. 谈谈 HTML 中的语法错误问题

HTML 的语法错误的处理措施非常宽松，某种程度上 HTML 语法的灵活性让错误的语法产生了不完整的行为。

`HTML`的语法错误在浏览器中是可以被允许的，不良的语法结构将导致 DOM 语法树的结构不够直观。

来看看如下语法结构：

```html
<p><i>She dreamt.
<p><i>She dreamt that she ate breakfast.
<p><i>Then lunch.
<p><i>And finally dinner.
```

浏览器通过解析器解析此结构最终在 DOM 语法树中的结果如下：

![image-20210526223813242](https://i.loli.net/2021/05/26/bfOFlSEG73CZqLn.png)

也许这与我们的期望相去甚远，原来两层的语法树却形成了多层的嵌套结构，我们可以从中看出几个语法错误的特点：

- HTML 的语法非常宽松，语法错误是可以被允许和正常解析的
- 错误的语法将在解析后产生意想不到的 DOM 结构，并且很有可能降低性能



### 5. 简单谈谈你对于 HTML 元标签的理解

`HTML`文档信息可以在其`head`标签内使用`meta`标签进行补充说明，一般的形式是以`key/value`键值对为结构描述关于文档的额外说明。

`<meta>`不支持嵌套，没有闭合标签，其内容不会再页面显示，通常我们会增加一些额外信息描述，这往往有利于搜索引擎和提高`SEO`效率，对于机器是可读的

`meta`的有效属性包含以下四个：

- `name` 属性名
- `content`属性值
- `scheme` 指定`content`的格式，但`H5`不支持
- `http-equiv` 把`content`关联到`HTTP`头部，例如控制页面刷新时间，设置字符集类型和文档类型
- `charset` 字符集

以下是我们日常工作中可能会用到的键值对数据，。

```html
<head>
<meta name="description" content="博客">
<meta name="keywords" content="HTML,CSS,XML,JavaScript">
<meta name="author" content="someone">
<meta name = "revised" content = "Tutorialspoint, 5/27/2021" />
<meta charset="UTF-8">
<meta http-equiv = "refresh" content = "5; url = https://www.google.com" />
</head>
```



### 6. HTML 无障碍方面有何了解

无障碍设计的目标是让健全或者残疾人，年轻人或老年人都可以平等，便捷地获取站点的服务，增加受益群体。

通常，最大的受益人群是不擅长访问互联网的普通人或者视力障碍用户，甚至是听力、精神、肢体障碍用户。

`W3C`推动了无障碍化实施规范，主要的辅助即使包括硬件放大镜或者软件放大镜，盲文显示器和读屏软件等。

在开发的时候，可以采用可读性高的设计方案，甚至是对比度高的字体和图片等。另外，编写语义化的`HTML`将会对屏幕阅读器非常友好。

在时间充分的情况下，建议遵循`WAI-ARIA`规范或者[IBM无障碍化网站开发检查项(IBM Web accessibility checklist – Version 5.2 )](http://www-03.ibm.com/able/guidelines/web/accessweb.html)进行开发。

在测试的时候，可以使用`webking`静态检测工具进行测试。



### 7. 关于 HTML 注释的知识点

对于任何语言来说，注释都是很有必要的，在浏览器中注释将会被忽略，但是对于复杂的页面来说，必要的注释能让阅读源码的人提高阅读效率。

`HTML`使用`<!-- ... -->`作为注释标签（注意，边界不能有多余的空格，否则注释将被视为普通字符串），注释可以跨行。

还有一种注释被称为条件注释：`<!--[if IE 8]> ... <![endif]-->`，这种注释在`IE`中能被有效识别，在其他浏览器中被忽略，因此尝尝被用于为`IE`浏览器设置兼容性属性。

> `<comment>`标签内部也可以被视为注释（IE 浏览器有效），但是在`HTML5`中已经无效

在一些旧浏览器中，依然支持如下两种注释：

```html
<!DOCTYPE html>
<html>
   <head>
      <title>Commenting Style Sheets</title>      
      <style>
         <!--
            .example {
               border:1px solid #4a7d49;
            }
         //-->
      </style>
      <script>
        <!-- 
        document.write("Hello World!")
        //-->
      </script>
   </head>
	
   <body>
      <div class = "example">Hello , World!</div>
   </body>
	
</html>
```

但是在现代浏览器中，上述`JS`和`CSS`部分注释都无效。



### 8. 对于 img 标签的理解

`img`标签必须设置`src`和`alt`属性，添加具有实际意义的`alt`属性可以让页面更友好。

`img`是替换内联元素，可以理解为`inline-block`。

可以提前为`img`标签添加`width`和`height`属性值和对齐方向属性`align`(H5 已弃用)，如此一来在加载过程中也能具有稳定的宽高显示，从而保证页面的稳定。如果要实现固定的宽高比，自适应宽高比，则可以预设宽高值之一为固定值，另一个为`auto`。

> `img`此类自闭合标签是无法在内部嵌套子元素的，因此也就没法使用伪类`::before`和`::after`

`img`标签的事件监听如下：

- `onload`: 图像顺利加载完成
- `onerror`: 图像资源 404、403、500、请求超时或者返回的资源不是有效的图片
- `onabort`: 图像加载被强制停止，例如主动点击浏览器`stop`按钮

`HTML5`的趋势之一，就是减少元素标签的属性值，关于样式的部分尽可能使用`CSS`文件来描述。

另外，`img`支持`usemap`属性，配合`map`标签内嵌`area`可以实现点击图片不同区域跳转到不同的目标区域或者地址的功能。

### 9. 列举几个 HTML 最佳实践

- 编写有效可读的`DOM`
  - 全部小写
  - 保持缩进
  - 自动关闭标签
  - 避免过渡注释
  - 组织`DOM`，尽量减少元素
- 尽量不使用内联样式和内联脚本，内联的样式必须是关键样式（渲染页面顶部所需的最小CSS集）
- 将脚本标签放在 body 底部
- 照顾无障碍用户，使用意义明确的标签和描述性属性值
- 正确使用 title 和 meta 标签，增强`SEO`
- 压缩文件和使用`CDN`加速
- 对数据交互进行验证，永远不要相信用户的输入，提高应用的安全性

### 10. 谈谈你所理解的 table 标签

曾经开发者们使用表格进行布局，现在`table`标签更纯粹了，绝大多数用来展示表格数据。

表格允许开发者们将图片、图像、链接等数据排列到单元格的行和列中。

一个表格标签，内部嵌套着行盒子`tr`(table row)和单元格`td`。如果有必要，可以添加一行`th`表格列标题。

甚至是使用`thead`、`tbody`、`tfoot`将整体结构拆开：

```html
<table>
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>
</table>
```

表格标签支持多属性控制样式，但是推荐使用`CSS`控制样式。

### 11. 关于列表

列表分为三种：

- 有序列表 `ol`
- 无序列表`ul`
- 自定义列表 `dl`

而非自定义列表项则统一使用`li`,列表可以使用类型属性`type`和排序起始属性`start`控制列表项前面的标志。

自定义列表则使用`dt`作为列表标题，`dd`作为列表项，且默认存在缩进。

如果需要对列表前的类型样式做修改，则可以使用`list-style-type`设置浏览器默认支持的几个元素。

如果需要自定义样式，则可以配合伪类`::marker`使用。

甚至只要是`display: list-item`且可内嵌子元素的标签，都支持左边自定义一个显示顺序内容，合理使用`counter()`可以为多个项设置计算后的顺序前缀内容，这对于创建菜单序号和级联序号非常有用。

### 12. 超链接

超链接可以在用户点击链接后进行当前页面跳转或打开新的标签页进行跳转，为用户提供不同站点之间的导航功能，开发者可以通过`a`标签创建超链接，点击超链接后的行为取决于 `a`标签的`target`属性值。

可以为`target`设置以下几个不同属性值：

- `_blank`：在新的浏览器标签页打开链接的地址
- `_self`：在相同的`frame`内打开链接地址（默认值）
- `_parent`：在父级`frame`打开链接地址
- `_top`：在当前标签顶层`body`下打开链接地址（chrome 将会提示离开当前页面）
- `targetframe`：在目标`frame`内打开链接地址

除了作为导航外，还可以实现下载功能：

```html
<a href="large.jpg" download>下载</a>
```

> IE 不支持`dowload`属性

提供一个`download`属性让浏览器处理下载功能，并且可以为`download`属性提供值作为下载的文件名。

但是此方案在跨域场景下各厂家实现区别很大，因此不同源的方案不如使用`download.js`这个第三方库。

另外，我们在使用邮件类型的地址的时候，需要为`href`属性值之前添加协议类型：`mailto:`，例如：

```html
<a href = "mailto: abc@example.com">Send Email</a>
```

浏览器对此链接的点击行为做出反应，调用默认的邮件处理程序预置目标邮件地址，并且可以在`mail`地址后添加参数，邮件处理程序会解析类似`主题`或`body`的预置内容。

### 13. Frames

浏览器可以通过创建不同的`Frame`分割视图区域，并且每个`Frame`有单独的`HTML`结构，浏览器标签所有的`Frame`的集合被称为`frameset`。

> `frameset`代替`body`标签，定义页面的行与列的布局。

这种技术的缺点也很明显：

- 小屏幕设备显示功能效果不好，难以让分割视图的特性发挥效果。
- 不同分辨率的终端显示效果可能不同
- 浏览器的返回按钮可能会出乎意料，甚至无法实现用户想要的效果
- 少数浏览器不支持此标签
- 跨`Frame`通信较为复杂

示例:

```html
<!DOCTYPE html>
<html>
   
   <head>
      <title>HTML Frames</title>
   </head>
   
   <frameset cols = "25%,50%,25%">
      <frame name = "left" src = "https://www.baidu.com" />
      <frame name = "center" src = "https://www.baidu.com" />
      <frame name = "right" src = "https://www.baidu.com" />
      
      <noframes>
         <body>Your browser does not support frames.</body>
      </noframes>
   </frameset>   
</html>
```

还有一个标签：`iframe`也是提供一个内嵌的`frame`功能，不过它可以脱离`frameset`使用，更具有灵活性。

这种技术的应用较为少见，请谨慎使用（笔者在广告功能中常能见到其踪影）。

### 14. 字体滚动

`marquee`的兼容性良好，但是此元素已经不再推荐使用，规范随时可能删除此标签，开发者们更应该通过`CSS`动画来实现文字滚动。



### 15. HTML 通用属性

> 在 base、head、html、meta、param、script、style、title 元素上无效

H5 之前有五个除了上述几个元素外其他所有元素共有的可用属性：

- class
- id
- style
- title
- tabindex
- accesskey

前四者较为常用，后两者却容易被忽视。`tabindex`属性用于获取或指定当前元素的`tab`键激活顺序，其值范围为：`0~32767`。

如果不设置，则默认值是 0，并且按出现顺序进行跳转，但是可以设置值为`-1`，使得元素不能被`TAB`键访问，如果某些元素是隐藏的，在其未显示之前不应该被`TAB`键访问到，因此可以设置`tabindex=-1`。

> 如果为`div`设置了`tabindex`，则其内部嵌套的元素如果没有设置`tabindex`，则无法通过方向键跳转。

如果针对某些元素设置了`tabindex`，则`tab`键将从大到小进行跳转，慎用此特性以免给惯用快捷键访问的用户造成困扰，但如果良好地设计`tabindex`，则可以提供良好的无障碍访问功能。

同样的，`accesskey`也容易被人忽略，即使其功能强大。

我们可以为元素设置`accesskey`的值，然后通过不同系统的浏览器快捷键+此属性的值进行快速访问。

![image-20210616060934949](https://raw.githubusercontent.com/youyiqin/markdown_imgs/master/image-20210616060934949.png)

> [HTML accesskey属性与web自定义键盘快捷访问 « 张鑫旭-鑫空间-鑫生活](https://www.zhangxinxu.com/wordpress/2017/05/html-accesskey/comment-page-1/#comment-414139)

如果你喜欢`vimium`的功能，我猜这个属性的功能能够让你很开心。但是很多应用都没有使用到这个属性，这是无障碍访问功能的一部分，常常被人忽视，使其看起来犹如屠龙之技。

并且不同浏览器之间快捷键不同，对于元素的交互行为也不一样，这两个缺陷使其应用性大打折扣。浏览器快捷键和操作系统之间的影响可以从上图中看出端倪，而行为上的不一致，最简明的例子就是`IE`浏览器和`chrome`浏览器之间对`<a>`元素的行为不一致。前者只是让其获得焦点，后者却可以触发点击行为。

[accesskey - npm](https://www.npmjs.com/package/accesskey)这里有一个支持增强`accesskey`功能和处理一致性行为的第三方库，或许以后用得上。

> 不过话说回来，这个属性提醒了我可以在`electron`技术上使用这个功能，这样就可以减少使用系统快捷键绑定的逻辑代码。

`HTML5`版本出来之后，新增了部分全局属性：

- contenteditable：是否可编辑
- Data-*：自定义的元素数据存储，可以配合`JavaScript`或者`CSS`属性选择器使用
- draggable：实验中的属性，是否可以拖动
- dropzone：较为少见的属性，不如使用此名第三方库（[dropzone/dropzone: Dropzone is an easy to use drag'n'drop library. It supports image previews and shows nice progress bars.](https://github.com/dropzone/dropzone)）
- hidden：常用
- spellcheck：拼写检查，也是实验中的功能



### 16. 字体知识

字体是相对于操作系统而言的，不同操作系统默认支持某些特定的字体，因此在样式表中我们可以指定多种字体以支持不同的操作系统，如果没有指定字体，则使用系统默认的字体。

CSS 定义了 5 个常用的字体名称: `serif, ``sans-serif, ``monospace`, `cursive,`和 `fantasy. `这些都是非常通用的，当使用这些通用名称时，使用的字体完全取决于每个浏览器，而且它们所运行的每个操作系统也会有所不同。

示例样式如下：

```css
p {
  font-family: "Trebuchet MS", Verdana, sans-serif;
}
```

提供了三种字体，前面的优先，如果系统不支持此字体则一次往后递增，最后使用默认字体。

我们可以使用`@font-face`自定义字体：

```css
@font-face {
    font-family: <fontFamily>; /* 自定义的字体名称; */
    src: <source> [<format>][,<source> [<format>]]*;  /* 自定义的字体的存放路径、格式; */
    [font-weight: <weight>]; /*  是否为粗体 */ 
    [font-style: <style>]; /*  定义字体样式，如斜体 */
}
```

字体具有不同的格式，源文件格式可能会是：

- .tff
- .otf

前者字体格式值为`TrueType`，后者为`OpenType`，甚至还有：

- Embedded Open Type (.eot)
- Web Open Font Format (.woff)

为了保证兼容性，可以同时提供多种自定义字体：

```css
@font-face {
    font-family: 'myFont';
    src: url('myFont.eot'); /* IE9 Compat Modes */
    src: url('myFont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
         url('myFont.woff') format('woff'), /* Modern Browsers */
}
```

自定义字体的另一个广泛使用案例：`图标字体`。

![image-20210618003909597](https://raw.githubusercontent.com/youyiqin/markdown_imgs/master/image-20210618003909597.png)

图标字体可以很方便的配合伪类使用，并且非常灵活，开发者可以轻松修改其颜色和大小等。另外，兼容性很好，在某些需要兼容`IE`的项目中可以放心使用。

使用图标字体还有以下几个优点：

- 轻松替换
- 不会失真
- 便捷，可压缩


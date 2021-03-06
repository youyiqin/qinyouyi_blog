---
title: '2021年：使用适宜的标签增强 HTML 整体语义化'
date: '2021/5/29'
tags:
- HTML
mainImg: 'https://images.unsplash.com/photo-1471440671318-55bdbb772f93?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MjIzMDA2MTc&ixlib=rb-1.2.1&q=80&w=1080'
coverImg: 'https://images.unsplash.com/photo-1471440671318-55bdbb772f93?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxNjUyNjZ8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MjIzMDA2MTc&ixlib=rb-1.2.1&q=80&w=400'
intro: 'HTML 是与时俱进的，我们应该时刻保持技术的敏感度，了解新技术和新知识，并且应用在日常开发之中。'
---

所有的 web 开发者都知道 `HTML`，但是大多数开发者并不重视，甚至可以说是轻视了`HTML`。大多数的开发者能够轻松编写可用的`HTML`结构，并且把重心放在了其他方面，例如调整`CSS`和优化`JS`，而忽视了编写现代的，具有良好访问性和语义的`HTML`结构的重要性。

web 技术在持续发展，`HTML`也有一些新增的内容需要我们学习，使用这些新特性和新知识，能够从多个方面来优化我们的应用，例如：

- SEO 优化
- 良好结构具有良好的可读性
- 访问性得到增强，对于某些需要无障碍功能的用户更友好
- 新增的一些标签可以带来一些功能和样式增强，避免开发者编写自定义的额外代码。

举个例子，`div`和`span`标签通常被用于一些布局结构，但它们并没有相关的语义，我们应该寻求更好的语义化标签，如果不行，也可以为其设定`role`属性，指定一个语义化值。

### 语义化标签的使用场景

为了更好地展示语义化增强的`HTML`结构，我将列出可能的文档结构及其使语义化标签示例。

##### 整体结构

首先，让我们来看看一个具有良好语义化的页面结构（这只是一个参考示例，在实际应用中并没有严格的使用规定）。

```html
<header>...</header>
<main>
  <nav>...</nav>
  <h1>...</h1>
  <section>
    <article>
   		<p>
        It is <em>relevant</em>, but this is <strong>much more</strong>.
This is rather <small>unimportant</small>, though
      </p> 
    </article>
  </section>
  <section>
    <article>...</article>
    <article>...</article>
  </section>
  <aside>...</aside>
</main>
<footer>...</footer>
```

#### 文本优先级

上述结构中，`p`标签内的文本在语义上具有不同的重要性级别。

文本的强调程度：`small` 最小，其次是常规文本，然后是`em`标签，最后是`strong`标签，如果我们的文本有着明确的重要性指标，则应该优先使用强调程度高的标签。

#### 文本修正

再看看下面这个文本修正的示例：

```html
In the end, I was <del>wrong</del><ins>right</ins>
```

`del` 和`ins`配合得很好，很好的表现了修正文本`wrong`到`right`的语义。

#### 联系信息

如果我们有一个个人或者公司的联系信息，例如联系方式、联系人、电话或者邮件地址等，都可以使用`address`标签。

```html
<address>
  E-mail: <a href="mailto:me@mail.me">me@mail.me</a>
  Carrot Street, 42 - 01010 My City
</address>
```

#### 时间和日期

示例如下：

```html
Published: <time datetime="2020-12-20T20:00:00">Dec. 20th</time>
```

推荐使用`time`标签表明这是一个时间信息，并且使用人类易读的`text`文本作为描述，而使用`datetime`属性和一个机器易读的值。

#### 引用和参考信息

```html
My uncle said, <q cite="https://myuncle.org/famous-quotes">That's life, kid</q>
<blockquote>
  <p>That's life, kids. Roll with it.</p>
  <cite>
    <a href="https://myuncle.org/famous-quotes">Famous quotes</a>, by my uncle
  </cite>
</blockquote>
```

上述示例中，行内嵌套时使用`q`标签（通常会自动加上引号），块级引用则使用`blockquote`，而`cite`标签则表明引用的来源信息。

#### 文本方向

```html
<p>This paragraph will go left-to-right.</p>  
<p><bdo dir="rtl">This paragraph will go right-to-left.</bdo></p>  
```

指明文本方向，这在某些特殊场景下很有用。

#### 按键输入和代码样本

```html
When things seem bleak, just press <kbd>Alt</kbd> + <kbd>F4</kbd>
The computer will not say <samp>Access denied</samp> anymore, yay!
```

`kbd`用于标识按键输入，这在一些表明快捷键的场景下很有用，`samp`则表示这是计算机程序代码（也可以使用`code`）。

#### 标记和高亮

<p>This is very important and should be <mark>marked</mark></p>

上述`marked`的代码是：

```html
This is very important and should be <mark>marked</mark>
```

`mark`用于标记和高亮关键内容。

#### 计算结果

```html
<form ...>
  Enter age: <input type="range" min="0" value="27">
  <output>You are good to go!</output>
</form>
```

`output`标签表明这是一个计算结果，例如某云服务器选购后计价展示价格结果使用`output`标签。

#### 自定义列表

```html
<dl>
  <dt>Mario</dt>
  <dd>An Italian plumber that wears red.</dd>
  <dt>Luigi</dt>
  <dd>An Italian plumber that wears green.</dd>
</dl>
<p><dfn>Mario</dfn> is an Italian plumber that wears red</p>
```

`dl`是一个定义列表，跟有序和无序列表不同的是，定义列表支持`dt`描述列表标题，`dd`则表述其内容，一个定义列表只支持一个`dt`（如果内部用`div`拆分，则每一个`div`内部支持单独的`dt`和`dd`），浏览器对定义列表有默认的样式，定义内容具有缩进（不要为了缩进而使用此标签）。

#### 标签的数据

```html
<data value="user-123">Bob</data> and
<data value="user-456">Jim</data>
```

`data`标签的`value`属性和值可以被读取，但是在页面是不会显示的。也就是说，`value`的值是机器可读的，而`text`是为了让用户可见的。

除了`data`标签具有此特性，`HTML5`还让所有标签具有`data-*`属性：

```html
<ul>
  <li onclick="showDetails(this)" id="owl" data-animal-type="bird">Owl</li>
  <li onclick="showDetails(this)" id="salmon" data-animal-type="fish">Salmon</li>  
  <li onclick="showDetails(this)" id="tarantula" data-animal-type="spider">Tarantula</li>  
</ul>
```

我们可以通过`js`获取元素的`data-*`值，而在页面上这被视为机器可读而用户不可见的。

#### 语义和功能聚合的标签

类似`img`或者`video`这些标签，语义和特定的功能是聚合在一起的。常用的此类标签之外，还有几个常被人忽视的标签：

- `details`： 适用于定义一个可以手动点击展开和隐藏的详细信息区，`summary`标签嵌套于内部作为提示信息。

```html
<details>
    <summary>Details</summary>
    Something small enough to escape casual notice.
</details>
```

- `figure`配合`figcaption`指定一个元素（图片、视频、代码等）的标题

```html
<figure>
  <img src="demo.jpg" alt="Trulli" style="width:100%">
  <figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption>
</figure>
```

- `picture` 和 `source`： 提供一个更灵活的图片资源，通常可以配合`media`属性指定媒体查询条件下的资源地址，某种意义上可以理解为备选或者特定场景下修改`img`的`src`属性以显示更适宜的图片。

```html
<picture>
    <source srcset="/media/cc0-images/surfer-240-200.jpg"
            media="(min-width: 800px)">
    <img src="/media/cc0-images/painted-hand-298-332.jpg" alt="" />
</picture>
```

- `ruby`和`rt`：用于日文注音或中文注音（`<rp>`：定义不支持 ruby 元素的浏览器所显示的内容）

```html
<ruby>
漢 <rp>(</rp><rt>kan</rt><rp>)</rp>
字 <rp>(</rp><rt>ji</rt><rp>)</rp>
</ruby>
```

- `meter`：度量衡，某些具有度量意义的数据需要展示的时候可用。
- `progress`：进度条，展示可变进度可用。



### 写在最后

最后，希望大家喜欢本文的内容，学习和应用新的知识可以提高我们的代码质量，但这并不是全部，本文旨在抛砖引玉，再会。

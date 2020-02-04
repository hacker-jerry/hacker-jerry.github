---
layout: post
title: "Optimize My Blog"
subtitle: 关于插入iframe标签，优化响应速度以及调整标题动效
date: 2020-01-19 12:38:37
catalog: true
tags: 
- 优化
- js
- css
- 前端
header-img: http://blog.img.hackerjerry.top/Fm5MVDOv4rTxbfuWy0rNyuUHhkza
post_copyright: true
author: Jerry
---

# 插入Bilibili视频

首先，[参考博客]( https://www.cnblogs.com/artoriax/p/10364915.html )在这里。

很简单，按照里面说的，直接在分享按钮里找到`iframe`代码，然后，**稍作修改**。

> 原`iframe`直接插入`<iframe src="//player.bilibili.com/player.html?aid=73280139&cid=135397662&page=11" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>`会得到这样子的浏览器

<iframe src="//player.bilibili.com/player.html?aid=73280139&cid=135397662&page=11" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
土爆了好吗！

因此,稍作修改，改成`<iframe src="//player.bilibili.com/player.html?aid=73280139&cid=135397662&page=11" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="95%" height="450"> </iframe>`

就成了↓

<iframe src="https://player.bilibili.com/player.html?aid=73280139&cid=135397662&page=11" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="95%" height="450"> </iframe>
注意 **URL少了传输协议，需要加上http:或者https:，否则会以file来传输** 

# 插入第三方页面

同样还是用的`<iframe>标签`，如法炮制。

不过需要加入`div标签`，用来约束。

```html
<div>
<iframe src="https://mubu.com/doc/explore/27635"  height="500px"  width="100%"   frameborder="0"       border="0" frameborder="no" framespacing="0" allowfullscreen="true" ></iframe>
</div>
```

效果如下：

<div>
<iframe src="https://mubu.com/doc/explore/27635"  height="500px"  width="100%"   frameborder="0"       border="0" frameborder="no" framespacing="0" allowfullscreen="true" ></iframe>
</div>

# 增加标题动效 

下面是增加标题动效了。

踩了不少坑，花了3天才整体迁移过来（并实现了三级标题动效）。

用到的知识点

- js
- jquery库
- css3

<div class="tip inlineBlock warning">第一版代码还是非常臃肿，暂时没有更好的思路简化，再埋下一个坑</div>
# 优化响应速度

`google`官方文件，原文如下：



How do you load third-party script efficiently?
If a third-party script is slowing down your page load, you have several options to improve performance:

Load the script using the async or defer attribute to avoid blocking document parsing.

Consider self-hosting the script if the third-party server is slow.

Consider removing the script if it doesn't add clear value to your site.

Consider Resource Hints like <link rel=preconnect> or <link rel=dns-prefetch> to perform a DNS lookup for domains hosting third-party scripts.

Use async or defer
JavaScript execution is parser blocking. This means when the browser encounters a script it must pause DOM construction, hand this over to the JavaScript engine and allow script execution before proceeding with DOM construction.

The async and defer attributes change this behavior.

With async, the browser downloads the script asynchronously while it continues to parse the HTML document. When the script finishes downloading, parsing is blocked while the script executes.

With defer, the browser downloads the script asynchronously while it continues to parse the HTML document. The script doesn't run until the parsing is complete.

## js异步加载

defer

async


## 图像转webp格式

https://web.dev/codelab-serve-images-webp/

## Lazy load offscreen images with lazysizes
https://web.dev/codelab-use-lazysizes-to-lazyload-images/

## 优化缓存（没看明白）
https://web.dev/uses-long-cache-ttl/?utm_source=lighthouse&utm_medium=unknown


使用fetch
https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch

# css

先总结总结一下css的核心思想吧。

首先，**css的框模型**可以说是最基本的思想了。

## 一切皆为框

div、h1 或 p 元素常常被称为块级元素。这意味着这些元素显示为**一块内容**，即"**块框**"。与之相反，span 和 strong 等元素称为“行内元素”，这是因为它们的内容显示在行中，即“**行内框**”。

>行框和行内框是两个概念
>由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。不过，设置行高可以增加这个框的高度。
>由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。不过，设置行高可以增加这个框的高度。


但是！可以使用`display`属性改变生成的框的类型，比如设置成`block`可以让行内元素表现的和块级元素一样，还可以通过把` display` 设置为 `none`，让生成的元素根本没有框。这样的话，该框及其所有内容就不再显示，不占用文档中的空间。

那么框的大小就成了第一个需要考虑的事情。

<img src="http://blog.img.hackerjerry.top/Fse8NdwoChZwroUIPk9HRokozVb_" style="zoom:67%;" />

<div class="tip inlineBlock important">这里特别注意:<br>如果没有指明是<code>margin-left</code>或者<code>padding-bottom</code>的话，它们的作用范围是四周，作用效果是长和宽各增加两倍</div>
<div class="tip inlineBlock success">外边距（margin)可以是负值，而且在很多情况下都要使用负值的外边距。</div>
## positon定位

position 属性值的含义：

- static

  元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。

- relative

  元素框偏移某个距离。元素仍保持其未定位前的形状，它原本所占的空间仍保留。

- absolute

  元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

- fixed

  元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。


## id和class选择器

对于`id选择器`，css选择器用`#id-name`来进行选择。

比如：

```html
<style>
    #hello {
        font-size:5px;
        padding-left:2px;
    }
</style>
<body>
    <div id="hello">
        hello
    </div>
</body>
```

而`class选择器`是用`.class-name`来选择的。

比如：
```html
<style>
    .happy {
        font-size:5px;
        padding-left:2px;
    }
</style>
<body>
    <p class="happy">
        hello
    </p>
</body>
```

而最更厉害的特性在于，可以对**特定标签的类**进行自定义css设置。比如，对`p标签`的`happy类`设置，可以这样：

```html
<style>
    p.happy {
        font-size:5px;
        padding-left:2px;
    }
</style>
<body>
    <p class="happy">
        happy
    </p>
    <div class="happy">
        happy
        </div>
</body>
```
## css伪类
对于伪类，比如hover,focus,active这类常见的伪类就是可以选择一些特殊条件的元素。

从而不需要js也可以完成一些DOM操作。

其他常用的伪类还有：

` p:last-child` 选择所有p元素的最后一个子元素

`p:nth-child(2)`选择所有 p 元素的父元素的第二个子元素

`p:only-child` 选择所有仅有一个子元素的p元素

`p:first-line`选择每个<p> 元素的第一行

`p:before`在每个<p>元素之前插入内容

`p:after`在每个<p>元素之后插入内容

## css transition
[教程](https://www.w3school.com.cn/cssref/pr_transition-property.asp
https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

## css3动画
[教程](https://www.runoob.com/css3/css3-animations.html)

<img src="http://blog.img.hackerjerry.top/FlDj0XNXKL-iMH5EBuD86Hn5BXC8" style="zoom: 50%;" />
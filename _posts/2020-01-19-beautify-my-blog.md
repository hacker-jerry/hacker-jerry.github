---
layout: post
title: "Beautify My Blog"
subtitle: 关于插入b站视频，以及调整标题动效
date: 2020-01-19 12:38:37
catalog: true
tags: 
header-img: 
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

# 增加标题动效 

下面是增加标题动效了。

踩了不少坑，花了3天才整体迁移过来（并实现了三级标题动效）。

用到的知识点

- js
- jquery库
- css3

<div class="tip inlineBlock warning">第一版代码还是非常臃肿，暂时没有更好的思路简化，再埋下一个坑</div>
---
layout:     post
title:      "前端笔记(一)"
subtitle:   " 爱你所爱，无问西东 "
date:       2019-07-03 19:16:08 
header-img: 
author:     "Jerry"
catalog:  true
tags:
    - 前端
---


# 基础元素
## 声明
`<!DOCTYPE>`用于说明页面的HTML版本
`<head>`
`<body>`具体内容
`<title>`显示在标签栏上
`<h1>  <h2>.......`标签
`<p>`段落
`<a href="">xxx</a>`把xxx作为超链接
`<img src="">`图片
`<br/>`换行（空元素）

## 常用属性
`<h1>:align` 对齐方式  `right` `left` `center`
`<a>:target` 在何处打开链接
`<body background>` 背景图片   
`<body bgcolor>` 背景颜色
## 通用属性
`class`类名
`<style type="">`用于引入css属性
## 格式化
`<b>`加重
`<big>`
`<em>`
`<i>`斜体
`<strong>`
`<sub>`下标
`<sup>`上标
`<del>`删除字（即横划线）
`<ins>`插入字
## 样式
### 标签
`<style>`样式定义
`<link>`资源引用
`<img>`
`<a>`链接标签
文本链接
图片链接
### 属性
`rel="stylesheet"`    外部样式表
`type="text/css"`     引入文档类型
`margin-left`        边距
`alt`               元素属性声明（在图片加载不出来的时候仍能显示的文本）
`name`              文档内链接（用于跳转到注释处）
例：
```HTML
<a name="tips">hello</a>
<a href="#tips">跳转到hello</a>
```
### 插入方法
#### 外部样式表
`<link rel="stylesheet" type="text/css" href="mystyle.css"`  直接在`<head>`标签里加入就可以，相关的元素直接就以**mystyle.css**中的样式显示。
#### 内部样式表
```HTML
<style type="text/css">
body {background-color: red}
p {margin-left: 20px}
</style>
```
这是定义了`body`元素和`p`元素的样式。
# 表格
`<table>`里面可以设定单元格边框border
				设定单元格大小cellpadding
                设定单元格间距cellspacing
                设定单元格颜色bgcolor
`<caption>`表格标题
`<th>`第一行表头
`<tr>`表格的定义
`<td>`一行的表格数据（要放在`<tr>`里）
`<ul>`标签

# 列表
## 无序列表
### 相关标签
`<ul>`定义
`<li>`项
### 属性
前面的标号：（在`<ul>`中定义type属性
`disc`实体圆
`circle`空心圆
`square`方块

## 有序列表
`<ol>`定义
`<li>`
### 属性
编号方式：
`A`
`a`
`I`罗马数字
`start`
## 嵌套列表
即列表中再嵌套一个列表
`<ul>`
`<ol>`
`<li>`
## 自定义列表
默认没有编号
`<dl>`定义
`<dt>`项名
`<dd>`具体描述
# HTML块
  块元素，总是以新行开始，不会连在一起。如`<h1>` `<p>` `ul`
## div元素
  `<div>`元素，用于引入css样式。
  用法如下：
  在**head**中添加**css**文件链接`<link rel="stylesheet" type="text/css" href="xxx.css">`
  然后在**body**中添加
  ```HTML
  <div id="xxx">
       <h>.......</h>
   </div>
  ```
  然后在**xxx.css**中定义id`#xxx {....}`即可。

## span元素

- 只用于文本元素的div的特殊下属

```html
<head lang="en">
	<style type="text/css">
		span{
			color: blue;
		   }
</head>
<body>
	<div id="divspan">
		<p><span>hello</span></p>
	</div>
</body>
```

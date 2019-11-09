---
layout: post
title: "Java容器类-学习笔记“"
category: 
tags: 
header-img: 
post_copyright: true
author: 
---

容器类的对象实例成为容器，用于保存对象。

# 容器

按照存储的元素形式，按照接口划分为两类：

## Collection
<div class="tip inlineBlock important">包括List，Set，Queue。</div>
1. List：按照元素被插入时的顺序保存的元素
   - ArrayList
   - LinkedList
2. Set：不能有重复元素
   - TreeSet
   - HashSet
     - LinkedHashSet
3. Queue：按照排队规则确定的元素顺序
   - PriorityQueue

## Map
<div class="tip inlineBlock important">一系列由键值对组成的序列，允许通过键查找值</div>
- HashMap
   - LinkedHashMap
- TreeMap

# 容器具体代码实现

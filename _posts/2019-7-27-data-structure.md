---
layout:     post
title:      "数据结构"
subtitle:   " 它好难呀"
date:      2019-05-31 21:51:53
header-img:
painhead:
author:     "Jerry"
catalog: true
tags:
    - 数据结构
---


## 串

###  链式存储
  ![](https://img.mubu.com/document_image/8e861bda-52cc-41de-83ff-466746ef2bc2-3245207.jpg)

#### 索引存储

##### 带长度的索引表
![](https://img.mubu.com/document_image/038ea293-fae3-4700-8f17-293c4a3c08f6-3245207.jpg)

##### 带末指针的索引表
   ![](https://img.mubu.com/document_image/95f8b9b8-2979-490d-8136-836ef84d5592-3245207.jpg)
##### 带特征位的索引表
   ![](https://img.mubu.com/document_image/fb1cb70f-cc64-4270-be31-096a9daf7018-3245207.jpg)
####  链式模式匹配算法

   精髓：定义三个指针------first,sptr,tptr
   用first指示当前剩余字符串中的第一个
   用sptr从first位从前往后匹配
  >用tptr指示待匹配的值并后移
  一旦不一致，first后移，sptr重置，tptr重置
  ![](https://img.mubu.com/document_image/3e78d3b4-f091-44f3-9880-8c461da739c4-3245207.jpg)
## 数组

### 稀疏矩阵三元组表

 >三元组=（行i，列j，非零元素值）——行优先

#### 数据结构描述
![](https://img.mubu.com/document_image/b4a6e555-b7dc-4efd-936d-e1f2d803047f-3245207.jpg)

三元组----先用一个node类型的一维数组储存一类值，然后在值内分配 i,j,v三个属性，从而超越了二维属性的限制

#### 转置算法

   本来应该直接把存储的行号列号交换一下就可以，但这样得到的是列优先的稀疏矩阵，我们需要行优先的

   第一步只是把“行数”和“列数”转换，并未对实际矩阵产生影响；第二步才是按列查找（因为它们转置成了行，而我们要以行优先储存），双重循环，才能实现排序！从0开始（因为它们是之后的行号）
  ![](https://img.mubu.com/document_image/1937b2ff-1c4a-4f04-b0d5-08a2ff50968a-3245207.jpg)
## 栈

### 定义
 ![](https://img.mubu.com/document_image/f4eecf57-f98b-4f6f-955b-d466ed2d49ff-3245207.jpg)

 ###形象结构
      ![](https://img.mubu.com/document_image/68a09350-4192-432b-a6c0-4817e85b19a6-3245207.jpg)
### 入栈
 ![](https://img.mubu.com/document_image/a0413bd9-e342-4dc6-b8d2-3069f89e2d2f-3245207.jpg)
### 出栈
![](https://img.mubu.com/document_image/c21ef859-ed45-4bc1-baf7-0fd273c75cd2-3245207.jpg)

## 队
### 定义
 ![](https://img.mubu.com/document_image/d647ecdd-13cc-4c30-9ea4-b7ef116636d5-3245207.jpg)

### 循环队列

#### 形象示例  
![](https://img.mubu.com/document_image/2650eba0-a135-4454-9b36-077dd79f21ea-3245207.jpg)
    
#### 置空队
![](https://img.mubu.com/document_image/60049f5e-5401-4268-9191-50d9fa874756-3245207.jpg)
#### 入队
![](https://img.mubu.com/document_image/8aeaa621-2ae5-4a4e-8994-af0b7da6c5dd-3245207.jpg)
#### 出队
![](https://img.mubu.com/document_image/3c711182-1e72-4004-8981-188f27ec287e-3245207.jpg)
#### 关于返回指针的函数在主函数中的调用
![](https://img.mubu.com/document_image/74b2007d-9014-4305-92ad-1e8cfe94395b-3245207.jpg)


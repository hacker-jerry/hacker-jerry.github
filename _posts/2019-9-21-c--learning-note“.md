---
layout:     post
title:      "c++学习笔记(一)"
subtitle:   "吾辈青年岂容卸甲，唯有自请长缨，日夜兼程。"
date:       2019-07-02 11:31:49
header-img: 
author:     "Jerry"
catalog: true
tags:
    - c++
---


# 变量声明


`#include<sdtio.h>`是`c`的头文件，而cpp的头文件是`#include<iostream>`
```cpp
#include<stdio.h>
#include<math.h>
int sum(char *p,char *f,int m,int n)
{

        double s=0.0;
        int i,j,c,d;
    for(i=0;i<m;i++)
       s+=(*(p+i)-'0')*(pow(10,m-i-1));
       for(j=0;j<n;j++)
       s+=(*(f+j)-'0')*(pow(10,n-j-1));
   char a[100]; 
        sprintf(a,"%.f",s);
        puts(a);
        return 0;
}
int main()
{
        char a[20],b[20];
        int m,n;
        int sum(char *p,char *f,int m,int n);
        char *p;
        char *f;
        scanf("%d %d",&m,&n);
        scanf("%s",a);
        scanf("%s",b);
        p=a;
        f=b;
        sum(p,f,m,n);
        return 0;
}
```

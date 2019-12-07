---
layout: post
title: "Drawing on Matlab"
subtitle:
category: 
catalog: true
tags: 
        - matlab
date: 2019-12-01
header-img: http://blog.img.hackerjerry.top/2019/12/07/15756973436224.jpg
post_copyright: true
author: Jerry
---

# 最重要的函数--plot()

是的就是它！
<div class="tip inlineBlock important">plot(x,y)<br>plot(x,y,Linespec)</div>

其中第一个最简单，x即x轴的点，y即y轴的点，根据要求设置。
第三个参数Linespec是线的属性，包括：

- 线型
	

| 符号  | 含义 |
| --- | ------ |
| -   | 细实线 |
| :   | 虚点线 |
| -.  | 点画线 |
| --  | 虚画线 |

![类似这样](http://blog.img.hackerjerry.top/1575201928829.png)
- 点型
![点型](http://blog.img.hackerjerry.top/1575202009113.png)
- 颜色
![颜色](http://blog.img.hackerjerry.top/1575202032992.png)

如果要在一个图里画多个曲线，则需要使用`plot(x1,y1,x2,y2)`和`plot(x1,y1,linespec,x2,y2,linspec)`
比如这样，
```matlab
x = -5:0.01:7;
y = normpdf(x,1,2);
z = normpdf(x,1,4);
plot(x,y,'r',x,z,'g');
set(gca,'XTick',[-5:1:7]);
grid on%用来开启刻度线
```
效果图
![正态分布](http://blog.img.hackerjerry.top/1575202790270.png)

# 第二个函数--set()

这个函数呢，是用来设置坐标轴的各种属性。（当然还可以设置其他的比如窗口什么的，现在先不要求掌握）
## 自定义刻度
`set(gca,'XTick',[-5:1:7]);`从-5到7以步长为1显示坐标
`set(gca,'xticklabel',{'最低','低','中','高','最高'}); `%x轴的标注上自定义字符（也就是上面可以标注的点）
效果图：
![set函数](http://blog.img.hackerjerry.top/1575203294887.png)


## 刻度调整

         `set(gca,'xtick'，[])`              %去掉x轴的刻度

         `set(gca,'tickdir','in/out');`     %决定坐标轴上的刻度线在图形里还是图形外

         `set(gca,'xlim',[xmin xmax])/set(gca,'ylim',[xminxmax]);`%设定图形的显示范围

         `set(gca, 'fontsize',8)`            % 此时x,y轴标注文字都会改变

         `set(gca,'xdir','reverse')/ set(gca,'ydir','reverse');`%坐标轴刻度翻转

         `set(gca,'xgrid','on')`              %X轴的grid开启

         `set(gca,'ygrid','on')`               %y轴的grid开启
另外还可以自动格式化坐标轴
```
x=get(gca,'xlim');%获取x轴的范围，并返回一个数组 

y=get(gca,'ylim'); 

set(gca,'xtick',[x(1) (x(1)+x(2))/2 x(2)]);%这里的x(1)就是最小值，x(2)是最大值

set(gca,'ytick',[y(1) (y(1)+y(2))/2 y(2)]); 
```
![](http://blog.img.hackerjerry.top/1575205431988.png)
```matlab
 y = 0:10:20000;
 x = 0:10:20000;
 plot(x,y)
 x=get(gca,'xlim');
 y=get(gca,'ylim');
 set(gca,'xtick',[x(1) (x(1)+x(2))/2 x(2)]);
 set(gca,'ytick',[y(1) (y(1)+y(2))/2 y(2)])
```

## 特殊字符

          1、bf，\it，\rm表示黑体，斜体，正体字符

          2、上标用 ^(指数)，下标用 _(下划线)

          调用方式为: ^{任意字符}, _{任意字符}, 注意{}的使用!

          3、希腊字母等特殊字符用 \加拼音如:
```matlab
                   α \alpha     β\beta     γ \gamma     θ \theta       Θ \Theta

                   Г \Gamma     δ\delta      Δ \Delta      ξ \xi       Ξ \Xi       Ω \Ommiga

                    η \elta     ε\epsilong     ζ \zeta     μ \miu       υ \nu    τ \tau

                   λ \lamda     Λ\Lamda     π \pi      Π \Pi      σ \sigma      \Sigma

                    φ \phi     Φ\Phi      ψ \psi     Ψ \Psi      χ \chi     ω \ommiga
```

   4、< \leq> \geq 不等于    \neq<< \ll >> \gg

           5、正负 \pm       左箭头 \leftarrow       右箭头\rightarrow      上箭头 \uparrow




参考：
https://blog.csdn.net/revivre/article/details/80136142
https://blog.csdn.net/sign1991/article/details/8468400
这是一篇比较详细的https://blog.csdn.net/qq_41187256/article/details/79822852

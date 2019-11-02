
---
layout:     post
title:      "数据结构"
subtitle:   " 它好难呀"
date:       2019-05-31 21:51:53
header-img: ""
author:     "Jerry"
catalog: true
tags:
    - 数据结构
---
<head>
<title>数据结构 - 幕布</title>
<meta charset="utf-8"/>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="renderer" content="webkit"/>
<meta name="author" content="mubu.com"/>
</head>
<body style="margin: 0;color: #333;font-family: SourceSansPro,-apple-system,BlinkMacSystemFont,'PingFang SC',Helvetica,Arial,'Microsoft YaHei',微软雅黑,黑体,Heiti,sans-serif,SimSun,宋体,serif">

<div class="export-wrapper"><div style="font-size: 22px; padding: 0 15px 0;"><div style="padding-bottom: 24px">数据结构</div><div style="background: #e5e6e8; height: 1px; margin-bottom: 20px;"></div></div>


   * ## <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">串</span>

  ###  <span class="content mubu-node" images="%5B%7B%22id%22%3A%2230216b07295448117-3245207%22%2C%22uri%22%3A%22document_image%2F8e861bda-52cc-41de-83ff-466746ef2bc2-3245207.jpg%22%2C%22ow%22%3A464%2C%22oh%22%3A150%2C%22w%22%3A367%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">链式存储</span>
  ![](https://img.mubu.com/document_image/8e861bda-52cc-41de-83ff-466746ef2bc2-3245207.jpg)

   * #### <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">索引存储</span>

   * ##### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2211c16b072cf1de0e8-3245207%22%2C%22uri%22%3A%22document_image%2F038ea293-fae3-4700-8f17-293c4a3c08f6-3245207.jpg%22%2C%22ow%22%3A519%2C%22oh%22%3A146%2C%22w%22%3A408%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">带长度的索引表</span>
![](https://img.mubu.com/document_image/038ea293-fae3-4700-8f17-293c4a3c08f6-3245207.jpg)

   * ##### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2216f16b072d917d185-3245207%22%2C%22uri%22%3A%22document_image%2F95f8b9b8-2979-490d-8136-836ef84d5592-3245207.jpg%22%2C%22ow%22%3A314%2C%22oh%22%3A137%2C%22w%22%3A247%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">带末指针的索引表</span>
      ![](https://img.mubu.com/document_image/95f8b9b8-2979-490d-8136-836ef84d5592-3245207.jpg)
   * ##### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2239a16b072eb3c9051-3245207%22%2C%22uri%22%3A%22document_image%2Ffb1cb70f-cc64-4270-be31-096a9daf7018-3245207.jpg%22%2C%22ow%22%3A371%2C%22oh%22%3A300%2C%22w%22%3A263%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">带特征位的索引表</span>
      ![](https://img.mubu.com/document_image/fb1cb70f-cc64-4270-be31-096a9daf7018-3245207.jpg)
  * ####  <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">链式模式匹配算法</span>

   * <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">精髓：定义三个指针------first,sptr,tptr
        * <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">用first指示当前剩余字符串中的第一个</span>
        * <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">用sptr从first位从前往后匹配</span>
        * <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">用tptr指示待匹配的值并后移</span>
        * <span class="content mubu-node" images="%5B%7B%22id%22%3A%2221b16b07a0c87903f-3245207%22%2C%22uri%22%3A%22document_image%2F3e78d3b4-f091-44f3-9880-8c461da739c4-3245207.jpg%22%2C%22ow%22%3A697%2C%22oh%22%3A434%2C%22w%22%3A410%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">一旦不一致，first后移，sptr重置，tptr重置</span><div style="padding: 3px 0">![](https://img.mubu.com/document_image/3e78d3b4-f091-44f3-9880-8c461da739c4-3245207.jpg)</div></span>
   ## <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数组</span>

  * ### <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">稀疏矩阵三元组表</span>

 >三元组=（行i，列j，非零元素值）——行优先

  * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2214316b07a2cce507a-3245207%22%2C%22uri%22%3A%22document_image%2Fb4a6e555-b7dc-4efd-936d-e1f2d803047f-3245207.jpg%22%2C%22ow%22%3A463%2C%22oh%22%3A238%2C%22w%22%3A339%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数据结构描述</span>
 ![](https://img.mubu.com/document_image/b4a6e555-b7dc-4efd-936d-e1f2d803047f-3245207.jpg)

  * <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">三元组----先用一个node类型的一维数组储存一类值，然后在值内分配 i,j,v三个属性，从而超越了二维属性的限制</span>

  * #### <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">转置算法</span>

   *   <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">本来应该直接把存储的行号列号交换一下就可以，但这样得到的是列优先的稀疏矩阵，我们需要行优先的</span>

        *   <span class="content mubu-node" images="%5B%7B%22id%22%3A%222d516b07a92f2d094-3245207%22%2C%22uri%22%3A%22document_image%2F1937b2ff-1c4a-4f04-b0d5-08a2ff50968a-3245207.jpg%22%2C%22ow%22%3A919%2C%22oh%22%3A817%2C%22w%22%3A352%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">第一步只是把“行数”和“列数”转换，并未对实际矩阵产生影响；第二步才是按列查找（因为它们转置成了行，而我们要以行优先储存），双重循环，才能实现排序！从0开始（因为它们是之后的行号）</span>
      ![](https://img.mubu.com/document_image/1937b2ff-1c4a-4f04-b0d5-08a2ff50968a-3245207.jpg)
   ## <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">栈</span>

   * ### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2212416b08026ac5187-3245207%22%2C%22uri%22%3A%22document_image%2Ff4eecf57-f98b-4f6f-955b-d466ed2d49ff-3245207.jpg%22%2C%22ow%22%3A389%2C%22oh%22%3A108%2C%22w%22%3A332%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">定义</span>
 ![](https://img.mubu.com/document_image/f4eecf57-f98b-4f6f-955b-d466ed2d49ff-3245207.jpg)

   * ### <span class="content mubu-node" images="%5B%7B%22id%22%3A%22b16b0807bb6a193-3245207%22%2C%22uri%22%3A%22document_image%2F68a09350-4192-432b-a6c0-4817e85b19a6-3245207.jpg%22%2C%22ow%22%3A210%2C%22oh%22%3A448%2C%22w%22%3A109%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">形象结构</span>
      ![](https://img.mubu.com/document_image/68a09350-4192-432b-a6c0-4817e85b19a6-3245207.jpg)
  * ### <span class="content mubu-node" images="%5B%7B%22id%22%3A%223bf16b0802efb9027-3245207%22%2C%22uri%22%3A%22document_image%2Fa0413bd9-e342-4dc6-b8d2-3069f89e2d2f-3245207.jpg%22%2C%22ow%22%3A855%2C%22oh%22%3A229%2C%22w%22%3A708%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">入栈</span>
 ![](https://img.mubu.com/document_image/a0413bd9-e342-4dc6-b8d2-3069f89e2d2f-3245207.jpg)
  * ### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2226916b0808c4d203e-3245207%22%2C%22uri%22%3A%22document_image%2Fc21ef859-ed45-4bc1-baf7-0fd273c75cd2-3245207.jpg%22%2C%22ow%22%3A446%2C%22oh%22%3A232%2C%22w%22%3A370%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">出栈</span>
    ![](https://img.mubu.com/document_image/c21ef859-ed45-4bc1-baf7-0fd273c75cd2-3245207.jpg)
   ## <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">队</span>

  * ### <span class="content mubu-node" images="%5B%7B%22id%22%3A%22c616b08cb2da40ff-3245207%22%2C%22uri%22%3A%22document_image%2Fd647ecdd-13cc-4c30-9ea4-b7ef116636d5-3245207.jpg%22%2C%22ow%22%3A325%2C%22oh%22%3A119%2C%22w%22%3A254%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">定义</span>
 ![](https://img.mubu.com/document_image/d647ecdd-13cc-4c30-9ea4-b7ef116636d5-3245207.jpg)

   * ### <span class="content mubu-node" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">循环队列</span>

   * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%222d916b08d164ee154-3245207%22%2C%22uri%22%3A%22document_image%2F2650eba0-a135-4454-9b36-077dd79f21ea-3245207.jpg%22%2C%22ow%22%3A517%2C%22oh%22%3A192%2C%22w%22%3A262%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">形象示例</span>
    ![](https://img.mubu.com/document_image/2650eba0-a135-4454-9b36-077dd79f21ea-3245207.jpg)

   * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2236e16b08d2e8d50bf-3245207%22%2C%22uri%22%3A%22document_image%2F60049f5e-5401-4268-9191-50d9fa874756-3245207.jpg%22%2C%22ow%22%3A779%2C%22oh%22%3A241%2C%22w%22%3A537%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">置空队</span>
      ![](https://img.mubu.com/document_image/60049f5e-5401-4268-9191-50d9fa874756-3245207.jpg)
   * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%2221f16b08d352d901b-3245207%22%2C%22uri%22%3A%22document_image%2F8aeaa621-2ae5-4a4e-8994-af0b7da6c5dd-3245207.jpg%22%2C%22ow%22%3A703%2C%22oh%22%3A272%2C%22w%22%3A515%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">入队</span>
      ![](https://img.mubu.com/document_image/8aeaa621-2ae5-4a4e-8994-af0b7da6c5dd-3245207.jpg)
   * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%221a416b08d463280d-3245207%22%2C%22uri%22%3A%22document_image%2F3c711182-1e72-4004-8981-188f27ec287e-3245207.jpg%22%2C%22ow%22%3A378%2C%22oh%22%3A481%2C%22w%22%3A248%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">出队</span>
      ![](https://img.mubu.com/document_image/3c711182-1e72-4004-8981-188f27ec287e-3245207.jpg)
   * #### <span class="content mubu-node" images="%5B%7B%22id%22%3A%221fc16b08d5be98152-3245207%22%2C%22uri%22%3A%22document_image%2F74b2007d-9014-4305-92ad-1e8cfe94395b-3245207.jpg%22%2C%22ow%22%3A779%2C%22oh%22%3A316%2C%22w%22%3A506%7D%5D" style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">关于返回指针的函数在主函数中的调用</span>
      ![](https://img.mubu.com/document_image/74b2007d-9014-4305-92ad-1e8cfe94395b-3245207.jpg)</div>

</body>
</html>
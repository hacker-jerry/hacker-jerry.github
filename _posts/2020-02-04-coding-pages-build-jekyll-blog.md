---
layout: post
title: "Coding Pages Build Jekyll Blog"
subtitle: 采用Coding平台，优化访问速度
date: 2020-02-04 11:50:02
catalog: true
tags: 
- 优化
header-img: http://blog.img.hackerjerry.top/FgqPOYxr_bQzd1cg1spbNFiADeyy
post_copyright: true
author: Jerry
---

采用Coding page自定义域名托管blog颇费周折。

首先，我采用码云gitee下载github项目，然后发现了它也有page功能，结果它不能绑定自定义域名，遂放弃。

转战coding，它在半年前还可以直接导入github的项目，结果现在

![](http://blog.img.hackerjerry.top/FknfMwNeZbTIUWI8mCUf7cWD6R_y)

只能在用gitlab中转了。

> 我为了优化访问速度，把各大代码托管商终于都逛遍了。

于是，[参考](https://www.cnblogs.com/tsingke/p/9632913.html)

![](http://blog.img.hackerjerry.top/FgKb9vJ3zsv8wezrbTai7xIGGeSD)

然后就是添加公钥

参考[官方文档](https://help.coding.net/docs/project/features/ssh.html?_ga=2.192796386.999518034.1580722898-79781026.1562586775)或者[博客](https://blog.csdn.net/weixin_41196185/article/details/79234078)

![](http://blog.img.hackerjerry.top/Fns9c0bRonbbz4rOcl_6UBhUvfAZ)

然后完全按照https://10101.io/2018/09/18/Blog_3的来

结果在push的时候我输错账号了，然后系统把那个临时凭据一直提交导致push失败，我又参考了https://blog.csdn.net/qq_41306610/article/details/85000771 把那个密码给修改了才成功push
![](http://blog.img.hackerjerry.top/FpbvGVHQHKbaVigQ6QRtbDibg4L5)

就在我兴冲冲地准备在coding上开启page服务的时候，我怎么也没有找到开关，

![](http://blog.img.hackerjerry.top/FlIxArPbMC6hw7fA_9JceZ-feT9V)

然后我查了一下，

<img src="http://blog.img.hackerjerry.top/Fq3j_4lVDK7mbVoZaZ_zssl50443" style="zoom: 77%;" />

？？？融合升级了？？

![](http://blog.img.hackerjerry.top/Fm7ZaOPff04-AEKVxa-525N9BCNZ)

~~官方说1月20日开始就开始融合升级了，然后最近疫情的原因，它一直没有上班……然后……暂停注册……看样子一时半会是优化不了CDN了，留个坑。~~

我又重新看了一下官方文档，原来是选择错了项目，应该是`DevOps项目`

![](http://blog.img.hackerjerry.top/FqEWJO35JZTXaBBYjm3p1SiMO2-r)

- [将 Jekyll 博客同时托管在 Github Pages 和 Coding Pages ](https://10101.io/2018/09/18/Blog_3)

- [详细记录使用jekyll/GitHub/Coding搭建个人博客全过程](http://www.shenl.com/2016/08/19/hello-jekyll/)

- [旧版Coding Pages](https://blog.csdn.net/qq_36667170/article/details/79318665)

- [实现Github和Coding仓库等Git服务托管更新](https://www.cnblogs.com/selier/p/9634418.html)

然后真的弄好Page后，发现coding的服务器好慢……比github还慢，而且昨天我记得修改了一个git的config文件，结果今天怎么也搜不到，然后github desktop不能push了，只能命令行了。~~以后再想法子解决吧。~~

![](http://blog.img.hackerjerry.top/FsExmao3Ry3BLDd0pBb1txL66V__)

然后发现，原来是github客户端不支持同时git提交github和coding，~~又介于coding page性能如此不佳，我还是用github做服务器吧……~~

但是我不甘心呀，我就又查，发现大概是我的项目名称搞错了？

就是说，必须是`项目名=用户名`,像这里

![](http://blog.img.hackerjerry.top/FmxxiqJyjW6-7uXKGSuYlSsr6rUb)

这里再多提供一个[阿里在线域名检测工具](https://zijian.aliyun.com/?spm=a2c1d.8251892.content.3.66695b76g71m9J#/domainDetect)

![可以看出它确实指向了Coding-Page](http://blog.img.hackerjerry.top/FsCT9cLuLuXOOygTcdNBj4il1bl-)
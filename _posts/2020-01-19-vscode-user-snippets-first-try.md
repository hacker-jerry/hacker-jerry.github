---
layout: post
title: "Vscode User snippets First Try"
subtitle: 自定义代码标签
date: 2020-01-19 16:52:20
catalog: true
tags: 
header-img: 
post_copyright: true
author: Jerry
---

自定义代码片段是为了更加高效的输入某些标签（暂时对于html），方法也很简单。

<img src="http://blog.img.hackerjerry.top/FgvRTAPdULovqI9w55GeqQCtnej3" style="zoom:67%;" />

这里面的`user snippets`,点击后

<img src="http://blog.img.hackerjerry.top/FmkFVuOCllNH6lXcGO26cGSUSYR0" style="zoom: 67%;" />

直接搜对应的文件类型或创建全局文件，然后创建对应的`json`格式的片段，例如：

```json
"set tipi": {  
        "prefix": "tipi",  
        "body": [ 
			"<div class=\"tip inlineBlock important\">$0</div>",
        ],
        "description": "set_important_tip"  
	},
	"set tips": {  
        "prefix": "tips",  
        "body": [ 
			"<div class=\"tip inlineBlock success\">$0</div>"
        ],
        "description": "set_success_tip"  
	},
	"set tipw": {  
        "prefix": "tipw", 
        "body": [  
			"<div class=\"tip inlineBlock warning\">$0</div>"
        ],
        "description": "set_warning_tip" 
    }
```
>注意！json文件不能加注释……虽然它的确能执行但是！官方是不允许加注释的！

而我希望在markdown文件中实现这个智能联想的功能，但是并没有（vscode的小bug），反馈给官方之后得到的折中方案是手动触发联想，具体操作是`ctrl+space`，但是，win系统这个快捷键基本都是绑定的切换输入法，所以我换了一下默认的绑定，比如`alt+x`，就成功啦。



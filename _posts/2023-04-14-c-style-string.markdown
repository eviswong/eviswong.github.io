---
layout: post
title:  "带有引用计数的C风格字符串设计"
date:   2023-04-14 16:41:17 +0800
categories: jekyll update
---

在大型项目中，与OS打交道的功能，常常要调用 OS Api （比如 NT Api)。而这些API都是由 C 语言写成的。为了更好的兼容性，最好使用 C 语言开发这部分功能。


比如我最近开发的性能监控软件，它的结构如下。
![structure](assets\c-style-string-with-ref-counting\structure.png)


---
layout: post
title:  "TSC静态景物制作教程"
date:   2023-04-18 14:05:17 +0800
categories: jekyll update
---
# TSC 静态景物制作教程

## 我的环境
* 游戏版本： Train Simulator Classic
* Autodesk 3dsmax **2017**
* Adobe Photoshop CS 6

## 前期准备
关于制作模组前的前期准备，你可以看[这篇文章](https://eviswong.github.io/jekyll/update/2023/01/05/provider-product-setup.html)。

## 建模要点
### 塌陷所有修改器
其实把 **Collapse** 翻译为**塌陷**，是很生硬的。 **Collapse**指的是把所有修改器所产生的效果"合体"。执行塌陷后，模型的修改器堆栈上只能看到 **Editable Poly**。

### 检查模型命名
模型命名必须要是 *x_xxxx_name*。name不一定要和插件的名字重名。这里，x 代表 LOD 级别， xxxx代表可视距离。这里我先用 *1_1000_object* 做名字。
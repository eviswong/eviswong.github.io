---
layout: post
title:  "TSC线性景物制作教程"
date:   2023-04-17 16:41:17 +0800
categories: jekyll update
---
# Train Simulator Classic 线性景物制作教程

## 我的环境
* 游戏版本： Train Simulator Classic
* Autodesk 3dsmax **2017**
* Adobe Photoshop CS 6

## 写在最前
制作线性景物的方法，在 [Train Simulator 官方文档](https://sites.google.com/a/railsimdev.com/dtgts1sdk/reference-manual/art-guidelines/procedural-lofted-geometry)中描述，国内也有一些教程有说明，但是这些教程忽略了很多细节。这篇教程中，通过“护栏”实例，记录我在制作线性景物时所踩的坑。希望大家少走弯路。

![最终效果](assets/procedual-lofted-scenery-tutorial/preview.jpg)

## 3DsMax 单位设置
为了保证模型的正确比例，在3dsmax 中需要设置单位。 Train Simulator 要求单位设置为**Meter**。但是为了精确建模，通常将单位设置为**Centimeter**，并在导出时，利用RwPlugin的单位转换功能，做一次单位转换。这么做，同样可以保证模型的比例。






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

![最终效果](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/preview.jpg)

## 单位设置
为了保证模型的正确比例，在3dsmax 中需要设置单位。 Train Simulator 要求单位设置为**Meter**。但是为了精确建模，通常将单位设置为**Centimeter**，并在导出时，利用RwPlugin的单位转换功能，做一次单位转换。这么做，同样可以保证模型的比例。

![单位转换](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/preview.jpg)

## 线性景物原理（1）
Train Simulator 生成线性景物的方法非常简单，就是对**X-Z平面**上的线条轮廓沿着**Y轴正方向**挤出，形成一个三维对象。

![样条线](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/fig41.png)

如图所示。马路的轮廓用红线标出，这条轮廓处于 **X-Z**平面上。Train Simulator 会把这条轮廓沿着**Y轴正向**挤出，形成一个三维的平面。

## 建模（1）
了解原理之后，可以很快做出模型。具体的建模过程我就不多说了,但是下面几点一定要注意。



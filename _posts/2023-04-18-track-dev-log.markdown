---
layout: post
title:  "TSC轨道开发日志"
date:   2023-04-18 12:34:17 +0800
categories: jekyll update
author: Evis Wong
---
# TSC 静态景物制作教程

* 游戏版本： Train Simulator Classic
* Autodesk 3dsmax **2017**
* Adobe Photoshop CS 6

## 写在最前
从头搭建属于自己的铁路沙盘，一直是我的梦想。千里之行，始于足下，我决定从制作第一条属于自己的轨道开始。 轨道的制作方式很简单，但是制作既好看，又省资源的轨道，是没有那么容易的。

我花了几天时间研究，达到了下面的效果。

![预览1](https://eviswong.github.io/assets/track-dev-log/preview_0.png)

![预览2](https://eviswong.github.io/assets/track-dev-log/preview_1.png)

![预览3](https://eviswong.github.io/assets/track-dev-log/preview_2.png)

把天气设为冬天后，积雪模型会显现出来，覆盖在铁路上，只露出钢轨。

![冬季预览1](https://eviswong.github.io/assets/track-dev-log/preview_wi_0.png)

## Procedual Lofted Object & Populated Object
Loft 有一个意思，在字典上查不到，叫“放样”。它是指，将某个二维轮廓沿一定路径移动，以产生某种三维物体。 *Procedual Lofted Object*就是我们熟悉的“线性景物”。关于制作线性景物的方法与技巧，你可以看我写的这篇文章。不过，我们在这里不是为了咬文嚼字，而是要讨论现有的轨道制作方案。也就是说，怎么样把道砟、枕木和轨道搭配起来，既能满足视觉，又能节约内存？

### 方案一
第一种方案，是大多数人常用的。这种方法把枕木和轨道做成线性景物，而把枕木模型“附加”在轨道模型上，每隔一段距离（Population Frequency）就生成一个。这种方法非常简单，而且枕木的距离精准，可以很容易的制作出想要的插件。

影响视觉的重要因素之一，就是“重复”。如果你的模型出现了重复的纹理，马上就会产生一种“穿帮”的感觉。而且，如果存在密集的、同方向的物体，会产生“摩尔纹”。

### 方案二


## 纹理
现在 PBR 技术已经非常成熟了。但是 PBR Workflow 只适合 TS 的静态景物， 而且不能完全发挥出威力。对于轨道这种“线性景物”来说，使用处理过的真实照片作为纹理，效果更好一些，插件的开发速度也相对快些。

我利用 Photoshop 的 “透视裁剪” 功能，从自己拍摄的多张真实照片上取样。调整图层的曝光度、色相、饱和度后，利用“仿制图章”和“污点修复”把这些照片片段合成一张“纹理”。

>为了保证足够的分辨率。建议使用单反相机拍摄，并保证光照均匀。


![]()

*【注】：以上照片拍摄于深圳罗湖区“工业站“文化园。*

## 材质
从 TS 官方发布的最新信息来看。TS 的图形 API 还是 Direct3D 9，它非常落后（目前主流游戏大多采用 Direct3D 11 / 12 做图形API）。所以 TS 材质所支持的效果并不多，只有 5 种：
* Diffuse (漫反射)
* Speculate （反射）
* Normal (法线)
* AO （环境光遮蔽）
* Transparent （透明）

这五种进行任意组合，就是大家在 3dmax 中所看到的，那些以 **.fx** 后缀结尾的选项。这些 .fx 文件决定了物体在 TS 世界中的渲染结果。

我的轨道材质以 Diffuse + Normal 为主（TS 的线性景物支持法线效果，着色器名字为 * *），并没有使用 AO 贴图（主要是因为懒）。

为了使用纹理中的 Alpha 信息，需要开启 TRANSPARENT 选项。

## 季节

TS 只能在不同的季节显示不同的贴图，但不能在不同的季节显示不同的模型。

季节贴图的制作方法非常简单。如果我的轨道贴图集里，有一张贴图为 *Ballast_wood_1.ace*。你只要把对应的冬季贴图，改名为 *Ballast_wood_1_wi.ace*，再把 Previewer 的季节设置为“冬季", 就可以看到效果了。

贴图的表现力还是远远不够的。比如在冬季时，想要模型产生积雪效果，用贴图就没法做到了。

但我们可以曲线救国，通过贴图的 *Alpha* 通道控制特定模型的显示与隐藏。

【未完待续】

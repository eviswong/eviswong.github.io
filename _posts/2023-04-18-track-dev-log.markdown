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

## 材质
TS 的自由度并不太高，而且也不支持 PBR ，只能支持 Diffuse（漫反射） / Speculate （反光）/ Transparent（透明） / Normal (法线) 四种贴图。 但可以只使用这四种贴图，做出惊人的效果。

## 季节

TS 只能在不同的季节显示不同的贴图，但不能在不同的季节显示不同的模型。

季节贴图的制作方法非常简单。如果我的轨道贴图集里，有一张贴图为 *Ballast_wood_1.ace*。你只要把对应的冬季贴图，改名为 *Ballast_wood_1_wi.ace*，再把 Previewer 的季节设置为“冬季", 就可以看到效果了。

贴图的表现力还是远远不够的。比如在冬季时，想要模型产生积雪效果，用贴图就没法做到了。

但我们可以曲线救国，通过贴图的 *Alpha* 通道进行控制。

【未完待续】

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

## 建模
了解原理之后，可以很快做出模型。具体的建模过程我就不多说了,但是下面几点一定要注意。

* 模型轮廓的坐标 ： 形成轮廓的所有顶点（红色点）必须在**X-Z**平面上，也就是说，它们的**Y**坐标必须为0。


* 挤出方向：一定要向Y轴正向挤出。


## 纹理
### UV展开
处理线性景物的UV，有一个原则。就是**平行于Y轴的边，它的UV要与V轴平行**。这句话看起来很抽象，但我用一个图演示，你就明白了。

![UV对应关系](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/unwrap-uv.jpg)

选中的边（紫色）和它UV数据的对应关系，用绿色的线表示。 如果你让X方向边所对应的UV，与U轴平行，会导致纹理错乱。


>很多教程都提到线性模型的UV要“沿Y轴展开”，但我表示困惑。因为UV数据是不存在XYZ轴的，UV只有U轴和V轴。

至于是否需要让UV平铺，我认为并不是那么重要，但可能会导致模型上的纹理存在接缝。

## 材质


## 导出
在导出前，最好做一些检查。如果有一些地方做错了，会导致模型无法显示。
### 命名
名称没有特殊的要求，遵循 Train Simulator 的命名规则即可。我这里的名字是 *1_1000_fence*。
### Reset Pivot
![Reset xForm](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/reset-pivot.jpg)

### Reset xForm
[Reset xForm](https://help.autodesk.com/view/3DSMAX/2023/ENU/?guid=GUID-B98414B9-4F28-45F4-A1F4-9DA994548ED9) 并不是3dsmax所独有的操作。只要你在3D软件之间传递数据（模型互倒），必须进行这至关重要的一步(但我所看过的教程中，都没有提及)。

在导出模型之前，你需要对模型添加 *Reset xForm*，结果如下：

![Reset xForm](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/reset-xForm.jpg)
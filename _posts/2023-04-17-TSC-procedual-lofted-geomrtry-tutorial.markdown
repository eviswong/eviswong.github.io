---
layout: post
title:  "TSC线性景物制作教程"
date:   2023-04-17 16:41:17 +0800
categories: jekyll update
author: Evis Wong
---


## 我的环境
* 游戏版本： Train Simulator Classic
* Autodesk 3dsmax **2017**
* Adobe Photoshop CS 6

## 写在最前
制作线性景物的方法，在 [Train Simulator 官方文档](https://sites.google.com/a/railsimdev.com/dtgts1sdk/reference-manual/art-guidelines/procedural-lofted-geometry)中描述，国内也有一些教程有说明，但是这些教程忽略了很多细节。这篇教程中，通过“护栏”实例，记录我在制作线性景物时所踩的坑。希望大家少走弯路。

![最终效果](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/preview.jpg)

## 单位设置
为了保证模型的正确比例，在3dsmax 中需要设置单位。 Train Simulator 要求单位设置为**Meter**。但是为了精确建模，通常将单位设置为**Centimeter**，并在导出时，利用RwPlugin的单位转换功能，做一次单位转换。这么做，同样可以保证模型的比例。

![3DsMax单位设置](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/unit_settings.png)![导出时的设置](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/unit_convert.png)



## 线性景物原理
Train Simulator 生成线性景物的方法非常简单，就是对**X-Z平面**上的线条轮廓沿着**Y轴正方向**挤出，形成一个三维对象。

![样条线](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/fig41.png)

如图所示。马路的轮廓用红线标出，这条轮廓处于 **X-Z**平面上。Train Simulator 会把这条轮廓沿着**Y轴正向**挤出，形成一个三维的平面。

## 建模
了解原理之后，可以很快做出模型。具体的建模过程我就不多说了,但是下面几点一定要注意。

* 模型轮廓的坐标 ： 形成轮廓的所有顶点（红色点）必须在**X-Z**平面上，也就是说，它们的**Y**坐标必须为0。

  ![坐标](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/modeling_1.png)


* 挤出方向：一定要向Y轴正向挤出。

  ![朝向](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/modeling_2.png)


## 纹理
### UV展开
处理线性景物的UV，有一个原则。就是**平行于Y轴的边，它的UV要与V轴平行**。这句话看起来很抽象，但我用一个图演示，你就明白了。

![UV对应关系](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/unwrap-uv.jpg)

选中的边（紫色）和它UV数据的对应关系，用绿色的线表示。 如果你做对了，会是下面这种效果。

![UV错乱](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/right_uv.png)


>很多教程都提到线性模型的UV要“沿Y轴展开”，但我表示困惑。因为UV数据是不存在XYZ轴的，UV只有U轴和V轴。

如果你让Y方向边所对应的UV，与U轴平行，会导致纹理错乱。

![UV错乱](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/wrong_uv.png)

至于是否需要让UV平铺整个空间，我认为并不是那么重要，但可能会导致模型上的纹理存在接缝。

![UV不平铺](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/scaled_uv.png)

## 材质

### 着色器

你只要使用*LoftTexDiff.fx*着色器即可。如果你的纹理中包含alpha通道（透明），请使用*LoftTexDiffAlpha.fx*，并进行如下设置。

![UV不平铺](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/transparent_material.png)

### 贴图格式

如果你的纹理格式为**.tga**，请将它转换为**.ace**。

> 如果你使用**.dds**格式的纹理，不需要转换为**.ace**

> 纹理格式转换有个小技巧， 你只要把要转换格式的纹理拖到 *RwAceTool.exe*图标上，就可以得到**.ace**格式的纹理了。

## 导出

在导出前，最好做一些检查。如果有一些地方做错了，会导致模型无法显示。
### 命名
名称没有特殊的要求，遵循 Train Simulator 的命名规则即可。我这里的名字是 *1_1000_fence*。
### Reset Pivot

确保你的模型**Pivot**位于(0,0,0)处。可以通过**Hierarchy->Pivot->Affect Pivot Only**进行调整。

![Reset xForm](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/reset-pivot.jpg)

### Reset xForm
[Reset xForm](https://help.autodesk.com/view/3DSMAX/2023/ENU/?guid=GUID-B98414B9-4F28-45F4-A1F4-9DA994548ED9) 并不是3dsmax所独有的操作。只要你在3D软件之间传递数据（模型互倒），必须进行这至关重要的一步(但我所看过的教程中，都没有提及)。

在导出模型之前，你需要对模型添加 *Reset xForm*，**Utility->Reset xForm->Reset Selected**. 结果如下：

![Reset xForm](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/reset-xForm.jpg)

## 蓝图

在 **Blueprint Editor** 中新建一个 *Loft Section Blueprint*。在目前阶段，你只需要填如下两项即可。填写完毕后，点**Preview**可以预览你的线性景物。

![Blueprint设置](https://eviswong.github.io/assets/procedual-lofted-scenery-tutorial/blueprint_1.png)

## 增加细节

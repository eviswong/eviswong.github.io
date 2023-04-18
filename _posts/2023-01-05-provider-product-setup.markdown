---
layout: default
title:  "TSC插件开发前期准备"
date:   2023-01-05 18:05:17 +0800
categories: jekyll update
---
# Train Simulator 创建你自己的插件
## 创建目录
如果你是个木匠，那你一定要有工作室。不同型号的钉子、钻头都要分门别类地装到盒子里。在开发Train Simulator(简称TS)插件之前，你需要搭建自己的工作目录。

你需要来到 TS 根目录下的 Source 文件夹，在这里面创建如下的目录树
```
Source *
       |--ProviderName *
                       |--ProductName *
                                      |-- Scenery
```

* *Provider Name* 指的是工作室的名称。 TS 插件开发者遍布全球，是谁家的插件，需要加以区分。

* *ProductName* 指的是插件名。一个工作室可能开发很多插件，不同的插件拥有不同的名字。

* *Scenery* 是一个固定的名称，它会被 Blueprint Editor 所识别。你所创建的所有插件，都要放在这个目录下。

除了 *Scenery* 文件夹，你还可以创建别的。 如果你要制作音效，可以创建一个 *Audio* 文件夹。 当然，这些文件夹都是 TS 固定的。

![文件目录](https://sites.google.com/a/railsimdev.com/dtgts1sdk/reference-manual/content-basics/provider-product-setup/add-on-folder-structure/fig001.PNG?attredirects=0)

当你想使用自己的插件时，可以在下拉列表里找到对应的 *Provider Name*，并勾选 *Provider Name*，就可以看到想要的插件。

![active object set](https://sites.google.com/a/railsimdev.com/dtgts1sdk/reference-manual/content-basics/provider-product-setup/using-provider-product-assets-in-train-simulator/UsingProviderProduct1.jpg?attredirects=0)

![active object set](https://sites.google.com/a/railsimdev.com/dtgts1sdk/reference-manual/content-basics/provider-product-setup/using-provider-product-assets-in-train-simulator/UsingProviderProduct2.jpg?attredirects=0)

## 配置 3DsMax
[敬请期待]
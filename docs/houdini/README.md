# Houdini相关概述

## 阅读提示

>* 注意：其中的记录难免有错误，如果发现问题所在联系我，我会加以改善.
>* 如果提出的建议仍有争议及准确度欠佳，我会被和业内人员交流存废或者保留并标注争议部分。
>* 所有内容我尽量是中立性，但是，在内容也会带有明显的个人观点。
>* 本文是在持续不断的扩充中。

## 文档说明

### Houdini简介

* Houdini （电影特效魔术师） Side Effects Software的旗舰级产品，是创建高级视觉效果的有效工具，因为它有横跨公司的整个产品线的能力，Houdini Master为那些想让[电脑动画](https://baike.baidu.com/item/电脑动画/3927561)更加精彩的动画制作家们提供了空前的能力和工作。
* Houdini自带的渲染器是Mantra，是完全基于节点模式设计的产物，其结构、操作方式等和其它的三维软件有很大的差异。Houdini也有第三方渲染器的接口，比如：[RenderMan](https://zh.wikipedia.org/wiki/RenderMan)、[Mental ray](https://zh.wikipedia.org/wiki/Mental_Ray)、[V-Ray](https://zh.wikipedia.org/wiki/V-Ray)和Torque等，可以把场景导出到这些渲染引擎进行渲染。
### 软件目前的状态

| 软件名称 | Houdini | 软件语言 | 英文|
| :----: | :----: | :----: | :----: |
| 开发商 | Side Effects Software Inc.（简称SESI） | 软件大小 | 至少要求 900MB 磁盘空间 |
| 软件平台 | Windows（64bit）、Linux、Mac OS | 软件授权 | 未知 |
| 软件版本 | houdini 18 | 软件分类 | 三维建模渲染和三维动画制作 |
| 更新时间 | 2020 | 脚本语言 | python |

### 模组介绍

* Objects Object scene 场景描述模块
* SOPs Surface OPerations 表面编辑模组
* POPs Particle OPerations 粒子编辑模组
* CHOPs CHannel OPerations 通道编辑模组
* COPs Compositing OPerations 图像合成模组
* SHOPs Shader OPerations 材质编辑模组
* VOPs Vex OPerations VEX模组
* Outputs Render outputs 渲染输出模块
* DOPs Dynamics OPerations 动力学编辑模组
### 使用的脚本
#### HOM

Houdini在9.0的时候加入了对Python的支持，成为替代HScript的脚本，为了保持文件在各版本间自上而下的兼容，HScript现在还是保留的，但推荐使用Python。你可以用python建立一个自定的节点。和vex写的节点有所不同，Python SOP可以允许建立或删除几何体，当然它的速度是不比vex的。目前HOM还没有完善，仅限于建立SOP node。
#### VEX   

VEX是Vector EXpression的简称，是一种处理大量数据的高性能脚本语言，语法类似C语言，对有编程背景的人来说很容易学。Houdini里的很多地方使用VEX来处理数据。Houdini和Mantra里使用SIMD来实现VEX。Houdini里的VOPs，表示Vex OPerators，用于以节点方式建立VEX操作和材质。你可以用VEX建立以下类型的自定义节点：
* ·Modeling
* ·Rendering用于编写shader，
* ·Compositing
* ·Particle
* ·Channel Operator
* ·Fur
#### HScript

Houdini的一种脚本语言，逐步会被Python所取代。



## 主要内容

本模块主要添加的内容和houdini相关。包括二次开发、渲染等的基本使用，已经异常处理的方法，并且会加入版本说明。

## 文件结构
等待更新

## 附加说明

### 外部链接

#### 公司和产品相关

* Houdini产品官网[点击进入](https://www.sidefx.com/)
* Houdini讨论区[点击进入](https://www.sidefx.com/forum/)

#### 帮助文档
后续更新

### 参考文献
* 维基百科
* Houdini发布页
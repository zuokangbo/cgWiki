# UV的原理

## uv的原理详细的介绍

关于物体的坐标，不仅仅是xyz轴，而是位置：XYZ  旋转：欧拉XYZ  缩放：XYZ  
总共是9个数值。
![uv](http://artiststd.xyz/blender/UVuv.jpg)
而纹理的坐标只有两种。纹理坐标有两种  矢量和向量，都是3个数值。

下面是生成的坐标数据。
![uv](http://artiststd.xyz/blender/UVuv1.jpg)
黑色是数值的一部分 0为黑色 1为轴的颜色  中间是混合。
![uv](http://artiststd.xyz/blender/UVuv2.jpg)
这个是UV的原理。

只要能控制X轴和Y轴的色彩  就能控制纹理的位置。
分离后是1个数值  合并是3个数值  注意  矢量是3个数值组合而成的。

注意：物体空间位置是由9个数值组合而成的。

## 演示部分

移动颜色，控制贴图的位置：

![uv](http://artiststd.xyz/uv_3.gif)

![](http://artiststd.xyz/blender/uv/blender_uv_4.gif)

![](http://artiststd.xyz/blender/uv/blender_uv_5.gif)

![](http://artiststd.xyz/blender/uv/blender_uv_6.gif)

## 详解

从黑色到坐标颜色  代表轴的数值 
这里
0为：X坐标轴=0  
1为：X坐标轴=1
中间是0-1的数值

![](http://artiststd.xyz/blender/uv/blender_uv8.jpg)

![](http://artiststd.xyz/blender/uv/blender_uv9.jpg)

**这个空间称为01空间  也就是所谓的UV**

并且这个精度和贴图的精度也有关系，比如：

![](http://artiststd.xyz/blender/uv/blender_uv11.jpg)

![](http://artiststd.xyz/blender/uv/blender_uv10.jpg)

如果知道了这些，还需要明白一些颜色计算的原理，这样就能随心所欲的改变uv的状态。

比如：
原本的X轴是左边   他给变成右边那样。
![](http://artiststd.xyz/blender/uv/blender_uv12.jpg)

![](http://artiststd.xyz/blender/uv/blender_uv13.jpg)

用贴图直观感受下  就是这样的。

![](http://artiststd.xyz/blender/uv/blender_uv14.jpg)

乘法：   0x2=0 ，1x2=2 
原先：0到1  
计算后：0到2 
呈现的就是放大的效果
加法：0+2=2 ， 1+2=3
原先：0到1
计算后：2到3
数值跨度不变   但是都向更高的数移动了  呈现效果就是移动。

使用加法的时候。
两个点同步移动   变形到贴图上就是移动贴图。
乘法的时候由于0乘以任何数都得0   则位置0的点不动   位置1的点倍数移动   它们的距离拉长了  贴图上表现为放大
但是，很多时候这些数值是肉眼看不出来的。
所有，超过的部分是留着用作其他的计算或者其他的使用目的。
通常说 黑色为0  白色为1   但是数值可以再加  1以上就会更白  黑一下就会更黑。我们能看到的九十0到1的范围。超过就无法感知。

在显示的屏幕上，显示器每个单元有RGB三个灯组合而成  每个灯都有极限亮度  极限亮度为1   灯灭了为0    超过1的数值  灯无法表示。

所以得出一个道理。
超过1的数值不是用于表达颜色用的  矢量数用于纹理坐标，明度用于灯光。
比如你在场景里要做一个太阳  太阳照度很强  这个时候需要一个很大的数值来计算它的明度  这是明度的作用。

# Mari基础篇

## Project项目创建

1.安装完Mari后首先我们要特别注意的是设置好**Mari的缓存路径**，我们要选择一个相对内存比较大空间来储存制作信息。Mari本身对电脑的硬件要求很高，若不注意这一步，后面的操作可能因为内存不足导致电脑运行迟缓.

![images](http://artiststd.xyz/mari_basic_1.jpg)

![images](http://artiststd.xyz/mari_basic_2.jpg)


上图是Mari的缓存路径以及视图操作更改位置。

## 基本视图操作：

* Alt+鼠标左键旋转。
* Alt+鼠标右键缩放。
* Alt+鼠标中键平移。
* Edit--Preference--Navigate中可修改Maya、MAX等软件操作方式，这边我修改为Maya。

## 初识项目视图

![images](http://artiststd.xyz/mari_basic_3.jpg)

项目视图中我这边介绍一下Open Archive跟Archive。Archive是对项目文件进行打包的一个命令，可以用来对项目文件进行导出，输出为Mra格式，以便在不同的电脑上打开使用。
Open Archive则是打开的意思了。

![images](http://artiststd.xyz/mari_basic_4.jpg)

## 创建项目
1.用习惯老版本的朋友应该对新版本界面有点陌生，下面我对新老版本项目创建界面做个简单的对比。

![images](http://artiststd.xyz/mari_basic_5.jpg)    
![images](http://artiststd.xyz/mari_basic_6.jpg)

2.明显4.1版本变化了很多，它将每一块区域都单独给了一个面板，不像老版本一样把命令都挤在一块面板上。（新版改变的位置我也用不同颜色的线条给标记出来了，一一对应）
3.下面我们来开始介绍面板中常用的导入功能，如何将贴图以及模型导入进Mari。

![images](http://artiststd.xyz/mari_basic_7.jpg)

如图所示，点击Geometry下方路径位置点开，选择自己的OBJ文件存放位置打开即可，图中绿框Ptx文件格式我会在下方给大伙一个网上编译。Abc格式的话就是一个代理文件格式了(在场景中常用的缓存文件格式）。

  Ptex：ptex是迪士尼开发的一个纹理映射系统，Ptex的技术特点是对细分或多边形网格的每个面应用一个单独的纹理，这意味着ptex系统不需要对物体进行UV拆分即可编辑纹理材质，同时Ptex文件格式可以有效地在单个文件中存储成百上千个纹理图像。

模型有多少个面就会有多少个纹理贴图，数量可以存在几百万个，最后打包成Ptex文件供模型制作材质使用，可以用于任何三维软件。


![images](http://artiststd.xyz/mari_basic_8.jpg)


图中黄色框内标记的点解释如下：

1.Uv ifavailable，Ptex otherwise。指的是贴图绘制和无视贴图直接模型绘制。若导入的模型有UV那么软件就会自动识别成UV if available，若模型没有UV，则软件自动识别Ptex otherwise。Force Ptex是指不管模型有没有UV，软件会直接强制性选择Ptex绘制绘制方法。
我们在选择时默认UV if available，Ptex otherwise即可。

2.Create from face groups是指在其他三维软件中合并过的模型，在mari中都可以根据合并信息来对导入的模型进行分组，跟maya中的大纲视图是一个道理，方便选择。

3. Merge Geometries into one，是将模型合并成一个，若是模型中有很多零部件，建议是选择这个。Createseparate Geometries是创建分离的模型，适用与零部件不是很多的模型。

## Channels通道讲解

![images](http://artiststd.xyz/mari_basic_9.jpg)


  1.导入模型后咱们切换到Channels通道层，图中1.2.3.即时导入贴图的步骤了，若模型做好了纹理材质，可以这样导入进来，我们可以点击Scan来扫描出导入文件夹内的信息。
  2.在通道这一层需要注意的是：

1.Creat是单独创建通道，而Import是导入纹理信息，这里可以根据需要来打钩，一般若是导入制作好的颜色图时要把两者都勾上，若单独在Mari中创建通道的话只要勾上Create即可。

2.Size下方可以修改贴图尺寸。

3.Colorspace：一般制作颜色图都是用SRGB，默认即可，但是使用遮罩或是置换时就可以切换Linear形式。

4.Type下方可以修改贴图类别，是颜色图还是灰度图，例如：导入置换，Mask，bump等就要切换color为scalar。

5.File Space:如果是绘制普通贴图的时候就默认选择Normal，如果要绘制特殊贴图就选择Vector矢量贴图，Flipped Y(Normal、Vector）翻转Y轴矢量或是Normal。（不太懂的朋友这边可以不用管，默认即可）

6.Fill意思是给创建好的贴图填充一个底色，一般都是50%灰。

7.Depth：色彩深度，根据需要可以在8位.16.位.32位之间切换。

8.在导入贴图时若是选择整个文件夹导入的话，之后点击Scan会扫描出各种格式的文件，这里需要注意！（绿框已提醒）

## 创建新通道演示

![images](http://artiststd.xyz/mari_basic_10.jpg)

在通道栏下方空白处右键单击Add Custom即可添加新的通道，
Color处可以修改填充颜色，50%灰度，绿框中标记修改位置。Intensity 0.5强度。

Creat New Project！！！
新项目创建完成

![images](http://artiststd.xyz/mari_basic_11.jpg)

这就是项目创建完成后Mari的视图面板。

在图中我用绿色线框标记的窗口都是可以通过右边红色窗口控制的。觉得面板多看起来花就可以点击红色框中的命令收起打开需要面板。

### 视图操作


按键操作：（Mari4.1这个版本跟之前其他版本的UI摆放改变了很多，重要的工具我在下文基本都会用绿线标记改动位置）

快捷键S：切换到选择工具;
快捷键P：绘画工具;
选择工具：选择工具分几种选择类型，大致是（框选、套索、直线框选、按UV选择）shift加选、ctrl减选(工具栏的工具基本跟ps是很相似的）

快捷键：(哎哎哎，这些百度有，到处都是！）我就搬运.ahhhh
E：橡皮擦.
J：调色板.
I：选择热盒.
K: 笔刷选择.
P：基础绘制.
W+左键拖动旋转笔刷.
Q+左键拖动压缩笔刷.
R+左键拖动调整笔刷大小.
O+左键拖动调整笔刷透明度.
B：烘焙纹理（可以设置为自动烘焙）.
U：调用image mangager中选中的图片.
L：弹出image mangager选择窗口.
C：从屏幕上吸取颜色（类似ps的吸管).
~：图章工具，直接映射图片到模型上.
D：设置前景色和背景色为黑白色，并在黑/白之前切换.
；：开启/关闭图片重复图片功能。默认超出图片绘制范围会进行裁切，开启后会重复图片。
* 操作视图会遇到的问题：
  1.当咱们把模型导进来后，发现视图操作不对劲的话，需要勾选（编辑Edit）下方（首选项Preferences）找到（Navigation导航）下方Lock To World Up打钩即可。

![images](http://artiststd.xyz/mari_basic_12.jpg)

对工具栏位置的明确以及一些显示问题：

1.  显示问题：
我们在操作过程中可能需要把一些影响操作的物件隐藏显示，比如说：模型自身网格，环境HDR,世界网格。
看下图标记：

![images](http://artiststd.xyz/mari_basic_13.jpg)

贴图的尺寸大小如何修改，以及三种显示模式的切换对比！！

![images](http://artiststd.xyz/mari_basic_14.jpg)

图中黄色框标记的就是几种材质显示模式，我们在映射纹理的时候最常用的就是Flat平光模式。

图中绿色线框内是贴图尺寸的修改位置，这里要注意的是UDIM多象限UV在Mari里是很有规矩的，Mari所能识别到的UV象限横向最多只能是十格，而纵向没有限制。这里需要大家在摆放UV的时候注意下。

## 自定义工作面板

![images](http://artiststd.xyz/mari_basic_15.jpg)

如图所示

首先咱们看到中间这个黄色框，显示这个框，只需要鼠标在菜单栏空白处右击就出来了，然后选择Selection Groups，此时mari的大纲视图就会出现在左侧。

然后咱们看到红色框内，这是mari的几种选择方式，分别是Object Mode（物体选择模式），Patch Mode(根据UV块选择)，FaceMode（面选择模式）。

![images](http://artiststd.xyz/mari_basic_16.jpg)

上图我想跟大伙讲的是Mari的工具面板其实是有很多方式可以打开的，在4.1这个版本中已经将Palettes放置在了视图最右侧，很快捷的就能打开使用，极大的提高了工作效率。这里我也建议大家可以将Mari视图面板自定义设置。

这里呢，我也把常用的工具都拖出来单独放置了。大伙可以参考。

## Mari视图切换


 Mari他分了几种视图，分别是纯UV视图，透视+UV视图，透视图，正焦视图（无透视）这几类，我们一般在映射纹理时是在无透视视图中进行。这都是根据自己喜好所定的啦。（图中红色框标记位置则是几种特殊视图的切换）。

然后Mari的正侧俯后这几种视图的切换也是有快捷键的，依次是QWERT上方的1.2.3.4.5.6.来切换。




# Arnold命令行渲染kick技巧

!> 简介。

?> Arnold 的命令行渲染器称为 kick。此渲染器读取 `.ass` 或 `.usd` 文件，使用 Arnold 渲染场景并输出图像文件。Kick 也可用于查询 Arnold 节点的参数和默认值。此外，还可用于场景调试。
Kick 包含在插件下载中。安装后，您可以在 Arnold 分发版本的 bin 子目录中找到它。

## 运行Kick

要运行 kick，请先打开 Shell（终端）。下面是 Windows 操作系统上的一个示例。

?> kick 始终从当前目录加载着色器和程序，因此请不要在有许多其他 DLL/SO/DYLIB 的文件夹中运行 kick。kick 会尝试加载每个 DLL/SO/DYLIB，检查其中是否包含着色器或程序。

```python
$ set ARNOLD_BIN_PATH=C:\solidangle\Arnold-5.0.0.0\bin
$ %ARNOLD_BIN_PATH%\kick
Arnold 5.0.0.0 [2cfbe09c] linux clang-3.9.1 oiio-1.7.12 osl-1.8.2 vdb-4.0.0 rlm-12.2.2 2017/04/10 16:48:44
No arguments. Try kick --help for a command summary
```

---------------------------------------------------------------------------------------------------------

## 可能会遇到的问题

---------------------------------------------------------------------------------------------------------

* 1. 渲染出来有水印的问题：

这个的解决方法主要是许可证未指定，可以使用以下命令查看。

![arnold_kick_03](http://artiststd.xyz/img/arnold_kick_03.png)

指定 RLM的路径添加到环境变量`RLM_LICENSE`。主要在渲染，水印问题就没了。

![arnold_kick_02](http://artiststd.xyz/img/arnold_kick_02.png)

* 2.如果ass文件中有多个相机，需要指定其中一个渲染可以使用`-c`命令来指定相机的名称：
* 3.需要注意的问题，渲染的文件只能是单帧，每个ass文件只能输出一帧文件，所有需要渲染序列，就得导出序列ass文件。不过如果文件比较大，也会导致数据量比较大，不过在一些特定下有一些优化技巧，例如只有相机动画，可以把除了相机意外的ass文件导出，最后在把导出的代理导入，选择相机一块导出，打开ass文件，找到`procedural`可以看到里面的描述信息，场景的ass信息是参考进来的，相机文件就几k大小，只有导出序列的速度就快很多了。

```
procedural
{
 name aiStandInShape
 visibility 255
 matrix
 1 0 0 0
 0 1 0 0
 0 0 1 0
 0 0 0 1
 override_nodes off
 filename "C:/Users/zuokangbo/Desktop/test/test.ass"
 declare maya_full_name constant STRING
 maya_full_name "|aiStandIn|aiStandInShape"
}
```
* 4.渲染序列ass文件的时候，有两种方法：
1. 写一个bat文件来执行，例如：

```
@echo off
REM # 设置帧的数量
set count=5

REM # 设置ass序列的文件.不包含帧和后缀
set SCENE=D:\Arnold_Export\ass\arnold_export_01\arnold_export01

REM # 设置arnold的安装路径
set MTOA_PATH=C:\solidangle\mtoadeploy\2018

set MTOA_BIN_PATH=%MTOA_PATH%\bin

REM # 设置序列渲染的for循环
for /L %%i in (1, 1, %count%) do (
     set "frame=000%%i"
     set frame=!frame:~-4!
     %MTOA_BIN_PATH%\kick.exe -i %SCENE%.!frame!.ass
)

```

2. 第二种就更简单了，输出ass序列完毕后，可以直接使用Deadline 渲染。

![arnold_kick_04](http://artiststd.xyz/img/arnold_kick_04.png)

---------------------------------------------------------------------------------------------------------

## 常用命令

* 其中一个最有用的命令是“-h”或“--help”。该命令将显示 kick 中所有可用选项的列表：

```python
kick -h
```

* 使用“-i”选项可读取 .ass 文件并对其进行渲染：

```
kick -i path/to/cornell.ass
```

* 请注意，“-i”选项非必选项，kick 会自动识别以 .ass 结尾的参数，因此以下命令也是有效的：

```
kick path/to/cornell.ass
```

* 默认情况下，渲染图像时，将弹出一个显示该图像的窗口。您可以使用“`-dw`”选项关闭该显示窗口：

```
kick cornell.ass -dw
```

![arnold_kick_01](http://artiststd.xyz/img/arnold_kick_01.png)

* 如果几何体显示为粉红色，可能是因为需要提供着色器的路径。可以使用“`-l`”标志添加该路径：

```
kick cornell.ass -l /path/to/plugin/shaders/
```

* 日志信息会发送到标准输出。您可以使用“-v `<n>`”选项提高或降低日志详细级别（默认的详细级别为 1）。详细级别最高的选项是“`-v 6`”：

```
kick cornell.ass -v 2
```

* 使用“`-v 0`”将关闭日志输出：

```
kick cornell.ass -v 0
```

* 要在输出文件中保存渲染的图像，请使用“-o”标志：

```
kick cornell.ass -o cornell.exr
```

* 使用“`-r <width> <height>`”选项可以更改渲染显示大小：

```
kick cornell.ass -r 1024 720
```

* 输出 Arnold 版本号或整个版本字符串：

```
kick -av
kick --version
```

* 输出有关许可服务器的诊断信息并列出已安装许可中的可用许可和正在使用的许可：

```
kick -licensecheck
```

* 覆盖抗锯齿采样：

```
kick cornell.ass -as 3
```

* 覆盖漫反射 GI 采样：

```
kick cornell.ass -ds 3
```

* 禁用逐步精细化模式：

```
kick cornell.ass -dp
```

* 出于调试目的，您可以在全局范围内禁用纹理、灯光和着色器、运动模糊、细分曲面、置换或 SSS 等几项功能：

```
kick cornell.ass -it
kick cornell.ass -il
kick cornell.ass -is
kick cornell.ass -imb -isd -idisp -isss
```

* 您可以使用以下命令从动态库`（.dll 或 .so）`加载自定义 `Arnold`节点进行安装：

```
kick cornell.ass -l path\to\plugin -l path\to\more\plugins
```

* 也可以使用以下命令获取所有已安装节点（内置节点和动态加载的节点）的列表：

```
kick -nodes
kick -l path\to\plugins -nodes
```

* 您可以使用“-info”检查节点：

```
kick -info polymesh
kick -info options
kick -l path\to\plugins -info custom_plugin_node
```

* 也可以获取有关给定参数的更多信息：
```
kick -info polymesh.sidedness
kick -info options.bucket_scanning
```

* 使用“`-set`”命令可覆盖任何节点的任何参数：

```
kick cornell.ass -set options.AA_samples 3
```

* 覆盖特定类型的所有节点的任何参数：

```
kick cornell.ass -set curves.mode thick
```

* 如果未找到有效的许可，则使 kick 中止渲染，而不是使用水印进行渲染：

```
kick cornell.ass -set options.abort_on_license_fail true
```

* 覆盖多个参数：

```
kick first.ass -set options.AA_samples 3 -set options.bucket_size 16
```
## 交互模式

要在交互模式下进行渲染，请使用“-ipr q”选项。这样将可以（非常粗略地）导航浏览场景，并切换到不同的调试着色模式，比如平面/平滑法线、UV、线框等：

```
kick cornell.ass -ipr q
```

* 在选定的交互模式下导航（平移/缩放）：“q”表示 `Quake` 控件` (WASD)`，“m”表示 Maya 控件（Alt + 鼠标键）。
* 使用“[”和“]”键增加或减少图像曝光。
* 在渲染窗口中单击并按小写字母“i”可忽略任何现有着色器。您可以按大写字母“I”还原场景着色器。
* `macOS` 和`Linux`：使用数字键（0、1、2、3、4、5、6、7、8、9）可在不同的调试着色模式之间切换。

## 获取所有可用的颜色空间

```
$ kick -lcs scene.ass
Available color spaces from color manager "defaultColorMgtGlobals" of type "color_manager_syncolor:
   ARRI LogC
   camera Rec 709
   Sony SLog2
   Log film scan (ADX)
   Log-to-Lin (cineon)
   Log-to-Lin (jzp)
   Raw
   ACES2065-1
   ACEScg
   scene-linear CIE XYZ
   scene-linear DCI-P3
   scene-linear Rec 2020
   scene-linear Rec 709/sRGB
   gamma 1.8 Rec 709
   gamma 2.2 Rec 709
   gamma 2.4 Rec 709 (video)
   sRGB
   ACES RRT v0.7
   ACES RRT v1.0
   Log
   1.8 gamma
   2.2 gamma
   Rec 709 gamma
   sRGB gamma
   Raw
   Stingray tone-map

```

### 在显示窗口中指定特定的色彩空间

```
$ kick -ocs “Log” scene.ass
```
集成颜色管理后，.ass文件现在依赖于对Autodesk颜色管理目录的访问（启用颜色管理时）。该路径存在于color_manager_syncolor节点中。但是，为了具有更大的灵活性，可以使用环境变量SYNCOLOR覆盖路径。

```
$ export SYNCOLOR=/path/to/synColorConfig.xml
```

!> 您可以在Maya首选项文件夹中找到配置文件的示例。

-----------------------

!> 相关链接：

Arnold help 链接：https://docs.arnoldrenderer.com/display/A5AFMUG/Getting+Started+With+Kick

KickAssGUI: https://github.com/crewshin/KickAssGUI

Arnold USD: https://github.com/Autodesk/arnold-usd

# Nuke离线编辑工具 说明文档

> Nuke离线编辑工具 说明文档 
> 注意当前版本为V0.1，如果后续有更新，需要查询对应的版本

[TOC]

## 一、平台简介

此工具主要用于安装了Nuke11以上的合成软件使用。使用Python语言编写，运行Nuke内置的python解释器。

-----

## 二、 开发环境

1.nuke11.3
2.python2.7.3（nuke内置）
3.PySide2（Nuke内置）
4.系统环境：win10 版本1903
5.代码编辑IDE:PyCharm

--------

## 三、功能简介

此工具主要的功能是在不打开 Nuke的情况下，对Nuke工程进行编辑，比如修改Nuke的Read或者输出路径等素材的来源和输出进行批量的编辑。并且支持对当前的工程进行命令行渲染，能对渲染的工程进行基本的设置。并且支持对Nuke工程文件的整体打包。
* 主界面如下图：
![MainUi](help/ui.png)

--------

## 四、使用工作流（win10）
### 1.程序的启动设置
* 首先确定你的计算机中安装了Nuke版本在Nuke11以上程序，并且查看Nuke程序是否能正常运行。
* 本程序的压缩包可以解压到任何位置，不能改变文件夹的结构。主要路径不要存在英文以外的其他字符。
* 指定Nuke的运行路径,这里主要有两种方法：
	1.在当前目录下，找到bin/setNukePath.txt文件。打开文件并把nuke的路径粘贴到文本编辑器中，例如：Y:\Program Files\Nuke11.3v5\Nuke11.3.exe
	2.直接点击文件目录中的start.bat文件。如果你的路径不正确会出现如下图所示情况。
	![config](help/ui2.png)
	会出现一个报错提示，并且命令行的背景是红色显示。然后你需要按照要求，把nuke.exe文件拖拽到绿色箭头指的位置，或者是复制路径到此粘贴。然后回车即可。
	最后，如果没有其他错误程序会启动成功。并且命令行的并且会以灰色显示。

* 其他其他方式也可以，例如自定义一个bat启动。在当前文件夹中新建一个bat后缀格式的文件，然后右键编辑。然后填入以下语句并报错。

```python
"你nuke的完整路径" --tg nukePath.py
```
* 启动完成后，命令行窗口不能关闭。

### 2.窗口介绍
* 在没有打开nuke工程的情况下，大部分按钮都是不可用的，只有当你打开之后，其他菜单和按钮才会是可用状态。
* 当打开工程后，状态和结构如下。
* ![mainui](help/mainui1.jpg)
这样就可以对当前的文件进行编辑和修改，所以菜单都是可用状态，修改完成后的nuke需要另存。

* file菜单：
	open：打开nuke文件，nk的文件版本必须保证你指定的这个nuke能打开的。
	save：保存当前打开的nk文件，注意不能做覆盖文件操作。
* edit菜单：
	Refresh：对当前工程的nk文件刷新操作，注意如果你的文件有修改，需要保存，否则会丢失。
	Repath：对选择的路径进行操作。
* Select：对source List 中的列表进行快速选择的操作。例如按类型选择。
* show：对source List中的列表显示和隐藏的操作，可以隐藏和显示一些特定的类型。
* Help：本程序的帮助文档。

### 修改路径
* 替换路径前的准备：
1.首先需要打开nk文件，并且是带有外部资源的节点。例如Read等节点。
2.选中要修改的路径，点击Repath source按钮，这个时候会出现新的版本，如果你选择的是单个，新出现的窗口如下：
	 ![repath](help/repathui4.png)
	 在这里直接选择要重新指定的路径，点击确定即可，注意要根据相应节点的要求，输入的路径名必须是合法的路径。
	 如果是选择了多个路径：
	 ![repath2](help/repathui3.png)
	 这里添加的路径会显示在下方的列表中，替换的顺序会和你选择的顺序一样。数量也必须一致，否则不成功，如果有多条路径，你可以添加到一个后缀为.txt的文本文件中，然后打开的时候选择txt文件，会把其中的路径自动填入到下方的列表中。并且可以用鼠标拖动对他们的顺序进行调整。注意这里调整的顺序必须要和你以前选择的顺序一致。

3.如果都准备完成点击运行按钮即可替换完成。然后记住需要对文件进行保存。

### 文件渲染
* 渲染前的准备：
1.确保你打开的文件中有Write节点，并且处于激活状态。
2.确保Write的输出路径为合法的路径。
* 完成以上工作后，点击render project按钮，如没然后提示，会出现以下面板：
*  ![render](help/renderui4.png)
1.在Write List会显示所有的Write节点，在设置好起始和结束帧，某人会获取nuke原来的设置，勾选上render All，会渲染全部Write。
2.选择列表中的节点，会渲染选中的节点。
3.Creat Bat会在nuke工程文件夹中生成bat的渲染文件。
4.最后设置完成后，点击rnder Project即可。

### 文件打包
* 打包前的准备：
1.确保nuke中的Read等节点读取的素材都是合法的。
* 点击归档文件按钮，然后会出现以下面板。
* ![archive](help/ui3.png)
* 设置好目标文件路径。
* 勾选keep folder文件，会保存nk文件的素材结构，如果素材的路径没有在nk文件下，会全部复制到source文件中。
* 点击运行按钮，程序会在后台复制文件，不要关闭当前窗口。当文件复制完成后，会在nk文件的目录中，生成一个log文件，可以查看是否有没有成功的素材。

## 五、注意事项及参数合法性

* 打开文件对话框后，输入的素材应为 Read 节点所能支持的
图片、视频、RAW 文件及序列帧，不合法的文件将会带来错误。输出路径的设
置需要注意文件格式，如果不是 Write 节点所支持的格式，也会后续输出的时候出错。 
* 如果是批量替换路径，需要注意选择的顺序，否则也会出现替换出错。

## 六、仍然存在的一些问题

* 保存或者另存为的时候不能覆盖文件，如果强行覆盖会执行不成功。
* 批量修改路径的时候，添加的路径是否合法，没有去做判断。
* 必须要nuke11以上的版本才可以用。
* 在GUI模式下运行可能会出现一些问题。
* 编辑完成后，如果点击关闭，不会提示保存，会直接退出。
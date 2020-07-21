# 设置Clarisse iFX快捷键方法
[TOC]

## 简介

当我要修改clarisse的快捷键的时候，翻遍了所有的菜单都没有找到，这表明了Clarisse没有内置的快捷键编辑器。不过好在可以通过其python脚本文件手动编辑其中的大多数内容。这样就能通过这种方式去修改快捷键了。具体实现如下：

## 修改步骤

* 1,打开Clarisse的安装目录：如安装为：
```
D:\Program Files\Isotropix\Clarisse iFX 4.0 SP2\Clarisse\python\menus\main_menu
```
这个目录下的所有文件都能找到GUI模式下的所有菜单命令。
![clarisseSetKey1](http://artiststd.xyz/img/clarisseSetKey1.png)

* 2，在要修改的快捷键或者想设置新快捷键的主菜单名称，找到对应的文件夹，会有一个名称为_populate.py文件。
* 3，由于不知道文件夹是否有冲突，所以需要提前备份一下这个文件。
* 4，然后在使用文本编辑器打开文件。可以根据需要更改或添加快捷方式，修改完成保存即可。
![clarisseSetKey2](http://artiststd.xyz/img/clarisseSetKey2.png)
* 5，例如：
我要添加一个 删除全部对象的命令：
```
menu.add_command("Edit>Deselect All", "./deselect_all.py","alt+d", "Deselect all items")
```
这样就能修改或者添加新的快捷键。不过要注意，快捷键冲突问题。
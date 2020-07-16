# Nuke Python 入门

[TOC]

本章的例子帮你初步了解Nuke Python API的使用。脚本大小写敏感，需要输入正确才能运行。拷贝时注意缩进，如报错请自己更正。

创建节点设置节点控制

此部分演示如何创建节点，设置节点控制
## 在用户界面创建节点

在用户界面创建类似 menu toolbar的响应节点，使用下面语法:
```
nuke.createNode( "nodename" )
# nodename 输入的是节点类型
```

nodename 就是你要创建节点的名字.这句话在用户界面创建一个新的节点，会在节点图中挂接到用户选择的节点上，并打开节点的属性面板。另外，新节点上默认的knob也设置了。
想创建blur节点，用这句话，输入：

```
nuke.createNode("Blur")
```
### 创建脚本节点
为脚本，批渲染，某些后台程序使用而创建的节点，请使用下面的语法：
```
nuke.nodes.nodename(...)
```
其中nodename是节点的名字。这创建一个新的node对象。在节点视图中**没有和其他节点相连**，也不会打开节点的**属性面板**，也不会设置默认knob。
```
nuke.nodes.Blur()
```

**和其他节点连接**：
```
nuke.nodes.Blur().setInput( 0, nuke.selectedNode() )
```
上面表示的是连接到选择的节点

### 创建时添加控制

创建节点时添加必要的控制属性，语法如下：
```
nuke.nodes.node( control = value )
```

例子：
```
nuke.nodes.Blur( size = 10 )
```

* 创建一个节点，并重命名：
```
nuke.nodes.nodename( name="newname")
```

* 创建一个名为Projection_Cam的摄像机：
```
nuke.nodes.Camera( name="Projection_Cam" )
```
* 创建指向文件的读取节点：
`
nuke.nodes.Read( file = " filePath/filename.txt" )`

## 赋值

既然在创建节点后想操纵它，那给其赋值就合情理。可以用变量来引用节点。添加一个节点，并赋值给变量：
```
variable = nuke.nodes.nodename()
b = nuke.nodes.Blur()
b["size"].setValue( 10)
```

## 获取已存在节点

有时候需要读取节点图中已经有的节点。通过名字去读节点：
`nuke.toNode("dagnodename")`

如果节点图里面有个叫 Blur1 的节点，使用下面的语句来读取：
`myblurNode = nuke.toNode('Blur1')`
## 获取选中的节点

获取当前选择的节点：
`selectNode = nuke.selectedNode()`

如果选了多个节点，nuke返回最底部的节点。想读取所有的节点，请使用返回选择的列表：
`selectNodes = nuke.selectNodes()`

## 添加控制

现在我们看看如何给已经存在的节点设置属性。如果你想添加一个新的控制呢？ 你要使用下面的句子：
```
b = nuke.nodes.nodename(...)
k = nuke.Array_Knob( "name", "label")
b.addKnob(k)
```

假设你输入了下面语句：
```
b = nuke.nodes.Blur()
k = nuke.Array_Knob("myctrl", "My Control" )
b.addKnob(k)
```

如果你想创建滑动控制，而不是输入框，请用下面的句子（ 把Array_Knob替换成 WH_Knob)
```
b = nuke.nodes.Blur()
k = nuke.WH_Knob("myctrl", "My Control" )
b.addKnob(k)
```

下面的句子，会添加一个checkbox：
```
b = nuke.nodes.Blur()
k = nuke.Boolean_Knob("myctrl", "My Control" )
b.addKnob(k)
```

现在有了控制，但没有提示，咱添一个，给tool tip添加提示 My tooltip：
`k.setTooltip('My tooltip' )`

# maya粒子(nParticles)替代对象

## 前期准备

1.准备好需要替换对象的场景，如下图所示：

![](http://artiststd.xyz/img/npar1.jpg)

2、选择全部需要替换的对象，添加一个index的属性。如图：

![npar2](http://artiststd.xyz/img/npar2.jpg)

![npar3](http://artiststd.xyz/img/npar3.jpg)

3、利用下面的代码，给选择的被对象批量添加index的值：

```python
import maya.cmds as cmds

pointEm = cmds.ls(sl = True)
if pointEm:
    count = 1
    for i in pointEm:
        cmds.setAttr("{}.repleIndex".format(i), count)
        count +=1

```

在给需要替换的模型随机一个index：

```python
import maya.cmds as cmds
import random
pointEm = cmds.ls(sl = True)
if pointEm:
    for i in pointEm:
        cmds.setAttr("{}.role".format(i), random.randint(0,1))
```


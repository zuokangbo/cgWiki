# maya的粒子系统散布植物

## 散布山体植被

### 前期准备

1、导入需要散布植物的山体模型.

![np1](http://artiststd.xyz/np1.jpg)

2.导入的模型必须是有uv的，然后为模型添加snow材质，调整属性中的Threshold值，可以控制雪线产生的位置，使陡峭区域不产生雪效果。模拟雪线的位置，用于植树粒子的发射。

![np2](http://artiststd.xyz/np2.jpg)

3、选择模型和snow材质的shader，执行贴图转换命令。

![np3](http://artiststd.xyz/np3.jpg)

### 创建粒子部分
1.为所需要的对象，在表面创建粒子发生器。
将发射器类型改为surface方式。发射速率为比较大的一个数据

![np4](http://artiststd.xyz/np4.jpg)

2、把刚刚bake好的黑白图，链接到粒子发生器，并开启enable texture rate选项。

![np5](http://artiststd.xyz/np5.jpg)

3、发射完成后的粒子状态。

![np6](http://artiststd.xyz/np6.jpg)

由于要保持粒子的状态，所以执行以下操作。

![np7](http://artiststd.xyz/np7.jpg)

如果有多个对象，需要统一去设置基础参数：可以使用脚本去批量操作：
* 批量更改发射率
* 发射的类型
* 启用贴图控制

```python
import maya.cmds as cmds

pointEm = cmds.ls(type = 'pointEmitter')
if pointEm:
    for i in pointEm:
        cmds.setAttr("{}.emitterType".format(i), 2)
        cmds.setAttr("{}.rate".format(i), 10000)
        cmds.setAttr("{}.enableTextureRate".format(i), 1)

```
### 创建实例对象

1、创建实例替代对象。

![np8](http://artiststd.xyz/np8.jpg)

2、创建后的状态：

![np9](http://artiststd.xyz/np9.jpg)

#### 设置实例化的属性

1、添加每粒子替代控制的属性。INstancerId 、scalePP、rotatePP名称可以自己定义，但是不能和也有的属性重名。

![np10](http://artiststd.xyz/np10.jpg)

2、在表达式编辑器中，输入粒子创建时表达式。

![np11](http://artiststd.xyz/np11.jpg)

3、设置实例属性：

![np12](http://artiststd.xyz/np12.jpg)

4、完成后的状态：

![np13](http://artiststd.xyz/np13.jpg)


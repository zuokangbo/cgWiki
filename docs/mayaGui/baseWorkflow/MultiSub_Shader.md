# maya 多套材质使用一套SG节点
主要实现方法是将多种材质或者多种纹理通过index方式分配给不同物体。
## 思路：
主要用到的节点，aiSwitch可以切换多种shader输出，所以，可以给每个物体添加不同的index值，或者使用其他方式获取各个区域的面ID，并将其传递到aiSwitch的index属性上。

## 实现方法：
依次将多个shader连接到aiSwitch的输入中，创建一个aiUserDataFloat节点，将outvalue输出到aiSwitch的index上:

![shader_base1](http://artiststd.xyz/img/shader_base1.png)

如果使用了面材质，可以把顶点颜色的值转换成对应的整数值。

aiUserDataFloat节点上的attribute上填写传递的属性名称，比如index。

![shader_base2](http://artiststd.xyz/img/shader_base2.png)

选择物体的Shape节点，并给其添加一个浮点类型的属性，mtoa对自定义属性命名格式如下：

```python
mtoa_constant_<attribute-name>
```

在这里，我们建立一个index的属性名称，则为mtoa_constant_index。数据类型为浮点，其它默认:

![shader_base3](http://artiststd.xyz/img/shader_base3.png)

创建属性完毕后会在物体的Shape节点下多出index属性:

![shader_base4](http://artiststd.xyz/img/shader_base4.png)
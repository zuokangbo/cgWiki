# houdini导出多套顶点着色到maya

主要使用的是：

输出ABC到MAYA就有colorset了
渲染的话 要先把物体shape节点下的export vertex color导出顶点色勾上
然后使用aiuserdatacolor提取通道

比如下图：
可以利用模型填充的区域顶点颜色。

![houdini](http://artiststd.xyz/houdini_color1.png)

可以对生成的顶点颜色进行其他的操作。

![houdini](http://artiststd.xyz/houdini_color2.png)

把所需要的颜色利用

![houdini](http://artiststd.xyz/houdini_color3.png)

attribreate节点来添加颜色属性。
如果有多个同样的方式来操作，这样到maya中，color编辑器里面就能看到多个颜色集。

![houdini](http://artiststd.xyz/houdini_color4.png)

在导出的时候，把不需要的属性删除掉。

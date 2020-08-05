# 离线转换mb to ma格式

## 功能介绍

在不打开maya的情况下，完成格式的转换。

* 环境：
标准库：sys
maya.standalone

## 准备

在命令行进入maya自己的python环境。

例如：mayapy

直接在里面导入要用到的库

```
import sys
import mayastandalone

```

然后需要在后台启动maya

```
maya.standalone.initialize()
```

然后获取maya文件的路径：
```
from pymel.core import openFile, saveAs


```

利用这两个函数可以对文件离线操作。

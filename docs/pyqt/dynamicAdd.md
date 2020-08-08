
# 动态添加信号好槽函数

```python
# -*- coding: utf-8 -*-
# @Time    : 2020/3/31 13:21
# @Author  : zuokangbo
# @Email   : 1156298563@qq.com
# @File    : test.py
# @software: PyCharm

from PyQt5.Qt import *

from PyQt5.QtCore import *

from PyQt5.QtGui import *

class Widget(QWidget):

    def __init__(self,parnet=None):

        super(Widget,self).__init__(parnet)

        layout=QVBoxLayout()

        inters=[(0,'aaa'),(1,'bbb'),(2,'bbd'),(3,'dfee')]

        for id_,text in inters:

            checkbox=QCheckBox(text,self)
            
            checkbox.id_ = id_
            print(checkbox)
            checkbox.stateChanged.connect(self.checks)

            layout.addWidget(checkbox)

        self.la=QLabel(self)

        layout.addWidget(self.la)

        self.setLayout(layout)

 

    def checks(self,start):

        checkbox=self.sender()#获取发射信号对象

        if start==Qt.Unchecked:

            self.la.setText(u'取消{0}:{1}'.format(checkbox.id_,checkbox.text()))

        elif start==Qt.Checked:

            self.la.setText(u'选择了{0}: {1}'.format(checkbox.id_, checkbox.text()))

 

if __name__=='__main__':

    import sys

    app =QApplication(sys.argv)

    widget = Widget()

    widget.show()

    sys.exit(app.exec_())
    ```
# 【第五节】PyQt5对话框]
[TOC]
## 目录
对话框窗口或对话框是现代GUI应用程序最不可或缺的一部分。一个对话框被定义为两个或两个以上的人之间的谈话。在计算机应用程序对话框窗口用于“交谈”应用程序。一个对话框用于输入数据,修改数据,更改应用程序设置等。

## QInputDialog

QInputDialog提供了一种简单方便的对话框从用户得到一个值。输入值可以是字符串,一个数字,或一个项目从一个列表。

```
# -*- coding: utf-8 -*-

"""
PyQt5 tutorial 

In this example, we determine the event sender
object.

author: py40.com
last edited: 2017年3月
"""


import sys
from PyQt5.QtWidgets import (QWidget, QPushButton, QLineEdit, 
    QInputDialog, QApplication)


class Example(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):      

        self.btn = QPushButton('Dialog', self)
        self.btn.move(20, 20)
        self.btn.clicked.connect(self.showDialog)
        
        self.le = QLineEdit(self)
        self.le.move(130, 22)
        
        self.setGeometry(300, 300, 290, 150)
        self.setWindowTitle('Input dialog')
        self.show()
        
        
    def showDialog(self):
        
        text, ok = QInputDialog.getText(self, 'Input Dialog', 
            'Enter your name:')
        
        if ok:
            self.le.setText(str(text))
        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```
这个例子显示一个按钮和一个文本框，用户点击按钮显示一个输入框，用户输入信息会显示在文本框中。
```
text, ok = QInputDialog.getText(self, 'Input Dialog', 
    'Enter your name:')
```
这行代码显示输入对话框。第一个字符串是一个对话框标题,第二个是对话框中的消息。对话框返回输入的文本和一个布尔值。点击Ok按钮,布尔值是True。
```
if ok:
    self.le.setText(str(text))
```
对话框收到的文本消息会显示在文本框中

------   
## QColorDialog

QColorDialog显示一个用于选择颜色值的对话框。
```
# -*- coding: utf-8 -*-

"""
PyQt5 tutorial 

In this example, we determine the event sender
object.

author: py40.com
last edited: 2017年3月
"""


import sys
from PyQt5.QtWidgets import (QWidget, QPushButton, QFrame, 
    QColorDialog, QApplication)
from PyQt5.QtGui import QColor


class Example(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):      

        col = QColor(0, 0, 0) 

        self.btn = QPushButton('Dialog', self)
        self.btn.move(20, 20)

        self.btn.clicked.connect(self.showDialog)

        self.frm = QFrame(self)
        self.frm.setStyleSheet("QWidget { background-color: %s }" 
            % col.name())
        self.frm.setGeometry(130, 22, 100, 100)            
        
        self.setGeometry(300, 300, 250, 180)
        self.setWindowTitle('Color dialog')
        self.show()
        
        
    def showDialog(self):
      
        col = QColorDialog.getColor()

        if col.isValid():
            self.frm.setStyleSheet("QWidget { background-color: %s }"
                % col.name())
            
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```
这个应用程序显示一个按钮和一个QFrame。QFrame的背景为黑色。通过QColorDialog,我们可以改变它的背景。

```
col = QColor(0, 0, 0) 
```
初始化QFrame的颜色为黑色
```
col = QColorDialog.getColor()
```
这一行代码弹出QColorDialog
```
if col.isValid():
    self.frm.setStyleSheet("QWidget { background-color: %s }"
        % col.name())
```
我们要先检查col的值。如果点击的是Cancel按钮，返回的颜色值是无效的。当颜色值有效时，我们通过样式表(style sheet)来改变背景颜色。
## QFontDialog

QFontDialog对话框用以选择字体

```
# -*- coding: utf-8 -*-

"""
PyQt5 tutorial 

In this example, we determine the event sender
object.

author: py40.com
last edited: 2017年3月
"""
import sys
from PyQt5.QtWidgets import (QWidget, QVBoxLayout, QPushButton, 
    QSizePolicy, QLabel, QFontDialog, QApplication)


class Example(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):      

        vbox = QVBoxLayout()

        btn = QPushButton('Dialog', self)
        btn.setSizePolicy(QSizePolicy.Fixed,
            QSizePolicy.Fixed)
        
        btn.move(20, 20)

        vbox.addWidget(btn)

        btn.clicked.connect(self.showDialog)
        
        self.lbl = QLabel('Knowledge only matters', self)
        self.lbl.move(130, 20)

        vbox.addWidget(self.lbl)
        self.setLayout(vbox)          
        
        self.setGeometry(300, 300, 250, 180)
        self.setWindowTitle('Font dialog')
        self.show()
        
        
    def showDialog(self):

        font, ok = QFontDialog.getFont()
        if ok:
            self.lbl.setFont(font)
        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```
在这个例子中，我们创建了一个按钮和一个标签，通过QFontDialog来改变标签的字体
```
font, ok = QFontDialog.getFont()
```
这一行代码弹出字体选择对话框，getFont()方法返回字体名称和ok参数，如果用户点击了ok他就是True,否则就是false

```
if ok:
    self.label.setFont(font)
```
如果我们点击了ok，标签的字体就会被改变

## QFileDialog

QFileDialog是一个让用户选择文件和目录的对话框，可用以选择打开或保存文件

```
# -*- coding: utf-8 -*-

"""
PyQt5 tutorial 

In this example, we determine the event sender
object.

author: py40.com
last edited: 2017年3月
"""
import sys
from PyQt5.QtWidgets import (QMainWindow, QTextEdit, 
    QAction, QFileDialog, QApplication)
from PyQt5.QtGui import QIcon


class Example(QMainWindow):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):      

        self.textEdit = QTextEdit()
        self.setCentralWidget(self.textEdit)
        self.statusBar()

        openFile = QAction(QIcon('open.png'), 'Open', self)
        openFile.setShortcut('Ctrl+O')
        openFile.setStatusTip('Open new File')
        openFile.triggered.connect(self.showDialog)

        menubar = self.menuBar()
        fileMenu = menubar.addMenu('&File')
        fileMenu.addAction(openFile)       
        
        self.setGeometry(300, 300, 350, 300)
        self.setWindowTitle('File dialog')
        self.show()
        
        
    def showDialog(self):

        fname = QFileDialog.getOpenFileName(self, 'Open file', '/home')

        if fname[0]:
            f = open(fname[0], 'r')

            with f:
                data = f.read()
                self.textEdit.setText(data)        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())

```
这个例子展示了一个菜单栏，中部TextEdit控件和一个状态栏。菜单项Open会显示用于选择文件的QtGui.QFileDialog对话框。选定文件的内容会加载到TextEdit控件中。
```
class Example(QMainWindow):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
```
示例窗体继承自QMainWindow，因为我们要将TextEdit控件置于窗体中央。
```
fname = QFileDialog.getOpenFileName(self, 'Open file', '/home')
```
弹出QFileDialog对话框，第一个字符串参数是对话框的标题，第二个指定对话框的工作目录，默认情况下文件筛选器会匹配所有类型的文件(\*)

```
if fname[0]:
    f = open(fname[0], 'r')

    with f:
        data = f.read()
        self.textEdit.setText(data)        
```
读取了选择的文件并将文件内容显示到了TextEdit控件。

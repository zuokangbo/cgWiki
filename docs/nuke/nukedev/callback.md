#  Gizmo中的回调函数

[TOC]

gizmo中常用的回调函数类型
knobChanged
updateUI
autolabel

-------------
## knobChanged
这里的knobChanged节点是用户操作节点的参数设置面板并修改了某个控件的值的时候。就会触发这个事件。
knobChanged的回调函数：
会得到用户现在操作的控件
```python
nuke.thisKonb()
```
在打开节点控制面板的时候，当前控件会指向一个名为showPanel的控件，而让用户改变输入的时候，当前的节点会指向一个名为inputChange的控件。
showPanel的例子：
```Python
def test():
    k = nuke.thisKnob()
    if k.name() == "showPanel":
    print('show')

nuke.addKnobChanged(test,nodeClass = 'NoOp')
```
他们执行的顺序是有优先级的，knobChanged》updateUI》autolabel依次执行的。
例如：以下的注册函数后，需要等待执行顺序去执行。
```python
def test():
    return 'newNode'
   
nuke.addAutolabel(test,nodeClass = 'NoOp')
```
使用回调函数，仅仅指对一个节点生效：避免不需要的时候去触发这个回调函数。
```Python
callback_func = """
if nuke.thisKnob().name() == 'inputChange':
    print(nuke.thisNode().input(0).name())
"""
nuke.toNode('NoOp')['knobChanged'].setValue(callback_func)
```
### 借助knobChanged在批量修改控件
```Python
def sync_knob():
    if nuke.thisNode().Class() == 'Merge2':
        knob = nuke.thisKnob()
        if knob.name() not in  ('showPanel','hidePanel','inputChange'):
            for node in nuke.selectedNodes('Merge2'):
                node[knob.name()].setValue(knob.value())
nuke.addKnobChanged(sync_konb)
```
## 自动识别read节点文件名
```Python
import os
import nuke

def show_read_file_name(node):
    fname = os.path.basename(node.input(0)['file'].value())
    node['watermark_name'].setValue(fname)
    return fname

def add_checkbox_by_name(node,name):
    index = 0
    for name_part in name.split("_"):
        if '.' not in name_part:
            k = nuke.Boolean_knob('u_{}_{}'.format(index,name_part),name_part)
            k.setValue(1)
            node.addKnob(k)
            index +=1
            
            else:
            first = True
                for part in name_part.split('.'):    # td_010_0010_comp_v002.%04d.jpg
                    if first:
                        k = nuke.Boolean_knob('u_{}_{}'.format(index,part),part)
                        first = False
                    else:
                        k = nuke.Boolean_Knob('d_{}_{}'.format(index,part),part)
                    k.setValue(1)
                    node.addKnob(k)
                    index +=1

def claer_name():
    for k in node.allKnobs():
        if k.name().startswith('u_') or k.name.startswith('d_'):
            node.removeKnob(k)
    node['watermark_name'].setValue('')

def change_name():
    name = ''
    # 获取组成这个watermark_name的文本一共有多少项
    part_knobs = [k for k in node.allKnobs() if k.name().startswith('u_') or k.name().startswith('d_')]
    count = len(part_knobs)
    #判断那些ckeckbox是被选中的，那些是未被选中的。
    # 这个part_knobs里面就只有当前仍然被选中的那些ckeckbox
    part_knobs = [k for k in part_knobs if k.value()]
    for i in range(count):
        for k in part_knobs:
            # 判断对应的index的knob是否在这个part_knobs里面：
            if k.name().startswith('u_{}'.format(i)):
                name +='_{}'.format(k.label())
            elif k.name().startswith('d_{}'.format(i)):
                name +=".{}".format(k.label())
                #去掉第一个字符
    name = name[1:]
    node['watermark_name'].setValue(name)
        

def on_knob_changed():
    # 获取当前节点和当前控件
    n = nuke.thisNode()
    k = nuke.thisKnob()
    if k.name() == 'inputChange':
        # 判断一下，我们是连上了read节点，还是取消了链接。
        if n.inputs() and n.input(0).Class() == 'Read':
            fname = show_read_file_name(n)
            # 创建checkbox控件
            add_checkbox_by_name(n,fname)
            # 重read上取消链接
        else:
            claer_name(n)
            # 取消选择的回调函数
        elif k.name().startswith('u_') or k.name().startswith('d_'):
            change_name(n)
            
            
nuke.toNode('Group1')['knobChanged'].setValue('on_knob_changed()')
```

## 总结  
knobchanged 是最常见的实现控件联动的函数事件。
需要注意的是showPanel/hidePanel/inputChange这几种特殊的临时控件。
使用nuke.thisKnob()来获取当前被操作的控件。
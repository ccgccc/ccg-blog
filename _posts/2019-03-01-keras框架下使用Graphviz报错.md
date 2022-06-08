---
layout:     post
title:      keras框架下使用Graphviz报错（jupyter环境）
date:       2019-03-01
author:     CCG
header-style: text
catalog: true
tags:
    - Keras
---

## keras框架下使用Graphviz报错（jupyter环境）

### 安装pydot与Graphviz方法
- 打开Anaconda Prompt
- pip install pydot
- pip install graphviz
- 官网下载Graphviz：https://www.graphviz.org/download/ ，下载后安装，并将安装路径（如E:\Program Files (x86)\Graphviz2.38\bin）加入环境变量PATH中

### 问题再现
在jupyter中调用
```
plot_model(happyModel, to_file='HappyModel.png')
SVG(model_to_dot(happyModel).create(prog='dot', format='svg'))
```
运行错误，显示错误信息为：
```
During handling of the above exception, another exception occurred:

OSError                                   Traceback (most recent call last)
<ipython-input-16-94e567feb269> in <module>
----> 1 plot_model(happyModel, to_file='HappyModel.png')
      2 SVG(model_to_dot(happyModel).create(prog='dot', format='svg'))

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in plot_model(model, to_file, show_shapes, show_layer_names, rankdir)
    132             'LR' creates a horizontal plot.
    133     """
--> 134     dot = model_to_dot(model, show_shapes, show_layer_names, rankdir)
    135     _, extension = os.path.splitext(to_file)
    136     if not extension:

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in model_to_dot(model, show_shapes, show_layer_names, rankdir)
     55     from ..models import Sequential
     56 
---> 57     _check_pydot()
     58     dot = pydot.Dot()
     59     dot.set('rankdir', rankdir)

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in _check_pydot()
     29     except OSError:
     30         raise OSError(
---> 31             '`pydot` failed to call GraphViz.'
     32             'Please install GraphViz (https://www.graphviz.org/) '
     33             'and ensure that its executables are in the $PATH.')

OSError: `pydot` failed to call GraphViz.Please install GraphViz (https://www.graphviz.org/) and ensure that its executables are in the $PATH.
```
但是Graphviz已经正确安装，并且环境变量也已配置正确。

### 原因分析
在Anaconda安装目录keras包中的...\Anaconda3\Lib\site-packages\keras\utils\vis_utils.py文件中有：
```python
# `pydot` is an optional dependency,
# see `extras_require` in `setup.py`.
try:
    import pydot
except ImportError:
    pydot = None

def _check_pydot():
    """Raise errors if `pydot` or GraphViz unavailable."""
    if pydot is None:
        raise ImportError(
            'Failed to import `pydot`. '
            'Please install `pydot`. '
            'For example with `pip install pydot`.')
    try:
        # Attempt to create an image of a blank graph
        # to check the pydot/graphviz installation.
        pydot.Dot.create(pydot.Dot())
    except OSError:
        raise OSError(
            '`pydot` failed to call GraphViz.'
            'Please install GraphViz (https://www.graphviz.org/) '
            'and ensure that its executables are in the $PATH.')
```
再调用Graphviz前会先进行pydot.Dot.create(pydot.Dot())，判断是否能调用Graphviz，但是由于pydot的版本更新，导致与Graphviz不太兼容，所以抛出异常。

### 解决方法
#### 方法1
使用pydot-ng，可以理解成pydot的兼容版本
```
pydot: Python interface to Graphviz's Dot language
pydot-ng: Python interface to Graphviz's Dot language compatible with Python 2 nad Python 3
```
**网址：**  
https://pypi.org/project/pydot-ng  
https://github.com/pydot/pydot-ng  
**安装方法：** 打开Anaconda Prompt，运行pip install pydot-ng  
**使用方式：**  import pydot_ng  
**解决此问题：**  
对于解决此问题，需将上述keras包中 vis_utils.py 文件中做更改：
```
try:
    #import pydot
    import pydot_ng as pydot #用pydot-ng来代替pydot
except ImportError:
    pydot = None
```
另外，将...\Anaconda3\Lib\site-packages\pydot_ng\__init__.py的find_graphviz()函数做以下更改:
```python
# Method 3 (Windows only)
    #--ccg modify: origin start
    '''
    if os.sys.platform == 'win32':

        # Try and work out the equivalent of "C:\Program Files" on this
        # machine (might be on drive D:, or in a different language)
        if 'PROGRAMFILES' in os.environ:
            # Note, we could also use the win32api to get this
            # information, but win32api may not be installed.
            path = os.path.join(os.environ['PROGRAMFILES'], 'ATT',
                                'GraphViz', 'bin')
        else:
            # Just in case, try the default...
            path = r"C:\Program Files\att\Graphviz\bin"

        progs = __find_executables(path)

        if progs is not None:
            return progs

    for path in (
            '/usr/bin', '/usr/local/bin',
            '/opt/local/bin',
            '/opt/bin', '/sw/bin', '/usr/share',
            '/Applications/Graphviz.app/Contents/MacOS/'):

        progs = __find_executables(path)
        if progs is not None:
            return progs

    # Failed to find GraphViz
    return None
    '''
    # -- ccg modify: origin end
    
    # -- ccg modify: new start
    if os.sys.platform == 'win32':   
        # Try and work out the equivalent of "C:\Program Files" on this
        # machine (might be on drive D:, or in a different language)
        #        
       if False:#os.environ.has_key('PROGRAMFILES'):        
            # Note, we could also use the win32api to get this
            # information, but win32api may not be installed.            
           path = os.path.join(os.environ['PROGRAMFILES'], 'ATT', 'GraphViz', 'bin')            
       else:        
           #Just in case, try the default...
            path = r"E:\Program Files (x86)\Graphviz2.38\bin"  #更改成自己Graphviz的安装路径      
       progs = __find_executables(path)

       if progs is not None :        
            #print "Used default install location"
           return progs

    for path in (
        '/usr/bin', '/usr/local/bin',
        '/opt/bin', '/sw/bin', '/usr/share',
        '/Applications/Graphviz.app/Contents/MacOS/' ):        
        progs = __find_executables(path)

        if progs is not None :
            #print "Used path"
            return progs
    # Failed to find GraphViz
    #

    return None
    # -- ccg modify: new end
```
注意：path = r"E:\Program Files (x86)\Graphviz2.38\bin"  更改成自己Graphviz的安装路径下的bin目录。

**进一步分析：**(选读)  
如果不更改path，会报以下错误：
```
InvocationException                       Traceback (most recent call last)
<ipython-input-10-94e567feb269> in <module>
----> 1 plot_model(happyModel, to_file='HappyModel.png')
      2 SVG(model_to_dot(happyModel).create(prog='dot', format='svg'))

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in plot_model(model, to_file, show_shapes, show_layer_names, rankdir)
    132             'LR' creates a horizontal plot.
    133     """
--> 134     dot = model_to_dot(model, show_shapes, show_layer_names, rankdir)
    135     _, extension = os.path.splitext(to_file)
    136     if not extension:

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in model_to_dot(model, show_shapes, show_layer_names, rankdir)
     55     from ..models import Sequential
     56 
---> 57     _check_pydot()
     58     dot = pydot.Dot()
     59     dot.set('rankdir', rankdir)

D:\Anaconda3\lib\site-packages\keras\utils\vis_utils.py in _check_pydot()
     26         # Attempt to create an image of a blank graph
     27         # to check the pydot/graphviz installation.
---> 28         pydot.Dot.create(pydot.Dot())
     29     except OSError:
     30         raise OSError(

D:\Anaconda3\lib\site-packages\pydot_ng\__init__.py in create(self, prog, format)
   1856             if self.progs is None:
   1857                 raise InvocationException(
-> 1858                     'GraphViz\'s executables not found')
   1859 
   1860         if prog not in self.progs:

InvocationException: GraphViz's executables not found
```
此时，在jupyter中运行：
```python
import pydot_ng as pydot
pydot.Dot.create(pydot.Dot())
```
就会报该错误，但是在Anaconda Prompt中进入python中运行则不会报错，应该是管理员权限问题。参考: [解决windows+python3环境下,keras可视化遇到pydot&graphviz无法导入问题](https://blog.csdn.net/jwayingxp/article/details/79440444)

#### 方法2
使用pydotplus
```
PyDotPlus is an improved version of the old pydot project that provides a Python Interface to Graphviz’s Dot language.
http://pydotplus.readthedocs.org/

Differences with pydot:
Compatible with PyParsing 2.0+.
Python 2.7 - Python 3 compatible.
Well documented.
CI Tested.
```
**网址：**  
https://pypi.org/project/pydotplus
https://github.com/carlos-jenkins/pydotplus  
**安装方法：** 打开Anaconda Prompt，运行pip install pydotplus  
**使用方式：**  import pydotplus  
**解决此问题：**  
原理同上，此时需将上述keras包中 vis_utils.py 文件中做更改：
```
try:
    #import pydot
    #import pydot_ng as pydot 
    import pydotplus as pydot #用pydot-ng来代替pydot
except ImportError:
    pydot = None
```
另外，将...\Anaconda3\Lib\site-packages\pydotplus\graphviz.py的find_graphviz()函数跟方法一做相同修改。
参考：[Pydot 与 Graphviz 的安装](https://blog.csdn.net/fy_eng/article/details/81366723)

#### 其他方法
退回低版本pydot1.1.0：  
[CSDN: 《安装pydot（和Graphviz）》](https://blog.csdn.net/WuchangI/article/details/79589542)  
[stackoverflow: Importing theano: AttributeError: 'module' object has no attribute 'find_graphviz'](https://stackoverflow.com/questions/38446771/importing-theano-attributeerror-module-object-has-no-attribute-find-graphvi)
---
layout:     post
title:      Keras 报错 - OSError-pydot failed to call GraphViz 解决办法与原因分析
date:       2019-04-16
author:     CCG
header-style: text
catalog: true
tags:
    - Keras
---

# Keras 报错 - OSError: `pydot` failed to call GraphViz.Please install GraphViz

Keras 报错 - OSError: `pydot` failed to call GraphViz.Please install GraphViz
或 pydot 报错 - FileNotFoundError: [WinError 2] "dot" not found in path. 的解决方法与真正原因

环境：windows、Anaconda、pydot 1.4.1

## 问题
出现以下两种情况的其中一种：
1. keras 中调用 plot_model 函数报错：OSError: `pydot` failed to call GraphViz.Please install GraphViz (https://www.graphviz.org/) and ensure that its executables are in the $PATH.
2. pydot 报错：FileNotFoundError: [WinError 2] "dot" not found in path.


## 解决方法
一、首先确保 Graphviz 已正确安装，并已将其安装路径下的 bin 目录添加到环境变量。  
二、使用：
```
import pydot
pydot?

Type:        module
String form: <module 'pydot' from 'D:\\Anaconda3\\lib\\site-packages\\pydot.py'>
File:        d:\anaconda3\lib\site-packages\pydot.py
Docstring:   An interface to GraphViz.
```
找到 pydot.py 路径。  
三、更改 pydot.py ，有两种更改方式，选择一种即可：  
1. 将 def get_executable_extension() 函数里的 ```return '.bat' if is_anacoda() else '.exe'``` 改成 ```return '.bat' if not is_anacoda() else '.exe'```。如下：
```
def get_executable_extension():
    # type: () -> str
    if is_windows():
        #return '.bat' if is_anacoda() else '.exe'
        #ccg modify
        return '.bat' if not is_anacoda() else '.exe'
    else:
        return ''
```

2. 将 class Dot 里 __init__ 函数的 self.prog 从 dot 改成 dot.exe，如下：
```
class Dot(Graph):

    def __init__(self, *argsl, **argsd):

        #self.prog = 'dot'
        #ccg modify
        self.prog = 'dot.exe'
```

## 原因分析

如此例中所示：
```python
from keras.models import Sequential
from keras.layers import Input, Dense
from keras.utils.vis_utils import plot_model

model = Sequential()
model.add(Dense(50, input_shape=(100,)))
model.add(Dense(10))

plot_model(model, show_shapes=True)
```
在 Keras 中调用 plot_model 会报以下错误信息：（OSError: `pydot` failed to call GraphViz.Please install GraphViz (https://www.graphviz.org/) and ensure that its executables are in the $PATH.）
```
---------------------------------------------------------------------------
FileNotFoundError                         Traceback (most recent call last)
D:\Anaconda3\lib\site-packages\pydot.py in create(self, prog, format, encoding)
   1917                 arguments=arguments,
-> 1918                 working_dir=tmp_dir,
   1919             )

D:\Anaconda3\lib\site-packages\pydot.py in call_graphviz(program, arguments, working_dir, **kwargs)
    138         stdout=subprocess.PIPE,
--> 139         **kwargs
    140     )

D:\Anaconda3\lib\subprocess.py in __init__(self, args, bufsize, executable, stdin, stdout, stderr, preexec_fn, close_fds, shell, cwd, env, universal_newlines, startupinfo, creationflags, restore_signals, start_new_session, pass_fds, encoding, errors)
    728                                 errread, errwrite,
--> 729                                 restore_signals, start_new_session)
    730         except:

D:\Anaconda3\lib\subprocess.py in _execute_child(self, args, executable, preexec_fn, close_fds, pass_fds, cwd, env, startupinfo, creationflags, shell, p2cread, p2cwrite, c2pread, c2pwrite, errread, errwrite, unused_restore_signals, unused_start_new_session)
   1016                                          os.fspath(cwd) if cwd is not None else None,
-> 1017                                          startupinfo)
   1018             finally:

FileNotFoundError: [WinError 2] 系统找不到指定的文件。

During handling of the above exception, another exception occurred:

FileNotFoundError                         Traceback (most recent call last)
e:\mygit\projects\keras\keras\utils\vis_utils.py in _check_pydot()
     25         # to check the pydot/graphviz installation.
---> 26         pydot.Dot.create(pydot.Dot())
     27     except OSError:

D:\Anaconda3\lib\site-packages\pydot.py in create(self, prog, format, encoding)
   1924                     prog=prog)
-> 1925                 raise OSError(*args)
   1926             else:

FileNotFoundError: [WinError 2] "dot" not found in path.

During handling of the above exception, another exception occurred:

OSError                                   Traceback (most recent call last)
<ipython-input-2-93da5b8388dd> in <module>
----> 1 plot_model(model, show_shapes=True)

e:\mygit\projects\keras\keras\utils\vis_utils.py in plot_model(model, to_file, show_shapes, show_layer_names, rankdir, expand_nested, dpi)
    216     """
    217     dot = model_to_dot(model, show_shapes, show_layer_names, rankdir,
--> 218                        expand_nested, dpi)
    219     _, extension = os.path.splitext(to_file)
    220     if not extension:

e:\mygit\projects\keras\keras\utils\vis_utils.py in model_to_dot(model, show_shapes, show_layer_names, rankdir, expand_nested, dpi, subgraph)
     62     from ..models import Sequential
     63 
---> 64     _check_pydot()
     65     if subgraph:
     66         dot = pydot.Cluster(style='dashed', graph_name=model.name)

e:\mygit\projects\keras\keras\utils\vis_utils.py in _check_pydot()
     27     except OSError:
     28         raise OSError(
---> 29             '`pydot` failed to call GraphViz.'
     30             'Please install GraphViz (https://www.graphviz.org/) '
     31             'and ensure that its executables are in the $PATH.')

OSError: `pydot` failed to call GraphViz.Please install GraphViz (https://www.graphviz.org/) and ensure that its executables are in the $PATH.
```

通过错误信息加上分析源码发现徐错误流如下：  
-->&ensp; vis_utils.py &ensp; plot_model()  
-->&ensp; vis_utils.py &ensp; model_to_dot()  
-->&ensp; vis_utils.py &ensp; _check_pydot()  
-->&ensp; vis_utils.py &ensp; pydot.Dot.create(pydot.Dot())  
测试：
```
import pydot
pydot.Dot.create(pydot.Dot())
```
会得到以下报错：（FileNotFoundError: [WinError 2] "dot" not found in path.）
```
---------------------------------------------------------------------------
FileNotFoundError                         Traceback (most recent call last)
D:\Anaconda3\lib\site-packages\pydot.py in create(self, prog, format, encoding)
   1919                 arguments=arguments,
-> 1920                 working_dir=tmp_dir,
   1921             )

D:\Anaconda3\lib\site-packages\pydot.py in call_graphviz(program, arguments, working_dir, **kwargs)
    138         stdout=subprocess.PIPE,
--> 139         **kwargs
    140     )

D:\Anaconda3\lib\subprocess.py in __init__(self, args, bufsize, executable, stdin, stdout, stderr, preexec_fn, close_fds, shell, cwd, env, universal_newlines, startupinfo, creationflags, restore_signals, start_new_session, pass_fds, encoding, errors)
    728                                 errread, errwrite,
--> 729                                 restore_signals, start_new_session)
    730         except:

D:\Anaconda3\lib\subprocess.py in _execute_child(self, args, executable, preexec_fn, close_fds, pass_fds, cwd, env, startupinfo, creationflags, shell, p2cread, p2cwrite, c2pread, c2pwrite, errread, errwrite, unused_restore_signals, unused_start_new_session)
   1016                                          os.fspath(cwd) if cwd is not None else None,
-> 1017                                          startupinfo)
   1018             finally:

FileNotFoundError: [WinError 2] 系统找不到指定的文件。

During handling of the above exception, another exception occurred:

FileNotFoundError                         Traceback (most recent call last)
<ipython-input-4-2d049bb9ae08> in <module>
----> 1 pydot.Dot.create(pydot.Dot())

D:\Anaconda3\lib\site-packages\pydot.py in create(self, prog, format, encoding)
   1925                 args[1] = '"{prog}" not found in path.'.format(
   1926                     prog=prog)
-> 1927                 raise OSError(*args)
   1928             else:
   1929                 raise

FileNotFoundError: [WinError 2] "dot" not found in path.
```

-->&ensp; pydot.py &ensp; Dot.create() &ensp;  错误的原因即在此处，在 create 函数中调用 call_graphviz 时抛出了异常。可见 call_graphviz 的 program 参数传入的是 prog = self.prog = 'dot'。
```
class Dot(Graph):

    def __init__(self, *argsl, **argsd):
        ......
        
        self.prog = 'dot'
        
        ......
    def create(self, prog=None, format='ps', encoding=None):

        if prog is None:
            prog = self.prog

        ......

        try:
            stdout_data, stderr_data, process = call_graphviz(
                program=prog,
                arguments=arguments,
                working_dir=tmp_dir,
            )
        except OSError as e:
            if e.errno == errno.ENOENT:
                args = list(e.args)
                args[1] = '"{prog}" not found in path.'.format(
                    prog=prog)
                raise OSError(*args)
            else:
                raise

        ......

        return stdout_data
```
而 call_graphviz 函数对 program 参数的处理是 ```program += get_executable_extension()``` ，即给 'dot' 加上后缀名，照理说应该是 '.exe'。
```
def call_graphviz(program, arguments, working_dir, **kwargs):

    if program in DEFAULT_PROGRAMS:
        extension = get_executable_extension()
        program += extension

    ......

    env = {
        'PATH': os.environ.get('PATH', ''),
        'LD_LIBRARY_PATH': os.environ.get('LD_LIBRARY_PATH', ''),
    }

    ......

    return stdout_data, stderr_data, process
```
&emsp;&emsp;但是，get_executable_extension 得到的后缀名却并不是 '.exe'，代码如下，调用 get_executable_extension 得到的后缀名却是 '.bat'。pydot.py 中这部分的代码让人费解，这里正是问题的根源所在。  
&emsp;&emsp;首先 ```is_windows()``` 肯定是 ```True``` 的，```return``` 的时候用了python的三目运算，当 ```is_anacoda()=Ture``` 时返回 '.bat'，当 ```is_anacoda()=False```时返回 '.exe'。  
&emsp;&emsp;而安装了 Anaconda 环境 ```is_anacoda()``` 判断的结果就是 ```True```，所以返回的后缀名就是 '.bat'。而 Graphviz 安装 bin 目录下的程序是 dot.exe，并没有 dot.bat ，所以此时就程序就找不到了，从而报错。  
```
def is_windows():
    # type: () -> bool
    return os.name == 'nt'

def is_anacoda():
    # type: () -> bool
    return os.path.exists(os.path.join(sys.prefix, 'conda-meta'))

def get_executable_extension():
    # type: () -> str
    if is_windows():
        return '.bat' if is_anacoda() else '.exe'
    else:
        return ''
```
&emsp;&emsp;不知道 pydot 代码为什么这么写，但是知道原因就可以对症下药了，解决方法中的方式1即是在 ```is_anacoda()``` 前加了个 ```not``` 使程序后缀名返回 .exe。  
&emsp;&emsp;而方式2是在class Dot 中 self.prog 从 'dot' 改成了 'dot.exe'，这样传入 call_graphviz 的参数 program 就是 'dot.exe'，并且此时无法通过```if program in DEFAULT_PROGRAMS```的判断，也就不会再进行后面的 ```program+=get_executable_extension()``` 了，此时程序也能找到 dot.exe 了。

&emsp;&emsp;终于可以愉快地使用 pydot 了，上面的简单模型画出来如下：

![model](https://note.youdao.com/yws/api/personal/file/0149AB62832146029EE415EDBC45C0B3?method=download&shareKey=e2a0ff821250c78ee0b334d036c2feaa)


**参考：**  
[windows python3库pydot运行出现：FileNotFoundError: [WinError 2] "dot" not found in path. - sinat_38653840的博客 - CSDN博客](https://blog.csdn.net/sinat_38653840/article/details/84776806)
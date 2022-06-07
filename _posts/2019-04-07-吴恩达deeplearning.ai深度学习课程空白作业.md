---
layout:     post
title:      吴恩达deeplearning.ai深度学习课程空白作业
date:       2019-04-07
author:     CCG
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - 吴恩达
    - 深度学习
---


&emsp;&emsp;吴恩达deeplearning.ai深度学习课程的空白作业，包括深度学习微专业五门课程的全部空白编程作业，经多方整理而来。网上找来的作业好多都是已经被别人写过的，不便于自己练习，而且很多都缺失各种数据文件，找起来费时费力。所以我特地整理了一遍，搞到全部空白作业与所有的数据文件，并上传到CSDN，欢迎下载：  
&emsp;&emsp;https://download.csdn.net/download/ccgcccccc/12126611

&emsp;&emsp;由于CSDN上传文件大小有限制，所以我把需要用到的一些比较大的数据文件放到了百度云，并在相应作业的 readme-by ccg.txt 进行了说明并放上了我相应百度云的下载链接。同时为了方便，在此上传的资源根目录下的 readme 中，我也放上了已经将所有数据文件都包含在内的版本，是百度云链接，文件比较大，流量充裕的可以直接去下载。我也整理了自己完成了的作业版本，里面包含已经实现了的代码和运行结果，如果实现起来比较头疼可以参考。我也将已经完成了的作业版本的百度云链接也放在了该 readme 中，同样文件比较大，自由下载。总之就是，下载了这个就啥都有了。

&emsp;&emsp;由于使用python、tensorflow等各种版本不同问题，所以即使做空白作业可能也会遇到问题和错误，我将自己在完成作业过程中遇到的错误写在了 readme - by ccg.txt 记事本中，包含在相应作业的文件夹中，如果遇到问题不妨去看一下，在这样的问题上浪费太多时间并不值得。我所练习测试的环境版本主要如下（全部环境附在最后）：
```
# packages in environment at D:\Anaconda3:
#
# Name                    Version                   Build    Channel
anaconda                  2018.12                  py37_0    defaults
jupyter                   1.0.0                    py36_7    defaults
jupyter_client            5.2.4                    py36_0    defaults
keras                     2.2.4                    pypi_0    pypi
keras-applications        1.0.7                    pypi_0    pypi
keras-preprocessing       1.0.9                    pypi_0    pypi
numpy                     1.16.1                   pypi_0    pypi
numpy-base                1.16.2           py36hc3f5095_0    defaults
python                    3.6.8                h9f7ef89_7    defaults
tensorboard               1.12.2           py36h33f27b4_0    defaults
tensorflow                1.13.0rc2                pypi_0    pypi
tensorflow-base           1.12.0          mkl_py36h81393da_0    defaults
tensorflow-estimator      1.13.0                   pypi_0    pypi
```


### 吴恩达深度学习课程地址：
>deeplearning.ai官网地址：https://www.deeplearning.ai/
>coursera地址：https://www.coursera.org/specializations/deep-learning
>网易视频地址：https://163.lu/nPtn42

### 深度学习课程目录

>
>#### 第一门课 神经网络和深度学习(Neural Networks and Deep Learning)
>
>第一周：深度学习引言(Introduction to Deep Learning) 
>
>第二周：神经网络的编程基础(Basics of Neural Network programming) 
>
>第三周：浅层神经网络(Shallow neural networks)
>
>第四周：深层神经网络(Deep Neural Networks)
>
>#### 第二门课 改善深层神经网络：超参数调试、正则化以及优化(Improving Deep Neural Networks:Hyperparameter tuning, Regularization and Optimization)
>
>第一周：深度学习的实用层面(Practical aspects of Deep Learning) 
>
>第二周：优化算法 (Optimization algorithms) 
>
>第三周：超参数调试，batch正则化和程序框架（Hyperparameter tuning, Batch Normalization and Programming Frameworks)
>
>#### 第三门课 结构化机器学习项目 (Structuring Machine Learning Projects)
>
>第一周：机器学习策略（1）(ML Strategy (1))
>
>第二周：机器学习策略（2）(ML Strategy (2))
>
>#### 第四门课 卷积神经网络（Convolutional Neural Networks）
>
>第一周：卷积神经网络(Foundations of Convolutional Neural Networks)
>
>第二周：深度卷积网络：实例探究(Deep convolutional models: case studies)	
>
>第三周：目标检测（Object detection）
>
>第四周：特殊应用：人脸识别和神经风格转换（Special applications: Face recognition &Neural style transfer）
>
>#### 第五门课 序列模型(Sequence Models)
>
>第一周：循环序列模型（Recurrent Neural Networks）
>
>第二周：自然语言处理与词嵌入（Natural Language Processing and Word Embeddings）
>
>第三周：序列模型和注意力机制（Sequence models & Attention mechanism）

## 作业中可能遇到的小问题

当作业中出现：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190406175038436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NjZ2NjY2NjYw==,size_16,color_FFFFFF,t_70)
像这样的乱码时，双击或按Enter进入编辑：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190406175101965.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NjZ2NjY2NjYw==,size_16,color_FFFFFF,t_70)
变红的那些即为异常显示的原因，只需将变红部分上下的空行删除（Ctrl+X是删除一行快捷键）即可：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190406175127318.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NjZ2NjY2NjYw==,size_16,color_FFFFFF,t_70)
此时按Ctrl+Enter即可正常显示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019040617514445.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NjZ2NjY2NjYw==,size_16,color_FFFFFF,t_70)
(我已基本改了过来，如果仍遇到可以自己再改)


**附: 测试全部环境**
```
(base) C:\Users\Administrator>conda list
# packages in environment at D:\Anaconda3:
#
# Name                    Version                   Build  Channel
_ipyw_jlab_nb_ext_conf    0.1.0                    py36_0    defaults
_nb_ext_conf              0.4.0                    py36_1    https://mirrors.tun
a.tsinghua.edu.cn/anaconda/pkgs/free
_tflow_select             2.3.0                       mkl    defaults
absl-py                   0.7.0                    pypi_0    pypi
alabaster                 0.7.12                   py36_0    defaults
anaconda                  2018.12                  py37_0    defaults
anaconda-client           1.7.2                    py36_0    defaults
anaconda-navigator        1.9.6                    py36_0    defaults
anaconda-project          0.8.2                    py36_0    defaults
asn1crypto                0.24.0                   py36_0    defaults
astor                     0.7.1                    py36_0    defaults
astroid                   2.1.0                    py36_0    defaults
astropy                   3.1.2            py36he774522_0    defaults
atomicwrites              1.3.0                      py_0    defaults
attrs                     18.2.0           py36h28b3542_0    defaults
babel                     2.6.0                    py36_0    defaults
backcall                  0.1.0                    py36_0    defaults
backports                 1.0                      py36_1    defaults
backports.os              0.1.1                    py36_0    defaults
backports.shutil_get_terminal_size 1.0.0                    py36_2    defaults
beautifulsoup4            4.7.1                    py36_1    defaults
bitarray                  0.8.3            py36hfa6e2cd_0    defaults
bkcharts                  0.2              py36h7e685f7_0    defaults
blas                      1.0                         mkl    defaults
blaze                     0.11.3                   py37_0    defaults
bleach                    3.1.0                    py36_0    defaults
blosc                     1.14.4               he51fdeb_0    defaults
bokeh                     1.0.4                    py36_0    defaults
boto                      2.49.0                   py36_0    defaults
bottleneck                1.2.1            py36h452e1ab_1    defaults
bzip2                     1.0.6                hfa6e2cd_5    defaults
ca-certificates           2019.1.23                     0    defaults
certifi                   2019.3.9                 py36_0    defaults
cffi                      1.12.1           py36h7a1dbc1_0    defaults
chardet                   3.0.4                    py36_1    defaults
click                     7.0                      py36_0    defaults
cloudpickle               0.8.0                    py36_0    defaults
clyent                    1.2.2                    py36_1    defaults
colorama                  0.4.1                    py36_0    defaults
comtypes                  1.1.7                    py36_0    defaults
conda                     4.6.8                    py36_0    defaults
conda-build               3.17.8                   py36_0    defaults
conda-env                 2.6.0                         1    defaults
conda-verify              3.1.1                    py36_0    defaults
console_shortcut          0.1.1                         3    defaults
contextlib2               0.5.5            py36he5d52c0_0    defaults
cryptography              2.5              py36h7a1dbc1_0    defaults
curl                      7.63.0            h2a8f88b_1000    defaults
cycler                    0.10.0           py36h009560c_0    defaults
cython                    0.29.5           py36ha925a31_0    defaults
cytoolz                   0.9.0.1          py36hfa6e2cd_1    defaults
dask                      1.1.3                      py_0    defaults
dask-core                 1.1.3                      py_0    defaults
datashape                 0.5.4                    py36_1    defaults
decorator                 4.3.2                    py36_0    defaults
defusedxml                0.5.0                    py36_1    defaults
distributed               1.26.0                   py36_1    defaults
django-extensions         2.1.6                    pypi_0    pypi
docutils                  0.14             py36h6012d8f_0    defaults
emoji                     0.5.1                    pypi_0    pypi
entrypoints               0.3                      py36_0    defaults
et_xmlfile                1.0.1            py36h3d2d736_0    defaults
faker                     1.0.2                    pypi_0    pypi
fastcache                 1.0.2            py36hfa6e2cd_2    defaults
filelock                  3.0.10                   py36_0    defaults
flask                     1.0.2                    py36_1    defaults
flask-cors                3.0.7                    py36_0    defaults
freetype                  2.9.1                ha9979f8_1    defaults
future                    0.17.1                   py36_0    defaults
gast                      0.2.2                    pypi_0    pypi
get_terminal_size         1.0.0                h38e98db_0    defaults
gevent                    1.4.0            py36he774522_0    defaults
glob2                     0.6                      py36_1    defaults
greenlet                  0.4.15           py36hfa6e2cd_0    defaults
grpcio                    1.18.0                   pypi_0    pypi
h5py                      2.8.0            py36hf7173ca_2    defaults
hdf5                      1.8.20               hac2f561_1    defaults
heapdict                  1.0.0                    py36_2    defaults
html5lib                  1.0.1                    py36_0    defaults
icc_rt                    2019.0.0             h0cc432a_1    defaults
icu                       58.2                 ha66f8fd_1    defaults
idna                      2.8                      py36_0    defaults
imageio                   2.5.0                    py36_0    defaults
imagesize                 1.1.0                    py36_0    defaults
importlib_metadata        0.7                      py36_0    defaults
intel-openmp              2019.1                      144    defaults
ipykernel                 5.1.0            py36h39e3cac_0    defaults
ipython                   7.3.0            py36h39e3cac_0    defaults
ipython_genutils          0.2.0            py36h3c5d0ee_0    defaults
ipywidgets                7.4.2                    py36_0    defaults
isort                     4.3.8                    py36_0    defaults
itsdangerous              1.1.0                    py36_0    defaults
jdcal                     1.4                      py36_0    defaults
jedi                      0.13.3                   py36_0    defaults
jinja2                    2.10                     py36_0    defaults
jpeg                      9b                   hb83a4c4_2    defaults
jsonschema                2.6.0            py36h7636477_0    defaults
jupyter                   1.0.0                    py36_7    defaults
jupyter_client            5.2.4                    py36_0    defaults
jupyter_console           6.0.0                    py36_0    defaults
jupyter_core              4.4.0                    py36_0    defaults
jupyterlab                0.35.3                   py36_0    defaults
jupyterlab_server         0.2.0                    py36_0    defaults
keras                     2.2.4                    pypi_0    pypi
keras-applications        1.0.7                    pypi_0    pypi
keras-preprocessing       1.0.9                    pypi_0    pypi
keyring                   18.0.0                   py36_0    defaults
kiwisolver                1.0.1            py36h6538335_0    defaults
krb5                      1.16.1               hc04afaa_7    defaults
lazy-object-proxy         1.3.1            py36hfa6e2cd_2    defaults
libarchive                3.3.3                h0643e63_5    defaults
libcurl                   7.63.0            h2a8f88b_1000    defaults
libiconv                  1.15                 h1df5818_7    defaults
liblief                   0.9.0                ha925a31_2    defaults
libmklml                  2019.0.3                      0    defaults
libopencv                 3.4.2                h20b85fd_0    defaults
libpng                    1.6.35               h2a8f88b_0    defaults
libprotobuf               3.6.1                h7bd577a_0    defaults
libsodium                 1.0.16               h9d3ae62_0    defaults
libssh2                   1.8.0                h7a1dbc1_4    defaults
libtiff                   4.0.9                h36446d0_2    defaults
libxml2                   2.9.8                hadb2253_1    defaults
libxslt                   1.1.32               hf6f1972_0    defaults
llvmlite                  0.27.0           py36ha925a31_0    defaults
locket                    0.2.0            py36hfed976d_1    defaults
lxml                      4.3.0            py36h1350720_0    defaults
lz4-c                     1.8.1.2              h2fa13f4_0    defaults
lzo                       2.10                 h6df0209_2    defaults
m2w64-gcc-libgfortran     5.3.0                         6    defaults
m2w64-gcc-libs            5.3.0                         7    defaults
m2w64-gcc-libs-core       5.3.0                         7    defaults
m2w64-gmp                 6.1.0                         2    defaults
m2w64-libwinpthread-git   5.0.0.4634.697f757               2    defaults
markdown                  3.0.1                    py36_0    defaults
markupsafe                1.1.1            py36he774522_0    defaults
matplotlib                3.0.2            py36hc8f65d3_0    defaults
mccabe                    0.6.1                    py36_1    defaults
menuinst                  1.4.14           py36hfa6e2cd_0    defaults
mistune                   0.8.4            py36he774522_0    defaults
mkl                       2019.1                      144    defaults
mkl-service               1.1.2            py36hb782905_5    defaults
mkl_fft                   1.0.10           py36h14836fe_0    defaults
mkl_random                1.0.2            py36h343c172_0    defaults
mock                      2.0.0                    pypi_0    pypi
more-itertools            5.0.0                    py36_0    defaults
mpmath                    1.1.0                    py36_0    defaults
msgpack-python            0.6.1            py36h74a9793_1    defaults
msys2-conda-epoch         20160418                      1    defaults
multipledispatch          0.6.0                    py36_0    defaults
music21                   5.5.0                    pypi_0    pypi
navigator-updater         0.2.1                    py36_0    defaults
nb_anacondacloud          1.4.0                    py36_0    https://mirrors.tun
a.tsinghua.edu.cn/anaconda/pkgs/free
nb_conda                  2.2.0                    py36_0    https://mirrors.tun
a.tsinghua.edu.cn/anaconda/pkgs/free
nb_conda_kernels          2.1.0                    py36_0    https://mirrors.tun
a.tsinghua.edu.cn/anaconda/pkgs/free
nbconvert                 5.4.1                    py36_0    defaults
nbformat                  4.4.0            py36h3a5bc1b_0    defaults
nbpresent                 3.0.2                    py36_0    https://mirrors.tun
a.tsinghua.edu.cn/anaconda/pkgs/free
networkx                  2.2                      py36_1    defaults
nltk                      3.4                      py36_1    defaults
nose                      1.3.7                    py36_2    defaults
notebook                  5.7.4                    py36_0    defaults
numba                     0.42.0           py36hf9181ef_0    defaults
numexpr                   2.6.9            py36hdce8814_0    defaults
numpy                     1.16.1                   pypi_0    pypi
numpy-base                1.16.2           py36hc3f5095_0    defaults
numpydoc                  0.8.0                    py36_0    defaults
odo                       0.5.1            py36h7560279_0    defaults
olefile                   0.46                     py36_0    defaults
opencv                    3.4.2            py36h40b0b35_0    defaults
openpyxl                  2.6.0                    py36_0    defaults
openssl                   1.1.1b               he774522_1    defaults
packaging                 19.0                     py36_0    defaults
pandas                    0.24.1           py36ha925a31_0    defaults
pandoc                    1.19.2.1             hb2460c7_1    defaults
pandocfilters             1.4.2                    py36_1    defaults
parso                     0.3.4                    py36_0    defaults
partd                     0.3.9                    py36_0    defaults
path.py                   11.5.0                   py36_0    defaults
pathlib2                  2.3.3                    py36_0    defaults
patsy                     0.5.1                    py36_0    defaults
pbr                       5.1.2                    pypi_0    pypi
pep8                      1.7.1                    py36_0    defaults
pickleshare               0.7.5                    py36_0    defaults
pillow                    5.4.1            py36hdc69c19_0    defaults
pip                       19.0.3                   py36_0    defaults
pkginfo                   1.5.0.1                  py36_0    defaults
pluggy                    0.9.0                    py36_0    defaults
ply                       3.11                     py36_0    defaults
prometheus_client         0.6.0                    py36_0    defaults
prompt_toolkit            2.0.9                    py36_0    defaults
protobuf                  3.6.1                    pypi_0    pypi
psutil                    5.5.0            py36he774522_0    defaults
py                        1.8.0                    py36_0    defaults
py-lief                   0.9.0            py36ha925a31_2    defaults
py-opencv                 3.4.2            py36hc319ecb_0    defaults
pycodestyle               2.5.0                    py36_0    defaults
pycosat                   0.6.3            py36hfa6e2cd_0    defaults
pycparser                 2.19                     py36_0    defaults
pycrypto                  2.6.1            py36hfa6e2cd_9    defaults
pycurl                    7.43.0.2         py36h7a1dbc1_0    defaults
pydot                     1.4.1                    pypi_0    pypi
pydot-ng                  2.0.0                    pypi_0    pypi
pydotplus                 2.0.2                    pypi_0    pypi
pydub                     0.23.1                   pypi_0    pypi
pyflakes                  2.1.0                    py36_0    defaults
pygments                  2.3.1                    py36_0    defaults
pylint                    2.2.2                    py36_0    defaults
pyodbc                    4.0.26           py36ha925a31_0    defaults
pyopenssl                 19.0.0                   py36_0    defaults
pyparsing                 2.3.1                    py36_0    defaults
pyqt                      5.9.2            py36h6538335_2    defaults
pysocks                   1.6.8                    py36_0    defaults
pytables                  3.4.4            py37he6f6034_0    defaults
pytest                    4.3.0                    py36_0    defaults
pytest-arraydiff          0.3              py36h39e3cac_0    defaults
pytest-astropy            0.5.0                    py36_0    defaults
pytest-doctestplus        0.2.0                    py36_0    defaults
pytest-openfiles          0.3.2                    py36_0    defaults
pytest-remotedata         0.3.1                    py36_0    defaults
python                    3.6.8                h9f7ef89_7    defaults
python-dateutil           2.8.0                    py36_0    defaults
python-graphviz           0.10.1                   pypi_0    pypi
python-libarchive-c       2.8                      py36_6    defaults
pytz                      2018.9                   py36_0    defaults
pywavelets                1.0.1            py36h8c2d366_0    defaults
pywin32                   223              py36hfa6e2cd_1    defaults
pywinpty                  0.5.5                 py36_1000    defaults
pyyaml                    3.13             py36hfa6e2cd_0    defaults
pyzmq                     17.1.2           py36hfa6e2cd_0    defaults
qt                        5.9.7            vc14h73c81de_0  [vc14]  defaults
qtawesome                 0.5.6                      py_0    defaults
qtconsole                 4.4.3                    py36_0    defaults
qtpy                      1.6.0                      py_0    defaults
requests                  2.21.0                   py36_0    defaults
rope                      0.12.0                   py36_0    defaults
ruamel_yaml               0.15.46          py36hfa6e2cd_0    defaults
scikit-image              0.14.1           py36ha925a31_0    defaults
scikit-learn              0.20.2           py36h343c172_0    defaults
scipy                     1.2.1            py36h29ff71c_0    defaults
seaborn                   0.9.0                    py36_0    defaults
send2trash                1.5.0                    py36_0    defaults
setuptools                40.8.0                   py36_0    defaults
simplegeneric             0.8.1                    py36_2    defaults
singledispatch            3.4.0.3          py36h17d0c80_0    defaults
sip                       4.19.8           py36h6538335_0    defaults
six                       1.12.0                   py36_0    defaults
snappy                    1.1.7                h777316e_3    defaults
snowballstemmer           1.2.1            py36h763602f_0    defaults
sortedcollections         1.1.2                    py36_0    defaults
sortedcontainers          2.1.0                    py36_0    defaults
soupsieve                 1.7.1                    py36_0    defaults
sphinx                    1.8.4                    py36_0    defaults
sphinxcontrib             1.0                      py36_1    defaults
sphinxcontrib-websupport  1.1.0                    py36_1    defaults
spyder                    3.3.3                    py36_0    defaults
spyder-kernels            0.4.2                    py36_0    defaults
sqlalchemy                1.2.18           py36he774522_0    defaults
sqlite                    3.26.0               he774522_0    defaults
statsmodels               0.9.0            py36h452e1ab_0    defaults
sympy                     1.3                      py36_0    defaults
tblib                     1.3.2            py36h30f5020_0    defaults
tensorboard               1.12.2           py36h33f27b4_0    defaults
tensorflow                1.13.0rc2                pypi_0    pypi
tensorflow-base           1.12.0          mkl_py36h81393da_0    defaults
tensorflow-estimator      1.13.0                   pypi_0    pypi
tensorflow-gpu            1.13.1                   pypi_0    pypi
termcolor                 1.1.0                    pypi_0    pypi
terminado                 0.8.1                    py36_1    defaults
testpath                  0.4.2                    py36_0    defaults
text-unidecode            1.2                      pypi_0    pypi
tk                        8.6.8                hfa6e2cd_0    defaults
toolz                     0.9.0                    py36_0    defaults
tornado                   5.1.1            py36hfa6e2cd_0    defaults
tqdm                      4.31.1                     py_0    defaults
traitlets                 4.3.2            py36h096827d_0    defaults
typed-ast                 1.3.1            py36he774522_0    defaults
unicodecsv                0.14.1           py36h6450c06_0    defaults
urllib3                   1.24.1                   py36_0    defaults
vc                        14.1                 h0510ff6_4    defaults
vs2015_runtime            14.15.26706          h3a45250_0    defaults
wcwidth                   0.1.7            py36h3d5aa90_0    defaults
webencodings              0.5.1                    py36_1    defaults
werkzeug                  0.14.1                   py36_0    defaults
wheel                     0.33.1                   py36_0    defaults
widgetsnbextension        3.4.2                    py36_0    defaults
win_inet_pton             1.1.0                    py36_0    defaults
win_unicode_console       0.5              py36hcdbd4b5_0    defaults
wincertstore              0.2              py36h7fe50ca_0    defaults
winpty                    0.4.3                         4    defaults
wrapt                     1.11.1           py36he774522_0    defaults
xlrd                      1.2.0                    py36_0    defaults
xlsxwriter                1.1.5                    py36_0    defaults
xlwings                   0.15.3                   py36_0    defaults
xlwt                      1.3.0            py36h1a4751e_0    defaults
xz                        5.2.4                h2fa13f4_4    defaults
yaml                      0.1.7                hc54c509_2    defaults
zeromq                    4.2.5                he025d50_1    defaults
zict                      0.1.3                    py36_0    defaults
zlib                      1.2.11               h62dcd97_3    defaults
zstd                      1.3.7                h508b16e_0    defaults
```
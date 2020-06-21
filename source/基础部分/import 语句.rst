============
import 语句
============


Python 是一门动态语言，意味着你定义变量的时候不必预先确定它的类型。

同时在运行过程中可以导入其他文件中的代码，这意味着你可以在使用前的任意位置来导入函数。
但是为了增强可读性和移植性，建议所有的导入写在文件开头方便检查。

import 可以从别的文件中导入函数。

函数
----------

首先明确函数的概念，一些常用的代码我们可以把它们封装起来，方便使用。

如下的函数把一个没有单位的数字保留两位小数并添加单位 ms（毫秒）。

.. code-block:: python

    def function(time_without_unit):
        print(round(time_without_unit, 2), end='')
        print('ms')

我的一段代码中需要输出一些时间，不使用函数的代码如下：

.. code-block:: python

    clock_time = 0
    
    # do something...
    
    print(round(time_without_unit, 2), end='')
    print('ms')
    # do something...
    print(round(time_without_unit, 2), end='')
    print('ms')
    # do something...
    print(round(time_without_unit, 2), end='')
    print('ms')

使用函数的代码如下：

.. code-block:: python

    def print_with_unit(time_without_unit):
        print(round(time_without_unit, 2), end='')
        print('ms')

    clock_time = 0
    
    # do something...
    print_with_unit(clock_time)    
    # do something...
    print_with_unit(clock_time)
    # do something...
    print_with_unit(clock_time)

显然，函数封装后可以提高代码的可读性，减少代码量。
并且其他文件中有需求的话不用重复编写，直接导入就可以了。

import
----------

假设在 Code 文件夹下有两个文件，lib.py 和 run.py。

.. role:: raw-html(raw)
    :format: html

./ Code      
:raw-html:`<br />`
- lib.py     
:raw-html:`<br />`
- run.py     
:raw-html:`<br />`

lib.py:

.. code-block:: python

    def print_with_unit(time_without_unit):
        print(round(time_without_unit, 2), end='')
        print('ms')

run.py:

.. code-block:: python

    import lib
    
    time_num = 0
    
    '''
    do something
    time_num += 5
    '''

    lib.print_with_unit(time_num)

在 run.py 中导入了 lib.py 中的函数，使用的时候 ``lib.print_with_unit(time_num)`` 表明
使用的是 lib.py 中的 ``print_with_unit`` 函数。这样不同的包/模块中可以使用相同的函数名，调用的
时候加上来源表明使用的哪个函数。

另一种写法：
:raw-html:`<br />`
run.py:

.. code-block:: python

    from lib import print_with_unit
    
    time_num = 0
    
    '''
    do something
    time_num += 5
    '''

    print_with_unit(time_num)

这种写法把  ``print_with_unit`` 函数导入了 run.py 中，
使用的时候不用声明来源，但是要注意函数命名冲突。这种写法和下面的等效:

run.py:

.. code-block:: python

    from lib import *
    
    time_num = 0
    
    '''
    do something
    time_num += 5
    '''

    print_with_unit(time_num)

这个 ``*`` 是导入了 lib.py 中的所有函数，使用起来和上一种一样。同样要注意函数命名的冲突问题。
而如果 lib.py 中函数特别多的时候，使用 ``from lib import *`` 导入全部函数可能会比较慢，
如果只使用其中的几个函数的话就用 ``from lib import print_with_unit`` 来导入需要的函数就会快一些。

以 Numpy 的导入为例:

.. code-block:: python

    import Numpy as np

意思就是把 Numpy 导入进来，改个名字叫 np，这样写起来干净利索些。
调用函数的话就直接 ``np.loadtxt()`` 这样即可。

总结
------

总而言之，建议使用

.. code-block:: python

    import Numpy as np
    import cv2

这种写法，可以避免一些潜在的命名冲突。

如果只用某个模块中的一个函数，可以使用

.. code-block:: python


    from lib import print_with_unit

这种。

而 Matplotlib 比较特殊一些，由于使用习惯的问题大家都写成 ``from import * `` 的格式，所以就沿用下来了。
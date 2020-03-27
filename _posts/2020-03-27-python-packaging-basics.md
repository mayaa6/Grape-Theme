---
layout: post
title: 怎么样打包Python命令行程序
subtitle : Python Packaging Basics
tags: [Dev]
category: blog
author: No Wonder
comments : True
---

怎样打包发布Python写的命令行程序？有两种方法：

1. Pyinstaller
2. Python Packaging

使用Pyinstaller可以将python程序连同python运行环境一起打包成一个文件，方便在没有安装python的电脑上运行。这种方法的缺点是文件体积大（300M以上）和运行时间长（需要先解压文件，布置python运行环境）。

对于使用python的用户，还是使用python packaging方法比较好。

## Python包格式

有两种python程序包的格式：

1. eggs
2. wheels

Eggs是setuptools引入的包格式，发布时间较早。Wheels是新发布的格式，较Eggs有较大的优势，详见[wheel-vs-egg](https://packaging.python.org/discussions/wheel-vs-egg/)。PIP上大部分的包都已经使用wheels，具体数据见[pythonwheels.com](http://pythonwheels.com/)。

## 设置文件

Python打包的主要工作是编写`setup.py`文件和`setup.cfg`文件。前者是对package的定义，后者是对wheels文件的定义。

## 使用entry_points，避免使用scripts

[click setup tools integration](https://click.palletsprojects.com/en/7.x/setuptools/)中写出了在`setup.py`中使用entry_points而不是scripts的三个原因。最主要的区别是：使用scripts时，pip显性地将命令脚本文件拷贝到系统PATH中；而使用entry_points时，pip自动针对不同操作系统，使用不同的策略将生成命令脚本并添加到PATH中，这样就避免了脚本在windows中不能执行的麻烦。

## 一句话总结

在setup.py中设置`entry_points`,使用pip打包成wheels文件。

一个最简单的参考`setup.py`文件如下：

```python
from setuptools import setup, find_packages
setup(
    name="PackageName",
    version="0.1",
    packages=find_packages(),
    entry_points={
        'console_scripts': [
            'your-command=your_command.main:cli',
        ],
    },
    install_requires=[
        'Click',
        'pandas'
    ],
)
```

## 参考文档

1. [python-packaging.readthedocs.io](https://python-packaging.readthedocs.io/en/latest/index.html)
2. [Setuptools document](https://setuptools.readthedocs.io/en/latest/setuptools.html)

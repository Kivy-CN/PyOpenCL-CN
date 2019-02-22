欢迎来到 PyOpenCL 中文文档
====================================

[原文地址](https://documen.tician.de/pyopencl/index.html)
翻译:[CycleUser](https://github.com/cycleuser)
_________________________

PyOpenCL 让你可以以Pythonic风格,简单地使用[OpenCL](http://www.khronos.org/opencl/) 的并行计算接口(parallel computation API).它具有如下的特点:

- 与对象生命周期(ifetime of objects)绑定的对象清理(Object cleanup). 在C++中这个术语(idiom)也叫做
 [RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization)(中文直译为"资源获取即初始化",具体来说是在构造函数中申请资源，析构函数中释放资源).这样有利于写正确代码,避免代码出现泄漏或者崩溃.
- 完备性(Completeness). PyOpenCL 为开发人员提供了全部的 OpenCL API 支持. 所有的`get_info()` 查询(query)以及所有的`CL`调用(calls)都是可用的(accessible).
- 自动错误检查.所有的错误都会自动翻译成 Python 异常(exceptions).
- 速度. PyOpenCL 的底层是用 C++ 写的, 所以速度非常快.
- 有帮助的文档. 也就是你现在在读的这个. ;).
- 自由的授权协议(Liberal license). PyOpenCL 在 MIT 协议下开源发布,可以自由用于商业用途/学术用途或者私人用途(free for commercial, academic, 和 
 private use).

[样例代码地址](https://github.com/inducer/pyopencl/blob/master/examples/demo.py)

指南(Tutorials)
=========

- Gaston Hillar 在Dr. Dobb 的Journal上写了一份 [PyOpenCL 简单指南](http://www.drdobbs.com/open-source/easy-opencl-with-python/240162614)很适合入门认识,这份文档目前正在询问原作者是否可以翻译,如果能翻译也会翻译一份过来.
- [Simon McIntosh-Smith](http://www.cs.bris.ac.uk/~simonm/) 以及 [Tom
 Deakin](http://www.tomdeakin.com/)合作的课程[H 和 s-on
 OpenCL](http://h 和 sonopencl.github.io/)中包含了[课程讲义](https://github.com/H 和 sOnOpenCL/Lecture-Slides/releases)
 和 [练习(有答案参考)](https://github.com/H 和 sOnOpenCL/Exercises-Solutions)
 (这一课程不仅讲 PyOpenCL, 也讲了 OpenCL 的 C 和 C++ 语言的 API).
- [PASI](http://bu.edu/pasi)的 PyOpenCL 课程 : 
 [1](https://www.youtube.com/watch?v=X9mflbX1NL8)
 [2](https://www.youtube.com/watch?v=MqvfCE_bKOg)
 [3](https://www.youtube.com/watch?v=TAvKmV7CuUw)
 [4](https://www.youtube.com/watch?v=SsuJ0LvZW1Q) (YouTube, 2011)
- [DTU GPULab](http://gpulab.imm.dtu.dk/) 和
 [Simula](http://simula.no/)也有 PyOpenCL 的课程 (2011): [Lecture
 1](http://tiker.net/pub/simula-pyopencl-lec1.pdf) [Lecture
 2](http://tiker.net/pub/simula-pyopencl-lec2.pdf) [Problem set
 1](http://tiker.net/pub/simula-pyopencl-probset1.pdf) [Problem set
 2](http://tiker.net/pub/simula-pyopencl-probset2.pdf)
- Ian Johnson 也写了一份[PyOpenCL
 tutorial](https://web.archive.org/web/20170907175053/http://enja.org:80/2011/02/22/adventures-in-pyopencl-part-1-getting-started-with-python).

PyOpenCL 相关的软件项目
=============================================

- Jon Roose 的 [pyclblas](https://pyclblas.readthedocs.io/en/latest/index.html)
 ([代码地址](https://github.com/jroose/pyclblas)) 提供了 [clBLAS](https://github.com/clMathLibraries/clBLAS) 形式的 BLAS, 被用在了 PyOpenCL 的代码中.(译者注:BLAS,是 Basic Linear Algebra Subprograms 的缩写,是一个基础线性代数库.)

 另外还有两个早期的封装(earlier wrappers),作者分别是 [Eric
 Hunsberger](https://github.com/hunse/pyopencl_blas) 以及 [Lars
 Ericson](http://lists.tiker.net/pipermail/pyopencl/2015-June/001890.html).

- Cedric Nugteren 提供了对 [CLBlast](https://github.com/CNugteren/CLBlast), 一个OpenCL BLAS 库的封装(wrappers):
 [PyCLBlast](https://github.com/CNugteren/CLBlast/tree/master/src/pyclblast).
- Gregor Thalhammer 的 [gpyfft](https://github.com/geggo/gpyfft)
 是一个 OpenCL FFT 的 Python 封装, 基于 AMD 的 clFFT.(译者注: FFT 是 Fast Fourier Transform 的缩写,快速傅里叶变换的意思.).
- Bogdan Opanchuk 的 [reikna](http://pypi.python.org/pypi/reikna) 提供了很多基于 GPU 的算法 (快速傅里叶变换,随机数生成,矩阵乘法),这些算法是设计用于 pyopencl.array.Array 对象.
- Troels Henriksen, Ken Friis Larsen, 和 Cosmin Oancea 的
 [Futhark](http://futhark-lang.org/) 编程语言提供了在对 pyopencl.array.Array 实例(instance)的数据进行缩减和扫描, 以编写网络并行程序( nested-parallel programs)的良好方法.
- Robbert Harms 和 Alard Roebroeck 的
 [MOT](https://github.com/cbclab/MOT) 提供了各种基于 GPU 的非线性优化算法(non-linear optimization algorithms) 和 MCMC 采样方法(sampling routines) 来进行并行优化 (parallel optimization) 和多重采样 (sampling of multiple problems).

如果你觉得有某些软件应该添加到这个列表里面,可以到[GitHub 上的 PyOpenCL 项目上](https://github.com/inducer/pyopencl/issues) 告知开发者,或者直接提交补丁就更好了.


内容(Contents)
========

要注意这份文档并不会解释 OpenCL 的编程和技术细节,这部分内容请参考[Khronos 官方网站的 OpenCL 文档](http://khronos.org/opencl)

PyOpenCL 也有自己的 [官方网站](http://mathema.tician.de/software/pyopencl), 你可以在官网来查找更新,新版本,文档,以及获取支持.

目录和列表
==================

- genindex
- modindex
- search


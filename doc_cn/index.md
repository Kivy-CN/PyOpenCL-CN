欢迎来到 PyOpenCL 中文文档
====================================

[原文地址](https://documen.tician.de/pyopencl/index.html)
翻译:[CycleUser](https://github.com/cycleuser)
_________________________

PyOpenCL 让你可以以Pythonic风格,简单地使用[OpenCL](http://www.khronos.org/opencl/) 的并行计算接口(parallel computation API).它具有如下的特点:

-   与对象生命周期(ifetime of objects)绑定的对象清理(Object cleanup). 在C++中这个术语(idiom)也叫做
    [RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization)(中文直译为"资源获取即初始化",具体来说是在构造函数中申请资源，析构函数中释放资源).这样有利于写正确代码,避免代码出现泄漏或者崩溃.
-   完备性(Completeness). PyOpenCL 为开发人员提供了全部的 OpenCL API 支持. 所有的`get_info()` 查询(query)以及所有的`CL`调用(calls)都是可用的(accessible).
-   自动错误检查.所有的错误都会自动翻译成 Python 异常(exceptions).
-   速度. PyOpenCL 的底层是用 C++ 写的, 所以速度非常快.
-   有帮助的文档Helpful Documentation. You're looking at it. ;)
-   Liberal license. PyOpenCL is open-source under the
    MIT license \<license\> and free for commercial, academic, and
    private use.

Here's an example, to give you an impression:

(You can find this example as examples/demo.py \<../examples/demo.py\>
in the PyOpenCL source distribution.)

Tutorials
=========

-   Gaston Hillar's [two-part article
    series](http://www.drdobbs.com/open-source/easy-opencl-with-python/240162614)
    in Dr. Dobb's Journal provides a friendly introduction to PyOpenCL.
-   [Simon McIntosh-Smith](http://www.cs.bris.ac.uk/~simonm/) and [Tom
    Deakin](http://www.tomdeakin.com/)'s course [Hands-on
    OpenCL](http://handsonopencl.github.io/) contains both [lecture
    slides](https://github.com/HandsOnOpenCL/Lecture-Slides/releases)
    and [exercises (with
    solutions)](https://github.com/HandsOnOpenCL/Exercises-Solutions)
    (The course covers PyOpenCL as well as OpenCL's C and C++ APIs.)
-   PyOpenCL course at [PASI](http://bu.edu/pasi): Parts
    [1](https://www.youtube.com/watch?v=X9mflbX1NL8)
    [2](https://www.youtube.com/watch?v=MqvfCE_bKOg)
    [3](https://www.youtube.com/watch?v=TAvKmV7CuUw)
    [4](https://www.youtube.com/watch?v=SsuJ0LvZW1Q) (YouTube, 2011)
-   PyOpenCL course at [DTU GPULab](http://gpulab.imm.dtu.dk/) and
    [Simula](http://simula.no/) (2011): [Lecture
    1](http://tiker.net/pub/simula-pyopencl-lec1.pdf) [Lecture
    2](http://tiker.net/pub/simula-pyopencl-lec2.pdf) [Problem set
    1](http://tiker.net/pub/simula-pyopencl-probset1.pdf) [Problem set
    2](http://tiker.net/pub/simula-pyopencl-probset2.pdf)
-   Ian Johnson's [PyOpenCL
    tutorial](https://web.archive.org/web/20170907175053/http://enja.org:80/2011/02/22/adventures-in-pyopencl-part-1-getting-started-with-python).

Software that works with or enhances PyOpenCL
=============================================

-   Jon Roose's
    [pyclblas](https://pyclblas.readthedocs.io/en/latest/index.html)
    ([code](https://github.com/jroose/pyclblas)) makes BLAS in the form
    of [clBLAS](https://github.com/clMathLibraries/clBLAS) available
    from within pyopencl code.

    Two earlier wrappers continue to be available: one by [Eric
    Hunsberger](https://github.com/hunse/pyopencl_blas) and one by [Lars
    Ericson](http://lists.tiker.net/pipermail/pyopencl/2015-June/001890.html).

-   Cedric Nugteren provides a wrapper for the
    [CLBlast](https://github.com/CNugteren/CLBlast) OpenCL BLAS library:
    [PyCLBlast](https://github.com/CNugteren/CLBlast/tree/master/src/pyclblast).
-   Gregor Thalhammer's [gpyfft](https://github.com/geggo/gpyfft)
    provides a Python wrapper for the OpenCL FFT library clFFT from AMD.
-   Bogdan Opanchuk's [reikna](http://pypi.python.org/pypi/reikna)
    offers a variety of GPU-based algorithms (FFT, random number
    generation, matrix multiplication) designed to work with
    pyopencl.array.Array objects.
-   Troels Henriksen, Ken Friis Larsen, and Cosmin Oancea's
    [Futhark](http://futhark-lang.org/) programming language offers a
    nice way to code nested-parallel programs with reductions and scans
    on data in pyopencl.array.Array instances.
-   Robbert Harms and Alard Roebroeck's
    [MOT](https://github.com/cbclab/MOT) offers a variety of GPU-enabled
    non-linear optimization algorithms and MCMC sampling routines for
    parallel optimization and sampling of multiple problems.

If you know of a piece of software you feel that should be on this list,
please let me know, or, even better, send a patch!

Contents
========

Note that this guide does not explain OpenCL programming and technology.
Please refer to the official [Khronos OpenCL
documentation](http://khronos.org/opencl) for that.

PyOpenCL also has its own [web
site](http://mathema.tician.de/software/pyopencl), where you can find
updates, new versions, documentation, and support.

Indices and tables
==================

-   genindex
-   modindex
-   search


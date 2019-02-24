OpenCL Runtime: 基本内容
======================


#### 原作者: Andreas Kloeckner <inform@tiker.net>
#### [原文地址](https://documen.tician.de/pyopencl/runtime.html)
#### 翻译:[CycleUser](https://github.com/cycleuser)

___________________________________



版本查询(Version Queries)
---------------

#### pyopencl.VERSION

返回 PyOpenCL 的版本,形式为整数(integer)组成的元组(tuple).这样更容易进行版本检查.例如`VERSION >= (0, 93)`.

#### pyopencl.VERSION_STATUS

返回 PyOpenCL 版本状态,形式为文本字符串,比如是`rc4`或者`beta`,验证当前的发行版本.

#### pyopencl.VERSION_TEXT

返回 PyOpenCL 的完整版本信息,形式为文本字符串,如`0.93rc4`.

#### pyopencl.get_cl_header_version()

返回 OpenCL 的完整版本号,形式为整数(integer)组成的元组(tuple),例如`(1,2)`.


出错反馈(Error Reporting)
---------------

#### class pyopencl.Error

PyOpenCL 中所有的 异常(exceptions)的基类.

#### class pyopencl.MemoryError

顾名思义,内存错误.

#### class pyopencl.LogicError

逻辑错误.

#### class pyopencl.RuntimeError

运行错误.
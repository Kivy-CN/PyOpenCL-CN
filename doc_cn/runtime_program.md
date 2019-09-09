OpenCL Runtime: 程序(Programs), 内核(Kernels)
===============================================

#### 原作者: Andreas Kloeckner <inform@tiker.net>
#### [原文地址](https://documen.tician.de/pyopencl/runtime_program.html)
#### 翻译:[CycleUser](https://github.com/cycleuser)

___________________________________

程序(Program)
-------

#### class Program(context, src)
 Program(context, devices, binaries)

二进制文件*binaries* 必须包含设备*devices*中的每一项(entry)对应的一个二进制项目*binary*。
如果参数*src*是一个字节对象（`bytes` object）且开头为一个有效的（valid）—标准可移植中间件表示（SPIR-V）的神奇数字（magic number），就会被鸳鸯传递到 OpenCL 实现，而不是作为 OpenCL C 代码（SPIR-V 要求 OpenCL 2.1 版本以及更新的版本）。

添加于版本 2016.2

增加对 SPIR-V 的支持

##### 属性 info

常量 `program_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

##### 方法 get_info(param)

查看 `program_info` 获取 *param* 的值.

##### 方法 get_build_info(device, param)

查看 `program_build_info` 获取 *param* 的值.

##### 方法 build(options=[], devices=None, cache_dir=None)

*options* 是一系列编译标志符（compiler flags）的字符串。
返回 *self*。

如果 *cache_dir* 非空 - 生成的二进制文件就会被缓存在指定路径中。
如果 *cache_dir* 为空，但该程序的上下文环境（context）创建时有非空的缓存目录，就将其用作缓存目录。
如果 *cache_dir* 为空，而且上下文环境（context）创建时也没有指定缓存目录，生成的二进制文件就将会缓存在目录`pyopencl-compiler-cache-vN-uidNAME-pyVERSION` 中，这个目录的位置可以通过函数`tempfile.gettempdir` 获取。
设置环境变量`PYOPENCL_NO_CACHE`为任意非空值，这个缓存就会被覆盖（suppressed）。环境变量`PYOPENCL_BUILD_OPTIONS`里面的所有选项都会被附加到 *options* 上。

添加于版本 2011.1
*options* 现在也是由字符串（`str`）组成的列表（`list`）。

添加于版本 2013.1
增加环境变量 `PYOPENCL_NO_CACHE`.
增加环境变量 `PYOPENCL_BUILD_OPTIONS`.

##### 方法 compile(self, options=[], devices=None, headers=[])

:param headers: 一个列表（list）由元组（tuple）组成 *(name, program)*.

添加于版本 CL 1.2.

添加于版本 2011.2

##### 属性 kernel_name

可以使用 ``program.kernel_name`` 从一个程序（program）中获取核对象（`Kernel`
objects）。要注意的是这样的查询方法每次都会产生一个新的核对象，所以下面这种代码**不可行**:


```Python
prg.sum.set_args(a_g, b_g, res_g)
ev = cl.enqueue_nd_range_kernel(queue, prg.sum, a_np.shape, None)
```

解决办法就是使用 (推荐的 recommended, 无状态的 stateless) 调用接口（calling interface）:

```Python
prg.sum(queue, prg.sum, a_np.shape, None)
```

或者将核作为一个临时变量（temporary variable）:

```Python
sum_knl = prg.sum
sum_knl.set_args(a_g, b_g, res_g)
ev = cl.enqueue_nd_range_kernel(queue, sum_knl, a_np.shape, None)
```

要注意这里的程序 `Program` 必须是构建完毕的 (查看 方法 `build`) 才能进行属性查询。

###### 注意 

这里的属性 `program_info` 存在于同一命名空间并且比核名称（`Kernel` names）更优先。 

##### 方法 all_kernels()

将程序（`Program`）中的所有核对象（`Kernel` objects）以一个列表的形式返回。

.. automethod： from_int_ptr
.. autoattribute： int_ptr

|comparable|

函数 create_program_with_built_in_kernels(context, devices, kernel_names)

添加于版本 CL 1.2.

添加于版本 2011.2

函数 link_program(context, programs, options=[], devices=None)

添加于版本 CL 1.2.

添加于版本 2011.2

函数 unload_platform_compiler(platform)

添加于版本 CL 1.2.

添加于版本 2011.2

内核（Kernel）
------

#### class Kernel(program, name)

##### 属性 info

常量`kernel_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

##### 方法 get_info(param)

查看 `kernel_info` 获取 *param* 的值.

##### 方法 get_work_group_info(param, device)

查看 `kernel_work_group_info` 获取 *param* 的值.

##### 方法 get_arg_info(arg_index, param)

查看 `kernel_arg_info` 获取 *param* 的值.

添加于 OpenCL 1.2 以及之后的版本。

##### 方法 set_arg(self, index, arg)

*arg* 可以试试

* `None`: 这可以是传递自 `__global` 内存索引（memory references）来传递一个空指针（NULL pointer）给核（kernel）。
* 所有符合 Python 缓存接口（Python buffer interface）的内容，比如 `numpy.ndarray`, `str`, 或者`numpy`的有符号标量（sized scalars）,比如`numpy.int32`
或者 `numpy.float64`.

 ###### 注意 

一定要注意，这里用 Python 自己原生的 `int`或者 `float` 可是不行的。如果要用这些类型，需要参考方法 `Kernel.set_scalar_arg_dtypes` 来进行调整使之工作。或者可以使用 Python 标准库中的结构体模块 `struct` 将 Python 的原生数据类型转换成字符形式（ `str`）的二进制数据（binary data）。

* 内存对象实例 `MemoryObject`. (比如 缓存 `Buffer`, 图像 `Image`, 等等)
* 局部内侧实例 `LocalMemory`.
* 抽样器实例 `Sampler`.
* 命令队列实例 `CommandQueue`. (仅限于 CL 2.0 以及更新的版本)

##### 方法 set_args(self, *args)

对 *args* 中的每个元素按照顺序依次调用方法 `set_arg`。

添加于版本 0.92

##### 方法 set_scalar_arg_dtypes(arg_dtypes)

将核参数（`Kernel` arguments）的标量的符号类型（sized types）告知程序封装（wrapper）。*arg_dtypes* 针对每个参数（argument）都有一个对应项（entry）。对于非标量（non-scalar），这就必须为空（*None*）。对于标量，就必须是一个对象，该对象需要能够被 `numpy.dtype` 构造器（constructor）所接收，也就意味着对应的标量参数是该类型的。

在搭配适当信息调用该函数后，大多数适合的数据类型都会自动传递成为核调用中的正确类型。

###### 注意 

上面方法所设置的信息是附加到某一单独核实例（a single kernel instance）的。而每次你使用`program.kernel` 进行属性读取的时候就会建立一个新的核实例。所以下面的代码就是不能正常工作的：

```Python
 prg = cl.Program(...).build()
 prg.kernel.set_scalar_arg_dtypes(...)
 prg.kernel(queue, n_globals, None, args)
```

##### 方法 __call__(queue, global_size, local_size, *args, global_offset=None, wait_for=None, g_times_l=False)

使用 函数 `enqueue_nd_range_kernel` 来讲一个核执行（kernel execution）提交队列（enqueue），这之前要使用方法 `set_args` 来依次设置每个参数（argument）。查看文档中关于方法 `set_arg` 的内容来了解允许的参数类型（argument types）有哪些。

*None* 可以传递给局部规模（local_size)。

如果指定了 *g_times_l* ，全局规模就是用这个值乘以局部规模（local size），这个特性和 NVIDIA 的 CUDA 相似。这种情况下，全局规模 *global_size* 和 局部规模 *local_size* 也不必须有同样的维度数(number
of dimensions)。

###### 注意 

方法 `__call__` is *not* thread-safe. It sets the arguments using 方法 `set_args`
and then runs 函数 `enqueue_nd_range_kernel`. Another thread could race it
in doing the same things, with undefined outcome. This issue is inherited
from the C-level OpenCL API. The recommended solution is to make a kernel
(i.e. access `prg.kernel_name`, which corresponds to making a new kernel)
for every thread that may enqueue calls to the kernel.

A solution involving implicit locks was discussed and decided against on the
mailing list in `October 2012
<http://lists.tiker.net/pipermail/pyopencl/2012-October/001311.html>`_.

添加于版本 0.92
*local_size* was promoted to third positional argument from being a
keyword argument. The old keyword argument usage will continue to
be accepted with a warning throughout the 0.92 release cycle.
This is a backward-compatible change (just barely!) because
*local_size* as third positional argument can only be a
`tuple`或者 *None*. `tuple` instances are never valid
`Kernel` arguments, and *None* is valid as an argument, but
its treatment in the wrapper had a bug (now fixed) that prevented
it from working.

添加于版本 2011.1
Added the *g_times_l* keyword arg.

##### 方法 capture_call(filename, queue, global_size, local_size, *args, global_offset=None, wait_for=None, g_times_l=False)

This method supports the exact same interface as 方法 `__call__`, but
instead of invoking the kernel, it writes a self-contained PyOpenCL program
to *filename* that reproduces this invocation. Data and kernel source code
will be packaged up in *filename*'s source code.

This is mainly intended as a debugging aid. For example, it can be used
to automate the task of creating a small, self-contained test case for
an observed problem. It can also help separate a misbehaving kernel from
a potentially large或者 time-consuming outer code.

To use, simply change：

evt = my_kernel(queue, gsize, lsize, arg1, arg2, ...)

to：

evt = my_kernel.capture_call("bug.py", queue, gsize, lsize, arg1, arg2, ...)

添加于版本 2013.1

.. automethod： from_int_ptr
.. autoattribute： int_ptr

|comparable|

#### class LocalMemory(size)

A helper class to pass `__local` memory arguments to kernels.

添加于版本 0.91.2

##### 属性 size

The size of local buffer in bytes to be provided.

函数 enqueue_nd_range_kernel(queue, kernel, global_work_size, local_work_size, global_work_offset=None, wait_for=None, g_times_l=False)

|std-enqueue-blurb|

If *g_times_l* is specified, the global size will be multiplied by the
local size. (which makes the behavior more like Nvidia CUDA) In this case,
*global_size* and *local_size* also do not have to have the same number
of dimensions.

添加于版本 2011.1
Added the *g_times_l* keyword arg.

函数 enqueue_task(queue, kernel, wait_for=None)

|std-enqueue-blurb|

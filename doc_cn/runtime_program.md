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

*binaries* must contain one binary for each entry in *devices*.
If *src* is a `bytes` object starting with a valid `SPIR-V
<https://www.khronos.org/spir>`_ magic number, it will be handed
off to the OpenCL implementation as such, rather than as OpenCL C source
code. (SPIR-V support requires OpenCL 2.1.)

添加于版本 2016.2

增加对 SPIR-V 的支持

##### 属性 info

Lower case versions of the `program_info` constants
may be used as attributes on instances of this class
to directly query info attributes.

##### 方法 get_info(param)

查看 `program_info` 获取 *param* 的值.

##### 方法 get_build_info(device, param)

查看 `program_build_info` 获取 *param* 的值.

##### 方法 build(options=[], devices=None, cache_dir=None)

*options* is a string of compiler flags.
Returns *self*.

If *cache_dir* is not None - built binaries are cached in an on-disk cache
with given path.
If passed *cache_dir* is None, but context of this program was created with
not-None cache_dir - it will be used as cache directory.
If passed *cache_dir* is None and context was created with None cache_dir:
built binaries will be cached in an on-disk cache called
:file:`pyopencl-compiler-cache-vN-uidNAME-pyVERSION` in the directory
returned by :func:`tempfile.gettempdir`. By setting the environment
variable :envvar:`PYOPENCL_NO_CACHE` to any non-empty value, this
caching is suppressed. Any options found in the environment variable
:envvar:`PYOPENCL_BUILD_OPTIONS` will be appended to *options*.

添加于版本 2011.1
*options* may now also be a `list` of `str`.

添加于版本 2013.1
Added :envvar:`PYOPENCL_NO_CACHE`.
Added :envvar:`PYOPENCL_BUILD_OPTIONS`.

##### 方法 compile(self, options=[], devices=None, headers=[])

:param headers: a list of tuples *(name, program)*.

Only available with CL 1.2.

添加于版本 2011.2

##### 属性 kernel_name

You may use ``program.kernel_name`` to obtain a `Kernel`
objects from a program. Note that every lookup of this type
produces a new kernel object, so that this **won't** work::

prg.sum.set_args(a_g, b_g, res_g)
ev = cl.enqueue_nd_range_kernel(queue, prg.sum, a_np.shape, None)

Instead, either use the (recommended, stateless) calling interface::

prg.sum(queue, prg.sum, a_np.shape, None)

or keep the kernel in a temporary variable::

sum_knl = prg.sum
sum_knl.set_args(a_g, b_g, res_g)
ev = cl.enqueue_nd_range_kernel(queue, sum_knl, a_np.shape, None)

Note that the `Program` has to be built (查看 :meth:`build`) in
order for this to work simply by attribute lookup.

###### 注意 

The `program_info` attributes live
in the same name space and take precedence over
`Kernel` names.

##### 方法 all_kernels()

Returns a list of all `Kernel` objects in the `Program`.

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

|comparable|

函数 create_program_with_built_in_kernels(context, devices, kernel_names)

Only available with CL 1.2.

添加于版本 2011.2

函数 link_program(context, programs, options=[], devices=None)

Only available with CL 1.2.

添加于版本 2011.2

函数 unload_platform_compiler(platform)

Only available with CL 1.2.

添加于版本 2011.2

内核（Kernel）
------

#### class Kernel(program, name)

##### 属性 info

Lower case versions of the `kernel_info` constants
may be used as attributes on instances of this class
to directly query info attributes.

##### 方法 get_info(param)

查看 `kernel_info` 获取 *param* 的值.

##### 方法 get_work_group_info(param, device)

查看 `kernel_work_group_info` 获取 *param* 的值.

##### 方法 get_arg_info(arg_index, param)

查看 `kernel_arg_info` 获取 *param* 的值.

Only available in OpenCL 1.2 and newer.

##### 方法 set_arg(self, index, arg)

*arg* may be

* `None`: This may be passed for `__global` memory references
 to pass a NULL pointer to the kernel.
* Anything that satisfies the Python buffer interface,
 in particular `numpy.ndarray`, `str`,
 or :mod:`numpy`'s sized scalars, such as `numpy.int32`
 or `numpy.float64`.

 ###### 注意 

 Note that Python's own `int` or `float`
 objects will not work out of the box. See
 :meth:`Kernel.set_scalar_arg_dtypes` for a way to make
 them work. Alternatively, the standard library module
 :mod:`struct` can be used to convert Python's native
 number types to binary data in a `str`.

* An instance of `MemoryObject`. (e.g. `Buffer`,
 `Image`, etc.)
* An instance of `LocalMemory`.
* An instance of `Sampler`.
* An instance of `CommandQueue`. (CL 2.0 and higher only)

##### 方法 set_args(self, *args)

Invoke :meth:`set_arg` on each element of *args* in turn.

添加于版本 0.92

##### 方法 set_scalar_arg_dtypes(arg_dtypes)

Inform the wrapper about the sized types of scalar
`Kernel` arguments. For each argument,
*arg_dtypes* contains an entry. For non-scalars,
this must be *None*. For scalars, it must be an
object acceptable to the `numpy.dtype`
constructor, indicating that the corresponding
scalar argument is of that type.

After invoking this function with the proper information,
most suitable number types will automatically be
cast to the right type for kernel invocation.

###### 注意 

The information set by this rountine is attached to a single kernel
instance. A new kernel instance is created every time you use
`program.kernel` attribute access. The following will therefore not
work::

  prg = cl.Program(...).build()
  prg.kernel.set_scalar_arg_dtypes(...)
  prg.kernel(queue, n_globals, None, args)


##### 方法 __call__(queue, global_size, local_size, *args, global_offset=None, wait_for=None, g_times_l=False)

Use :func:`enqueue_nd_range_kernel` to enqueue a kernel execution, after using
:meth:`set_args` to set each argument in turn. 查看 the documentation for
:meth:`set_arg` to 查看 what argument types are allowed.
|std-enqueue-blurb|

*None* may be passed for local_size.

If *g_times_l* is specified, the global size will be multiplied by the
local size. (which makes the behavior more like Nvidia CUDA) In this case,
*global_size* and *local_size* also do not have to have the same number
of dimensions.

###### 注意 

:meth:`__call__` is *not* thread-safe. It sets the arguments using :meth:`set_args`
and then runs :func:`enqueue_nd_range_kernel`. Another thread could race it
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
`tuple` or *None*. `tuple` instances are never valid
`Kernel` arguments, and *None* is valid as an argument, but
its treatment in the wrapper had a bug (now fixed) that prevented
it from working.

添加于版本 2011.1
Added the *g_times_l* keyword arg.

##### 方法 capture_call(filename, queue, global_size, local_size, *args, global_offset=None, wait_for=None, g_times_l=False)

This method supports the exact same interface as :meth:`__call__`, but
instead of invoking the kernel, it writes a self-contained PyOpenCL program
to *filename* that reproduces this invocation. Data and kernel source code
will be packaged up in *filename*'s source code.

This is mainly intended as a debugging aid. For example, it can be used
to automate the task of creating a small, self-contained test case for
an observed problem. It can also help separate a misbehaving kernel from
a potentially large or time-consuming outer code.

To use, simply change::

evt = my_kernel(queue, gsize, lsize, arg1, arg2, ...)

to::

evt = my_kernel.capture_call("bug.py", queue, gsize, lsize, arg1, arg2, ...)

添加于版本 2013.1

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

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

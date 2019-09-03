OpenCL Runtime: 平台(Platforms), 设备(Devices), 上下文(Contexts)
===============================================

#### 原作者: Andreas Kloeckner <inform@tiker.net>
#### [原文地址](https://documen.tician.de/pyopencl/runtime_platform.html)
#### 翻译:[CycleUser](https://github.com/cycleuser)

___________________________________

平台(Platform)
--------

#### pyopencl.get_platforms()

返回一个平台实例(`Platform` instances)组成的列表(list).

#### class pyopencl.Platform

##### info

`platform_info` 常量(constant)的小写字母版本,可以用于这个类的实例中作为属性(attribute)来直接查询(query) info 属性(attribute).

##### get_info(param)

参数(param)值参考`platform_info `常量中的相关内容.

##### get_devices(device_type=device_type.ALL)

返回符合`device_type`参数的设备列表.`device_type`的值参考`device_type`常量中的相关内容.

在 2013.2 版本中进行过变更,在此之前如果没有找到匹配参数的设备(device)会返回一个异常,从这个版本以后开始改成了返回一个空列表.

##### from_int_ptr(int_ptr_value: int, retain: bool=True)

pyopencl._cl.Platform
(静态方法(static method))返回一个新的 Python 对象,指向(referencing) C语言层面(C-level)的  cl_platform_id 对象,所在的内存位置由`int_ptr_value`所示.

如果`retain`为 True,相关的函数`clRetain*()`会被调用.如果对象的迁移厕所有者不释放当前指针(`reference`),`retain` 就会被设为 False, 来有效地将所有权转交给 pyopencl.

在 2013.2 版本中加入的, 其中 `retain`添加于 2016.1 版本.

##### int_ptr

返回一个整数(integer),对应的是`cl_platform_id.` 下的指针值(pointer value).使用 `from_int_ptr()` 来转换成一个 Python 对象(object).

添加自 2013.2.

这个类的实例是可哈希的(hashable),此类的两个实例之间可以使用`==`或者`!=~来进行对比.(上述特性添加自 2011.2 版本.) 如果两个对象所指向的 OpenCL 对象是相同的, 就认为这两个对象相同, 这是建立在 C 语言里面指针相等的基础上的.

设备(Device)
------

#### class pyopencl.Device

##### info

常量 `device_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。


##### get_info(param)

查看 `device_info` 得到 `param` 的值。

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

##### create_sub_devices(properties)

`properties` 是一个数组（array），数组元素可以是下面的一种或者多种:

    [ dpp.EQUALLY, 8]
    [ dpp.BY_COUNTS, 5, 7, 9, dpp.PARTITION_BY_COUNTS_LIST_END]
    [ dpp.BY_NAMES, 5, 7, 9, dpp.PARTITION_BY_NAMES_LIST_END]
    [ dpp.BY_AFFINITY_DOMAIN, dad.L1_CACHE]

其中的 `dpp` 是 `device_partition_property` 的缩写，直接翻译就是`设备分区性质`
而 `dad` 是 `device_affinity_domain`的缩写，直接翻译就是`设备关系域`

`PROPERTIES_LIST_END_EXT` 是自动添加的。

在 CL 1.2 以及更新的版本才支持。

添加于版本 2011.2

这个类（class）的两个实例（instances）之间的比较要使用 `=="` and `"!="`.

上下文(Context)
-------

#### class pyopencl.Context(devices=None, properties=None, dev_type=None, cache_dir=None)

创建一个新的上下文（context），其属性`properties`是一个键值对元组（key-value tuples）的列表（list），其中每个键（key）必须是上下文属性 `context_properties`之一。至少设备`devices`和设备类型`dev_type`都不能是空`None`，这里的设备`devices`是一个由设备实例（`Device` instances）组成的列表，而`dev_type`是设备类型`device_type`实例中的一个。

如果啥都没指定，就会创建一个`dev_type`为默认属性`device_type.DEFAULT`的上下文。
如果缓存目录`cache_dir`非空（不是`None`），就会对所有的`Program`实例使用默认的缓存目录`cache_dir`（这部分还可以参考关于`Program.build`方法的文档）。

##### 注意

在最近的一些支持 OpenCL 可安装客户端驱动 (Installable Client Drivers 缩写为 ICD)的 CL 驱动中，不加参数使用构造函数（constructor）可能会失败。如果想要最简单的开箱即用的上下文创建行为，推荐函数 `create_some_context`。例如可以参考这份
[`来自AMD的官方解释`](http://developer.amd.com/support/KnowledgeBase/Lists/KnowledgeBase/DispForm.aspx?ID=71).

##### 注意

在 OpenCL 1.1 版本以及以后的版本中，由于加入了 可安装客户端驱动  (Installable Client Drivers 缩写为 ICD)的支持而进行了调整，下面的代码`看上去`很合理没啥问题但经常不能工作：

```Python
    import pyopencl as cl
    ctx = cl.Context(dev_type=cl.device_type.ALL)
```

解决方案就是在通过类型选择设备（device）的时候选择一个平台（platform）：

```Python
    import pyopencl as cl

    platforms = cl.get_platforms()
    ctx = cl.Context(
            dev_type=cl.device_type.ALL,
            properties=[(cl.context_properties.PLATFORM, platforms[0])])
```

##### 注意

对于
`context_properties.CL_GL_CONTEXT_KHR`,
`context_properties.CL_EGL_DISPLAY_KHR`,
`context_properties.CL_GLX_DISPLAY_KHR`,
`context_properties.CL_WGL_HDC_KHR`, 以及
`context_properties.CL_CGL_SHAREGROUP_KHR`
`context_properties.CL_CGL_SHAREGROUP_APPLE`
键值对（key-value pair）中的值是一个 PyOpenGL 上下文环境（context）或者是显示实例（display instance）。

**此修改发生于版本** 0.91.2
构造函数增加了参数 `dev_type` 。

##### info

常量 `context_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

##### get_info(param)

查看 `context_info`  得到 `param` 的值。

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

##### static from_int_ptr(int_ptr_value: int, retain: bool = True) → pyopencl._cl.Context

静态方法(static method)，返回一个新的 Python 对象，该对象指向 C 语言层次的 CL 上下文对象（C-level cl_context object），其地址由`int_ptr_value`所指向。
如果设置保留参数（retain）为真（True），则会调用相关的函数 clRetain*()。如果该对象的前一个所有者不释放该引用，保留参数（retain）应该设置为假（False），以便将所有权有效率地转移到 pyopencl。

于版本 2013.2 中新增该项。

于版本 2016.1 中作出修改：增加 保留 *retain* 选项。

##### int_ptr

返回 CL 上下文(cl_context)的地址指针为一个整数（integer）。使用 `from_int_ptr()` 将其转换成一个 Python 对象。

于版本 2013.2 中新增该项。

这个类（classs）的实例（instance）是散列的（hashable），两个该类实例的对比要使用双等号 “==” 以及叹号加等号 “!=”。（可散列性（hashability）是在2011.2版本中开始添加的。）如果两个地址所指向的是同样的 OpenCL 对象，就认为这两个对象相等，这一点和 C 语言里面的指针是等价的。

#### pyopencl.create_some_context(interactive=True, answers=None, cache_dir=None)

创建一个上下文环境 （`Context`）。

如果平台或者设备都存在多个选择，`interactive`为真（True），另外`sys.stdin.isatty()` 也为真（True），然后程序会询问用户要选择哪个设备来使用。否则的话就会根据内部定义的规则（implementation-defined manner）来选择一个设备(device)。
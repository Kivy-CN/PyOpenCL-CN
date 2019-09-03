OpenCL Runtime: 命令队列(Command Queue), 事件(Events)
===============================================

#### 原作者: Andreas Kloeckner <inform@tiker.net>
#### [原文地址](https://documen.tician.de/pyopencl/runtime_queue.html)
#### 翻译:[CycleUser](https://github.com/cycleuser)

___________________________________

命令队列（Command Queue）
-------------

#### class CommandQueue(context, device=None, properties=None)

创建一个新的命令队列(command queue)。属性 `properties` 是一个位字段（bit field），包含命令队列属性 `command_queue_properties`的值。

如果设备`device`为空（None），上下文（`context`）中的设备（devices）之一以实现定义的方式（implementation-defined manner）来选择。

属性 `properties` 可以试试一个位组合（bitwise combination），取值自队列属性`queue_properties` (或者设置为空`None` 也就等价于传递过去一个`0`。) 这一特性在 OpenCL 1.X 和 2.X 中都兼容。

对 OpenCL 2.0 以及更新的版本，属性 `properties`也可以是一个键值对（keys and values）的序列（sequence），键值对取值自队列属性 `queue_properties` ，该属性为函数 `clCreateCommandQueueWithProperties`所接收 (具体信息参考 OpenCL 参数文档）。后缀的 `0` 是自动添加的不需要包含。

命令队列 `CommandQueue` 也可以用作一个上下文管理器（context manager），例如：

```Python
with cl.CommandQueue(self.cl_context) as queue:
    enqueue_stuff(queue, ...)
```

方法 `finish` 会在带分隔的上下文（with-delimited context）的末尾自动添加。

添加于版本 2013.1

实现了上下文管理器的兼容性（Context manager capability）。

版本变更于 2018.2

针对 OpenCL 2 增加了属性队列接口（sequence-of-properties interface)。

##### info

常量 `command_queue_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

##### get_info(param)

查看 `command_queue_info` 得到 `param` 的值。

##### set_property(prop, enable)

查看 `command_queue_properties` 来获取 `prop` 可取的值。
`enable` 是一个布尔值 `bool`.

在 OpenCL 1.1 以及更新的版本中就不被支持了。

##### flush()
##### finish()

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

|comparable|

事件（Event）
-----

#### class Event

##### info

常量 `event_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

##### profile.info

常量 `profiling_info` 的小写版本，可以用作该类（class）实例（instances）的实例（instances）的属性（attributes），可以直接查询 'info' 属性。

例如，你可以使用 `evt.profile.end` 来代替
`evt.get_profiling_info(pyopencl.profiling_info.END)`。

##### get_info(param)

查看 `event_info` 得到 `param` 的值。

##### get_profiling_info(param)

查看 `profiling_info` 得到 `param` 的值。

查看 `profile` 以更简单方式获取相关信息。

##### wait()

.. automethod:: from_int_ptr
.. autoattribute:: int_ptr

##### set_callback(type, cb)

Add the callback `cb` with signature ``cb(status)`` to the callback
queue for the event status `type` (one of the values of
`command_execution_status`, except :attr:`command_execution_status.QUEUED`).


添加回调 callback `cb` ，附带签名（signature） ``cb(status)`` 来回调针对事件状态（event status）为 `type` 的队列（queue），这里的 `type` 是 命令执行状态`command_execution_status`的一个值，例如 `command_execution_status.QUEUED`。

查询参考 OpenCL 的文档信息来查看参数 `cb` 的效果。

添加于版本 2015.2

|comparable|

事件子类（Event Subclasses）
----------------

#### class UserEvent(context)

事件`Event`的子类。仅在 OpenCL 1.1 以及更新的版本中可用。

添加于版本 0.92

##### set_status(status)

查看 `command_execution_status` 获取 `status` 的可选取值。

#### class NannyEvent

在宿主和设备之间的数据转换然后就返回这个类型的事件（event）。这类事件持有（hold）一个引用，指向宿主方（host-side）的缓存空间（buffer），然后等待数据转换完毕就释放掉。因此可以用于监控对象的析构（destruction），安全地释放引用。

事件 `Event` 的子类（subclass）。

添加于版本 2011.2

##### get_ward()

##### wait()

除了发挥和`Event.wait()`事件相似的作用，这个方法还会释放掉所监控对象（guarded object）的引用（reference）。

同步函数（Synchronization Functions）
-------------------------

##### wait_for_events(events)

##### enqueue_barrier(queue, wait_for=None)

提交一个围栏操作（barrier operation）到队列。确保命令队列（command_que）所有队列中的命令都结束之星。这个命令就是一个同步点（synchronization
point）

添加于版本 0.91.5
版本变更于 2011.2
接收 `wait_for` 然后返回一个事件 `Event`

##### enqueue_marker(queue, wait_for=None)

返回一个 `Event`.

版本变更于 2011.2
接收 `wait_for`.
Built-in Utilities
==================

Memory Pools
------------

The constructor pyopencl.Buffer can consume a fairly large amount of
processing time if it is invoked very frequently. For example, code
based on pyopencl.array.Array can easily run into this issue because a
fresh memory area is allocated for each intermediate result. Memory
pools are a remedy for this problem based on the observation that often
many of the block allocations are of the same sizes as previously used
ones.

Then, instead of fully returning the memory to the system and incurring
the associated reallocation overhead, the pool holds on to the memory
and uses it to satisfy future allocations of similarly-sized blocks. The
pool reacts appropriately to out-of-memory conditions as long as all
memory allocations are made through it. Allocations performed from
outside of the pool may run into spurious out-of-memory conditions due
to the pool owning much or all of the available memory.

Using pyopencl.array.Array instances with a MemoryPool is not
complicated:

    mem_pool = pyopencl.tools.MemoryPool(pyopencl.tools.ImmediateAllocator(queue))
    a_dev = cl_array.arange(queue, 2000, dtype=np.float32, allocator=mem_pool)

CL-Object-dependent Caching
---------------------------

Testing
-------

Device Characterization
-----------------------

Parallel Algorithms
===================

Element-wise expression evalution ("map")
-----------------------------------------

Evaluating involved expressions on pyopencl.array.Array instances by
using overloaded operators can be somewhat inefficient, because a new
temporary is created for each intermediate result. The functionality in
the module pyopencl.elementwise contains tools to help generate kernels
that evaluate multi-stage expressions on one or several operands in a
single pass.

Here's a usage example:

(You can find this example as
examples/demo\_elementwise.py \<../examples/demo\_elementwise.py\> in
the PyOpenCL distribution.)

Sums and counts ("reduce")
--------------------------

Here's a usage example:

    a = pyopencl.array.arange(queue, 400, dtype=numpy.float32)
    b = pyopencl.array.arange(queue, 400, dtype=numpy.float32)

    krnl = ReductionKernel(ctx, numpy.float32, neutral="0",
            reduce_expr="a+b", map_expr="x[i]*y[i]",
            arguments="__global float *x, __global float *y")

    my_dot_prod = krnl(a, b).get()

Prefix Sums ("scan")
--------------------

A prefix sum is a running sum of an array, as provided by e.g.
numpy.cumsum:

    >>> import numpy as np
    >>> a = [1,1,1,1,1,2,2,2,2,2]
    >>> np.cumsum(a)
    array([ 1,  2,  3,  4,  5,  7,  9, 11, 13, 15])

This is a very simple example of what a scan can do. It turns out that
scans are significantly more versatile. They are a basic building block
of many non-trivial parallel algorithms. Many of the operations enabled
by scans seem difficult to parallelize because of loop-carried
dependencies.

### Usage Example

This example illustrates the implementation of a simplified version of
pyopencl.algorithm.copy\_if, which copies integers from an array into
the (variable-size) output if they are greater than 300:

    knl = GenericScanKernel(
            ctx, np.int32,
            arguments="__global int *ary, __global int *out",
            input_expr="(ary[i] > 300) ? 1 : 0",
            scan_expr="a+b", neutral="0",
            output_statement="""
                if (prev_item != item) out[item-1] = ary[i];
                """)

    out = a.copy()
    knl(a, out)

    a_host = a.get()
    out_host = a_host[a_host > 300]

    assert (out_host == out.get()[:len(out_host)]).all()

The value being scanned over is a number of flags indicating whether
each array element is greater than 300. These flags are computed by
*input\_expr*. The prefix sum over this array gives a running count of
array items greater than 300. The *output\_statement* the compares
prev\_item (the previous item's scan result, i.e. index) to item (the
current item's scan result, i.e. index). If they differ, i.e. if the
predicate was satisfied at this position, then the item is stored in the
output at the computed index.

This example does not make use of the following advanced features also
available in PyOpenCL:

-   Segmented scans
-   Access to the previous item in *input\_expr* (e.g. for comparisons)
    See the
    [implementation](https://github.com/inducer/pyopencl/blob/master/pyopencl/scan.py#L1353)
    of unique for an example.

### Making Custom Scan Kernels

#### Debugging aids

### Simple / Legacy Interface

For the array [1,2,3], inclusive scan results in [1,3,6], and exclusive
scan results in [0,1,3].

Here's a usage example:

    knl = InclusiveScanKernel(context, np.int32, "a+b")

    n = 2**20-2**18+5
    host_data = np.random.randint(0, 10, n).astype(np.int32)
    dev_data = cl_array.to_device(queue, host_data)

    knl(dev_data)
    assert (dev_data.get() == np.cumsum(host_data, axis=0)).all()

Predicated copies ("partition", "unique", ...)
----------------------------------------------

Sorting (radix sort)
--------------------

Building many variable-size lists
---------------------------------

Bitonic Sort
------------

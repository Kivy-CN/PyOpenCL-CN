Multi-dimensional arrays
========================

The functionality in this module provides something of a work-alike for
numpy arrays, but with all operations executed on the CL compute device.

Data Types
----------

PyOpenCL provides some amount of integration between the numpy type
system, as represented by numpy.dtype, and the types available in
OpenCL. All the simple scalar types map straightforwardly to their CL
counterparts.

### Vector Types

### Custom data types

If you would like to use your own (struct/union/whatever) data types in
array operations where you supply operation source code, define those
types in the *preamble* passed to
pyopencl.elementwise.ElementwiseKernel,
pyopencl.reduction.ReductionKernel (or similar), and let PyOpenCL know
about them using this function:

This function helps with producing C/OpenCL declarations for structured
numpy.dtype instances:

A more complete example of how to use custom structured types can be
found in examples/demo-struct-reduce.py in the PyOpenCL distribution.

### Complex Numbers

PyOpenCL's Array type supports complex numbers out of the box, by simply
using the corresponding numpy types.

If you would like to use this support in your own kernels, here's how to
proceed: Since OpenCL 1.2 (and earlier) do not specify native complex
number support, PyOpenCL works around that deficiency. By saying:

    #include <pyopencl-complex.h>

in your kernel, you get complex types cfloat\_t and cdouble\_t, along
with functions defined on them such as cfloat\_mul(a, b) or
cdouble\_log(z). Elementwise kernels automatically include the header if
your kernel has complex input or output. See the [source
file](https://github.com/inducer/pyopencl/blob/master/pyopencl/cl/pyopencl-complex.h)
for a precise list of what's available.

If you need double precision support, please:

    #define PYOPENCL_DEFINE_CDOUBLE

before including the header, as DP support apparently cannot be reliably
autodetected.

Under the hood, the complex types are struct types as defined in the
header. Ideally, you should only access the structs through the provided
functions, never directly.

The Array Class
---------------

### Constructing Array Instances

### Manipulating Array instances

### Conditionals

### Reductions

See also custom-reductions.

Elementwise Functions on Array Instances
----------------------------------------

The pyopencl.clmath module contains exposes array versions of the C
functions available in the OpenCL standard. (See table 6.8 in the spec.)

Generating Arrays of Random Numbers
-----------------------------------

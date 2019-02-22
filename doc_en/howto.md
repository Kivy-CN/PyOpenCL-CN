How-tos
=======

How to use struct types with PyOpenCL
-------------------------------------

We import and initialize PyOpenCL as usual:

Then, suppose we would like to declare a struct consisting of an integer
and a floating point number. We first create a numpy.dtype along these
lines:

> **note**
>
> Not all numpy dtypes are supported yet. For example strings (and
> generally things that have a shape of their own) are not supported.

Since OpenCL C may have a different opinion for numpy on how the struct
should be laid out, for example because of
[alignment](https://en.wikipedia.org/wiki/Data_structure_alignment). So
as a first step, we match our dtype against CL's version:

We then tell PyOpenCL about our new type.

Next, we can create some data of that type on the host and transfer it
to the device:

We can then operate on the array with our own kernels:

as well as with PyOpenCL's built-in operations:

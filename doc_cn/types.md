OpenCL Type Mapping
===================

Scalar Types
------------

For ease of use, a the cltypes module provides convenient mapping from
OpenCL type names to their equivalent numpy types. This saves you from
referring back to the OpenCL spec to see that a cl\_long is 64 bit
unsigned integer. Use the module as follows:

Vector Types
------------

The corresponding vector types are also made available in the same
package, allowing you to easily create numpy arrays with the appropriate
memory layout.

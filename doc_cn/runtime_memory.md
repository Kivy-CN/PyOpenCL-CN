OpenCL Runtime: Memory
======================

Memory Migration
----------------

Buffer
------

Shared Virtual Memory (SVM)
---------------------------

Shared virtual memory allows the host and the compute device to share
address space, so that pointers on the host and on the device may have
the same meaning. In addition, it allows the same memory to be accessed
by both the host and the device. *Coarse-grain* SVM requires that
buffers be mapped before being accessed on the host, *fine-grain* SVM
does away with that requirement.

SVM requires OpenCL 2.0.

### Allocating SVM

### Operations on SVM

(See also mem-transfer.)

### SVM Allocation Holder

Image
-----

Transfers
---------

Mapping Memory into Host Address Space
--------------------------------------

Samplers
--------

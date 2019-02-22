Installation
============

Installing from Conda Forge
---------------------------

By far the easiest way to install PyOpenCL is to use the packages
available in [Conda Forge](https://conda-forge.org/). Conda Forge is a
repository of community-maintained packages for the
[Conda](https://conda.io/docs/) package manager.

On Linux or OS X, the following set of instructions should work:

1.  Install a version of [miniconda](https://conda.io/miniconda.html)
    that fits your system. Both Python 2 and Python 3 work. You can
    install these pieces of software in your user account and do not
    need root/administrator privileges.

    Note that if you already have Continuum Anaconda installed on your
    system, you may just use that and do *not* need to install
    Miniconda.

2.  `source /WHERE/YOU/INSTALLED/MINICONDA/bin/activate root`
3.  `conda config --add channels conda-forge`
4.  `conda install pyopencl`

The analogous steps for Windows should also work.

Note that PyOpenCL is no fun (i.e. cannot run code) without an OpenCL
device driver (a so-called "ICD", for "installable client driver") that
provides access to hardware through OpenCL. If you get an error message
like
`pyopencl.cffi_cl.LogicError: clGetPlatformIDs failed: <unknown error -1001>`,
that means you have no OpenCL drivers installed.

Note that drivers (ICDs) are separate pieces of software from PyOpenCL.
They might be provided by your hardware vendor (e.g. for Nvidia or AMD
GPUs). If you have such hardware, see below for instructions on how to
make those work with PyOpenCL from Conda Forge.

It is important to note that OpenCL is not restricted to GPUs. In fact,
no special hardware is required to use OpenCL for computation--your
existing CPU is enough. On Linux or macOS, type:

1.  `conda install pocl`

to install a CPU-based OpenCL driver. On Windows, you may install e.g.
the [CPU OpenCL driver from
Intel](https://software.intel.com/en-us/articles/opencl-drivers#latest_CPU_runtime).
On macOS, pocl can offer a marked robustness (and, sometimes,
performance) improvement over the OpenCL drivers built into the
operating system.

You are now ready to run code based on PyOpenCL, such as the [code
examples](https://github.com/inducer/pyopencl/tree/master/examples).

### Using vendor-supplied OpenCL drivers (mainly on Linux)

The instructions above help you get a basic OpenCL environment going
that will work independently of whether you have specialized hardware
(such as GPUs or FPGAs) available. If you *do* have such hardware, read
on for how to make it work.

On Linux, PyOpenCL finds which drivers are installed by looking for
files with the extension `.icd` in a directory. PyOpenCL as installed
from Conda will look for these files in
/WHERE/YOU/INSTALLED/MINICONDA/etc/OpenCL/vendors. They are just simple
text files containing either just the file names or the fully qualified
path names of the shared library providing the OpenCL driver.

> **note**
>
> If you ran the commands above in a [Conda
> environment](https://conda.io/docs/user-guide/tasks/manage-environments.html)
> (i.e. if the environment indicator on your command line prompt says
> anything other than `(root)`), then you may need to use a path like
> the following instead:
>
> /WHERE/YOU/INSTALLED/MINICONDA/envs/ENVIRONMENTNAME/etc/OpenCL/vendors
>
> Note that you should replace `ENVIRONMENTNAME` with the name of your
> environment, shown between parentheses on your command line prompt.

On Linux, if you have other OpenCL drivers installed (such as for your
GPU), those will be in /etc/OpenCL/vendors. You can make them work with
PyOpenCL from Conda Forge by placing a symbolic link to
/etc/OpenCL/vendors in the directory described above. The version of
ocl-icd installed with PyOpenCL from Conda Forge in Linux will
automatically recurse and find system-wide ICDs *if* that link is
present.

If you are looking for more information, see
[ocl-icd](https://github.com/OCL-dev/ocl-icd) and its documentation.
Ocl-icd is the "ICD loader" used by PyOpenCL when installed from Conda
Forge on Linux. It represents the code behind libOpenCL.so.

On macOS, the packaging of PyOpenCL for Conda Forge relies on the
[Khronos ICD Loader](https://github.com/KhronosGroup/OpenCL-ICD-Loader),
and it is packaged so that the OpenCL drivers built into the operating
system are automatically available, in addition to other ICDs installed
manually.

Installing from source
----------------------

Information on how to install PyOpenCL *from source* is maintained
collaboratively on the [PyOpenCL
Wiki](http://wiki.tiker.net/PyOpenCL/Installation), but that should
mostly not be necessary unless you have very specific needs or would
like to modify PyOpenCL yourself.

Tips
====

Syntax highlighting
-------------------

You can obtain Vim syntax highlighting for OpenCL C inlined in Python by
checking [this
file](https://github.com/inducer/pyopencl/blob/master/contrib/pyopencl.vim).

Note that the triple-quoted strings containing the source must start
with """//CL// ...""".

IPython integration
-------------------

PyOpenCL comes with IPython integration, which lets you seamlessly
integrate PyOpenCL kernels into your IPython notebooks. Simply load the
PyOpenCL IPython extension using:

    %load_ext pyopencl.ipython_ext

and then use the `%%cl_kernel` 'cell-magic' command. See [this
notebook](http://nbviewer.ipython.org/urls/raw.githubusercontent.com/inducer/pyopencl/master/examples/ipython-demo.ipynb)
(which ships with PyOpenCL) for a demonstration.

You can pass build options to be used for building the program
executable by using the `-o` flag on the first line of the cell (next to
the `%%cl_kernel` directive). For example:
%%cl\_kernel -o "-cl-fast-relaxed-math".

There are also line magics: cl\_load\_edit\_kernel\` which will load a
file into the next cell (adding `cl_kernel` to the first line) and
`cl_kernel_from_file` which will compile kernels from a file (as if you
copy-and-pasted the contents of the file to a cell with `cl_kernel`).
Both of these magics take options `-f` to specify the file and
optionally `-o` for build options.

Guidelines
==========

API Stability
-------------

I consider PyOpenCL's API "stable". That doesn't mean it can't change.
But if it does, your code will generally continue to run. It may however
start spewing warnings about things you need to change to stay
compatible with future versions.

Deprecation warnings will be around for a whole year, as identified by
the first number in the release name. (the "2014" in "2014.1") I.e. a
function that was deprecated in 2014.n will generally be removed in
2015.n (or perhaps later). Further, the stability promise applies for
any code that's part of a released version. It doesn't apply to
undocumented bits of the API, and it doesn't apply to unreleased code
downloaded from git.

Relation with OpenCL's C Bindings
---------------------------------

We've tried to follow these guidelines when binding the OpenCL's C
interface to Python:

-   Remove the cl\_, CL\_ and cl prefix from data types, macros and
    function names.
-   Follow 8, i.e.
    -   Make function names lowercase.
    -   If a data type or function name is composed of more than one
        word, separate the words with a single underscore.
-   get\_info functions become attributes.
-   Object creation is done by constructors, to the extent possible.
    (i.e. minimize use of "factory functions")
-   If an operation involves two or more "complex" objects (like e.g. a
    kernel enqueue involves a kernel and a queue), refuse the temptation
    to guess which one should get a method for the operation. Instead,
    simply leave that command to be a function.

Interoperability with other OpenCL software
-------------------------------------------

Just about every object in pyopencl supports the following interface
(here shown as an example for pyopencl.MemoryObject, from which
pyopencl.Buffer and pyopencl.Image inherit):

-   pyopencl.MemoryObject.from\_int\_ptr
-   pyopencl.MemoryObject.int\_ptr

This allows retrieving the C-level pointer to an OpenCL object as a
Python integer, which may then be passed to other C libraries whose
interfaces expose OpenCL objects. It also allows turning C-level OpenCL
objects obtained from other software to be turned into the corresponding
pyopencl objects.

User-visible Changes
====================

Version 2018.2
--------------

> **note**
>
> This version is currently under development. You can get snapshots
> from PyOpenCL's [git repository](https://github.com/inducer/pyopencl)

-   Use pybind11.
-   Many bug fixes.
-   Support arrays with offsets in scan kernels.

Version 2018.1
--------------

-   Introduce *eliminate\_empty\_output\_lists* argument of
    pyopencl.algorithm.ListOfListsBuilder.
-   Many bug fixes.

Version 2017.2
--------------

-   Many bug fixes.

Version 2017.1
--------------

-   Introduce pyopencl.cltypes

Version 2016.2
--------------

-   Deprecate RANLUXCL. It will be removed in the 2018.x series of
    PyOpenCL.
-   Introduce Random123 random number generators. See pyopencl.clrandom
    for more information.
-   Add support for **range** and **slice** kwargs and data-less
    reductions to pyopencl.reduction.ReductionKernel.
-   Add support for SPIR-V. (See pyopencl.Program.)
-   Add support for svm.
-   pyopencl.MemoryMap is usable as a context manager.

Version 2016.1
--------------

-   The `from_int_ptr` methods now take a *retain* parameter for more
    convenient ownership management.
-   Kernel build options (if passed as a list) are now properly quoted.
    (This is a potentially compatibility-breaking change.)
-   Many bug fixes. (GL interop, Windows, event callbacks and more)

Version 2015.2.4
----------------

-   Fix building on Windows, using mingwpy and VS 2015.

Version 2015.2.3
----------------

-   Fix one more Ubuntu 14.x build issue.

Version 2015.2.2
----------------

-   Fix compatibility with CL 1.1
-   Fix compatibility with Ubuntu 14.x.
-   Various bug fixes

Version 2015.2.1
----------------

-   Fix global\_offset kernel launch parameter

Version 2015.2
--------------

-   **[INCOMPATIBLE]** Changed PyOpenCL's complex numbers from `float2`
    and `double2` OpenCL vector types to custom `struct`. This was
    changed because it very easily introduced bugs where

    -   complex\*complex
    -   real+complex

    *look* like they may do the right thing, but silently do the wrong
    thing.
-   Rewrite of the wrapper layer to be based on CFFI
-   Pypy compatibility
-   Faster kernel invocation through Python launcher code generation
-   POCL compatibility

Version 2015.1
--------------

-   Support for new-style buffer protocol
-   Numerous fixes

Version 2014.1
--------------

-   ipython-integration
-   Bug fixes

Version 2013.2
--------------

-   Add pyopencl.array.Array.map\_to\_host.
-   Support *strides* on pyopencl.enqueue\_map\_buffer and
    pyopencl.enqueue\_map\_image.
-   pyopencl.ImageFormat was made comparable and hashable.
-   pyopencl.reduction supports slicing (contributed by Alex Nitz)
-   Added interoperability
-   Bug fixes

Version 2013.1
--------------

-   Vastly improved custom-scan.
-   Add pyopencl.tools.match\_dtype\_to\_c\_struct, for better
    integration of the CL and numpy type systems.
-   More/improved Bessel functions. See [the
    source](https://github.com/inducer/pyopencl/tree/master/src/cl).
-   Add PYOPENCL\_NO\_CACHE environment variable to aid debugging. (e.g.
    with AMD's CPU implementation, see [their programming
    guide](http://developer.amd.com/sdks/AMDAPPSDK/assets/AMD_Accelerated_Parallel_Processing_OpenCL_Programming_Guide.pdf))
-   Deprecated pyopencl.tools.register\_dtype in favor of
    pyopencl.tools.get\_or\_register\_dtype.
-   Clean up the pyopencl.array.Array constructor interface.
-   Deprecate pyopencl.array.DefaultAllocator.
-   Deprecate pyopencl.tools.CLAllocator.
-   Introduce pyopencl.tools.DeferredAllocator,
    pyopencl.tools.ImmediateAllocator.
-   Allow arrays whose beginning does not coincide with the beginning of
    their pyopencl.array.Array.data pyopencl.Buffer. See
    pyopencl.array.Array.base\_data and pyopencl.array.Array.offset.
    Note that not all functions in PyOpenCL support such arrays just
    yet. These will fail with pyopencl.array.ArrayHasOffsetError.
-   Add pyopencl.array.Array.\_\_getitem\_\_ and
    pyopencl.array.Array.\_\_setitem\_\_, supporting generic slicing.

    It is *possible* to create non-contiguous arrays using this
    functionality. Most operations (elementwise etc.) will not work on
    such arrays.

    Note also that some operations (specifically, reductions and scans)
    on sliced arrays that start past the beginning of the original array
    will fail for now. This will be fixed in a future release.

-   pyopencl.CommandQueue may be used as a context manager (in a `with`
    statement)
-   Add pyopencl.clmath.atan2, pyopencl.clmath.atan2pi.
-   Add pyopencl.array.concatenate.
-   Add pyopencl.Kernel.capture\_call.

> **note**
>
> The addition of pyopencl.array.Array.\_\_getitem\_\_ has an unintended
> consequence due to [numpy bug
> 3375](https://github.com/numpy/numpy/issues/3375). For instance, this
> expression:
>
>     numpy.float32(5) * some_pyopencl_array
>
> may take a very long time to execute. This is because numpy first
> builds an object array of (compute-device) scalars (!) before it
> decides that that's probably not such a bright idea and finally calls
> pyopencl.array.Array.\_\_rmul\_\_.
>
> Note that only left arithmetic operations of pyopencl.array.Array by
> numpy scalars are affected. Python's number types (float etc.) are
> unaffected, as are right multiplications.
>
> If a program that used to run fast suddenly runs extremely slowly, it
> is likely that this bug is to blame.
>
> Here's what you can do:
>
> -   Use Python scalars instead of numpy scalars.
> -   Switch to right multiplications if possible.
> -   Use a patched numpy. See the bug report linked above for a pull
>     request with a fix.
> -   Switch to a fixed version of numpy when available.

Version 2012.1
--------------

-   Support for complex numbers.
-   Support for Bessel functions. (experimental)
-   Numerous fixes.

Version 2011.2
--------------

-   Add pyopencl.enqueue\_migrate\_mem\_object.
-   Add pyopencl.image\_from\_array.
-   IMPORTANT BUGFIX: Kernel caching was broken for all the 2011.1.x
    releases, with severe consequences on the execution time of
    pyopencl.array.Array operations. Henrik Andresen at a [PyOpenCL
    workshop at DTU](http://gpulab.imm.dtu.dk/courses.html) first
    noticed the strange timings.
-   All comparable PyOpenCL objects are now also hashable.
-   Add pyopencl.tools.context\_dependent\_memoize to the documented
    functionality.
-   Base pyopencl.clrandom on
    [RANLUXCL](https://bitbucket.org/ivarun/ranluxcl), add
    functionality.
-   Add pyopencl.NannyEvent objects.
-   Add pyopencl.characterize.
-   Ensure compatibility with OS X Lion.
-   Add pyopencl.tools.register\_dtype to enable scan/reduction on
    struct types.
-   pyopencl.enqueue\_migrate\_mem\_object was renamed
    pyopencl.enqueue\_migrate\_mem\_object\_ext.
    pyopencl.enqueue\_migrate\_mem\_object now refers to the OpenCL 1.2
    function of this name, if available.
-   pyopencl.create\_sub\_devices was renamed
    pyopencl.create\_sub\_devices\_ext. pyopencl.create\_sub\_devices
    now refers to the OpenCL 1.2 function of this name, if available.
-   Alpha support for OpenCL 1.2.

Version 2011.1.2
----------------

-   More bug fixes.

Version 2011.1.1
----------------

-   Fixes for Python 3 compatibility. (with work by Christoph Gohlke)

Version 2011.1
--------------

-   All *is\_blocking* parameters now default to *True* to avoid
    crashy-by-default behavior. (suggested by Jan Meinke) In particular,
    this change affects pyopencl.enqueue\_read\_buffer,
    pyopencl.enqueue\_write\_buffer,
    pyopencl.enqueue\_read\_buffer\_rect,
    pyopencl.enqueue\_write\_buffer\_rect,
    pyopencl.enqueue\_read\_image, pyopencl.enqueue\_write\_image,
    pyopencl.enqueue\_map\_buffer, pyopencl.enqueue\_map\_image.
-   Add pyopencl.reduction.
-   Add reductions.
-   Add pyopencl.scan.
-   Add pyopencl.MemoryObject.get\_host\_array.
-   Deprecate context arguments of pyopencl.array.to\_device,
    pyopencl.array.zeros, pyopencl.array.arange.
-   Make construction of pyopencl.array.Array more flexible (*cqa*
    argument.)
-   Add memory-pools.
-   Add vector types, see pyopencl.array.vec.
-   Add pyopencl.array.Array.strides, pyopencl.array.Array.flags. Allow
    the creation of arrays in C and Fortran order.
-   Add pyopencl.enqueue\_copy. Deprecate all other transfer functions.
-   Add support for numerous extensions, among them device fission.
-   Add a compiler cache.
-   Add the 'g\_times\_l' keyword arg to kernel execution.

Version 0.92
------------

-   Add support for OpenCL 1.1.
-   Add support for the
    [cl\_khr\_gl\_sharing](ghttp://www.khronos.org/registry/cl/extensions/khr/cl_khr_gl_sharing.txt)
    extension, leading to working GL interoperability.
-   Add pyopencl.Kernel.set\_args.
-   The call signature of pyopencl.Kernel.\_\_call\_\_ changed to
    emphasize the importance of *local\_size*.
-   Add pyopencl.Kernel.set\_scalar\_arg\_dtypes.
-   Add support for the
    [cl\_nv\_device\_attribute\_query](http://www.khronos.org/registry/cl/extensions/khr/cl_nv_device_attribute_query.txt)
    extension.
-   Add pyopencl.array.Array and related functionality.
-   Make build not depend on Boost C++.

Version 0.91.5
--------------

-   Add pyopencl.ImageFormat.channel\_count,
    pyopencl.ImageFormat.dtype\_size, pyopencl.ImageFormat.itemsize.
-   Add missing pyopencl.enqueue\_copy\_buffer.
-   Add pyopencl.create\_some\_context.
-   Add pyopencl.enqueue\_barrier, which was previously missing.

Version 0.91.4
--------------

A bugfix release. No user-visible changes.

Version 0.91.3
--------------

-   All parameters named *host\_buffer* were renamed *hostbuf* for
    consistency with the pyopencl.Buffer constructor introduced in 0.91.
    Compatibility code is in place.
-   The pyopencl.Image constructor does not need a *shape* parameter if
    the given *hostbuf* has *hostbuf.shape*.
-   The pyopencl.Context constructor can now be called without
    parameters.

Version 0.91.2
--------------

-   pyopencl.Program.build now captures build logs and adds them to the
    exception text.
-   Deprecate pyopencl.create\_context\_from\_type in favor of second
    form of pyopencl.Context constructor
-   Introduce pyopencl.LocalMemory.
-   Document kernel invocation and pyopencl.Kernel.set\_arg.

Version 0.91.1
--------------

-   Fixed a number of bugs, notably involving pyopencl.Sampler.
-   pyopencl.Device, pyopencl.Platform, pyopencl.Context now have nicer
    string representations.
-   Add Image.shape. (suggested by David Garcia)

Version 0.91
------------

-   Add gl-interop.
-   Add a test suite.
-   Fix numerous get\_info bugs. (reports by David Garcia and the test
    suite)
-   Add pyopencl.ImageFormat.\_\_repr\_\_.
-   Add pyopencl.addressing\_mode.to\_string and colleagues.
-   The pitch arguments to pyopencl.create\_image\_2d,
    pyopencl.create\_image\_3d, pyopencl.enqueue\_read\_image, and
    pyopencl.enqueue\_write\_image are now defaulted to zero. The
    argument order of enqueue\_{read,write}\_image has changed for this
    reason.
-   Deprecate pyopencl.create\_image\_2d, pyopencl.create\_image\_3d in
    favor of the pyopencl.Image constructor.
-   Deprecate pyopencl.create\_program\_with\_source,
    pyopencl.create\_program\_with\_binary in favor of the
    pyopencl.Program constructor.
-   Deprecate pyopencl.create\_buffer, pyopencl.create\_host\_buffer in
    favor of the pyopencl.Buffer constructor.
-   pyopencl.MemoryObject.get\_image\_info now actually exists.
-   Add pyopencl.MemoryObject.image.info.
-   Fix API tracing.
-   Add constructor arguments to pyopencl.ImageFormat. (suggested by
    David Garcia)

Version 0.90.4
--------------

-   Add build fixes for Windows and OS X.

Version 0.90.3
--------------

-   Fix a GNU-ism in the C++ code of the wrapper.

Version 0.90.2
--------------

-   Fix pyopencl.Platform.get\_info.
-   Fix passing properties to pyopencl.CommandQueue. Also fix related
    documentation.

Version 0.90.1
--------------

-   Fix building on the Mac.

Version 0.90
------------

-   Initial release.

License
=======

Frequently Asked Questions
==========================

The FAQ is maintained collaboratively on the [Wiki FAQ
page](http://wiki.tiker.net/PyOpenCL/FrequentlyAskedQuestions).

Citing PyOpenCL
===============

We are not asking you to gratuitously cite PyOpenCL in work that is
otherwise unrelated to software. That said, if you do discuss some of
the development aspects of your code and would like to highlight a few
of the ideas behind PyOpenCL, feel free to cite [this
article](http://dx.doi.org/10.1016/j.parco.2011.09.001):

> Andreas Klöckner, Nicolas Pinto, Yunsup Lee, Bryan Catanzaro, Paul
> Ivanov, Ahmed Fasih, PyCUDA and PyOpenCL: A scripting-based approach
> to GPU run-time code generation, Parallel Computing, Volume 38, Issue
> 3, March 2012, Pages 157-174.

Here's a Bibtex entry for your convenience:

    @article{kloeckner_pycuda_2012,
       author = {{Kl{\"o}ckner}, Andreas
            and {Pinto}, Nicolas
            and {Lee}, Yunsup
            and {Catanzaro}, B.
            and {Ivanov}, Paul
            and {Fasih}, Ahmed },
       title = "{PyCUDA and PyOpenCL: A Scripting-Based Approach to GPU Run-Time Code Generation}",
       journal = "Parallel Computing",
       volume = "38",
       number = "3",
       pages = "157--174",
       year = "2012",
       issn = "0167-8191",
       doi = "10.1016/j.parco.2011.09.001",
    }

Acknowledgments
===============

Contributors
------------

Too many to list. Please see the [commit
log](https://github.com/inducer/pyopencl/commits/master) for detailed
acknowledgments.

Funding
-------

Andreas Klöckner's work on pyopencl was supported in part by

-   US Navy ONR grant number N00014-14-1-0117
-   the US National Science Foundation under grant numbers DMS-1418961
    and CCF-1524433.

AK also gratefully acknowledges a hardware gift from Nvidia Corporation.
The views and opinions expressed herein do not necessarily reflect those
of the funding agencies.

OpenCL Runtime: Constants
=========================

#### 警告:

这部分 PyOpenCL 文档不完整,因为是在不支持 OpenGL 的 PyOpenCL 构建版本基础上生成的.penCL build that did not support OpenGL.

#### class addressing_mode
CLAMP
CLAMP_TO_EDGE
MIRRORED_REPEAT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NONE
REPEAT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class channel_order
A
ABGR

##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

BGRA
INTENSITY
LUMINANCE
R
RA
RG
RGB
RGBA
RGBx
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

RGx
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

Rx
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

sBGRA
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

sRGB
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

sRGBA
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

sRGBx
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class channel_type
FLOAT
HALF_FLOAT
SIGNED_INT16
SIGNED_INT32
SIGNED_INT8
SNORM_INT16
SNORM_INT8
UNORM_INT16
UNORM_INT8
UNORM_INT_101010
UNORM_SHORT_555
UNORM_SHORT_565
UNSIGNED_INT16
UNSIGNED_INT32
UNSIGNED_INT8
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class command_execution_status
COMPLETE
QUEUED
RUNNING
SUBMITTED
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class command_queue_info
CONTEXT
DEVICE
PROPERTIES
REFERENCE_COUNT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class command_queue_properties
ON_DEVICE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

ON_DEVICE_DEFAULT
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

OUT_OF_ORDER_EXEC_MODE_ENABLE
PROFILING_ENABLE
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class command_type
ACQUIRE_GL_OBJECTS
BARRIER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

COPY_BUFFER
COPY_BUFFER_RECT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

COPY_BUFFER_TO_IMAGE
COPY_IMAGE
COPY_IMAGE_TO_BUFFER
FILL_BUFFER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

FILL_IMAGE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

MAP_BUFFER
MAP_IMAGE
MARKER
MIGRATE_MEM_OBJECTS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NATIVE_KERNEL
NDRANGE_KERNEL
READ_BUFFER
READ_BUFFER_RECT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

READ_IMAGE
RELEASE_GL_OBJECTS
SVM_FREE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_MAP
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_MEMCPY
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_MEMFILL
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_UNMAP
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

TASK
UNMAP_MEM_OBJECT
USER
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

WRITE_BUFFER
WRITE_BUFFER_RECT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

WRITE_IMAGE
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class context_info
DEVICES
INTEROP_USER_SYNC
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NUM_DEVICES
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

PROPERTIES
REFERENCE_COUNT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class context_properties
OFFLINE_DEVICES_AMD
##### 支持于 cl_amd_offline_devices 扩展(extension).

##### 添加自版本 2011.1.

PLATFORM
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_affinity_domain
L1_CACHE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

L2_CACHE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

L3_CACHE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

L4_CACHE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NEXT_PARTITIONABLE
NUMA
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_exec_capabilities
KERNEL
NATIVE_KERNEL
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_fp_config
CORRECTLY_ROUNDED_DIVIDE_SQRT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

DENORM
FMA
INF_NAN
ROUND_TO_INF
ROUND_TO_NEAREST
ROUND_TO_ZERO
SOFT_FLOAT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_info
ADDRESS_BITS
ATTRIBUTE_ASYNC_ENGINE_COUNT_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

AVAILABLE
BOARD_NAME_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

BUILT_IN_KERNELS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

COMPILER_AVAILABLE
COMPUTE_CAPABILITY_MAJOR_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

COMPUTE_CAPABILITY_MINOR_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

DOUBLE_FP_CONFIG
##### 支持于 cl_khr_fp64 扩展(extension).

##### 添加自版本 2011.1.

DRIVER_VERSION
ENDIAN_LITTLE
ERROR_CORRECTION_SUPPORT
EXECUTION_CAPABILITIES
EXTENSIONS
EXT_MEM_PADDING_IN_BYTES_QCOM
##### 支持于 cl_qcom_ext_host_ptr 扩展(extension).

##### 添加自版本 2016.2.

GLOBAL_FREE_MEMORY_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

GLOBAL_MEM_CACHELINE_SIZE
GLOBAL_MEM_CACHE_SIZE
GLOBAL_MEM_CACHE_TYPE
GLOBAL_MEM_CHANNELS_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

GLOBAL_MEM_CHANNEL_BANKS_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

GLOBAL_MEM_CHANNEL_BANK_WIDTH_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

GLOBAL_MEM_SIZE
GLOBAL_VARIABLE_PREFERRED_TOTAL_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

GPU_OVERLAP_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

HALF_FP_CONFIG
##### 支持于 cl_khr_fp16 扩展(extension).

##### 添加自版本 2011.1.

HOST_UNIFIED_MEMORY
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

IL_VERSION
##### 支持于 OpenCL 2.1.

##### 添加自版本 2016.2.

IMAGE2D_MAX_HEIGHT
IMAGE2D_MAX_WIDTH
IMAGE3D_MAX_DEPTH
IMAGE3D_MAX_HEIGHT
IMAGE3D_MAX_WIDTH
IMAGE_MAX_ARRAY_SIZE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE_MAX_BUFFER_SIZE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE_SUPPORT
INTEGRATED_MEMORY_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

KERNEL_EXEC_TIMEOUT_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

LINKER_AVAILABLE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LOCAL_MEM_BANKS_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

LOCAL_MEM_SIZE
LOCAL_MEM_SIZE_PER_COMPUTE_UNIT_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

LOCAL_MEM_TYPE
MAX_ATOMIC_COUNTERS_EXT
##### 支持于 cl_ext_atomic_counters_64 扩展(extension).

##### 添加自版本 2013.2.

MAX_CLOCK_FREQUENCY
MAX_COMPUTE_UNITS
MAX_CONSTANT_ARGS
MAX_CONSTANT_BUFFER_SIZE
MAX_GLOBAL_VARIABLE_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MAX_MEM_ALLOC_SIZE
MAX_NUM_SUB_GROUPS
##### 支持于 OpenCL 2.1.

##### 添加自版本 2016.2.

MAX_ON_DEVICE_EVENTS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MAX_ON_DEVICE_QUEUES
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MAX_PARAMETER_SIZE
MAX_PIPE_ARGS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MAX_READ_IMAGE_ARGS
MAX_READ_WRITE_IMAGE_ARGS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MAX_SAMPLERS
MAX_WORK_GROUP_SIZE
MAX_WORK_ITEM_DIMENSIONS
MAX_WORK_ITEM_SIZES
MAX_WRITE_IMAGE_ARGS
MEM_BASE_ADDR_ALIGN
MIN_DATA_TYPE_ALIGN_SIZE
NAME
NATIVE_VECTOR_WIDTH_CHAR
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_DOUBLE
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_FLOAT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_HALF
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_INT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_LONG
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

NATIVE_VECTOR_WIDTH_SHORT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

OPENCL_C_VERSION
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

PAGE_SIZE_QCOM
##### 支持于 cl_qcom_ext_host_ptr 扩展(extension).

##### 添加自版本 2016.2.

PARENT_DEVICE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PARTITION_AFFINITY_DOMAIN
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PARTITION_MAX_SUB_DEVICES
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PARTITION_PROPERTIES
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PARTITION_TYPE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PCI_BUS_ID_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

PCI_SLOT_ID_NV
PIPE_MAX_ACTIVE_RESERVATIONS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

PIPE_MAX_PACKET_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

PLATFORM
PREFERRED_GLOBAL_ATOMIC_ALIGNMENT
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

PREFERRED_INTEROP_USER_SYNC
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PREFERRED_LOCAL_ATOMIC_ALIGNMENT
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

PREFERRED_PLATFORM_ATOMIC_ALIGNMENT
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

PREFERRED_VECTOR_WIDTH_CHAR
PREFERRED_VECTOR_WIDTH_DOUBLE
PREFERRED_VECTOR_WIDTH_FLOAT
PREFERRED_VECTOR_WIDTH_HALF
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

PREFERRED_VECTOR_WIDTH_INT
PREFERRED_VECTOR_WIDTH_LONG
PREFERRED_VECTOR_WIDTH_SHORT
PRINTF_BUFFER_SIZE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PROFILE
PROFILING_TIMER_OFFSET_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

PROFILING_TIMER_RESOLUTION
QUEUE_ON_DEVICE_MAX_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

QUEUE_ON_DEVICE_PREFERRED_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

QUEUE_ON_DEVICE_PROPERTIES
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

QUEUE_ON_HOST_PROPERTIES
QUEUE_PROPERTIES
REFERENCE_COUNT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

REGISTERS_PER_BLOCK_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

SIMD_INSTRUCTION_WIDTH_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

SIMD_PER_COMPUTE_UNIT_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

SIMD_WIDTH_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

SINGLE_FP_CONFIG
SPIR_VERSIONS
##### 支持于 cl_khr_spir 扩展(extension).

##### 添加自版本 2016.2.

SUB_GROUP_INDEPENDENT_FORWARD_PROGRESS
##### 支持于 OpenCL 2.1.

##### 添加自版本 2016.2.

SVM_CAPABILITIES
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

TOPOLOGY_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

TYPE
VENDOR
VENDOR_ID
VERSION
WARP_SIZE_NV
##### 支持于 cl_nv_device_attribute_query 扩展(extension).

##### 添加自版本 0.92.

WAVEFRONT_WIDTH_AMD
##### 支持于 cl_amd_device_attribute_query 扩展(extension).

##### 添加自版本 2013.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_local_mem_type
GLOBAL
LOCAL
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_mem_cache_type
NONE
READ_ONLY_CACHE
READ_WRITE_CACHE
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_partition_property
BY_AFFINITY_DOMAIN
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

BY_COUNTS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

BY_COUNTS_LIST_END
EQUALLY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_svm_capabilities
ATOMICS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

COARSE_GRAIN_BUFFER
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

FINE_GRAIN_BUFFER
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

FINE_GRAIN_SYSTEM
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class device_type
ACCELERATOR
ALL
CPU
CUSTOM
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

DEFAULT
GPU
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class event_info
COMMAND_EXECUTION_STATUS
COMMAND_QUEUE
COMMAND_TYPE
CONTEXT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

REFERENCE_COUNT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class filter_mode
LINEAR
NEAREST
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class gl_context_info

仅在编译有 GL 支持的 PyOpenCL 中可用, 参考 have_gl().

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class image_info
ARRAY_SIZE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

BUFFER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

DEPTH
ELEMENT_SIZE
FORMAT
HEIGHT
NUM_MIP_LEVELS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NUM_SAMPLES
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

ROW_PITCH
SLICE_PITCH
WIDTH
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_arg_access_qualifier
NONE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

READ_ONLY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

READ_WRITE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

WRITE_ONLY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_arg_address_qualifier
CONSTANT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

GLOBAL
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LOCAL
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

PRIVATE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_arg_info
ACCESS_QUALIFIER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

ADDRESS_QUALIFIER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NAME
TYPE_NAME
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

TYPE_QUALIFIER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_arg_type_qualifier
CONST
##### 支持于 OpenCL 1.2.

##### 添加自版本 2015.2.

NONE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2015.2.

PIPE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

RESTRICT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2015.2.

VOLATILE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_info
ATTRIBUTES
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

CONTEXT
FUNCTION_NAME
NUM_ARGS
PROGRAM
REFERENCE_COUNT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class kernel_work_group_info
COMPILE_WORK_GROUP_SIZE
GLOBAL_WORK_SIZE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LOCAL_MEM_SIZE
PREFERRED_WORK_GROUP_SIZE_MULTIPLE
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

PRIVATE_MEM_SIZE
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

WORK_GROUP_SIZE
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class map_flags
READ
WRITE
WRITE_INVALIDATE_REGION
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class mem_flags
ALLOC_HOST_PTR
COPY_HOST_PTR
HOST_NO_ACCESS
HOST_READ_ONLY
HOST_WRITE_ONLY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

KERNEL_READ_AND_WRITE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

READ_ONLY
READ_WRITE
USE_HOST_PTR
USE_PERSISTENT_MEM_AMD
##### 支持于 cl_amd_device_memory_flags 扩展(extension).

##### 添加自版本 2011.1.

WRITE_ONLY
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class mem_info
ASSOCIATED_MEMOBJECT
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

CONTEXT
FLAGS
HOST_PTR
MAP_COUNT
OFFSET
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

REFERENCE_COUNT
SIZE
TYPE
USES_SVM_POINTER
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class mem_migration_flags
CONTENT_UNDEFINED
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

HOST
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class mem_object_type
BUFFER
IMAGE1D
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE1D_ARRAY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE1D_BUFFER
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE2D
IMAGE2D_ARRAY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

IMAGE3D
PIPE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)¶
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class platform_info
EXTENSIONS
NAME
PROFILE
VENDOR
VERSION
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class profiling_info
COMPLETE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

END
QUEUED
START
SUBMIT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class program_binary_type
COMPILED_OBJECT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

EXECUTABLE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LIBRARY
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NONE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class program_build_info
BINARY_TYPE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

GLOBAL_VARIABLE_TOTAL_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

LOG
OPTIONS
STATUS
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class program_info
BINARIES
BINARY_SIZES
CONTEXT
DEVICES
KERNEL_NAMES
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

NUM_DEVICES
NUM_KERNELS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

REFERENCE_COUNT
SOURCE
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class program_kind
BINARY
SOURCE
UNKNOWN
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class queue_properties
PROPERTIES
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class sampler_info
ADDRESSING_MODE
CONTEXT
FILTER_MODE
LOD_MAX
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

LOD_MIN
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

MIP_FILTER_MODE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

NORMALIZED_COORDS
REFERENCE_COUNT
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class status_code
BUILD_PROGRAM_FAILURE
COMPILER_NOT_AVAILABLE
COMPILE_PROGRAM_FAILURE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

DEVICE_NOT_AVAILABLE
DEVICE_NOT_FOUND
DEVICE_PARTITION_FAILED
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

EXEC_STATUS_ERROR_FOR_EVENTS_IN_WAIT_LIST
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

IMAGE_FORMAT_MISMATCH
IMAGE_FORMAT_NOT_SUPPORTED
INVALID_ARG_INDEX
INVALID_ARG_SIZE
INVALID_ARG_VALUE
INVALID_BINARY
INVALID_BUFFER_SIZE
INVALID_BUILD_OPTIONS
INVALID_COMMAND_QUEUE
INVALID_COMPILER_OPTIONS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

INVALID_CONTEXT
INVALID_DEVICE
INVALID_DEVICE_PARTITION_COUNT
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

INVALID_DEVICE_QUEUE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

INVALID_DEVICE_TYPE
INVALID_EVENT
INVALID_EVENT_WAIT_LIST
INVALID_GLOBAL_OFFSET
INVALID_GLOBAL_WORK_SIZE
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

INVALID_GL_OBJECT
INVALID_HOST_PTR
INVALID_IMAGE_DESCRIPTOR
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

INVALID_IMAGE_FORMAT_DESCRIPTOR
INVALID_IMAGE_SIZE
INVALID_KERNEL
INVALID_KERNEL_ARGS
INVALID_KERNEL_DEFINITION
INVALID_KERNEL_NAME
INVALID_LINKER_OPTIONS
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

INVALID_MEM_OBJECT
INVALID_MIP_LEVEL
INVALID_OPERATION
INVALID_PIPE_SIZE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

INVALID_PLATFORM
INVALID_PROGRAM
INVALID_PROGRAM_EXECUTABLE
INVALID_QUEUE_PROPERTIES
INVALID_SAMPLER
INVALID_VALUE
INVALID_WORK_DIMENSION
INVALID_WORK_GROUP_SIZE
INVALID_WORK_ITEM_SIZE
KERNEL_ARG_INFO_NOT_AVAILABLE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LINKER_NOT_AVAILABLE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

LINK_PROGRAM_FAILURE
##### 支持于 OpenCL 1.2.

##### 添加自版本 2011.2.

MAP_FAILURE
MEM_COPY_OVERLAP
MEM_OBJECT_ALLOCATION_FAILURE
MISALIGNED_SUB_BUFFER_OFFSET
##### 支持于 OpenCL 1.1.

##### 添加自版本 0.92.

OUT_OF_HOST_MEMORY
OUT_OF_RESOURCES
PLATFORM_NOT_FOUND_KHR
##### 支持于 cl_khr_icd 扩展(extension).

##### 添加自版本 2011.1.

PROFILING_INFO_NOT_AVAILABLE
SUCCESS
to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

#### class svm_mem_flags
READ_ONLY
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

READ_WRITE
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_ATOMICS
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

SVM_FINE_GRAIN_BUFFER
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

WRITE_ONLY
##### 支持于 OpenCL 2.0.

##### 添加自版本 2015.2.

to_string(value)
将值作为字符串返回.  .

##### 添加自版本 0.91.

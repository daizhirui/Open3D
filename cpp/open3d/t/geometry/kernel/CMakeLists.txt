open3d_ispc_add_library(tgeometry_kernel OBJECT)
set_target_properties(tgeometry_kernel PROPERTIES CXX_VISIBILITY_PRESET "hidden")


target_sources(tgeometry_kernel PRIVATE
    Image.cpp
    ImageCPU.cpp
    PCAPartition.cpp
    PointCloud.cpp
    PointCloudCPU.cpp
    Metrics.cpp
    MinimumOBB.cpp
    TriangleMesh.cpp
    TriangleMeshCPU.cpp
    Transform.cpp
    TransformCPU.cpp
    UVUnwrapping.cpp
    VoxelBlockGrid.cpp
    VoxelBlockGridCPU.cpp
)

if (BUILD_CUDA_MODULE)
    target_sources(tgeometry_kernel PRIVATE
        ImageCUDA.cu
        NPPImage.cpp
        PointCloudCUDA.cu
        TriangleMeshCUDA.cu
        TransformCUDA.cu
        VoxelBlockGridCUDA.cu
    )
endif()

if (WITH_IPP)
    target_sources(tgeometry_kernel PRIVATE
        IPPImage.cpp
    )
endif()

open3d_show_and_abort_on_warning(tgeometry_kernel)
open3d_set_global_properties(tgeometry_kernel)
open3d_set_open3d_lib_properties(tgeometry_kernel HIDDEN)
open3d_link_3rdparty_libraries(tgeometry_kernel)

if(BUILD_CUDA_MODULE)
  target_include_directories(tgeometry_kernel SYSTEM
                             PRIVATE ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES})
endif()

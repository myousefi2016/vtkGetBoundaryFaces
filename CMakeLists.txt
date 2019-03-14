cmake_minimum_required(VERSION 3.9)
 
PROJECT(vtkGetBoundaryFaces VERSION 0.0 DESCRIPTION "Get vtk boundary faces")
 
find_package(VTK REQUIRED)
include(${VTK_USE_FILE})
 
add_library(vtkGetBoundaryFaces SHARED src/vtkGetBoundaryFaces.cxx)
 
target_link_libraries(vtkGetBoundaryFaces ${VTK_LIBRARIES})

set_target_properties(vtkGetBoundaryFaces PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
    PUBLIC_HEADER include/vtkGetBoundaryFaces.h)

target_include_directories(vtkGetBoundaryFaces PRIVATE include)
target_include_directories(vtkGetBoundaryFaces PRIVATE src)

include(GNUInstallDirs)

install(TARGETS vtkGetBoundaryFaces
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

configure_file(vtkGetBoundaryFaces.pc.in vtkGetBoundaryFaces.pc @ONLY)

install(FILES ${CMAKE_BINARY_DIR}/vtkGetBoundaryFaces.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -ftemplate-depth=1024 -fpermissive")

# CMakeList.txt : CMake project for Opencl-ex1, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)
project(Opencl-ex1)

set (CMAKE_CXX_STANDARD 11)
add_compile_options(-DH5_BUILT_AS_DYNAMIC_LIB)

#Adding Opencl libs and include files to the proj
find_package(OpenCL)
include_directories(${OpenCL_INCLUDE_DIRS})
link_directories(${OpenCL_LIBRARY})

#searching for the package 
set (GLEW_INCLUDE_DIRS "C:/glew-2.1.0/include")
set (GLEW_LIBRARIES "C:/glew-2.1.0/lib/Release/x64/glew32.lib")
set (GLUT_INCLUDE_DIRS "C:/freeglut/include")
set (GLUT_LIBRARIES "C:/freeglut/lib/x64/freeglut.lib")

find_package(OpenGL REQUIRED)

#adding hdf5 libs
#find_package(HDF5  static)
find_package(HDF5 REQUIRED COMPONENTS C )
#FIND_PACKAGE(HDF5 COMPONENTS C HL NO_MODULE REQUIRED static)
if (HDF5_FOUND)
    message("${HDF5_VERSION}")
    #set(DH5_USE_110_API "ON")
    message("HDF5 library found!")
    #include_directories(${HDF5_INCLUDE_DIRS})
    #link_directories(${HDF5_LIBRARIES})
    message ("${HDF5_INCLUDE_DIRS}")
    message ("${HDF5_LIBRARIES}")

endif()


#adding the Boost libs to the proj
set(BOOST_INC "C:/boost_1_76_0_b1_rc2")
set(BOOST_LIB "C:/boost_1_76_0_b1_rc2/lib64-msvc-14.2/")


include_directories(${BOOST_INC})
link_directories(${BOOST_LIB})

#compile files in COre and OpenCL external libs
file(GLOB CORE_SRC "Core/*.cpp" "Core/*.c")
file(GLOB OPENCL_SRC "OpenCL/*.cpp" "OpenCL/*.c")
file(GLOB HDF_SRC "HDF5/*.cpp")
file(GLOB CT_SRC "CT/*.cpp")
file(GLOB Math_SRC "Math/*.cpp")

file(GLOB BOOST_SRC "${BOOST_LIB}/*.lib")

if(MSVC)
    message ("MSVS")
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
    SET (H5_BUILT_AS_DYNAMIC_LIB 1)
endif()
#message("${HDF_SRC}")
# Add source to this project's executable.
add_executable (Opencl-ex1 "src/OpenCLExercise6_VolumeRendering.cpp" ${CORE_SRC}
                                                                ${OPENCL_SRC}
                                                                ${HDF_SRC}
                                                                ${CT_SRC}
                                                                ${Math_SRC}
                                                                )

target_include_directories (Opencl-ex1 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} 
                                              ${HDF5_INCLUDE_DIRS}    
                                              ${GLEW_INCLUDE_DIRS} ${GLUT_INCLUDE_DIRS}  )
target_link_libraries (Opencl-ex1 ${OpenCL_LIBRARY} ${HDF5_LIBRARIES} imagehlp ${GLEW_LIBRARIES} ${GLUT_LIBRARIES})

# TODO: Add tests and install targets if needed.

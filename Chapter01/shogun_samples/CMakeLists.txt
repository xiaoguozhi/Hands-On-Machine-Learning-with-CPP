cmake_minimum_required(VERSION 3.10)
project(shogun-samples)

set(SHOGUN_PATH "" CACHE PATH "path to shogun install dir")

if(NOT DEFINED SHOGUN_PATH)
  message(FATAL_ERROR "Missing Shogun install path, please specify SHOGUN_PATH")
else()
  message("Shogun path is ${SHOGUN_PATH}")
endif()

set(CMAKE_VERBOSE_MAKEFILE ON)

find_package(HDF5 REQUIRED)

set(CMAKE_CXX_FLAGS "-std=c++14 -msse3 -fopenmp -Wall -Wextra -Wno-unused-parameter")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG")
set(CMAKE_CXX_FLAGS_DEBUG "-g -O0")

include_directories(${SHOGUN_PATH}/include)
link_directories(${SHOGUN_PATH}/lib)

add_executable(linreg_shogun "linreg_shogun.cc")
target_link_libraries(linreg_shogun shogun)
target_link_libraries(linreg_shogun ${HDF5_LIBRARIES} json-c ${PROTOBUF_LIBRARIES} cblas lapack)


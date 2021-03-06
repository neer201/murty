cmake_minimum_required(VERSION 3.4...3.18)
project(murty)

find_package (Eigen3 3.3 REQUIRED NO_MODULE)
SET( EIGEN3_INCLUDE_DIR "/usr/include/eigen3" )

IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    SET(MACOSX TRUE)
    SET( EIGEN3_INCLUDE_DIR "/usr/local/include/eigen3" )
ENDIF()

IF( NOT EIGEN3_INCLUDE_DIR )
    MESSAGE( FATAL_ERROR "Please point the environment variable EIGEN3_INCLUDE_DIR to the include directory of your Eigen3 installation.")
ENDIF()
INCLUDE_DIRECTORIES ( "${EIGEN3_INCLUDE_DIR}" )

add_subdirectory(pybind11)
pybind11_add_module(murty src/murty.cpp)

# EXAMPLE_VERSION_INFO is defined by setup.py and passed into the C++ code as a
# define (VERSION_INFO) here.
target_compile_definitions(murty PRIVATE VERSION_INFO=${EXAMPLE_VERSION_INFO})
target_compile_features(murty PRIVATE cxx_std_14)

cmake_minimum_required(VERSION 2.8)

project(paddle_lite_ocr)
set(TARGET paddle_lite_ocr)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# Set ARMLINUX_ARCH_ABI to armv8 or armv7 or armv7hf
set(ARMLINUX_ARCH_ABI armv8)

# 1. path to Paddle-Lite lib
set(LITE_DIR "${CMAKE_SOURCE_DIR}/cxx")

# 2. link Paddle-Lite directory
link_directories(${LITE_DIR}/lib)
include_directories(${LITE_DIR}/include)

FIND_PACKAGE( OpenMP REQUIRED)
if(OPENMP_FOUND)
  message("OPENMP FOUND")
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

# opencv
set(OpenCV_DIR ${LITE_DIR}/opencv-linux-aarch64/share/OpenCV)
find_package(OpenCV REQUIRED)

set(CMAKE_CXX_STANDARD 14)

# 3.add executable output
add_executable(${TARGET} ocr_db_crnn.cc cls_process.cc db_post_process.cc crnn_process.cc clipper.cpp)
target_link_libraries(${TARGET} -lpaddle_light_api_shared ${OpenCV_LIBS})
target_link_libraries(${TARGET} -ldl)

set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/install/paddle_lite_ocr)
install(TARGETS paddle_lite_ocr DESTINATION ./)
#install(DIRECTORY model DESTINATION ./)


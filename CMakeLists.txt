cmake_minimum_required(VERSION 3.4...3.19)
project(_orb_slam3 LANGUAGES CXX)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -O3 -march=native")

add_subdirectory(pybind11)

pybind11_add_module(
  ${PROJECT_NAME}
  ${CMAKE_CURRENT_LIST_DIR}/orb_slam3/system.cc
)

find_package(Python 3.8 COMPONENTS Interpreter Development REQUIRED)

add_subdirectory(vendor/ORB_SLAM3)

include_directories(
  ${PROJECT_SOURCE_DIR}/vendor/ORB_SLAM3
  ${PROJECT_SOURCE_DIR}/vendor/ORB_SLAM3/include
  ${PROJECT_SOURCE_DIR}/vendor/ORB_SLAM3/include/CameraModels
  ${PROJECT_SOURCE_DIR}/vendor/ORB_SLAM3/Thirdparty/Sophus
  ${OpenCV_INCLUDE_DIRS}
  ${Pangolin_INCLUDE_DIRS}
)

target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE ORB_SLAM3
)

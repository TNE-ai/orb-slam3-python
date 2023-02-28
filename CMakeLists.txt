cmake_minimum_required(VERSION 3.4...3.19)
project(_orb_slam3 LANGUAGES CXX)

add_subdirectory(pybind11)

pybind11_add_module(
  ${PROJECT_NAME}
  ${CMAKE_CURRENT_LIST_DIR}/orb_slam3/system.cc
)

find_package(Python 3.8 COMPONENTS Interpreter Development REQUIRED)

add_subdirectory(ORB_SLAM3_)

include_directories(
  ${PROJECT_SOURCE_DIR}/ORB_SLAM3_
  ${PROJECT_SOURCE_DIR}/ORB_SLAM3_/include
  ${PROJECT_SOURCE_DIR}/ORB_SLAM3_/include/CameraModels
  ${PROJECT_SOURCE_DIR}/ORB_SLAM3_/Thirdparty/Sophus
  ${OpenCV_INCLUDE_DIRS}
  ${Pangolin_INCLUDE_DIRS}
)

target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE ORB_SLAM3
)

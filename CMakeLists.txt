cmake_minimum_required(VERSION 2.8.12)
project(hellovdb)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

# find_package for OpenVDB doesn't find its dependencies,
# but most of them come from or are shared with OpenEXR, which
# is handled with a find_package from extra-cmake-modules
find_package(OpenVDB REQUIRED)
include_directories(${OpenVDB_INCLUDE_DIR} SYSTEM)
find_package(ECM REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${ECM_FIND_MODULE_DIR})
find_package(OpenEXR REQUIRED)
include_directories(${OpenEXR_INCLUDE_DIRS} SYSTEM)
find_package(TBB REQUIRED)
include_directories(${TBB_INCLUDE_DIRS} SYSTEM)
find_package(Boost REQUIRED)
include_directories(${Boost_INCLUDE_DIRS} SYSTEM)

include_directories(.)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native -ffast-math")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror=return-type")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror=reorder")

if("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-missing-braces")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "" OR CMAKE_BUILD_TYPE STREQUAL "Debug")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Og")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_FORTIFY_SOURCE=2")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_GLIBCXX_ASSERTIONS")
#  _GLIBCXX_DEBUG conflicts with openvdb and causes errors at runtime
#  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_GLIBCXX_DEBUG")
endif()

add_executable(hellovdb hello.cxx)
target_link_libraries(hellovdb
  ${OpenVDB_LIBRARIES}
  ${OpenEXR_LIBRARIES}
  ${TBB_LIBRARIES}
  ${Boost_LIBRARIES}
)

add_executable(cwg create_write_grid.cxx)
target_link_libraries(cwg
  ${OpenVDB_LIBRARIES}
  ${OpenEXR_LIBRARIES}
  ${TBB_LIBRARIES}
  ${Boost_LIBRARIES}
)

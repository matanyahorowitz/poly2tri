cmake_minimum_required(VERSION 2.8)
project(Poly2Tri)
enable_language(CXX)

find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
include_directories(${GLFW_INCLUDE_DIRS})

set(SOURCE_FILES poly2tri/common/shapes.cc 
                 poly2tri/sweep/advancing_front.cc 
                 poly2tri/sweep/cdt.cc 
                 poly2tri/sweep/sweep.cc 
                 poly2tri/sweep/sweep_context.cc)

include_directories(${CMAKE_SOURCE_DIR}/poly2tri)
add_library(Poly2Tri ${SOURCE_FILES})

add_executable(p2t 
  testbed/main.cc
)

target_link_libraries(p2t
  Poly2Tri
  ${GLFW_STATIC_LIBRARIES}
)

install (TARGETS 
  p2t 
  Poly2Tri 
DESTINATION 
  <dir>/../build
)

install (FILES poly2tri.h DESTINATION <dir>/../build)
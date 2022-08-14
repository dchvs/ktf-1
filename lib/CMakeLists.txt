cmake_minimum_required(VERSION ${CMAKE_VERSION})

set(LIB_NAME ktf)
set(SRC_FILES ktf_debug.cpp ktf_unlproto.c ktf_run.cpp ktf_int.cpp)

set(INCLUDE_FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/ktf.h
  ${CMAKE_CURRENT_SOURCE_DIR}/ktf_int.h
  ${CMAKE_CURRENT_SOURCE_DIR}/ktf_debug.h
)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_GTEST REQUIRED gtest)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_LIBNL3 REQUIRED libnl-3.0)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_LIBNL3_GENERIC REQUIRED libnl-genl-3.0)

# Include directories
include_directories(
  ${CMAKE_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${PKG_GTEST_INCLUDE_DIRS}
  ${PKG_LIBNL3_INCLUDE_DIRS}/libnl3
  ${PKG_LIBNL3_GENERIC_INCLUDE_DIRS}
)

add_library(${LIB_NAME} SHARED ${SRC_FILES})

install(TARGETS ${LIB_NAME} DESTINATION lib)
install(FILES ${INCLUDE_FILES} DESTINATION include/ktf)

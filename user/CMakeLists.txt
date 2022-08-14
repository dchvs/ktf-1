cmake_minimum_required(VERSION ${CMAKE_VERSION})

set(SRC_NAME ktfrun)

# Add the executable
add_executable(${SRC_NAME} ${SRC_NAME}.cpp)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_GTEST REQUIRED gtest)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_GMOCK REQUIRED gmock)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_LIBNL3 REQUIRED libnl-3.0)

find_package(PkgConfig REQUIRED)
pkg_search_module(PKG_LIBNL3_GENERIC REQUIRED libnl-genl-3.0)

# Include directories
include_directories(
  ${CMAKE_SOURCE_DIR}/lib
  ${PKG_GTEST_INCLUDE_DIRS}
  ${PKG_GMOCK_INCLUDE_DIRS}
  ${PKG_LIBNL3_INCLUDE_DIRS}/libnl3
  ${PKG_LIBNL3_GENERIC_INCLUDE_DIRS}
)

# Link libraries' directories
link_directories(${SRC_NAME}
  ${CMAKE_SOURCE_DIR}/lib
  ${PKG_GTEST_LIBRARY_DIRS}
  ${PKG_GMOCK_LIBRARY_DIRS}
  ${PKG_LIBNL3_LIBRARY_DIRS}
  ${PKG_LIBNL3_GENERIC_LIBRARY_DIRS}
)

# Link libraries
target_link_libraries(${SRC_NAME} ktf gtest gmock nl-3 nl-genl-3)

# Install the binary
install(TARGETS ${SRC_NAME} DESTINATION bin)

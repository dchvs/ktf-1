cmake_minimum_required(VERSION 3.10.2)

set(SRC_NAME ktfrun)
set(LIB_NAME libktf)

# Add the executable
add_executable(${SRC_NAME} ${SRC_NAME}.cpp)

find_path(LIBNL3_INCLUDE_DIRS NAMES libnl3)
if(LIBNL3_INCLUDE_DIRS-NOTFOUND)
  message(FATAL_ERROR "Unable to find libnl3 headers")
endif()

find_library(LIBNL3_LIBRARIES libnl3)
if(LIBNL3_LIBRARIES-NOTFOUND)
  message(FATAL_ERROR "Unable to find libnl3 library")
endif()

# Include directories
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../lib
                    ${CMAKE_CURRENT_SOURCE_DIR} ${LIBNL3_INCLUDE_DIRS}/libnl3)

# -I...
link_directories(${SRC_NAME} ${CMAKE_CURRENT_SOURCE_DIR}/../lib
                 ${LIBNL3_INCLUDE_DIRS}/libnl3)

# -L...
target_link_libraries(${SRC_NAME} ktf gmock gtest nl-3 nl-genl-3)

# Install the binary
install(TARGETS ${SRC_NAME} DESTINATION bin)

include(CPack)

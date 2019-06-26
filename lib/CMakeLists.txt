cmake_minimum_required (VERSION 3.10.2)

set(LIB_NAME ktf)
set(SRC_FILES ktf_debug.cpp
              ktf_unlproto.c
              ktf_run.cpp
              ktf_int.cpp
 )

set (INCLUDE_FILES
              ${CMAKE_CURRENT_SOURCE_DIR}/../lib/ktf_int.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf_test.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf_map.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf_override.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf_nl.h
              ${CMAKE_CURRENT_SOURCE_DIR}/../kernel/ktf_unlproto.h )


find_path (LIBNL3_INCLUDE_DIRS NAMES libnl3)
if (LIBNL3_INCLUDE_DIRS-NOTFOUND)
    message(FATAL_ERROR "Unable to find libnl3 headers")
endif()

# Include directories
include_directories ( ${CMAKE_CURRENT_SOURCE_DIR}/..
                      ${LIBNL3_INCLUDE_DIRS}/libnl3
                    )

add_library(${LIB_NAME} SHARED ${SRC_FILES} ${INCLUDE_FILES})


install(TARGETS ${LIB_NAME} DESTINATION lib)
install(FILES ${INCLUDE_FILES} DESTINATION include/ktf)

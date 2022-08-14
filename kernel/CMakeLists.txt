cmake_minimum_required(VERSION ${CMAKE_VERSION})

if((NOT DEFINED KERNEL_SRC))
  message(
    FATAL_ERROR
      "Please define KERNEL_SRC into CMake configuration as -DKERNEL_SRC=<kernel-headers-path>.")
endif()

if((NOT DEFINED ARCH))
  message(
    FATAL_ERROR
    "Please define ARCH into CMake configuration as -DARCH=<ARCH>.")
endif()

set(TARGET_MODULE ktf.ko)

set(KBUILD_CMD
  make -f ${CMAKE_CURRENT_SOURCE_DIR}/Makefile KERNEL_SRC=${KERNEL_SRC} ARCH=${ARCH} O=${CMAKE_CURRENT_BINARY_DIR} CROSS_COMPILE=${CROSS_COMPILE} M=${CMAKE_CURRENT_BINARY_DIR} src=${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_command(OUTPUT ${TARGET_MODULE}
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  DEPENDS ${TARGET_MODULE}
  VERBATIM
)

add_custom_target(${TARGET_MODULE} ALL COMMAND ${KBUILD_CMD})

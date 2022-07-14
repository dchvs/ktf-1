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

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Makefile ${CMAKE_CURRENT_BINARY_DIR}/Makefile COPYONLY)

set(KBUILD_CMD
  make -C ${KERNEL_SRC} ARCH=${ARCH} scripts prepare &&
  make KERNEL_SRC=${KERNEL_SRC} ARCH=${ARCH} M=${CMAKE_CURRENT_BINARY_DIR} src=${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_command(OUTPUT ${TARGET_MODULE}
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  DEPENDS ${TARGET_MODULE}
  VERBATIM
)

add_custom_target(${TARGET_MODULE} ALL COMMAND ${KBUILD_CMD})

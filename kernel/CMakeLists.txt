cmake_minimum_required(VERSION ${CMAKE_VERSION})

if((NOT DEFINED ENV{KERNEL_SRC}))
  message(
    FATAL_ERROR
      "KERNEL_SRC variable not defined or points to an invalid location")
endif()

set(TARGET_MODULE ktf.ko)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Makefile ${CMAKE_CURRENT_BINARY_DIR}/Makefile COPYONLY)

set(KBUILD_CMD KERNEL_SRC=${STAGING_KERNEL_DIR}
  make -C ${KERNEL_SRC} ARCH=${ARCH} scripts prepare &&
  make ARCH=${ARCH} M=${CMAKE_CURRENT_BINARY_DIR} src=${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_command(OUTPUT ${TARGET_MODULE}
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  DEPENDS ${TARGET_MODULE}
  VERBATIM
)

add_custom_target(${TARGET_MODULE} ALL COMMAND ${KBUILD_CMD})

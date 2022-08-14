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

if((NOT DEFINED KERNEL_CONFIG))
  message(
    FATAL_ERROR
      "Please define KERNEL_CONFIG into CMake configuration as -DKERNEL_CONFIG=<defconfig>.

      Note: Use your target machine Kernel configuration here. Otherwise, you can set an experimental optimistic Kernel config like -DKERNEL_CONFIG=allyesconfig.
      ")
endif()

if((NOT DEFINED CROSS_COMPILE))
  message(
    FATAL_ERROR
    "Please define architecture cross-compiler into CMake configuration as -DCROSS_COMPILE=<$CROSS_COMPILE>.")
endif()

set(TARGET_MODULE ktf.ko)

set(KBUILD_CMD
  make -C ${KERNEL_SRC} ARCH=${ARCH} O=${CMAKE_CURRENT_BINARY_DIR} CROSS_COMPILE=${CROSS_COMPILE} ${KERNEL_CONFIG} &&
  make -C ${KERNEL_SRC} ARCH=${ARCH} O=${CMAKE_CURRENT_BINARY_DIR} CROSS_COMPILE=${CROSS_COMPILE} scripts prepare &&
  make -f ${CMAKE_CURRENT_SOURCE_DIR}/Makefile KERNEL_SRC=${KERNEL_SRC} ARCH=${ARCH} O=${CMAKE_CURRENT_BINARY_DIR} CROSS_COMPILE=${CROSS_COMPILE} M=${CMAKE_CURRENT_BINARY_DIR} src=${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_command(OUTPUT ${TARGET_MODULE}
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  DEPENDS ${TARGET_MODULE}
  VERBATIM
)

add_custom_target(${TARGET_MODULE} ALL COMMAND ${KBUILD_CMD})

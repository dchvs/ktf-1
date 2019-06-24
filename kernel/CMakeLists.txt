cmake_minimum_required (VERSION 3.10.2)

if ( (NOT DEFINED ENV{KERNEL_SRC}) )
    message(FATAL_ERROR "KERNEL_SRC variable not defined or points to an invalid location")
endif()
if ((NOT DEFINED ENV{KBUILD_OUTPUT}))
  set(ENV{KBUILD_OUTPUT} "$ENV{KERNEL_SRC}")
endif()
#if (NOT EXISTS "$ENV{KBUILD_OUTPUT}/include/generated/autoconf.h")
#  message(FATAL_ERROR "KERNEL OUTPUT directory is not configured")
#endif()


set (headers
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf_test.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf_map.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf_override.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf_nl.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ktf_unlproto.h
)


# Include directories
include_directories (
    ${CMAKE_CURRENT_SOURCE_DIR}
)
link_directories (
		${CMAKE_CURRENT_SOURCE_DIR}
)

# Targets
add_custom_target(driver ALL
	  COMMAND make -C ${CMAKE_CURRENT_SOURCE_DIR}/
)

# Install the module
install(FILES ktf.ko DESTINATION lib/modules/${CMAKE_SYSTEM_VERSION}/kernel/drivers )

include(CPack)

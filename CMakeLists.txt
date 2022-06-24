cmake_minimum_required(VERSION 3.10.2)

# Errors on warnings set(C_WARNINGS "-Wall -Wstrict-prototypes -Wshadow
# -Werror") set(CXX_WARNINGS "-Wall -Wshadow -Werror") set(CMAKE_C_FLAGS
# "${CMAKE_C_FLAGS} ${C_WARNINGS}") set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}
# ${CXX_WARNINGS}")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")

add_subdirectory(lib)
add_subdirectory(user)
add_subdirectory(kernel)

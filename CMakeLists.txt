cmake_minimum_required(VERSION ${CMAKE_VERSION})

project("KTF")

# Errors on warnings
set(C_WARNINGS "-Wall -Werror")
set(CXX_WARNINGS "-Wall -Werror")
set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} ${C_WARNINGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${CXX_WARNINGS}")

set(CMAKE_VERSION 3.10.2)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")

add_subdirectory(lib)
add_subdirectory(user)
add_subdirectory(kernel)

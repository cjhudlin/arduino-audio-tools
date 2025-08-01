cmake_minimum_required(VERSION 3.20)

set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0")

# set the project name
project(tests)
set (CMAKE_CXX_STANDARD 11)
set (DCMAKE_CXX_FLAGS "-Werror" )
# add_compile_options(-Wstack-usage=1024)

include(FetchContent)

# Build with arduino-audio-tools
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/.. ${CMAKE_CURRENT_BINARY_DIR}/arduino-audio-tools )
endif()


add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/resample ${CMAKE_CURRENT_BINARY_DIR}/resample)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/generator ${CMAKE_CURRENT_BINARY_DIR}/generator)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/effects ${CMAKE_CURRENT_BINARY_DIR}/effects)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/fft ${CMAKE_CURRENT_BINARY_DIR}/fft)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/ifft ${CMAKE_CURRENT_BINARY_DIR}/ifft)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/fft-effect ${CMAKE_CURRENT_BINARY_DIR}/fft-effect)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/filter ${CMAKE_CURRENT_BINARY_DIR}/filter)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/filter-wav ${CMAKE_CURRENT_BINARY_DIR}/filter-wav)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/url-test ${CMAKE_CURRENT_BINARY_DIR}/url-test)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/hdlc ${CMAKE_CURRENT_BINARY_DIR}/hdlc)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/codec)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/pipeline)

cmake_minimum_required(VERSION 3.12)

if(TEST_APP)
    set(PROJECT_NAME algorithm_test)
else()
    set(PROJECT_NAME algorithm)
endif()

set(PROJECT_MAJOR_VERSION 0)
set(PROJECT_MINOR_VERSION 0)
set(PROJECT_MICRO_VERSION 1)
set(PROJECT_VERSION "${PROJECT_MAJOR_VERSION}.${PROJECT_MINOR_VERSION}.${PROJECT_MICRO_VERSION}")

project(${PROJECT_NAME} LANGUAGES C CXX VERSION ${PROJECT_VERSION})

# if(CMAKE_VERSION VERSION_GREATER 3.12)
# set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
# endif()
if(POLICY CMP0054)
    cmake_policy(SET CMP0054 NEW)
endif()

# set executable output path
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# set library output path
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

set(CMAKE_VERBOSE_MAKEFILE ON)

include(cmake/common.cmake)
include(cmake/comm_macros.cmake)

include_directories(.)
include_directories(src)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-volatile -g -O2")

if(TEST_APP)
    SETUP_TEST(${PROJECT_NAME} ${PROJECT_VERSION})
else()
    SETUP_APP(${PROJECT_NAME} ${PROJECT_VERSION})
endif()

if(WIN32)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -limm32 -lglu32 -lgdi32 -lshell32")
endif()

target_link_directories(${PROJECT_NAME} PUBLIC ${LIBRARY_OUTPUT_PATH})

# target_link_libraries(${PROJECT_NAME} )

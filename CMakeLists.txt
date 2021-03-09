cmake_minimum_required(VERSION 3.7 FATAL_ERROR)
project(rtklib VERSION 0.1.0 LANGUAGES C)

#include(CTest)
#enable_testing()



#message(${CMAKE_SYSTEM_NAME})
#set(WIN32, TRUE)
set(SRC ${PROJECT_SOURCE_DIR}/src)
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH  ${CMAKE_BINARY_DIR}/lib)
set(rtklib_header ${SRC}/rtklib.h)
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
#set(SOURCES main.cpp 
#            lib/math/operations.cpp 
#            lib/math/operations.hpp)

#add_definitions("-Wall -ansi -pedantic -I$(SRC) -DTRACE -lpthread -DENAGLO -DENAQZS -DENAGAL -DNFREQ=3")

#set(CTARGET "-DENAGLO -DENAQZS -DENACMP -DENAGAL -DENAIRN -DNFREQ=5 -DSVR_REUSEADDR")
add_definitions("-Wall -O3 -ansi -pedantic -I$(SRC) -I.. -DTRACE -DENAGLO -DENAQZS -DENACMP -DENAGAL -DENAIRN -DNFREQ=5 -DSVR_REUSEADDR -g")

##include_directories(${SRC} ${SRC}/rcv)
##add_library(rtklib SHARED ${SRC}/rcv/test.c)

include_directories(${SRC})

set(rtkrcv_lib_name rtkrcv)
file(GLOB src_files "${SRC}/*.c" )
file(GLOB rtkrcv_files "${SRC}/rcv/*.c" )
#list(APPEND src_files " " rtkrcv_files)

include_directories(${SRC})

add_library(${rtkrcv_lib_name} SHARED ${src_files} ${rtkrcv_files})
target_link_libraries(${rtkrcv_lib_name} winmm.lib ws2_32.lib)
set_target_properties(
    ${rtkrcv_lib_name}
    PROPERTIES
    #PUBLIC_HEADER ${rtklib_header}
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
    PREFIX ""
    OUTPUT_NAME ${rtkrcv_lib_name}
    COMPILE_DEFINITIONS WIN_DLL=1
)



set(rtkrcv_lib_name rtkrcv)
file(GLOB rtkrcv_files "${SRC}/rcv/*.c")

include_directories(${SRC})

add_library(${rtkrcv_lib_name} SHARED ${rtkrcv_files})
target_link_libraries(${rtkrcv_lib_name} winmm.lib)
set_target_properties(
    ${rtkrcv_lib_name}
    PROPERTIES
    PUBLIC_HEADER ${rtklib_header}
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
    PREFIX ""
    OUTPUT_NAME ${rtkrcv_lib_name}
)
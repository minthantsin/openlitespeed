cmake_minimum_required(VERSION 2.8)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11 -Wall -lxml2 -lcurl")

include_directories(${PROJECT_SOURCE_DIR}/../thirdparty/ModSecurity/headers/)

execute_process( COMMAND getconf LFS_CFLAGS
            OUTPUT_VARIABLE  LFS_CFLAGS )

add_definitions( ${LFS_CFLAGS} )


add_library(mod_security SHARED
    mod_security.cpp
)


target_link_libraries(mod_security libmodsecurity.a -llmdb -lxml2 -lcurl -lcrypto -lssl -lyajl )

set_target_properties(mod_security PROPERTIES PREFIX "")

project(testu01_config C)
add_library(testu01_config INTERFACE
        ${CMAKE_CURRENT_BINARY_DIR}/config.h
        ${CMAKE_CURRENT_BINARY_DIR}/gdefconf.h
        )

target_include_directories(testu01_config INTERFACE ${CMAKE_CURRENT_BINARY_DIR})
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/gdefconf.h.in ${CMAKE_CURRENT_BINARY_DIR}/gdefconf.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

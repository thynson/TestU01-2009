cmake_minimum_required(VERSION 3.10)
project(testu01_mylib C)

set(TESTU01_MYLIB_GENERATED_HEADER
        gdef.h addstr.h bitset.h chrono.h mystr.h num.h num2.h tables.h util.h)

foreach(header ${TESTU01_MYLIB_GENERATED_HEADER})
    string(REGEX REPLACE "\\.h$" ".tex" TEXFILE ${header})
    add_custom_command(
            OUTPUT ${header}
            COMMAND tcode ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} ${header}
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} tcode
    )
endforeach()

list(TRANSFORM TESTU01_MYLIB_GENERATED_HEADER PREPEND ${CMAKE_CURRENT_BINARY_DIR}/)
message(STATUS "TESTU01_MYLIB_GENERATED_HEADER:" "${TESTU01_MYLIB_GENERATED_HEADER}")

add_library(testu01_mylib
        ${TESTU01_MYLIB_GENERATED_HEADER}
        gdef.c addstr.c bitset.c chrono.c mystr.c num.c num2.c tables.c util.c
        )
target_include_directories(testu01_mylib PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(testu01_mylib testu01_config)

set_target_properties(testu01_mylib PROPERTIES
        C_STANDARD 99
        C_STANDARD_REQUIRED ON
        C_EXTENSIONS OFF)

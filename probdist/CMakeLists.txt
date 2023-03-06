
cmake_minimum_required(VERSION 3.10)
project(testu01_probdist C)

set(TESTU01_PROBDIST_GENERATED_HEADER
        fmass.h fdist.h fbar.h finv.h gofs.h gofw.h statcoll.h wdist.h
        )

foreach(header ${TESTU01_PROBDIST_GENERATED_HEADER})
    string(REGEX REPLACE "\\.h$" ".tex" TEXFILE ${header})
    add_custom_command(
            OUTPUT ${header}
            COMMAND tcode ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} ${header}
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} tcode
    )
endforeach()

#string(PREPEND ${CMAKE_CURRENT_BINARY_DIR} "${TESTU01_MYLIB_GENERATED_HEADER}")
list(TRANSFORM TESTU01_PROBDIST_GENERATED_HEADER PREPEND ${CMAKE_CURRENT_BINARY_DIR}/)
message(STATUS "TESTU01_PROBDIST_GENERATED_HEADER:" "${TESTU01_PROBDIST_GENERATED_HEADER}")

add_library(testu01_probdist
        ${TESTU01_PROBDIST_GENERATED_HEADER}
        fmass.c fdist.c fbar.c finv.c gofs.c gofw.c statcoll.c wdist.c
        )
target_include_directories(testu01_probdist PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(testu01_probdist testu01_config)
target_link_libraries(testu01_probdist testu01_mylib)

set_target_properties(testu01_mylib PROPERTIES
        C_STANDARD 99
        C_STANDARD_REQUIRED ON
        C_EXTENSIONS OFF)

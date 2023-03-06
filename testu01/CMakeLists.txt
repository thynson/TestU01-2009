cmake_minimum_required(VERSION 3.10)
project(testu01 CXX)

set(TESTU01_GEN)
set(TESTU01_TESTU01_GENERATED_HEADER
        unif01.h ulcg.h umrg.h ucarry.h utaus.h ugfsr.h uinv.h uquad.h ucubic.h ulec.h utezuka.h umarsa.h
        uweyl.h uknuth.h uwu.h unumrec.h uvaria.h usoft.h ugranger.h ucrypto.h ufile.h udeng.h utouzin.h
        uautomata.h uxorshift.h ubrent.h rijndael-alg-fst.h tu01_sha1.h scatter.h swrite.h sres.h smultin.h
        sknuth.h smarsa.h sstring.h svaria.h snpair.h swalk.h sentrop.h sspectral.h scomp.h sspacings.h
        vectorsF2.h bbattery.h ffam.h fcong.h ffsr.h ftab.h fres.h fcho.h fmultin.h fmarsa.h fknuth.h fwalk.h
        fstring.h fspectral.h fvaria.h fnpair.h
        )


foreach(header ${TESTU01_TESTU01_GENERATED_HEADER})
    string(REGEX REPLACE "\\.h$" ".tex" TEXFILE ${header})
    add_custom_command(
            OUTPUT ${header}
            COMMAND tcode ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} ${header}
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/${TEXFILE} tcode
    )
endforeach()

list(TRANSFORM TESTU01_TESTU01_GENERATED_HEADER PREPEND ${CMAKE_CURRENT_BINARY_DIR}/)
add_library(testu01
        ${TESTU01_TESTU01_GENERATED_HEADER}
        TestU01.h
        unif01.c ulcg.c umrg.c ucarry.c utaus.c ugfsr.c uinv.c uquad.c ucubic.c ulec.c utezuka.c umarsa.c
        uweyl.c uknuth.c uwu.c unumrec.c uvaria.c usoft.c ugranger.c ucrypto.c ufile.c udeng.c utouzin.c
        uautomata.c uxorshift.c ubrent.c rijndael-alg-fst.c tu01_sha1.c scatter.c swrite.c sres.c smultin.c
        sknuth.c smarsa.c sstring.c svaria.c snpair.c swalk.c sentrop.c sspectral.c scomp.c sspacings.c
        vectorsF2.c bbattery.c ffam.c fcong.c ffsr.c ftab.c fres.c fcho.c fmultin.c fmarsa.c fknuth.c fwalk.c
        fstring.c fspectral.c fvaria.c fnpair.c
        )

target_include_directories(testu01 PUBLIC ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(testu01 testu01_config testu01_mylib testu01_probdist)
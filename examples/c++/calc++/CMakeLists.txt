#
# bison_examples\examples\c++\calc++\CMakeLists.txt
#

if (MSVC)
  set(FLEX_COMPILE_FLAGS "-DYY_NO_UNISTD_H")
endif()

BISON_TARGET(parser parser.yy ${CMAKE_CURRENT_BINARY_DIR}/parser.cc
    COMPILE_FLAGS "-v"
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/parser.hh
    )

FLEX_TARGET(scanner scanner.ll ${CMAKE_CURRENT_BINARY_DIR}/scanner.cc
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/scanner.hh
    COMPILE_FLAGS ${FLEX_COMPILE_FLAGS}
    )

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
# include_directories(${FLEX_INCLUDE_DIR})

add_executable(calc++
    calc++.cc
    driver.cc
    driver.hh
    ${BISON_parser_OUTPUTS}
    ${FLEX_scanner_OUTPUTS}
    Makefile # not really needed; reference only
    local.mk # not really needed; reference only
    parser.yy
    scanner.ll
    # test file
    calc++.test
    )
if (MSVC)
    target_compile_options(calc++
        PRIVATE 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()

set_target_properties(calc++ PROPERTIES FOLDER "examples/c++")

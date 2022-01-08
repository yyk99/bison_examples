#
# bison_examples\examples\c++\calc++\CMakeLists.txt
#

BISON_TARGET(parser parser.yy ${CMAKE_CURRENT_BINARY_DIR}/parser.cc
    COMPILE_FLAGS "-v"
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/parser.hh
    )

FLEX_TARGET(scanner scanner.ll ${CMAKE_CURRENT_BINARY_DIR}/scanner.cc
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/scanner.hh
    COMPILE_FLAGS "-DYY_NO_UNISTD_H"
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
    )

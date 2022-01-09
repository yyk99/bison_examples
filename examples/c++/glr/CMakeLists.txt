#
# bison_examples\examples\c++\glr\CMakeLists.txt
#

BISON_TARGET(parser c++-types.yy ${CMAKE_CURRENT_BINARY_DIR}/parser.cc
    COMPILE_FLAGS "-v"
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/parser.hh
    )

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
# include_directories(${FLEX_INCLUDE_DIR})

add_executable(c++-types
    ${BISON_parser_OUTPUTS}
    ${FLEX_scanner_OUTPUTS}
    c++-types.yy
    c++-types.test
    )

if (MSVC)
    target_compile_options(c++-types 
        PRIVATE 
            "/Zc:__cplusplus" 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()

set_target_properties(c++-types PROPERTIES FOLDER "examples/c++")

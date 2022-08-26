#
#
#

if (MSVC)
    set(FLEX_COMPILE_FLAGS "-DYY_NO_UNISTD_H")
endif()

# testxxLexer.l
FLEX_TARGET(scanner testxxLexer.l ${CMAKE_CURRENT_BINARY_DIR}/testxxLexer.l.cc
    DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/testxxLexer.l.hh
    COMPILE_FLAGS ${FLEX_COMPILE_FLAGS}
    )

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${FLEX_INCLUDE_DIR})

add_executable(testxxLexer
    ${BISON_parser_OUTPUTS}
    ${FLEX_scanner_OUTPUTS}
    # extra reference files
    ../CMakeLists.txt
    testxxLexer.l
    )
if (MSVC)
    target_compile_options(testxxLexer
        PRIVATE 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()

set_target_properties(testxxLexer PROPERTIES FOLDER "flex/examples")

#
# bison_examples\examples\c++\CMakeLists.txt
#

BISON_TARGET(variant11_parser variant-11.yy ${CMAKE_CURRENT_BINARY_DIR}/variant11_parser.cpp
             DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/variant11_parser.h)
add_executable(variant-11 
    ${BISON_variant11_parser_OUTPUTS}
    Makefile
    variant-11.yy
    )

if (MSVC)
    target_compile_options(variant-11 
        PRIVATE 
            "/Zc:__cplusplus" 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()
set_target_properties(variant-11 PROPERTIES FOLDER "examples/c++")

BISON_TARGET(variant_parser variant.yy ${CMAKE_CURRENT_BINARY_DIR}/variant_parser.cpp
             DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/variant_parser.h)
add_executable(variant
    ${BISON_variant_parser_OUTPUTS}
    Makefile
    variant.yy
    )
if (MSVC)
    target_compile_options(variant
        PRIVATE 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()
set_target_properties(variant PROPERTIES FOLDER "examples/c++")

BISON_TARGET(simple_parser simple.yy ${CMAKE_CURRENT_BINARY_DIR}/simple_parser.cpp
             DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/simple_parser.h)
add_executable(simple
    ${BISON_simple_parser_OUTPUTS}
    Makefile
    simple.yy
    )

if (MSVC)
    target_compile_options(simple
        PRIVATE 
            "-D_CRT_NONSTDC_NO_WARNINGS" 
            "-D_CRT_SECURE_NO_WARNINGS"
            "/wd4065"
        )
endif()
set_target_properties(simple PROPERTIES FOLDER "examples/c++")

add_subdirectory(calc++)
add_subdirectory(glr)
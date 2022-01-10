#
#
#

macro (add_cbison_app target grama)
    # message(STATUS "add_cbison_app: ${ARGV0} ARGC=${ARGC}")

	BISON_TARGET(${target}_parser ${grama}.y ${CMAKE_CURRENT_BINARY_DIR}/${grama}.c
          DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/${grama}.h
        )

      if (${ARGC} EQUAL 3)
	if (MSVC)
	  set(FLEX_COMPILE_FLAGS "-DYY_NO_UNISTD_H")
	endif()
        set(scan "${ARGV2}")
        set(extra_files ${scan}.l)
        FLEX_TARGET(${target}_scanner ${scan}.l ${CMAKE_CURRENT_BINARY_DIR}/${scan}.c
             DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/${scan}.h
             COMPILE_FLAGS ${FLEX_COMPILE_FLAGS}
             )
    
        message(STATUS "${ARGV0}: ${FLEX_${target}_scanner_OUTPUTS}")
    endif()

    add_executable(${target}
        ${BISON_${target}_parser_OUTPUTS}
        ${FLEX_${target}_scanner_OUTPUTS}
        Makefile
        ${grama}.y
        ${extra_files}
		../CMakeLists.txt
		../../CMakeLists.txt
        )

    if (MSVC)
        target_compile_options(${target}
            PRIVATE 
    #            "/Zc:__cplusplus" 
                "-D_CRT_NONSTDC_NO_WARNINGS" 
                "-D_CRT_SECURE_NO_WARNINGS"
                "-DYYMALLOC=malloc"
                "-DYYFREE=free"
                "/wd4065"
            )
    endif()
    if (UNIX)
	target_link_libraries(${target} -lm)
    endif (UNIX)
    set_target_properties(${target} PROPERTIES LINKER_LANGUAGE C)
    set_target_properties(${target} PROPERTIES FOLDER "examples/c")
endmacro(add_cbison_app)

add_subdirectory(bistromathic)
add_subdirectory(calc)
add_subdirectory(glr)
add_subdirectory(lexcalc)
add_subdirectory(mfcalc)
add_subdirectory(pushcalc)
add_subdirectory(reccalc)
add_subdirectory(rpcalc)

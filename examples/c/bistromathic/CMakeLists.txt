#
#
#

add_cbison_app(bistromathic parse)

if (MINGW)
	target_link_libraries(bistromathic readline)
endif()

if (UNIX)
  target_link_libraries(bistromathic -lreadline)
endif ()


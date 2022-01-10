#
#
#

add_cbison_app(bistromathic parse)
if (UNIX)
  target_link_libraries(bistromathic -lreadline)
endif ()


SET(PANDOC pandoc)

SET(PANDOC_ARGS --template=${CMAKE_CURRENT_SOURCE_DIR}/templates/template.FORMAT --smart --standalone --toc --toc-depth=3 --include-in-header=${CMAKE_CURRENT_SOURCE_DIR}/templates/inc_header.html --include-before-body=${CMAKE_CURRENT_SOURCE_DIR}/templates/inc_before.html --include-after-body=${CMAKE_CURRENT_SOURCE_DIR}/templates/inc_after.html
	)

MESSAGE(STATUS "Pandoc arguments: " ${PANDOC_ARGS})

ADD_CUSTOM_COMMAND(
	OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/index.html
	DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/index.md
	COMMAND ${PANDOC} ${PANDOC_ARGS} ${CMAKE_CURRENT_SOURCE_DIR}/index.md -o ${CMAKE_CURRENT_BINARY_DIR}/index.html
	)

ADD_CUSTOM_TARGET(
	MKD_HTML ALL
	DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/index.html
	)

INSTALL(DIRECTORY css/
	DESTINATION css/
	)

INSTALL(DIRECTORY js/
	DESTINATION js/
	)

INSTALL(DIRECTORY images/
	DESTINATION images/
	)

INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/index.html
	DESTINATION .)

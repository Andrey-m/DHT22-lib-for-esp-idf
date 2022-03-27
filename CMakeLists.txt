

file(GLOB_RECURSE SOURCES src/*.* include/*.*)

idf_component_register(SRCS ${SOURCES}
                       INCLUDE_DIRS src include)

set(srcs
    "src/DHT_c.c"
    "src/DHT.cpp")

set(includes "include")

idf_component_register(SRCS "${srcs}"
                       INCLUDE_DIRS ${includes}
                       REQUIRES driver)
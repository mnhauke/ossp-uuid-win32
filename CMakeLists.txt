cmake_minimum_required(VERSION 3.15)
project(ossp-uuid C)

set(OSSP-UUID_VERSION "1.6.2")

include(GNUInstallDirs)

set(OSSP-UUID_SOURCES
    uuid.c
    uuid_mac.c
    uuid_md5.c
    uuid_prng.c
    uuid_sha1.c
    uuid_str.c
    uuid_time.c
    uuid_ui128.c
    uuid_ui64.c
)

set(OSSP-UUID_HEADERS
    uuid.h
)

add_library(libossp-uuid SHARED
    ${OSSP-UUID_SOURCES}
)

set_target_properties(libossp-uuid PROPERTIES
    OUTPUT_NAME "ossp-uuid"
)

# create .pc file
set(prefix      ${CMAKE_INSTALL_PREFIX})
set(exec_prefix "\${prefix}")
set(libdir      "\${exec_prefix}/${CMAKE_INSTALL_LIBDIR}")
set(includedir  "\${prefix}/${CMAKE_INSTALL_INCLUDEDIR}")
set(VERSION     ${OSSP-UUID_VERSION})
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/uuid.pc.in
               ${CMAKE_CURRENT_BINARY_DIR}/ossp-uuid.pc @ONLY)

install(TARGETS libossp-uuid
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})

install(FILES ${OSSP-UUID_HEADERS}
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/ossp/")

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/ossp-uuid.pc
    DESTINATION lib/pkgconfig)


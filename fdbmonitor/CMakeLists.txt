set(FDBMONITOR_SRCS ConvertUTF.h SimpleIni.h fdbmonitor.cpp)

add_executable(fdbmonitor ${FDBMONITOR_SRCS})
if(UNIX AND NOT APPLE)
    target_link_libraries(fdbmonitor rt)
endif()
# FIXME: This include directory is an ugly hack. We probably want to fix this
# as soon as we get rid of the old build system
target_include_directories(fdbmonitor PRIVATE ${CMAKE_BINARY_DIR}/fdbclient)

install(TARGETS fdbmonitor DESTINATION "${FDB_LIB_NOSUFFIX}/foundationdb" COMPONENT server)

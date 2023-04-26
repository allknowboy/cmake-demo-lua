include_directories(
    ${PROJECT_SOURCE_DIR}/lua
)

add_library(socket_core SHARED auxiliar.c buffer.c compat.c except.c inet.c io.c luasocket.c options.c select.c tcp.c timeout.c udp.c wsocket.c )
set_target_properties(socket_core PROPERTIES PREFIX ""
    OUTPUT_NAME "core"
    ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib/socket"
    LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib/socket"
    RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin/socket"
)
target_link_libraries(socket_core ws2_32 lualib)

add_library(mime_core SHARED compat.c mime.c )
set_target_properties(mime_core PROPERTIES PREFIX ""
    OUTPUT_NAME "core"
    ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib/mime"
    LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib/mime"
    RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin/mime"
)
target_link_libraries(mime_core lualib)

install(
    TARGETS socket_core 
    RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/dist/socket
)

install(
    TARGETS mime_core
    RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/dist/mime
)

install(
    FILES
    mime.lua
    socket.lua
    ltn12.lua
    DESTINATION ${PROJECT_SOURCE_DIR}/dist
)

install(
    FILES
    smtp.lua
    ftp.lua
    headers.lua
    http.lua
    tp.lua
    url.lua
    DESTINATION ${PROJECT_SOURCE_DIR}/dist/socket
)

cmake_minimum_required(VERSION 3.15)

set(BBYEDPI_NAME "bbyedpi")

project(${BBYEDPI_NAME} C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

add_executable(${BBYEDPI_NAME}
    src/packets.c
    src/main.c
    src/conev.c
    src/proxy.c
    src/desync.c
    src/mpool.c
    src/extend.c
)

target_compile_definitions(${BBYEDPI_NAME} PRIVATE _DEFAULT_SOURCE)
target_compile_options(${BBYEDPI_NAME} PRIVATE
    -O2
    -Wall
    -Wno-unused
    -Wextra
    -Wno-unused-parameter
    -pedantic
)

if(WIN32)
    target_sources(${BBYEDPI_NAME} PRIVATE win_service.c)
    target_link_libraries(${BBYEDPI_NAME} PRIVATE ws2_32 mswsock)
endif()

install(TARGETS ${BBYEDPI_NAME} RUNTIME DESTINATION bin)

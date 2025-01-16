set(SUB_PROJECT_NAME mcp2515-c)

add_executable(${SUB_PROJECT_NAME})

target_link_libraries(${SUB_PROJECT_NAME} PUBLIC
    pico_stdlib
    hardware_spi
)

pico_enable_stdio_usb(${SUB_PROJECT_NAME} 1)
pico_enable_stdio_uart(${SUB_PROJECT_NAME} 0)

target_sources(${SUB_PROJECT_NAME} PRIVATE main.c mcp2515.c)

pico_add_extra_outputs(${SUB_PROJECT_NAME})


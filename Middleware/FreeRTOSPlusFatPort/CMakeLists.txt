add_library(freertos_plus_fat_port STATIC)
target_sources(freertos_plus_fat_port
    PRIVATE
    ff_sddisk.c)
target_link_libraries(freertos_plus_fat_port
    PUBLIC
    freertos_plus_fat_port_common
    PRIVATE
    freertos_kernel
    freertos_plus_fat)

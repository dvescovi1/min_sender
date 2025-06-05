add_library(freertos_plus_fat_port STATIC)
target_sources(freertos_plus_fat_port
    PRIVATE
    ff_sddisk.c)

    # Configure your custom include path
#target_include_directories(freertos_plus_fat_port
#    PUBLIC
#        your/include/path )

set( FREERTOS_PLUS_FAT_PORT "A_CUSTOM_PORT" CACHE STRING "Configure custom port" )

add_subdirectory( FreeRTOS-Plus-FAT )

target_link_libraries(freertos_plus_fat_port
    PUBLIC
        freertos_plus_fat_port_common
    PRIVATE
        freertos_kernel
        freertos_plus_fat)

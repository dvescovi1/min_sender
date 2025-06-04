cmake_minimum_required(VERSION 3.22)

#
# This file is generated only once,
# and is not re-generated if converter is called multiple times.
#
# User is free to modify the file as much as necessary
#

# Setup compiler settings
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)


# Define the build type
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug")
endif()

# Set the project name
set(CMAKE_PROJECT_NAME V4-563)

# Include toolchain file
include("cmake/gcc-arm-none-eabi.cmake")

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Core project settings
project(${CMAKE_PROJECT_NAME})
message("Build type: " ${CMAKE_BUILD_TYPE})

# Enable CMake support for ASM and C languages
enable_language(C ASM)

# Create an executable object type
add_executable(${CMAKE_PROJECT_NAME})

# Add STM32CubeMX generated sources
add_subdirectory(cmake/stm32cubemx)

#set(THIRD_PARTY_PATH "${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/Third_Party")
set(THIRD_PARTY_PATH "${CMAKE_CURRENT_SOURCE_DIR}/Middleware/Third_Party")

#add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/STM32FatFs)

#target_include_directories(stm32fatfs PUBLIC
#    # Add user defined include paths
#    ${CMAKE_CURRENT_SOURCE_DIR}/Core/Inc
#    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32H5xx_HAL_Driver/Inc
#)

# Select the native compile PORT
#set(FREERTOS_PLUS_FAT_PORT "STM32HXX" CACHE STRING "" FORCE)
#set(FREERTOS_PLUS_FAT_FETCH_FREERTOS "OFF" CACHE BOOL "" FORCE)
#set(FREERTOS_PLUS_FAT_DEV_SUPPORT OFF CACHE BOOL "" FORCE)


#add_subdirectory(${THIRD_PARTY_PATH}/FreeRTOS-Plus-FAT)

#target_sources(freertos_plus_fat_port PRIVATE
    # Add user sources here
#    ${CMAKE_CURRENT_SOURCE_DIR}/Middleware/FreeRTOSPlusFatPort/ff_sddisk.c
#)


# Link directories setup
target_link_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined library search paths
)

# Add sources to executable
target_sources(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user sources here
#    ${CMAKE_CURRENT_SOURCE_DIR}/Core/Src/ff_sddisk.c
    ${THIRD_PARTY_PATH}/STM32FatFs/diskio.c
    ${THIRD_PARTY_PATH}/STM32FatFs/ff_gen_drv.c
    ${THIRD_PARTY_PATH}/STM32FatFs/ff.c
    ${THIRD_PARTY_PATH}/STM32FatFs/ffunicode.c
    ${THIRD_PARTY_PATH}/STM32FatFs/sd_diskio.c
#    ${THIRD_PARTY_PATH}/Middlewares/STM32FatFs/ffsystem_cmsis_os.c
    ${THIRD_PARTY_PATH}/STM32FatFs/sd_diskio_dma_rtos.c
     )

# Add include paths
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined include paths
    ${CMAKE_CURRENT_SOURCE_DIR}/Core/Inc
    ${THIRD_PARTY_PATH}/STM32FatFs
    ${THIRD_PARTY_PATH}/FreeRTOS-Plus-FAT/include
    ${THIRD_PARTY_PATH}/FreeRTOS-Plus-TCP/include
)

# Add project symbols (macros)
target_compile_definitions(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined symbols
)

# Add linked libraries
target_link_libraries(${CMAKE_PROJECT_NAME}
    stm32cubemx
#    stm32fatfs
#    freertos_plus_fat
    # Add user defined libraries
)

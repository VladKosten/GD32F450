add_library(Device STATIC system_gd32f4xx.c)

target_include_directories(Device PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_compile_definitions(Device PUBLIC ${MCU_SERIES})

target_link_libraries(Device PRIVATE CompileOptions
                             PUBLIC  CMSIS
                             PRIVATE LowLevelDriverHeader)
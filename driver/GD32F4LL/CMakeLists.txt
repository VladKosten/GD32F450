
add_library(LowLevelDriverHeader INTERFACE)

target_include_directories(LowLevelDriverHeader INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/Include)

# Add the driver files
file(GLOB_RECURSE LowLevelDriverSource ${CMAKE_CURRENT_SOURCE_DIR}/Source/*.c)

add_library(LowLevelDriver STATIC ${LowLevelDriverSource})

target_compile_definitions(LowLevelDriver PUBLIC ${MCU_SERIES})

target_link_libraries(LowLevelDriver PUBLIC  Device
                                     PUBLIC  LowLevelDriverHeader
                                     PRIVATE CompileOptions)
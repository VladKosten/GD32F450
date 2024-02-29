# Not simple. GigaDevice programmers are not very good at their job.

# Add the header files Low level driver because he have dependencies on the device
add_library(LowLevelDriverHeader INTERFACE)

target_include_directories(LowLevelDriverHeader INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/Include)

# Final creation of the static library for the low level driver of the GigaDevice MCU
file(GLOB_RECURSE LowLevelDriverSource ${CMAKE_CURRENT_SOURCE_DIR}/Source/*.c)

add_library(LowLevelDriver STATIC ${LowLevelDriverSource})

target_compile_definitions(LowLevelDriver PUBLIC ${MCU_SERIES})

target_link_libraries(LowLevelDriver PUBLIC  Device
                                     PUBLIC  LowLevelDriverHeader
                                     PRIVATE CompileOptions)
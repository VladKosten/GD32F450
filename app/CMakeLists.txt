# Add our application (because we call main in startup file, we need to add it as a library, not as an executable, and link to startup file)
# Note: gd32f4xx_it.c is not used, but it is required by startup file (it is called in the interrupt handler, so we need to provide it)
add_library(App STATIC app.c
                       gd32f4xx_it.c)

target_include_directories(App PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(App PRIVATE CompileOptions
                          PUBLIC  LowLevelDriver)
# First, we need to check the version of CMake. If the version is less than 3.12, we need to stop the compilation process.
cmake_minimum_required(VERSION 3.15)

# Include the CMake ARM GCC toolchain file.
include(gcc-arm-none-eabi.cmake)

# Set the project name and enable the C and ASM languages.
project(GD32F450VET6 C ASM)

# Set the C standard to C99 (Not required, but it is a good practice).
set(CMAKE_C_STANDARD 99)

# Set the MCU parameters.
set(MCU_FAMILY GD32F4)                  # the MCU family
set(MCU_SERIES GD32F450)                # the MCU series
set(MCU_MODEL GD32F450VET6)             # the MCU model

# Set the linker script file.
set(LINKER_SCRIPT ${PROJECT_SOURCE_DIR}/device/GD32F450VET6.ld)

# Set the startup file.
set(STARTUP_SCRIPT ${PROJECT_SOURCE_DIR}/device/startup_gd32f450.s)

# Add the driver files
file(GLOB_RECURSE DRIVER ${PROJECT_SOURCE_DIR}/driver/StandardPeripheral/Source/*.c)

# Add application files
file(GLOB_RECURSE APPLICATION ${PROJECT_SOURCE_DIR}/app/*.c)

add_executable (${PROJECT_NAME} ${STARTUP_SCRIPT}                                   # the startup file
                                ${DRIVER}                                           # the driver files
                                ${APPLICATION}                                      # the application files
                                ${PROJECT_SOURCE_DIR}/device/system_gd32f4xx.c)     # the system file

# Include the header files.
target_include_directories(${PROJECT_NAME} PRIVATE  ${PROJECT_SOURCE_DIR}/app                                   # the application files
                                                    ${PROJECT_SOURCE_DIR}/driver/StandardPeripheral/Include     # the driver files
                                                    ${PROJECT_SOURCE_DIR}/device                                # the device files
                                                    ${PROJECT_SOURCE_DIR}/driver/CMSIS                          # the CMSIS files
                                                    )

target_compile_definitions(${PROJECT_NAME} PRIVATE ${MCU_SERIES}
                                                   ${CPU_PARAMETERS})

# Set the compile options.
target_compile_options(${PROJECT_NAME} PRIVATE  -Wall                           # the compiler will output warnings for common programming errors
                                                -Wextra                         # enables some extra warning flags that are not enabled by -Wall
                                                -Wpedantic                      # issue all the warnings demanded by strict ISO C and ISO C++
                                                -Wshadow                        # warn whenever a local variable or type declaration shadows another variable, parameter, type, class member
                                                -Wdouble-promotion              # warn if a float is implicitly promoted to a double
                                                -Wformat=2 -Wformat-truncation  # check calls to printf and scanf
                                                -Wundef                         # warn if an undefined identifier is evaluated in an #if directive
                                                -fno-common                     # In C, this option controls the placement of global variables defined without an initializer
                                                -Wno-unused-parameter           # do not warn about unused parameters
                                                -Wno-unused-variable            # do not warn about unused variables
                                                )
IF(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_options(${PROJECT_NAME} PRIVATE -O0      # no optimization
                                                   -g3      # generate debug information
                                                   -ggdb3)  # produce debugging information for use by GDB
ELSE ()
    target_compile_options(${PROJECT_NAME} PRIVATE -O3      # optimize yet more
                                                   -g0      # no debug information
                                                   -ggdb0)  # no debugging information
ENDIF()

target_link_options(${PROJECT_NAME} PRIVATE -T${LINKER_SCRIPT}                  # set the linker script
                                            -Wl,-Map=${CMAKE_PROJECT_NAME}.map  # generate a map file
                                            --specs=nosys.specs                 # use the nosys.specs file
                                            -Wl,--start-group                   # start a group of input sections
                                            -lc                                 # the C library
                                            -Wl,--end-group                     # end a group of input sections
                                            -Wl,--print-memory-usage)           # print memory usage

IF(MCU_MODEL STREQUAL "GD32F450VET6")
    target_link_options(${PROJECT_NAME} PRIVATE -mcpu=cortex-m4     # set the architecture
                                                -mthumb             # generate code for the Thumb instruction set
                                                -mfpu=fpv4-sp-d16   # set the FPU type
                                                -mfloat-abi=hard)   # set the floating-point ABI)

    target_compile_options(${PROJECT_NAME} PRIVATE  -mcpu=cortex-m4     # set the architecture
                                                    -mthumb             # generate code for the Thumb instruction set
                                                    -mfpu=fpv4-sp-d16   # set the FPU type
                                                    -mfloat-abi=hard)   # set the floating-point ABI)
ENDIF()
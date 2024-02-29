# GD32F450

## Description
This is a ready to use environment for the GD32F450 microcontroller. Just clone, Prepare the environment and start coding.

## Features
- CMake build system
- Debugging with OpenOCD
- Ready to use VSCode configuration
- Ready to use CMake configuration
- Ready to use OpenOCD configuration
- (**t-linkV2.1 work correctly*)
- GigaDevices Framework (Standard Peripheral Library). [Doc and example](https://www.gd32mcu.com/download/down/document_id/247/path_type/1)

## Dependencies
- [VSCode](https://code.visualstudio.com/)
- [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm) (Tested with version 10.3.1 (release))
- [CMake](https://cmake.org/download/) (Tested with version 3.21.3)
- [Ninja](https://ninja-build.org/) (Tested with version 1.10.2)
- [OpenOCD](OpenOCD) (Tested with version 0.11.0)

## VsCode requirement extensions
- [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
- [Cmake](https://marketplace.visualstudio.com/items?itemName=twxs.cmake)
- [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)

## Install dependencies on Ubuntu
1. Install VSCode:
```bash
sudo snap install --classic code
```
2. Install the GNU Arm Embedded Toolchain:
```bash
sudo apt install gcc-arm-none-eabi
```
3. Install CMake:
```bash
sudo apt install cmake
```
4. Install Ninja:
```bash
sudo apt install ninja-build
```
5. Install OpenOCD:
```bash
sudo apt install openocd
```

## Install dependencies on Windows
    I don't have a Windows machine to test the installation, but you can find the installation instructions on the official websites of the tools.
    I have recommended the use Chocolatey to install the tools on Windows.


## How to use
1. Clone the repository
2. Install the dependencies and the required extensions for VSCode (if you don't have them already)
3. Open the project with VSCode


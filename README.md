# Embedded System Build System Project

## Project Overview
This project is designed to create a build system for an embedded system application using **GNU Make**, **GCC**, and **GNU Makefiles**. The build system supports two target platforms:
1. **Host Platform** (Native system, using GCC)
2. **MSP432 Target Platform** (ARM Cortex-M4, using arm-none-eabi-gcc)

The build system is responsible for compiling, linking, and generating executables for both platforms, as well as creating intermediate files such as preprocessed outputs, assembly code, object files, and dependency files.

This build system:
- Uses **GNU Make** to automate the build process.
- Has Makefiles that can compile and link multiple source files.
- Supports cross-compilation for different platforms.
- Generates useful output files (e.g., preprocessed, assembly, object, map files).
- Cleans the build system with platform-specific settings.

## Directory Structure
```
project/
├── src/                     # Contains source files
│   ├── main.c
│   ├── memory.c
│   ├── interrupts_msp432p401r_gcc.c
│   ├── startup_msp432p401r_gcc.c
│   └── system_msp432p401r.c
├── include/                 # Contains header files
│   ├── common/
│   ├── msp432/
│   └── CMSIS/
├── Makefile                 # Main Makefile
├── sources.mk               # Source file list for the build system
└── msp432p401r.lds          # Linker script for MSP432 platform
```


## Key Files
- **Makefile**: The main build system configuration file that orchestrates the build process.
- **sources.mk**: Defines the source files to be compiled based on the target platform.
- **msp432p401r.lds**: Linker script used for the MSP432 platform.

## Platforms Supported
- **Host Platform**: Native GCC compiler for testing applications on your local machine.
- **MSP432 Platform**: Cross-compilation for the MSP432 embedded platform using the ARM GCC toolchain (`arm-none-eabi-gcc`).

## Features of the Build System
The build system supports several key features:
- **Compile and Link**: Automatically compiles and links the source files into an executable for the target platform.
- **Preprocessing**: Generates preprocessed source code (`%.i`).
- **Assembly Output**: Generates assembly code (`%.asm`).
- **Object Files**: Produces object files (`%.o`).
- **Dependency Files**: Generates `.d` files for managing dependencies between source files.
- **Map File**: Produces a memory map file (`demo.map`) during the build process.
- **Executable**: Generates a final executable file (`demo.out`).
- **Cross Compilation**: Supports both native compilation for the host platform and cross-compilation for the MSP432 embedded target.

## How to Use the Build System

### Requirements
- **GCC (GNU Compiler Collection)** for compiling on the host platform.
- **arm-none-eabi-gcc** for cross-compiling to the MSP432 platform.
- **GNU Make** for managing the build system.

### Build Commands

#### 1. Build for Host Platform
To compile and link the application for the host platform: ```make build PLATFORM=HOST```

This will produce an executable demo.out, object files (\*.o), a map file (demo.map), and dependency files (\*.d).

####  2. Build for MSP432 Target
To cross-compile the application for the MSP432 embedded platform:
```make build PLATFORM=MSP432 ```

The output will be an executable demo.out, object files, map file, and dependency files for the MSP432 target.

#### 3. Preprocess Files
Generate preprocessed output for any source file using:
```make <file_name>.i PLATFORM=<PLATFORM> ```

Example for the host platform:
```make main.i PLATFORM=HOST ```

#### 4. Generate Assembly Code
To generate assembly code for any source file:
```make <file_name>.asm PLATFORM=<PLATFORM>```

Example for the MSP432 platform:
```make memory.asm PLATFORM=MSP432```

#### 5. Compile All Object Files (No Linking)
To compile all the source files into object files without linking:

``` make compile-all PLATFORM=<PLATFORM> ```
#### 6. Clean the Build Directory
To remove all generated files (executables, object files, map files, etc.):
``` make clean ```

## Acknowledgement
This is the second assignment of the [Introduction to Embedded Systems Software and Development Environments](https://www.coursera.org/learn/introduction-embedded-systems) course, available on Coursera.

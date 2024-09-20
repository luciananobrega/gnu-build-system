#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# Makefile to automate the build process
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      %.i
#      %.asm
#      %.o
#      compile-all -> Compile all object files, but DO NOT link
#      build -> Compile all object files and link into a final executable.
#      clean -> This should remove all compiled objects, preprocessed outputs, assembly outputs, executable files and build output files.
#
# Platform Overrides:
#      MSP432
#      HOST
#
#------------------------------------------------------------------------------
include sources.mk

TARGET = demo
OBJS:=$(SOURCES:.c=.o) # from sources.mk

# Architectures Specific Flags
ifeq ($(PLATFORM), MSP432)
	LINKER_FILE = ../msp432p401r.lds
	CPU = cortex-m4
	ARCH = armv7e-m
	SPECS = nosys.specs
	CC = arm-none-eabi-gcc
	LD = arm-none-eabi-ld
	LDFLAGS = -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
	CFLAGS = -mcpu=$(CPU) -mthumb -march=$(ARCH) -mfloat-abi=hard -mfpu=fpv4-sp-d16 --specs=$(SPECS) -Wall -Werror -g -O0 -std=c99
	CPPFLAGs = -DMSP432 -MD -MP
else  # for HOST, CPU and ARCH are automatically defined by gcc
	CC = gcc
	LD = ld
	CFLAGS = -Wall -Werror -g -O0 -std=c99
	CPPFLAGs = -DHOST -MD -MP
endif  


# $^ all prerequisites
# $< first prerequisite
# $@ target

%.i : %.c
	$(CC) -E $(INCLUDES) $(CFLAGS) $(CPPFLAGs) $^ -o $@

%.asm : %.c
	$(CC) -S $(INCLUDES) $(CFLAGS) $(CPPFLAGs) $^ -o $@

%.o: %.c
	$(CC) -c $(INCLUDES) $(CFLAGS) $(CPPFLAGs) $^ -o $@

$(TARGET).out: $(OBJS)
	$(CC) $(OBJS) $(INCLUDES) $(CFLAGS) $(CPPFLAGs) $(LDFLAGS) -o $@


.PHONY: build
build: $(TARGET).out

.PHONY: compile-all
compile-all: $(OBJS)

.PHONY: clean
clean:
	# rm -f $(OBJS) $(TARGET).out $(TARGET).map
	rm -f *.o *.out *.map *.d *.i *.asm


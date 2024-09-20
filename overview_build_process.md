# Building process overview

``*.c/*.h`` files -> preprocessor -> ``*.i`` files -> compiler proper -> ``*.s`` files -> assembler -> ``*.o`` files -> linker -> relocatable file -> locator -> executable

## Preprocessing (-E)
1) Preprocess only: stop after preprocessing. If -o <*.i> is not included, the file will be output on the terminal.
    ``` 
	gcc -E main.c -o main.i
    ```

2) Define what should be compiled (compile time switch)
	```
	gcc -D<MACRO-NAME> -o main.i main.c
	```

## Compiler proper (-S)
1) Preprocess and compile: this will compile but stop before linking and output the code in assembly in a file called ``main.s``.
```
	gcc -std=c99 -S main.c -o main.asm
```
We can also include the output file name (however, it seems optional, because main.s file is created anyway)
```
	gcc -std=c99 -S main.c -o main.asm
```
2) Add ``-g`` flag to include debug symbols in the ``main.s`` file
```
	gcc -std=c99 -S -g main.c
```

## Assembler (-c)
1) Preprocess, compile and assemble
```
	gcc -std=c99 -c main.c -o main.o
```

### Linker and Locator (-o)
There are multiple flags!
1) Compile, Assemble, and Link
```
	gcc -o main.out main.c
```
2) We can also use compile time switch at this step and include multiple files for the *.out file!
```
	gcc -o main.out main.c kl25z.c msp.c my_file.c -DMSP
```
3) To add options to linker from compiler, we can use -Xlinker or -Wl
```
	gcc main.c –o main.out –Xlinker –T linker_file.lds
	gcc main.c –o main.out –Wl,–T,linker_file.lds
```
Other flags include:
- ``-o [NAME]`` Place the output in the filename [NAME]
- `-Map [NAME]`` Outputs a memory map file [NAME] from the result of linking => this map provides information on how all of these regions and memory segments were used and allocated and also gives you specific addresses for the allocations.
- ``-T [NAME]`` Specifies a linker script name [NAME]
- ``-Wl,<OPTION>`` Pass option to linker from compiler
- ``-Xlinker <OPTION>`` Pass option to linker from compiler
- ``-O<#>`` The level of optimizations from [#=0-3] (-O0, -O1, -O2, -O3)
- ``-Os`` Optimize for memory size
- ``-z stacksize=[SIZE]`` The amount of stack space to reserve
- ``-shared`` Produce a shared library (dynamic linking library)
- ``-l[LIB]`` Link with shared library 
- ``-L[DIR]`` Include the following library path


### General flags
- ``-v`` verbose output
- ``-I<DIR>`` to look for header files on <DIR> directory (good to use on makefiles)
- ``-Wall`` Enable All Warning Messages (not as errors)
- ``-Werror`` Treat All Warnings as Errors
- ``-std=STANDARD`` Specify Which Standard Version to Use (ex: c89,c99)

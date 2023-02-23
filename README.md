# stm32-hal-blink-minimal

This is a minimal project for the STM32 Blue Pill to blink the built-in LED. It
does not rely on STM32CubeIDE allowing the usage of more advanced IDEs.

Although this project specifically targets the Blue Pill, it can be modified to
work on any other STM board by modifying the top section of the Makefile and
adding the appropriate submodule to the `vendor` folder.

This project can be built and flashed using `make`.

```sh
$ make
[CC]      main.c 
[CC]      syscalls.c 
[LD]      build/main.elf 
[OBJDUMP] build/main.lst 
[SIZE]    build/main.elf 
   text    data     bss     dec     hex filename 
   3152      28    1976    5156    1424 build/main.elf 
[OBJCOPY] build/main.hex
```

For flashing, `openocd` and `st-flash` are required.

```sh
$ make flash
openocd -f interface/stlink-v2.cfg -f target/stm32f1x.cfg \ 
    -c "program build/main.elf verify reset exit" 
Open On-Chip Debugger 0.11.0 
Licensed under GNU GPL v2 
For bug reports, read 
    http://openocd.org/doc/doxygen/bugs.html 
WARNING: interface/stlink-v2.cfg is deprecated, please switch to interface/stlink.cfg 
Info : auto-selecting first available session transport "hla_swd". To override use 'transport select <transport>'. 
Info : The selected transport took over low-level target control. The results might differ compared to plain JTAG/SWD 
Info : clock speed 1000 kHz 
Info : STLINK V2J40S7 (API v2) VID:PID 0483:3748 
Info : Target voltage: 3.214943 
Info : stm32f1x.cpu: hardware has 6 breakpoints, 4 watchpoints 
Info : starting gdb server for stm32f1x.cpu on 3333 
Info : Listening on port 3333 for gdb connections 
target halted due to debug-request, current mode: Thread 
xPSR: 0x01000000 pc: 0x08000bc8 msp: 0x200027fc 
** Programming Started ** 
Info : device id = 0x10006412 
Info : flash size = 32kbytes 
** Programming Finished ** 
** Verify Started ** 
** Verified OK ** 
** Resetting Target ** 
shutdown command invoked
```

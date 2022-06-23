---
processors: ["Cortex-A73", "Cortex-A53"]
tools: ["Fastmodels"] 
softwares: ["bare-metal"]
title: "Modifying your first bare-metal embedded program to use the UART as the output mechanism"
linkTitle: "Modify your first embedded image to use the UART for printf output"
type: docs
description: >
    This guide shows you how to modify the output mechanism to use the UART capability of the target system.
---

## Overview 

In [Build and run your first embedded image](/pre-silicon/bm-software/build-bm.md), we relied on semihosting to handle the output from our embedded image. In this guide, you will modify the output mechanism to send output to a UART serial port. This is useful to know, because embedded systems often have limited display capabilities, or no display capabilities. However, during the debug process it is often useful to be able to print diagnostic messages while a program is running.
## Pre-requisites

Tools: 
  * [Arm Compiler for Embedded](/compilers/install_armclang)

  * [Arm Fixed Virtual Platforms](https://developer.arm.com/Tools%20and%20Software/Fixed%20Virtual%20Platforms)

## Detailed Steps


### Understanding Semihosting

Semihosting enables code running on a target system, the model, to interface with a debugger running on a host system, the computer, and to use its input and output (I/O) facilities. This means that you can interact with a model or microcontroller that may not possess I/O functionality.

In [Build and run your first embedded image](/pre-silicon/bm-software/build-bm.md), we used a `printf()` call in the code to display the "Hello World" message. This printf() call triggers a request to a connected debugger through the library function `_sys_write.` To see how this works, you can use fromelf to inspect the compiled code, as shown in the following instruction:

```
$ fromelf --text -c __image.axf --output=disasm.txt
```

This command generates a disassembly of `__image.axf` in the file disasm.txt. Within the disassembly, look at `_sys_write`, which contains a `HLT` instruction:

```
_sys_write
    0x00003a74:    d100c3ff    ....    SUB      sp,sp,#0x30
    0x00003a78:    a9027bfd    .{..    STP      x29,x30,[sp,#0x20]
    ...
    0x00003a9c:    d45e0000    ..^.    HLT      #0xf000
    ...
    0x00003aa8:    d65f03c0    .._.    RET
```

The debugger detects this halt as a semihosting operation, and interprets the `_sys_write` as a request to output to the console.

You can check if you are using semihosting by adding `__asm(".global __use_no_semihosting\n\t");` to `main()`. Linking the image will now throw an error for any functions that use semihosting.


### Retarget functions to use the UART

Real embedded systems operate without sophisticated debuggers, but many library functions depend on semihosting. You must modify, or retarget, these functions to use the hardware of the target instead of the host system.

To retarget `printf()` to use the PL011 UART of the model:

1. Write a driver for the UART. Copy and paste the following code into a new file with the filename `pl011_uart.c`:

```
struct pl011_uart {
    volatile unsigned int UARTDR;        // +0x00
    volatile unsigned int UARTECR;       // +0x04
    const volatile unsigned int unused0[4];    // +0x08 to +0x14 reserved
    const volatile unsigned int UARTFR;        // +0x18 - RO
    const volatile unsigned int unused1;       // +0x1C reserved
    volatile unsigned int UARTILPR;      // +0x20
    volatile unsigned int UARTIBRD;      // +0x24
    volatile unsigned int UARTFBRD;      // +0x28
    volatile unsigned int UARTLCR_H;     // +0x2C
    volatile unsigned int UARTCR;        // +0x30
    volatile unsigned int UARTIFLS;      // +0x34
    volatile unsigned int UARTIMSC;      // +0x38
    const volatile unsigned int UARTRIS;       // +0x3C - RO
    const volatile unsigned int UARTMIS;       // +0x40 - RO
    volatile unsigned int UARTICR;       // +0x44 - WO
    volatile unsigned int UARTDMACR;     // +0x48
};

// Instance of the dual timer
struct pl011_uart* uart;

// ------------------------------------------------------------
void uartInit(void* addr) {
    uart = (struct pl011_uart*) addr;
    // Ensure UART is disabled
    uart->UARTCR  = 0x0;
    // Set UART 0 Registers
    uart->UARTECR   = 0x0;  // Clear the receive status (i.e. error) register
    uart->UARTLCR_H = 0x0 | PL011_LCR_WORD_LENGTH_8 | PL011_LCR_FIFO_DISABLE | PL011_LCR_ONE_STOP_BIT | PL011_LCR_PARITY_DISABLE | PL011_LCR_BREAK_DISABLE;
    uart->UARTIBRD = PL011_IBRD_DIV_38400;
    uart->UARTFBRD = PL011_FBRD_DIV_38400;
    uart->UARTIMSC = 0x0;                     // Mask out all UART interrupts
    uart->UARTICR  = PL011_ICR_CLR_ALL_IRQS;  // Clear interrupts
    uart->UARTCR  = 0x0 | PL011_CR_UART_ENABLE | PL011_CR_TX_ENABLE | PL011_CR_RX_ENABLE;
    return;
}

// ------------------------------------------------------------
int fputc(int c, FILE *f) {
    // Wait until FIFO or TX register has space
    while ((uart->UARTFR & PL011_FR_TXFF_FLAG) != 0x0) {}
    // Write packet into FIFO/tx register
    uart->UARTDR = c;
    // Model requires us to manually send a carriage return
    if ((char)c == '\n') {
        while ((uart->UARTFR & PL011_FR_TXFF_FLAG) != 0x0){}
        uart->UARTDR = '\r';
    }
   return 0;
}

```
    
2 Modify `hello_world.c` to use the UART driver, so that the updated file contains:

```
#include <stdio.h>
#include "pl011_uart.h"

int main (void) {
  uartInit((void*)(0x1C090000));
  printf("hello world\n");
  return 0;
}
```

By redefining `fputc()` to use the UART you have retargeted `printf()`. This is because `printf()` ultimately calls `fputc()`.

3. Rebuild the image:

```
$ armclang -c -g --target=aarch64-arm-none-eabi startup.s
$ armclang -c -g --target=aarch64-arm-none-eabi hello_world.c
$ armclang -c -g --target=aarch64-arm-none-eabi pl011_uart.c
$ armlink --scatter=scatter.txt --entry=start64 startup.o pl011_uart.o hello_world.o

```
4. Disassemble the image:

```
$ fromelf --text -c __image.axf --output=disasm.txt

```

The disassembly in disasm.txt now shows no calls to `_sys_write` (although other semihosting functions such as _sys_exit will be present).

### Use Telnet to interface with the UART

All output is now directed to the model's UART serial port.

To see this output, we are going to use a Telnet Terminal to connect to the UART.

We will now launch the simulation model with the newly compiled image. 

```
$ FVP_Base_Cortex_A73x2_A53x4 -a __image.axf

```

You will see a telnet terminal pop-up with you run the simulation model with the output "hello world"

```

---
title: "8 Bit Laptop: Bank Switching Memory"
date: 2018-04-12T14:40:53+10:00
draft: false
---

I have been trying to wrap my head around exactly how the 74LS610 Memory Management Chip will work in my Hackaday Prize competition entry. There is not a lot of complete documentation on exactly how to implement the 74LS610. So, ultimately, I decided to scrap using the chip, and I decided to use a simpler and more rough-and-ready solution to how to extend the memory of this internet-enabled 8 bit laptop I am building.

I did some searching, and I found a solution I can actually understand: [http://www.zcontrol.narod.ru/diagrams/ZramBankSwitch.pdf](http://www.zcontrol.narod.ru/diagrams/ZramBankSwitch.pdf).

This document outlines how to extend the ROM of a computer to 128K bytes, and the RAM to 512K bytes. This is the schematic:

![Bank Switching Schematic](/8-bit-laptop/z80_bankswitch.png)

The incredible benefit of this solution is that it minimises the amount of programming needed in order to switch banks of ROM and RAM.

## Selecting Between the ROM and RAM

The implementation uses one half of a 74HCT139 decoder to select between the ROM and RAM. When A15 is high, RAM is selected; when A15 is low, ROM is selected. A15 is gated with /MREQ to assure that the memory chips are enabled only when the bus access is for memory, and only when the address lines are stable.

## The Bank Switch Latch

As the document outlines, a 74HCT273 eight-bit latch serves as the bank switch latch. Because this circuit is intended for a Z80 processor, the circuit requires the user to output bank switch information with a Z80 OUT instruction, which would generate the output strobe /BANK. Because we are using a 6502, I imagine we could do that with the VIA. 

The document specifies that a 74HCT138 or similar part (not shown in this schematic) would interface with the Z80 processor to recieve an OUT opcode to generate the bank switch strobe and other needed I/O strobes. At power-on, the /RESET signal resets all the bank switches to zero.

## The Eight AND Gates

The latched bank switch output signals, BS0 through BS7, are connected to one input of each of eight 74HCT08 AND gates. The outputs of these gates are used to generate extra address lines for the ROM and RAM chips—three for the ROM, and five for the RAM.

## Using A14 to Gate the Bank Switching

Each of the eight 74HCT08 AND gates has its other input tied to Z80 address line A14. When A14 is high, the extra address lines will follow the values latched in the 74HCT273 bank switch latch. When A14 is low, the extra address lines will all be set low, regardless of the values latched in the bank switch latch. However the last values stored in the bank switch latch remain there, ready for the next access
to a bank-switched memory area.

## Very Simple!

As you can see, this is a very simple solution to what could be a complex problem. Using the VIA chip already being used in this design, and just by using A14 and A15 of the 6502, we are able to increase our total ROM addressable to 128K bytes, and RAM to 512K bytes. I think this will be sufficient.

## The Memory Map

The document we are working with specifies this as the memory map of the design:

![The Design Memory Map](/8-bit-laptop/z80_bankswitch_memorymap.png)

There are four areas in the memory map. The power of this design is that there are 16K bytes each of ROM and RAM which are base ROM and RAM. This means that these areas are not switched out upon switching banks, which means permament program information can be stored in these banks, which is very useful. I imagine we can section of parts of these 16K byte areas for IO. The stack can be located in the base RAM area, and the reset vectors needed for the 6502 can be located in the base ROM area.

### A Bank Switch Shadow

There will need to be an area in the base RAM area which shadows the state of the bank switch latch. This is so the operating system of the computer can keep track of the state of the bank switch latch. This will be useful for multi-tasking applications.

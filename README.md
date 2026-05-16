# MOS Technology 6502 Homebrew System

This project is a modular homebrew computer system based on the 
:contentReference[oaicite:0]{index=0} CPU.

## 🔧 Overview

The main goal of this project was to design and build a highly modular and 
expandable hardware platform, allowing future system extensions depending 
on project requirements.

The system supports both CMOS and NMOS variants of the 6502 CPU.

## ⚙️ Hardware Design

The main board includes:
- clock generator and RESET circuitry
- PAL-based control logic for address decoding
- fully buffered address and data buses
- EPROM emulator support via DIP socket replacement
- UART and PIO interfaces
- additional input port based on 74HCT245

The design also implements RAM banking using a 74HCT174 flip-flop.
Three outputs are used for bank selection, while the remaining are reserved 
for user-defined functions. The register is cleared on power-up and defaults 
to the primary RAM bank.

All address and control signals are routed to a goldpin header for expansion 
and debugging purposes.

## 🧠 Memory Map

- `$0000–$7FFF` — primary RAM  
- `$8000–$BFFF` — additional RAM (banked)  
- `$C000–$FFFF` — ROM  
  - includes a dedicated 256-byte I/O page

The full 64 KB address space is decoded using two PAL devices:
- upper-level address decoding (256-byte granularity)
- dedicated I/O decoding logic

## 🚀 Boot Process

The system starts execution from the RESET vector (`$FFFC–$FFFD`).
After initialization, it jumps to `$C000`, where the bootloader resides.

The bootloader provides basic ROM-based routines and waits for a program 
to be transferred via UART (RS232 protocol). The binary is loaded directly 
into RAM, after which execution is transferred to the loaded program.

## 📁 Documentation
The full schematic of the board is included in the repository.

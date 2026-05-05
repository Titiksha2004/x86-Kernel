
# x86 Bootloader in Assembly

## Overview

I implemented a **minimal x86 bootloader in 16-bit assembly** that runs directly in real mode on BIOS-based systems. It initializes memory segments and stack, uses BIOS interrupts for screen control, and prints a message to demonstrate low-level hardware interaction without an operating system.

## Features

* **Explicit Segment & Stack Setup**
  Initializes `DS`, `SS`, and `SP` for controlled execution after BIOS handoff.

* **BIOS Interrupt Integration**
  Uses `int 0x10` for:

  * Clearing the screen
  * Moving the cursor
  * Printing characters

* **Modular Subroutines**

  * `clearscreen` — clears the display
  * `movecursor` — positions the cursor
  * `print` — outputs a null-terminated string

* **Boot Sector Compliance**

  * Fits within 512 bytes
  * Ends with required boot signature `0xAA55`

## How It Works

1. BIOS loads the boot sector at `0x7C00`
2. Execution begins in 16-bit real mode
3. The bootloader:

   * Sets up memory segments and stack
   * Clears the screen
   * Moves cursor to the top-left
   * Prints a string character-by-character
4. CPU execution halts

## Build & Run

### Assemble

```bash
nasm -f bin bootloader.asm -o bootloader.bin
```

### Run (QEMU)

```bash
qemu-system-x86_64 -drive format=raw,file=bootloader.bin
```

## Key Concepts

* Real-mode x86 programming
* BIOS interrupt handling
* Stack frames and calling conventions
* Boot sector structure
* Low-level memory control

## Limitations

* Single-stage bootloader
* No input handling or filesystem support
* BIOS-only (no UEFI support)

## Future Improvements

* Add keyboard input
* Load a second-stage bootloader
* Switch to protected mode
* Basic kernel loading

---

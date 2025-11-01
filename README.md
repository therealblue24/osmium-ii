# Osmium-II Microprocessor

16-bit microprocessor with a 24-bit address bus and a 16-bit data bus.

todo...

## Features

- 16 16-bit general purpose registers
- 4 16-bit segment registers

todo...

## Building and Running Emulator

To build the emulator, go to `emu-src/` and execute `make all` in the shell. The
executable should appear as `build/osmium-ii-emu`. To start it up immediately,
execute `make run`. You can delete the build folder using `make clean`.

## Building and Running Assembler

To build the assembler, go to `asm/` and execute `make`. The executable should appear as `bin/osmium-ii-as`. To use the assembler, simply pass the assembly file as first argument to assemble to `a.out`.

For more options check the documentation.

## Documentation and Resources

All documentation and resources are in `docs/`.

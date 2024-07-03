# Nanoprocessor Project

This project is part of the CS1050 Computer Architecture module, where we developed a nanoprocessor using VHDL on a Basys 3 board.

## Features

The nanoprocessor is capable of executing the following four instructions:
1. **Move** 
2. **Add**
3. **Jump**
4. **Negate**

## Components

- **Program ROM**: Instructions are hard-coded into the Program ROM.
- **Instruction Decoder**: Decodes the instructions for execution.
- **Adder/Subtractor**: A 4-bit unit connected through separate data buses to the register bank through two 8-way 4-bit Multiplexers.
- **Multiplexers**: Used to select appropriate data inputs.
- **Program Counter**: Keeps track of the instruction sequence.
- **Register Bank**: Acts as temporary memory storage.

## Testing

Each component of the nanoprocessor was tested separately using timing diagrams to ensure proper functionality.

## Usage

This repository contains the VHDL code for the nanoprocessor. To run the project on a Basys 3 board, follow these steps:

1. Clone the repository.
2. Open the project in Vivado Xilinx.
3. Synthesize the design.
4. Program the Basys 3 board with the synthesized bitstream.

## Contributing

S.M.A.N.A.Manchanayake - 210373G
Department of Computer Science & Engineering,
Faculty of Engineering,
University of Moratuwa.

K.C.K.Manawathilake - 210372D
Department of Computer Science & Engineering,
Faculty of Engineering,
University of Moratuwa.


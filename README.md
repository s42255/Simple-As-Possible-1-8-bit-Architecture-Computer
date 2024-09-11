# SAP-1 Architecture-based 8-bit Computer Design and Implementation

This project focuses on the design and implementation of a simple 8-bit computer system based on the SAP-1 (Simple as Possible) architecture. The SAP-1 computer consists of key modules such as a program counter, RAM, clock pulse generator, input/output units, accumulator, and an arithmetic logic unit (ALU). Below, we walk through the key components, design steps, and challenges faced during the software simulations.

## Project Overview
The SAP-1 computer consists of multiple stages, each contributing to the development of a functional 8-bit computer. Key components include:

1. **Program Counter (PC)**
   The program counter is a 4-bit counter responsible for addressing the next instruction in memory. It counts from `0000` to `1111` and increments after every instruction cycle. The clock pulse triggers the PC to fetch the next instruction from RAM.

2. **Memory Address Register (MAR)**
   The MAR is used to store the 4-bit address of data or instructions from RAM. In the RUN state, the PC sends addresses to the MAR, which then retrieves the corresponding instructions or data from RAM.

3. **Random Access Memory (RAM)**
   A 16 x 8-bit RAM was implemented to store data and instructions. The RAM receives a 4-bit address from the MAR and either stores or outputs an 8-bit data value. The RAM operates in either READ or WRITE mode based on external control signals.

4. **Instruction Register (IR)**
   The IR stores the 8-bit instructions fetched from RAM. These instructions are split into two parts: the upper nibble (opcode) goes to the controller sequencer, while the lower nibble is placed on the bus for execution.

5. **Controller Sequencer**
   The controller sequencer generates control signals that synchronize and direct the operation of each component. It ensures that all subsystems act in coordination by providing 12 control signals, such as loading data into the registers or enabling data transfer across the bus.

6. **Arithmetic Logic Unit (ALU)**
   The ALU processes arithmetic operations based on the instructions in the IR. It takes inputs from the accumulator and a B register to perform additions or subtractions.

7. **Clock Pulse Generator**
   The clock synchronizes operations by generating a continuous signal. The clock has two modes: automatic and manual. The automatic mode uses an astable multivibrator circuit, while the manual mode uses a monostable multivibrator, each implemented using a 555 timer IC.

8. **Accumulator and B Register**
   These 8-bit registers store the results of arithmetic operations. The accumulator holds intermediate results, while the B register provides inputs to the ALU.

9. **Output Register**
   The output register stores the final result of operations and displays the output when required.

## Design and Implementation

### Software Simulation
The system was simulated using Proteus software. The RAM, registers, and control circuits were tested in simulation to verify their behavior before proceeding with a full-scale virtual implementation. Each module was designed to transfer data between registers, manipulate data within the ALU, and manage timing using the clock pulse generator.

### Instruction Set and Execution Cycle
The SAP-1 computer supports five basic instructions: `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`. Each instruction follows a six-step instruction cycle, consisting of three fetch cycles and three execution cycles:

1. **Fetch Cycle** (T1-T3)
    - The instruction is fetched from RAM and stored in the instruction register.
    - The program counter is incremented.

2. **Execution Cycle** (T4-T6)
    - Based on the opcode, the instruction is executed. For example, the `LDA` instruction loads a value from RAM into the accumulator, while `ADD` and `SUB` perform arithmetic operations using the ALU.

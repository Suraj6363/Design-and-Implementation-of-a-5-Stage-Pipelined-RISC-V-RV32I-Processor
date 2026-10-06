# Design and Implementation of a 5-Stage Pipelined RISC-V RV32I Processor

A modular Verilog RTL implementation of a five-stage pipelined RISC-V RV32I processor with data forwarding, load-use hazard detection, pipeline stalling, control-hazard flushing, and self-checking functional verification.

---

## 📌 Overview

### 📖 What is RISC-V?

RISC-V is an open and royalty-free Instruction Set Architecture (ISA) that defines the instructions and programmer-visible behaviour of a processor.

### 🔢 What is RV32I?

RV32I is the 32-bit base integer instruction set of RISC-V.

---

## 🧠 Why RISC-V in This Project?

...

---

## 🎯 Objectives

- Design a five-stage pipelined RV32I processor in Verilog HDL.
- Implement a modular processor datapath and control logic.
- Implement data forwarding between pipeline stages.

---

## ✨ Key Features

### ALU Operations

- ADD
- SUB
- AND
- OR
- XOR
- SLL
- SRL
- SRA
- SLT
- SLTU

### I-Type Arithmetic

- ADDI
- ANDI
- XORI
- ORI

---

## 🏗️ Processor Architecture

...

---

## 🧩 RTL Module Description

...

---

## ⚙️ Working Principle

...

---

## 🧠 Instruction Support

### R-Type

| Instruction | Operation |
|---|---|
| ADD | Addition |
| SUB | Subtraction |
| AND | Bitwise AND |
| OR | Bitwise OR |

### I-Type Arithmetic

...

---

## 🔁 Hazard Handling

### Data Forwarding

...

### Load-Use Hazard

...

### Control Hazard

...

---

## 💻 Implementation Details

### ALU

...

### Immediate Generator

...

### Register File

...

### Branch / Jump Address Calculation

...

### Write-Back

...

---

## 🧪 Verification and Testing

...

---

## 📊 Results

| Verification Item | Result |
|---|---|
| R-type arithmetic and logical instructions | PASS |
| I-type arithmetic instructions | PASS |
| Load instructions | PASS |
| Store instructions | PASS |
| Load-use hazard and one-cycle stall | PASS |
| Taken branch and pipeline flush | PASS |
| JAL | PASS |
| JALR | PASS |
| LUI | PASS |
| AUIPC | PASS |
| x0 hard-wired-zero behaviour | PASS |
| **Total architectural checks** | **31 / 31 PASS** |

---

## 🔍 Challenges and Solutions

### Challenge 1 — Same-Cycle Register-File Read/Write Collision

...

### Challenge 2 — AUIPC Result Path

...

---

## 🛠️ Technologies and Tools

...

---

## 📂 Project Structure

...

---

## 🚀 How to Run

...

---

## 📋 Requirements

### Software

...

### Hardware

...

---

## ⚠️ Current Scope and Limitations

...

---

## 📈 Future Improvements

...

---

## 📚 Learning Outcomes

...

---

## 📄 Project Documentation

...

---

## 👨‍💻 Author

**Suraj Madiwal**

**Project Domain:** RTL Design

**Project Period:** May 2026 – July 2026

**Organization / Program:** SURE Trust – IERY

---

## ⭐ Conclusion

...
Design and Implementation of a 5-Stage Pipelined RISC-V RV32I Processor

A modular Verilog RTL implementation of a five-stage pipelined RISC-V RV32I processor with data forwarding, load-use hazard detection, pipeline stalling, control-hazard flushing, and self-checking functional verification.

📌 Overview

📖 What is RISC-V?

RISC-V is an open and royalty-free Instruction Set Architecture (ISA) that defines the instructions and programmer-visible behaviour of a processor.

Because the ISA is openly specified, RISC-V can be used for education, research, embedded systems, processor development, and other hardware applications without requiring a proprietary instruction-set licence.

🔢 What is RV32I?

RV32I is the 32-bit base integer instruction set of RISC-V.

RV → RISC-V

32 → 32-bit architecture

I → Base Integer Instruction Set

The RV32I base instruction set provides fundamental operations for integer computation, memory access, control flow, and data movement.

This project implements a selected subset of RV32I instructions using Verilog RTL.

Instruction Type

Implemented Instructions

R-Type

ADD, SUB, AND, OR, XOR, SLL, SRL, SRA, SLT, SLTU

I-Type

ADDI, ANDI, XORI, ORI

Load

LB, LH, LW, LBU, LHU

Store

SB, SH, SW

Branch

BEQ, BNE, BLT, BGE

Jump

JAL, JALR

U-Type

LUI, AUIPC

🧠 Why RISC-V in This Project?

RISC-V provides a practical architecture for studying processor design at RTL level. In this project, the RISC-V instruction formats and operations are translated into a modular processor datapath and control system.

A RISC-V instruction passes through the processor as follows:

Fetch the instruction using the Program Counter.

Decode the instruction and generate control signals.

Read the required operands from the register file.

Execute the operation using the ALU or branch logic.

Access memory for load/store instructions when required.

Write back the final result to the register file.

These operations are overlapped using the five-stage pipeline:

Instruction Fetch → Instruction Decode → Execute → Memory Access → Write-Back

This project implements and functionally verifies a classic five-stage pipelined processor based on the RISC-V RV32I base integer instruction set.

The processor is organized into the standard pipeline stages:

IF → ID → EX → MEM → WB

The design supports R-type and I-type arithmetic instructions, loads, stores, conditional branches, jumps, and U-type instructions. The pipeline includes forwarding logic for data hazards, load-use stall detection, and flushing for taken branches and jumps.

The RTL was developed as independent Verilog modules and integrated through a top-level processor datapath. Functional verification was performed with a self-checking testbench.

🎯 Objectives

Design a five-stage pipelined RV32I processor in Verilog HDL.

Implement a modular processor datapath and control logic.

Implement data forwarding between pipeline stages.

Detect and handle load-use data hazards using a pipeline stall.

Handle control hazards using pipeline flushing.

Support the targeted RV32I instruction classes.

Develop a self-checking verification environment.

Debug functional failures using cycle-by-cycle pipeline analysis.

Validate architectural register-file and data-memory results against expected values.

✨ Key Features

32-bit RV32I datapath.

Five-stage pipeline:

Instruction Fetch (IF)

Instruction Decode (ID)

Execute (EX)

Memory Access (MEM)

Write-Back (WB)

Modular Verilog RTL architecture.

ALU operations including:

ADD

SUB

AND

OR

XOR

SLL

SRL

SRA

SLT

SLTU

I-type arithmetic:

ADDI

ANDI

XORI

ORI

Load instructions:

LB

LH

LW

LBU

LHU

Store instructions:

SB

SH

SW

Conditional branches:

BEQ

BNE

BLT

BGE

Jump instructions:

JAL

JALR

U-type instructions:

LUI

AUIPC

EX-stage operand forwarding from MEM and WB stages.

Load-use hazard detection and one-cycle stalling.

Pipeline flushing for taken branches and jumps.

Register-file read-during-write bypass.

Self-checking verification with 31 architectural checks.

🏗️ Processor Architecture

The processor follows a five-stage pipeline:

                 ┌──────────────────────────────────────────────┐
Instruction ───► │ IF │──►│ ID │──►│ EX │──►│ MEM │──►│ WB │
                 └────┘   └────┘   └────┘   └─────┘   └────┘
                    │        │        │        │        │
                    │        │        │        │        └── Register File
                    │        │        │        └────────── Data Memory
                    │        │        └────────────────── ALU / Branch
                    │        └────────────────────────── Decoder / ImmGen
                    └────────────────────────────────── Program Counter

Pipeline stages

Stage

Main Function

IF

Program counter update and instruction fetch interface

ID

Instruction decoding, register-file reads, immediate generation and control generation

EX

ALU operations, operand forwarding, branch target calculation and branch decision

MEM

Load/store data-memory interface

WB

Selects the final result and writes it back to the register file

Pipeline registers transfer control and datapath information between stages.

🧩 RTL Module Description

Module

Purpose

Top_Module.v

Top-level processor integration and datapath connectivity

PC_unit.v

Program counter update, stall handling and branch/jump redirection

IF_Register.v

IF/ID pipeline register with stall and flush support

Decoder.v

Decodes opcode/function fields and generates control signals

Register_file.v

32 × 32-bit register file with x0 fixed at zero and read-during-write bypass

imm_Gen.v

Generates sign-extended immediates for I, S, B, U and J instruction formats

ID_Register.v

ID/EX pipeline register with reset and bubble insertion

ALU.v

Performs arithmetic, logical, shift and comparison operations

Imm_adder.v

Calculates PC-relative or register-relative immediate sums

Branch_unit.v

Evaluates supported branch conditions and generates branch-taken status

EX_Register.v

EX/MEM pipeline register

Store_unit.v

Generates store address, write data and byte/halfword/word write masks

Load_unit.v

Performs load-size selection and signed/unsigned extension

MEM_WB_Register.v

MEM/WB pipeline register

WB_mux.v

Selects ALU, load-data, PC+4 or immediate data for write-back

Hazard_unit.v

Detects load-use hazards, generates stalls/flushes and controls forwarding

Testbench_module.v

Provides the instruction/data-memory models and self-checking verification sequence

The top-level design includes the processor modules through Verilog include statements and connects the five pipeline stages through the associated pipeline registers.

⚙️ Working Principle

The PC unit provides the current instruction address and calculates PC + 4.

The fetched instruction and PC information are transferred through the IF/ID register.

The Decoder identifies the instruction and generates control signals.

The Register File provides source operands.

The Immediate Generator creates the required immediate value according to the instruction format.

The ID/EX register transfers the decoded control and datapath information into the Execute stage.

The Hazard Unit determines whether forwarding, stalling or flushing is required.

The ALU performs the required arithmetic, logical, shift or comparison operation.

The branch unit evaluates supported branch conditions and determines whether control flow must change.

The EX/MEM register transfers execution results and memory-control information to the Memory stage.

Load/store logic interfaces with the behavioural data-memory model.

The MEM/WB register transfers the required result toward Write-Back.

The Write-Back multiplexer selects the appropriate result source.

The selected result is written to the destination register when register write enable is asserted.

🧠 Instruction Support

R-Type

Instruction

Operation

ADD

Addition

SUB

Subtraction

AND

Bitwise AND

OR

Bitwise OR

XOR

Bitwise XOR

SLL

Logical left shift

SRL

Logical right shift

SRA

Arithmetic right shift

SLT

Signed less-than comparison

SLTU

Unsigned less-than comparison

I-Type Arithmetic

ADDI

ANDI

XORI

ORI

Load / Store

Loads: LB, LH, LW, LBU, LHU

Stores: SB, SH, SW

Branches

BEQ

BNE

BLT

BGE

Jumps

JAL

JALR

U-Type

LUI

AUIPC

🔁 Hazard Handling

Data Forwarding

The Hazard Unit provides forwarding controls for Execute-stage operands. Forwarding can select results from the Memory or Write-Back stages instead of waiting for the normal register-file write-back path.

The forwarding logic gives priority to the Memory-stage result when both Memory and Write-Back stages could provide a matching destination register.

Load-Use Hazard

A load-use dependency is detected when an instruction in the Execute stage is producing a load result required by the following instruction.

The design responds by:

Stalling the Fetch stage.

Stalling the Decode stage.

Flushing the Execute stage to insert a bubble.

This creates the required one-cycle delay before the dependent instruction continues.

Control Hazard

For taken branches and jumps:

The PC is redirected to the target address.

Younger instructions in the pipeline are flushed.

The pipeline continues from the correct control-flow target.

💻 Implementation Details

ALU

The ALU accepts two 32-bit operands and a 4-bit control signal. It supports arithmetic, logical, shift and comparison operations.

Immediate Generator

The immediate generator supports:

I-Type immediate

S-Type immediate

B-Type immediate

U-Type immediate

J-Type immediate

Register File

The processor uses 32 registers of 32 bits each.

Register x0 is maintained at zero. A read-during-write bypass is included so that a register being written in the current cycle can immediately provide the new value to a simultaneous read.

Branch / Jump Address Calculation

The immediate adder supports both:

PC + immediate

source register + immediate

This allows the datapath to support PC-relative and register-relative control-flow operations.

Write-Back

The Write-Back multiplexer selects one of the following sources:

ALU result

Load data

PC + 4

Immediate data

🧪 Verification and Testing

Functional verification was performed using a directed instruction sequence and a self-checking testbench.

The verification environment checks architectural register-file and data-memory results against expected values.

The testbench covers:

R-type arithmetic and logical operations.

I-type arithmetic operations.

Load operations.

Store operations.

Load-use hazard handling.

Branch-not-taken behaviour.

Branch-taken behaviour and pipeline flushing.

JAL.

JALR.

LUI.

AUIPC.

x0 hard-wired-zero behaviour.

Additional register-file and data-memory architectural checks.

The final verification suite contains 31 architectural checks: 28 register-file checks and 3 data-memory checks.

📊 Results

The final verified version passed all 31 self-checking architectural checks.

Verification Item

Result

R-type arithmetic and logical instructions

PASS

I-type arithmetic instructions

PASS

Load instructions

PASS

Store instructions

PASS

Load-use hazard and one-cycle stall

PASS

Taken branch and pipeline flush

PASS

JAL

PASS

JALR

PASS

LUI

PASS

AUIPC

PASS

x0 hard-wired-zero behaviour

PASS

Total architectural checks

31 / 31 PASS

Two functional defects were identified and corrected during development:

Same-cycle register-file read/write hazard:
A failure observed during the SUB test was traced through cycle-by-cycle pipeline analysis to a register-file read/write collision. A write-through bypass was added to the register file.

AUIPC datapath omission:
The AUIPC PC-relative result did not initially have a complete path to Write-Back. The datapath was extended to carry the PC + immediate result through the pipeline and into the Write-Back multiplexer.

After these corrections, all 31 architectural checks passed.

🔍 Challenges and Solutions

Challenge 1 — Same-Cycle Register-File Read/Write Collision

Problem:
A register value written in the same cycle was not being observed correctly by a simultaneous register-file read.

Root Cause:
The issue was initially associated with the SUB instruction, but signal-level pipeline tracing showed that the actual problem was a same-cycle register-file read/write collision.

Solution:
A write-through bypass was added to the register file so that newly written data is directly forwarded to a matching read address.

Challenge 2 — AUIPC Result Path

Problem:
The AUIPC instruction required a PC-relative PC + immediate result, but the required datapath path to Write-Back was missing.

Solution:
A dedicated PC-plus-immediate result path was added through the required pipeline registers and Write-Back multiplexer.

🛠️ Technologies and Tools

Category

Technology / Tool

ISA

RISC-V RV32I

HDL

Verilog HDL

RTL Design

Modular RTL architecture

Simulation / Verification

Synopsys VCS

Additional Simulation Tools

Verilator, GTKWave

Testbench

Self-checking Verilog/SystemVerilog constructs

Verification Method

Directed tests, architectural checks and pipeline monitoring

Target Domain

RTL Design / Digital Design / Computer Architecture

📂 Project Structure

The repository contains the RTL modules and testbench used for the processor implementation.

RISC-V-Processor/
├── ALU.v
├── Branch_unit.v
├── Decoder.v
├── EX_Register.v
├── Hazard_unit.v
├── ID_Register.v
├── IF_Register.v
├── Imm_adder.v
├── imm_Gen.v
├── Load_unit.v
├── MEM_WB_Register.v
├── PC_unit.v
├── Register_file.v
├── Store_unit.v
├── Testbench_module.v
├── Top_Module.v
├── WB_mux.v
└── README.md

Keep the filenames in this tree consistent with the filenames committed to the repository. If you reorganize the repository into folders such as rtl/, tb/, or docs/, update this section accordingly.

🚀 How to Run

The project report confirms simulation using Synopsys VCS and also identifies Verilator and GTKWave in the tool flow.

Because the uploaded project materials do not contain a verified final simulator command sequence, the README intentionally does not invent a command that may be incorrect for your local environment.

Recommended workflow

Clone or download the repository.

Open the project in the supported Linux/RTL simulation environment.

Compile the RTL source files together with Testbench_module.v.

Run the simulation.

Review the self-checking PASS/FAIL output.

Inspect waveforms with GTKWave when detailed pipeline debugging is required.

Simulation Command

[Add the verified Synopsys VCS or Verilator command used for this repository here]

Example repository setup

git clone <your-repository-url>
cd <your-repository-folder>

Replace <your-repository-url> and <your-repository-folder> with the actual repository details after creating the GitHub repository.

📋 Requirements

Software

Linux environment suitable for RTL simulation.

Verilog HDL support.

Synopsys VCS for the documented verification flow.

Verilator and GTKWave as applicable to the available simulation flow.

Git for repository management.

Hardware

No FPGA or ASIC hardware deployment is required for the current verified implementation.

The project report states that the current implementation is focused on RTL simulation and has not yet been taken through synthesis, timing closure, or FPGA/ASIC deployment.

⚠️ Current Scope and Limitations

The current implementation focuses on functional RTL correctness through simulation.

The project does not currently claim:

Logic synthesis.

Timing closure.

FPGA deployment.

ASIC implementation.

Synthesisable memory macros.

Instruction and data memories are modelled behaviourally within the testbench.

📈 Future Improvements

The documented future scope includes:

Carry the design through logic synthesis and FPGA deployment.

Validate timing closure and real hardware operation.

Extend the instruction set with remaining RV32I instructions such as FENCE and ECALL/EBREAK.

Add optional standard extensions such as the M multiplication/division extension.

Replace behavioural instruction/data memories with a synthesisable memory subsystem.

Add a standard memory-mapped bus interface.

Add exception and interrupt handling.

Introduce branch prediction to reduce control-hazard penalties.

📚 Learning Outcomes

This project provided practical experience in:

Verilog HDL and RTL coding.

Five-stage pipelined processor architecture.

RISC-V RV32I instruction decoding and execution.

Datapath and control-path design.

Pipeline register design.

Data forwarding.

Load-use hazard detection.

Pipeline stalling and bubble insertion.

Control-hazard flushing.

Self-checking verification.

Cycle-by-cycle simulation debugging.

Root-cause analysis of timing-dependent RTL defects.

Synopsys VCS-based functional verification.

Verilator and GTKWave-based simulation/debugging.

📄 Project Documentation

The complete project report is available separately and documents the architecture, methodology, verification process, results, challenges, learning outcomes and future scope.

👨‍💻 Author

Suraj Madiwal

Project Domain: RTL Design

Project Period: May 2026 – July 2026

Organization / Program: SURE Trust – IERY

⭐ Conclusion

This project demonstrates the design and functional verification of a modular five-stage pipelined RISC-V RV32I processor in Verilog HDL. The implementation includes instruction decoding, register-file operation, ALU processing, memory access, write-back, data forwarding, load-use hazard handling and control-hazard flushing.

The final design passed all 31 self-checking architectural tests after systematic debugging and correction of two functional defects. The project therefore provides a practical demonstration of RTL design, computer architecture, pipeline hazard handling and simulation-based verification.

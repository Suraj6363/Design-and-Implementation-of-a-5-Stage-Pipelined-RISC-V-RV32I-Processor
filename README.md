# Design and Implementation of a 5-Stage Pipelined RISC-V RV32I Processor

### A Modular Verilog RTL Processor with Data Forwarding, Load-Use Hazard Detection, Pipeline Stalling, Control-Hazard Flushing, and Self-Checking Verification

<p align="center">

![RISC-V](https://img.shields.io/badge/ISA-RISC--V%20RV32I-blue)
![Verilog](https://img.shields.io/badge/HDL-Verilog-orange)
![RTL](https://img.shields.io/badge/Design-RTL-green)
![Pipeline](https://img.shields.io/badge/Pipeline-5--Stage-purple)
![Verification](https://img.shields.io/badge/Verification-Self--Checking-success)
![Tests](https://img.shields.io/badge/Tests-31%2F31%20PASS-brightgreen)

</p>

## 🔗 Project Links

- 📂 **GitHub Repository:** [View Source Code](https://github.com/Suraj6363/Design-and-Implementation-of-a-5-Stage-Pipelined-RISC-V-RV32I-Processor)
- ▶️ **EDA Playground:** [Run RTL Simulation](https://edaplayground.com/x/fjmU)



## 📌 Project Overview

This project presents the **design and functional verification of a 32-bit, five-stage pipelined RISC-V RV32I processor** using **Verilog HDL**.

The processor is implemented using a **modular RTL architecture** consisting of independent datapath, control, pipeline-register, memory-interface, and hazard-handling modules.

The design supports:

- Arithmetic and logical operations
- Immediate operations
- Load/store instructions
- Conditional branches
- Jumps
- U-type instructions
- Data forwarding
- Load-use hazard detection
- Pipeline stalling
- Control-hazard flushing
- Register-file read-during-write bypass
- Self-checking functional verification

The final verified implementation successfully passed:

> ## ✅ 31 / 31 Architectural Checks

---

# 🧭 Table of Contents

- [Project Overview](#-project-overview)
- [What is RISC-V?](#-what-is-risc-v)
- [What is RV32I?](#-what-is-rv32i)
- [Project Objectives](#-project-objectives)
- [Key Features](#-key-features)
- [Processor Architecture](#-processor-architecture)
- [Pipeline Stages](#-pipeline-stages)
- [Instruction Set Support](#-instruction-set-support)
- [RTL Module Architecture](#-rtl-module-architecture)
- [Working Principle](#-working-principle)
- [Pipeline Hazard Handling](#-pipeline-hazard-handling)
- [Implementation Details](#-implementation-details)
- [Verification Strategy](#-verification-strategy)
- [Verification Results](#-verification-results)
- [Debugging and Challenges](#-debugging-and-challenges)
- [Technologies and Tools](#-technologies-and-tools)
- [Project Structure](#-project-structure)
- [How to Run](#-how-to-run)
- [Requirements](#-requirements)
- [Current Scope and Limitations](#-current-scope-and-limitations)
- [Future Improvements](#-future-improvements)
- [Skills Demonstrated](#-skills-demonstrated)
- [Learning Outcomes](#-learning-outcomes)
- [Project Documentation](#-project-documentation)
- [Author](#-author)
- [Conclusion](#-conclusion)

---

# 🧠 What is RISC-V?

**RISC-V** is an open and royalty-free **Instruction Set Architecture (ISA)** that defines the instructions and programmer-visible behaviour of a processor.

Because the ISA is openly specified, RISC-V can be used for education, research, embedded systems, processor development, and other hardware applications without requiring a proprietary instruction-set licence.

---

# 🔢 What is RV32I?

**RV32I** is the 32-bit base integer instruction set of RISC-V.

| Term | Meaning |
|---|---|
| **RV** | RISC-V |
| **32** | 32-bit architecture |
| **I** | Base Integer Instruction Set |

The RV32I base instruction set provides fundamental operations for:

- Integer computation
- Memory access
- Control flow
- Data movement

This project implements a **selected subset of RV32I instructions** using Verilog RTL.

---

# 🎯 Project Objectives

The primary objectives of this project were:

- Design a five-stage pipelined RV32I processor in Verilog HDL.
- Build a modular processor datapath and control system.
- Implement pipeline registers between processor stages.
- Implement data forwarding between pipeline stages.
- Detect load-use data hazards.
- Implement pipeline stalling and bubble insertion.
- Handle control hazards using pipeline flushing.
- Support the targeted RV32I instruction classes.
- Develop a self-checking verification environment.
- Debug RTL failures using cycle-by-cycle pipeline analysis.
- Validate register-file and data-memory architectural results.

---

# ✨ Key Features

## 🏗️ Processor

- 32-bit RISC-V RV32I datapath
- Five-stage pipeline
- Modular Verilog RTL architecture
- Separate datapath and control logic
- Pipeline registers between stages

## ⚙️ Execution

- Arithmetic operations
- Logical operations
- Shift operations
- Signed and unsigned comparisons
- Immediate operations
- Load/store operations
- Conditional branches
- Jumps
- U-type instructions

## 🚧 Hazard Management

- EX-stage forwarding
- MEM-stage forwarding
- WB-stage forwarding
- Load-use hazard detection
- One-cycle pipeline stall
- Bubble insertion
- Branch/jump pipeline flushing
- Register-file read-during-write bypass

## 🧪 Verification

- Directed instruction testing
- Self-checking testbench
- Architectural register checks
- Data-memory checks
- Pipeline monitoring
- Cycle-by-cycle debugging
- **31 / 31 checks passed**

---

# 🏗️ Processor Architecture

The processor follows the classic five-stage pipeline:

```text
                  ┌──────┐
                  │  IF  │
                  └──┬───┘
                     │
                     ▼
                  ┌──────┐
                  │  ID  │
                  └──┬───┘
                     │
                     ▼
                  ┌──────┐
                  │  EX  │
                  └──┬───┘
                     │
                     ▼
                  ┌──────┐
                  │ MEM  │
                  └──┬───┘
                     │
                     ▼
                  ┌──────┐
                  │  WB  │
                  └──────┘
```

### Complete Datapath View

```text
                    ┌─────────────────────┐
                    │   Program Counter   │
                    │        PC Unit      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Instruction Fetch   │
                    │        IF           │
                    └──────────┬──────────┘
                               │
                         IF / ID Register
                               │
                               ▼
             ┌────────────────────────────────┐
             │        Instruction Decode      │
             │                                │
             │  Decoder │ Register File       │
             │  ImmGen  │ Control Generation │
             └───────────────┬────────────────┘
                             │
                       ID / EX Register
                             │
                             ▼
             ┌────────────────────────────────┐
             │          Execute (EX)          │
             │                                │
             │ ALU │ Branch Unit │ Imm Adder │
             │       Forwarding Logic         │
             └───────────────┬────────────────┘
                             │
                       EX / MEM Register
                             │
                             ▼
             ┌────────────────────────────────┐
             │       Memory Access (MEM)      │
             │                                │
             │ Load Unit │ Store Unit         │
             └───────────────┬────────────────┘
                             │
                       MEM / WB Register
                             │
                             ▼
             ┌────────────────────────────────┐
             │         Write-Back (WB)        │
             │                                │
             │          WB Multiplexer        │
             └───────────────┬────────────────┘
                             │
                             ▼
                       Register File
```

---

# 🔄 Pipeline Stages

| Stage | Description |
|---|---|
| **IF — Instruction Fetch** | Program counter update and instruction fetch |
| **ID — Instruction Decode** | Instruction decoding, register reads, immediate generation and control generation |
| **EX — Execute** | ALU operations, operand forwarding, branch calculation and branch decision |
| **MEM — Memory Access** | Load/store memory interface |
| **WB — Write-Back** | Selects final result and writes it to the destination register |

The pipeline registers transfer datapath and control information between stages.

---

# 📚 Instruction Set Support

The processor implements the following targeted instruction subset.

## R-Type Instructions

| Instruction | Operation |
|---|---|
| `ADD` | Addition |
| `SUB` | Subtraction |
| `AND` | Bitwise AND |
| `OR` | Bitwise OR |
| `XOR` | Bitwise XOR |
| `SLL` | Logical left shift |
| `SRL` | Logical right shift |
| `SRA` | Arithmetic right shift |
| `SLT` | Signed less-than comparison |
| `SLTU` | Unsigned less-than comparison |

## I-Type Arithmetic

| Instruction | Operation |
|---|---|
| `ADDI` | Add immediate |
| `ANDI` | AND immediate |
| `XORI` | XOR immediate |
| `ORI` | OR immediate |

## Load Instructions

| Instruction |
|---|
| `LB` |
| `LH` |
| `LW` |
| `LBU` |
| `LHU` |

## Store Instructions

| Instruction |
|---|
| `SB` |
| `SH` |
| `SW` |

## Branch Instructions

| Instruction |
|---|
| `BEQ` |
| `BNE` |
| `BLT` |
| `BGE` |

## Jump Instructions

| Instruction |
|---|
| `JAL` |
| `JALR` |

## U-Type Instructions

| Instruction | Function |
|---|---|
| `LUI` | Load Upper Immediate |
| `AUIPC` | Add Upper Immediate to PC |

---

# 🧩 RTL Module Architecture

The processor is divided into modular RTL blocks.

| Module | Function |
|---|---|
| `Top_Module.v` | Top-level processor integration |
| `PC_unit.v` | PC update, stalls and branch/jump redirection |
| `IF_Register.v` | IF/ID pipeline register |
| `Decoder.v` | Instruction decoding and control generation |
| `Register_file.v` | 32 × 32-bit register file |
| `imm_Gen.v` | Immediate generation |
| `ID_Register.v` | ID/EX pipeline register |
| `ALU.v` | Arithmetic, logical, shift and comparison operations |
| `Imm_adder.v` | Immediate address/result calculations |
| `Branch_unit.v` | Branch condition evaluation |
| `EX_Register.v` | EX/MEM pipeline register |
| `Store_unit.v` | Store address, data and write-mask generation |
| `Load_unit.v` | Load-size selection and sign/zero extension |
| `MEM_WB_Register.v` | MEM/WB pipeline register |
| `WB_mux.v` | Write-back result selection |
| `Hazard_unit.v` | Hazard detection, forwarding, stalls and flushes |
| `Testbench_module.v` | Instruction/data-memory models and verification |

---

# ⚙️ Working Principle

The processor executes instructions through the following sequence.

### 1️⃣ Fetch

The PC Unit provides the current instruction address and calculates `PC + 4`.

### 2️⃣ Decode

The Decoder identifies the instruction and generates the required control signals.

### 3️⃣ Register Read

The Register File provides the source operands.

Register `x0` is permanently maintained at zero.

### 4️⃣ Immediate Generation

The Immediate Generator produces the required immediate value according to the instruction format.

Supported formats:

```text
I-Type
S-Type
B-Type
U-Type
J-Type
```

### 5️⃣ Execute

The ALU performs the required arithmetic, logical, shift or comparison operation.

The Branch Unit handles supported branch conditions.

### 6️⃣ Memory Access

Load and store operations interact with the behavioural data-memory model.

### 7️⃣ Write-Back

The Write-Back multiplexer selects the appropriate result and writes it to the destination register.

Possible write-back sources include:

```text
ALU Result
Load Data
PC + 4
Immediate Data
```

---

# 🔁 Pipeline Hazard Management

Pipeline hazards are one of the major challenges in a pipelined processor.

This project handles hazards using:

```text
┌─────────────────────────────┐
│       Hazard Unit           │
├─────────────────────────────┤
│ Data Forwarding             │
│ Load-Use Detection          │
│ Pipeline Stall              │
│ Bubble Insertion            │
│ Control-Hazard Flush        │
└─────────────────────────────┘
```

---

## 🔀 Data Forwarding

When an instruction requires a result that has not yet reached the Register File, the required value can be forwarded from a later pipeline stage.

The forwarding logic can select results from:

```text
MEM → EX
WB  → EX
```

When both stages provide a matching destination register, the **Memory-stage result receives priority**.

This reduces unnecessary pipeline stalls.

---

# ⏸️ Load-Use Hazard

A load-use hazard occurs when a load instruction produces data that is immediately required by the next instruction.

The processor responds by:

```text
1. Stall IF
2. Stall ID
3. Flush EX
4. Insert one-cycle bubble
```

Example:

```text
Instruction N       : LW
Instruction N + 1   : ADD   ← Depends on loaded data
                         ↓
                    Hazard Detected
                         ↓
                     1-Cycle Stall
```

The dependent instruction then continues after the required delay.

---

# 🚦 Control Hazards

For taken branches and jumps:

```text
Branch / Jump
     │
     ▼
Target Address Calculation
     │
     ▼
PC Redirect
     │
     ▼
Flush Younger Instructions
     │
     ▼
Continue from Target
```

This prevents incorrectly fetched instructions from modifying the architectural state.

---

# 💻 Important RTL Components

## ALU

The ALU accepts two 32-bit operands and a 4-bit control signal.

It supports:

- Arithmetic
- Logical operations
- Shifts
- Signed comparison
- Unsigned comparison

---

## Register File

The processor contains:

```text
32 × 32-bit Registers
```

Register `x0` is hard-wired to zero.

A **read-during-write bypass** allows newly written register data to be immediately available to a simultaneous read.

---

## Immediate Generator

The Immediate Generator supports:

```text
I-Type
S-Type
B-Type
U-Type
J-Type
```

---

## Branch / Jump Address Calculation

The immediate adder supports:

```text
PC + Immediate
```

and:

```text
Register + Immediate
```

This enables PC-relative and register-relative control-flow operations.

---

# 🧪 Verification Strategy

Functional verification was performed using a **directed instruction sequence and a self-checking testbench**.

The testbench verifies architectural results rather than relying only on waveform inspection.

### Verification Areas

- R-Type arithmetic
- R-Type logical operations
- I-Type arithmetic
- Load instructions
- Store instructions
- Load-use hazards
- Branch-not-taken behaviour
- Branch-taken behaviour
- Pipeline flushing
- JAL
- JALR
- LUI
- AUIPC
- x0 behaviour
- Register-file results
- Data-memory results

---

# 📊 Verification Results

## 🏆 Final Result

```text
╔══════════════════════════════════════╗
║      FINAL VERIFICATION RESULT       ║
╠══════════════════════════════════════╣
║                                      ║
║       31 / 31 CHECKS PASSED         ║
║                                      ║
║       Register Checks : 28 PASS      ║
║       Memory Checks   :  3 PASS      ║
║                                      ║
║       TOTAL           : 31 PASS      ║
║                                      ║
╚══════════════════════════════════════╝
```

| Verification Item | Result |
|---|---|
| R-Type arithmetic and logical instructions | ✅ PASS |
| I-Type arithmetic instructions | ✅ PASS |
| Load instructions | ✅ PASS |
| Store instructions | ✅ PASS |
| Load-use hazard and one-cycle stall | ✅ PASS |
| Taken branch and pipeline flush | ✅ PASS |
| JAL | ✅ PASS |
| JALR | ✅ PASS |
| LUI | ✅ PASS |
| AUIPC | ✅ PASS |
| x0 hard-wired-zero behaviour | ✅ PASS |
| **Total Architectural Checks** | **✅ 31 / 31 PASS** |

---

# 🐛 Debugging and Challenges

During development, two important functional defects were identified and corrected.

## Challenge 1 — Register-File Read/Write Collision

### Problem

A register written in the same cycle was not being observed correctly by a simultaneous register-file read.

### Investigation

The issue initially appeared during the `SUB` test.

Cycle-by-cycle pipeline analysis and signal tracing showed that the actual root cause was a **same-cycle register-file read/write collision**.

### Solution

A **write-through bypass** was implemented in the Register File.

```text
Register Write
      │
      ├──────────────► Register Storage
      │
      └──────────────► Read Bypass
                         │
                         ▼
                     Read Data
```

---

# 🐛 Challenge 2 — AUIPC Result Path

### Problem

`AUIPC` requires:

```text
PC + Immediate
```

but the required result path to Write-Back was initially incomplete.

### Solution

A dedicated PC-plus-immediate datapath was added through the required pipeline registers and Write-Back multiplexer.

### Final Result

After both corrections:

```text
31 / 31 Architectural Checks → PASS
```

---

# 🛠️ Technologies and Tools

| Category | Technology |
|---|---|
| ISA | RISC-V RV32I |
| HDL | Verilog HDL |
| Design Methodology | Modular RTL Design |
| Simulation | Synopsys VCS |
| Additional Simulation | Verilator |
| Waveform Analysis | GTKWave |
| Verification | Self-Checking Testbench |
| Verification Method | Directed Testing + Architectural Checks |
| Domain | RTL Design / Digital Design / Computer Architecture |

---

# 📂 Project Structure

```text
RISC-V-Processor/
│
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
│
└── README.md
```

> Keep this structure synchronized with the actual files committed to the repository.

---

# 🚀 How to Run

The documented project flow uses **Synopsys VCS**, with **Verilator** and **GTKWave** also identified as additional simulation/debugging tools.

Since the available project materials do not contain a verified final simulator command sequence, an incorrect command is intentionally not provided here.

## Recommended Workflow

### 1. Clone the Repository

```bash
git clone <your-repository-url>
```

### 2. Enter the Project Directory

```bash
cd <your-repository-folder>
```

### 3. Compile the RTL

Compile the RTL source files together with:

```text
Testbench_module.v
```

### 4. Run Simulation

Run the simulation using the supported RTL simulator.

### 5. Verify Results

Check the self-checking `PASS / FAIL` output.

### 6. Debug Waveforms

Use GTKWave when detailed pipeline and signal-level debugging is required.

## ▶️ Run on EDA Playground

The processor RTL can also be simulated online using the provided EDA Playground environment.

👉 **[Open EDA Playground Simulation](https://edaplayground.com/x/fjmU)**

The EDA Playground setup contains the required RTL and testbench files for functional simulation.

After running the simulation:

- Check the console output for `PASS / FAIL` results.
- Verify the final **31 / 31 Architectural Checks PASS** result.
- Use the waveform viewer for cycle-by-cycle signal analysis when required.

---

# 📋 Requirements

## Software

- Linux environment suitable for RTL simulation
- Verilog HDL support
- Synopsys VCS
- Verilator
- GTKWave
- Git

## Hardware

No FPGA or ASIC hardware deployment is required for the current verified implementation.

The current project focuses on **RTL simulation and functional verification**.

---

# ⚠️ Current Scope and Limitations

The current implementation focuses on **functional RTL correctness through simulation**.

The project does not currently claim:

- Logic synthesis
- Timing closure
- FPGA deployment
- ASIC implementation
- Synthesisable memory macros

The instruction and data memories are modelled behaviourally within the testbench.

---

# 📈 Future Improvements

## 🔧 Hardware Implementation

- Logic synthesis
- FPGA deployment
- Timing-closure analysis
- Real hardware validation

## 📚 Instruction Set Expansion

- Remaining RV32I instructions such as:
  - `FENCE`
  - `ECALL`
  - `EBREAK`
- Optional M extension:
  - Multiplication
  - Division

## 💾 Memory System

- Replace behavioural memories with a synthesisable memory subsystem.
- Add a standard memory-mapped bus interface.

## ⚡ Advanced Processor Features

- Exception handling
- Interrupt handling
- Branch prediction
- Reduced control-hazard penalties

---

# 🧠 Skills Demonstrated

This project demonstrates practical experience in:

### RTL Design

- Verilog HDL
- Modular RTL architecture
- Datapath design
- Control-path design
- Pipeline register design

### Computer Architecture

- RISC-V RV32I
- Five-stage pipelining
- Instruction decoding
- ALU architecture
- Register-file architecture
- Memory access

### Pipeline Design

- Data forwarding
- Load-use hazard detection
- Pipeline stalls
- Bubble insertion
- Control-hazard flushing

### Verification

- Self-checking testbench
- Directed testing
- Architectural checking
- Cycle-by-cycle debugging
- Waveform analysis
- Root-cause analysis

### Tools

- Synopsys VCS
- Verilator
- GTKWave
- Git

---

# 📚 Learning Outcomes

Through this project, I gained practical experience in:

- Verilog HDL and RTL coding
- RISC-V RV32I architecture
- Five-stage pipelined processor design
- Instruction decoding and execution
- Datapath and control-path implementation
- Pipeline register design
- Data forwarding
- Load-use hazard detection
- Pipeline stalling
- Bubble insertion
- Control-hazard flushing
- Self-checking verification
- Cycle-by-cycle simulation debugging
- RTL fault isolation
- Root-cause analysis
- Synopsys VCS-based functional verification
- Verilator and GTKWave-based debugging

---

# 📄 Project Documentation

The complete project report documents:

- Processor architecture
- Design methodology
- RTL implementation
- Verification methodology
- Verification results
- Debugging challenges
- Learning outcomes
- Future scope

---

# 👨‍💻 Author

## Suraj Madiwal

**Domain:** RTL Design  
**Project:** 5-Stage Pipelined RISC-V RV32I Processor  
**Project Period:** May 2026 – July 2026  
**Organization / Program:** SURE Trust – IERY

---

# ⭐ Conclusion

This project demonstrates the **design and functional verification of a modular five-stage pipelined RISC-V RV32I processor using Verilog HDL**.

The processor implements:

```text
RISC-V RV32I
      │
      ▼
Instruction Decode
      │
      ▼
Five-Stage Pipeline
      │
      ├── IF
      ├── ID
      ├── EX
      ├── MEM
      └── WB
      │
      ▼
Hazard Handling
      │
      ├── Forwarding
      ├── Load-Use Detection
      ├── Stalling
      └── Flushing
      │
      ▼
Self-Checking Verification
      │
      ▼
31 / 31 PASS
```

The final design passed **all 31 self-checking architectural tests** after systematic debugging and correction of two functional defects.

This project demonstrates practical knowledge of **RTL design, RISC-V architecture, processor pipelining, hazard handling, Verilog HDL, and simulation-based functional verification**.

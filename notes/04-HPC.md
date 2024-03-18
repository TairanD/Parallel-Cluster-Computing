# High Performance Computing 1

## 1 - Parallel Computing
### 1.1 - Sequential Execution
- Traditional software is written for **serial(sequential) computation**.
  - where each task is broken into a series of [instruction](concepts.md), which are executed in sequence (one after another)
  - **Only one** instruction may execute an any moment

### 1.2 - Parallel Execution
In parallel computing, we use multiple compute resources **at the same time** to solve a **_single_** problem.
- Requires computing resources: 
  - A single computer with multiple processors (or a single processor with multiple cores)
  - A computer with specialised compute resources such as GPUs, FPGAs, or Coprocessors
  - Multiple computers connected together with a network

Yet, NOT every problem can be solved in parallel. An algorithm that can be executed in parallel usually
has the following characteristics:
1. It can be broken into discrete pieces of work
2. These pieces can be executed at a time
3. It takes less time to solve if you use multiple compute resources


## 2 - The Von Neumann Architecture
Basically all modern processors are designed based on the same core concept - von Neumann architecture, which describes
the necessary components and operations to enable executing programs that are stored in memory.

### 2.1 - Component
Memory 
  - stores data and the instruction of the program

CPU
  - is capable of processing the instructions and data and producing results
    - to do so, it must be able to load instructions and read data from memory to execute the program and perform calculations.
    - it also should be able to write data into memory to remember results

### 2.2 - Operations
The core  of the architecture is the operation of the CPU:
1. Fetch - where an instruction is loaded from memory into the CPU.
2. Execute - where the instruction we have loaded is executed.

## 3 - Flynn's Taxonomy
Flynn’s Taxonomy is one of most used **classifications** for parallel computers.
Flynn’s taxonomy distinguishes multi-processor computer architectures along two independent dimensions: instruction & data

|                      | Single Data | Multiple Data |
|----------------------|-------------|---------------|
| Single Instruction   | SISD        | SIMD          |
| Multiple Instruction | MISD        | MIMD          |

### 3.1 SISD




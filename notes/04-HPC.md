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
a serial (non-parallel) computer.
Single instruction: only one instruction stream is being acted on by the CPU during any one clock cycle.
Single data: only one data is being used as input during any one clock cycle.

Execution result is always DETERMINISTIC.


### 3.2 - SIMD
A type of parallel computer.
Single instruction: only one instruction stream is being acted on by the CPU during any one clock cycle.
Multiple data: each processing unit can operate on a different data element.

- Synchronous and deterministic execution.

- Typically has an instruction dispatcher, a very high-bandwidth internal network, and a very large array of very
small-capacity instruction units.

- Suitable for problems characterized by a high degree of regularity, such as image processing

### 3.3 - MISD
A single data stream is fed into multiple processing units.
Each processing unit operates on the data independently via independent instruction streams.
Few actual examples of this class of parallel computer have ever exist.

### 3.4 - MIMD
The most common type of parallel computer.
- Multiple Instruction: every processor may be executing a different instruction stream.
- Multiple Data: every processor may be working with a different data stream.

Execution can be synchronous or asynchronous, deterministic or non-deterministic.


## 4 - Terminology
- Processor: a component in a computer that can **perform calculations**. The main processor of a computer is the CPU.
- Process: a unit of execution in most operating systems. It is an instance of a computer program being executed. 
Processes contain all the instructions of the programs, as well as any data. Processes also remember exactly which
instruction should be executed next.
- Task: a logically discrete section (unit) of computational work. This could be a whole program, or piece of a program.
- Parallel Task: a task that can be executed by multiple processors.
- Serial Execution: execution of a program sequentially, one statement at a time.
- Parallel Execution: execution of a program by more than one task, with each task being able to execute the same/different
statements at the same moment in time.
- Shared Memory: 
  - Hardware: a computer architecture where all processors have direct access to common physical memory
  - Software: a model where parallel tasks all have the same "picture" of memory and can directly address and access the
same logical memory locations regardless of where the physical memory actually exists.
- Distributed Memory:
  - Hardware: network based memory access for physical memory that is not common.
  - Software: task can only logically "see" local machine memory and must use communications to access memory on other
machines where other tasks are executing
- Communication: the exchange of data between parallel tasks.
- Synchronization: the coordination of parallel tasks in real time.
- Granularity: a qualitative measure of the ratio of computation to communication.
  - Coarse: relatively large amounts of computational work are done between communication events
  - Fine: relatively small amounts of computational work are done between communication events.
- Observed Speedup: a measure of improvement in speed of execution after it is converted to parallel execution
- Parallel Overhead: the amount of time required to coordinate parallel tasks, as opposed to doing useful work
  - including task start-up time, synchronizations, data communications, task termination time
- Massively Parallel: a parallel system that is made up of many processors
- Scalability: the ability to demonstrate a proportionate increase in parallel speedup with the addition of more processors
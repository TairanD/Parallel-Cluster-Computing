# High-performance computing (HPC)

- HPC is **the use of parallel processing for running programs**.
- Its main aim are:
    - Efficiency
    - Reliability
    - Speed

## 1 - How do we measure HPC

Originally, HPC was measured in instructions per second (IPS).

- Problem: some instructions can take longer to complete than others.

Modern measurements are usually done using floating point operations per second (FLOPS) (in terms of its ability to perform floating-point arithmetic operations).

- MegaFLOPS - MFLOPS - FLOPS * 1 million
- TeraFLOPS - TFLOPS - FLOPS * 1 billion

*HPC is for systems that function at several PetaFLOPS or more ↔ Term Supercomputing refers to the most brilliant system

## 2 - Cluster

A cluster is a **parallel computer system** comprising an integrated collection of independent nodes, in which each node is a system in its own right, capable of independent operation. They should function as a computer alone.

## 3 - Massively Parallel Processor (MPP)

A MMP is more tightly-integrated than a cluster. The nodes of a MMP cannot run on their own, and they are connected by a custom network (complex and expensive).

## 4 - Parallel Computing & Concurrent Computing

- **_Parallel computing_** is where many calculations or the execution of processes are carried out simultaneously. 
    - In parallel computing, a computational task is typically broken down in many very similar **subtasks**, which can be 
  processed **independently** and the results are combined afterwards.
- **_Concurrent computing_** is where multiple tasks are executed at the same time. 
    - We do not care these tasks are related or not (usually not related), unlike parallel computing where subtasks are always related.
    - Concurrent computing is how computers with a single processor can run multiple applications at the same time.
- *Clarification
    - It’s possible to have concurrency without parallelism
        - Time-sharing on a single CPU
    - It’s possible to have parallelism without concurrency
        - Bit or instruction level parallelism

#### Distributing computing
Distributed computing is more loosely coupled than parallel computing:
- a significant characteristic of distributed computing is the lack of a global clock


## 6 - Memory
There are two types of memory:
- Shared memory: the system has **a single memory space** that is used by all processors.
- Distributed memory: the processors in the system **each have their own memory**.

### 6.1 - Shared Memory
A system with shared memory has one big advantage: **the different processes in the task can communicate by sharing
information in memory**, which means information written to memory by one process can be read from memory by another process.

### 6.2 - Distributed Memory
In a distributed memory system, communication is not as easy. It requires some form of interconnection (normally a network)
to pass messages.

## 7 - Why HPC?
What types of problems required HPC?
- Compute intensive: a single problem requiring a large amount of computation.
- Memory intensive: a single problem requiring a large amount of memory.
- Data intensive: a single problem operating on a large amount of data.
- High throughput: many unrelated problems to be executed over a long period.
Application:
- in biology:
  - Genome Sequencing
  - Protein Folding Simulation
  - Gene Expression Analysis
  - ...
- in physics
  - Modelling stellar and galactic evolution
  - Condensed matter physics
  - Simulation of solar cell performance
  - ...
- in finance
  - Analysis of historical data
  - Financial forecasting
  - High speed trading
  - ...
- in industry
  - Oil & gas exploration
  - Product design & testing
  - ...
- in entertainment
  - Production of animated movies
  - Addition of graphics to real movies
  - ...












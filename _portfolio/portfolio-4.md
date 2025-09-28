---
title: "OS Simulation Suite"
excerpt: "Compact suite of operating system simulations in modern C++ spanning - linking/loading, CPU scheduling, memory paging, and disk I/O scheduling"
collection: portfolio
---
## Overview  

From August to December 2024, I built a compact suite of operating system simulations in modern C++. The suite spans four core OS topics—linking/loading, CPU scheduling, memory paging, and disk I/O scheduling—with a clean, modular design, deterministic drivers, and full reproducibility.

## Tech & Structure  

- **Language & style:** C++ (modular `.h` / `.cpp`), clear separation of concerns  
- **Organization:** Four lab directories (`Module1` through `Module3`), each containing drivers, simulators, policies, and test scripts  
- **Reproducibility:** `Makefile`s, `runit` scripts, and fixed random number input datasets under `rfile/` to enforce deterministic behavior  

## Modules

### Module 1 — Linker / Loader  

- **Features:** Two-pass linker implementing symbol resolution, relocation, error detection (duplicate symbols, out-of-bounds sections, unused symbols)  
- **Output:** Memory maps, symbol tables, diagnostic logs  

### Module 2 — CPU Scheduling  

- **Features:**  
  - Simulates process arrival, CPU/IO bursts, preemption  
  - Supports FCFS, SJF, SRTF, Round-Robin, Priority  
- **Outputs:** Per-process finish time, turnaround, waiting time; system-level usage & throughput  

### Module 3 — Memory Management (Paging / MMU)  

- **Approach:**  
  - Parses VMAs and memory-access traces  
  - Implements replacing policies: FIFO, Random, Clock, Aging, Working-Set  
  - Maintains frame table, PTE states (present, referenced, modified)  
- **Outputs:** Page faults, maps/unmaps, ins/outs, zeros, total time  

### Module 4 — Disk I/O Scheduling  

- **Features:** Simulated policies - FIFO, SSTF, LOOK, C-LOOK, FLOOK via discrete-event simulation of head motion (1 track/time unit), queued requests, starvation avoidance
- **Outputs:** Head movement counts, request turnaround and wait times, utilization metrics  


## Highlights & Outcomes  

- **Event-driven architecture** with plugable policy interfaces — easy to swap in/out scheduling, paging, I/O strategies  
- **Deterministic runs** via fixed seeds and driver scripts produce repeatable experiments  
- **Rich metrics & logs** that follow textbook OS definitions, used for benchmarking, correctness, and grading  
- **Cohesive stack:** The suite ties together linking, CPU scheduling, memory, and I/O into a unified, testable OS simulation environment  


## Code Availability  

To view the complete code for this simulation suite, please **contact me directly**

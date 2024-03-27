---
tags:
  - COSC-439
  - spring2024
---


# Motivation

Multiple tasks with the application can be implemented by separate threads
- Update display
- Fetch data
- Spell checking
- Answer a network request
- Process creation is heavy-weight while thread creation is light-weight
- Can simplify code, increase efficiency – Modular

Basic unit of CPU utilization
A thread comprises:
- A thread ID
- A program counter
- A register set
- A stack
- Threads belonging to the same process share OS resources such as open files and signals

![[basic_unit_cpu_utilization.png]]

Thread: a sequential execution stream within process (Sometimes called a“Lightweight process”)
Process still contains a single Address Space
No protection between threads (Shared resources)
A traditional/heavyweight process has a single thread of control.

![[single-threaded_vs_multi-threaded_process.png | 900]]

# Thread State

  
State shared by all threads in process/address space
- Contents of memory (global variables, heap)
- I/O state (file system, network connections, etc)
State “private” to each thread
- Kept in TCB $\equiv$ Thread Control Block
- CPU registers (including, program counter)
- Execution stack – Parameters, Temporary variables

# Examples of multithreaded programs

Embedded systems
- Elevators, Planes, Medical systems, Wristwatches
- Single Program, concurrent operations
Database Servers
- Access to shared data by many concurrent users
- Also background utility processing must be done
Network Servers
- Concurrent requests from network
- Again, single program, multiple concurrent operations
- File server, Web server, and airline reservation systems

# Multithreaded Server Architecture
![[multithreaded_server_architecture.png | 1000]]

## Benefits

Responsiveness
- Provide interactive feedback (example: browsers doing multiple tasks)

Resource Sharing and Cost Effective Sharing memory and resources by default, share same address space
- Less time-consuming to context-switching & creation
- Process creation is costly with new allocation of memory and resources

Utilization of multiprocessor architectures
- Parallel threads on different processors

# Concurrent Execution on a Single-core System

![[concurrent_execution_single-core_system.png | 1000]]


# Parallel Execution on a multi-core system

![[parallel_execution_multi-core_system.png | 1000]]



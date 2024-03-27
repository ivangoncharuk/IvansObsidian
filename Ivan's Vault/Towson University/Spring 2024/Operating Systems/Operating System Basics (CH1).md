---
tags:
  - spring2024
  - "#COSC-439"
---


## Computer System Structure

Can be divided into **four** components
1. Hardware (Resources)
	1. CPU
	2. Memory
	3. I/O devices
2. OS
	1. Controls and coordinates use of hardware among various apps and users
3. Application Programs - Define the ways in which the system resources are used
	1. Word processors
	2. Compilers
	3. Browsers
	4. Database systems
	5. Video games... etc
4. Users
	1. People
	2. Machines
	3. Other computers

![[Computer_System_Structure.png| 600]]

## What is an OS?

An Operating System is a program that acts as an **intermediary** between a user of a computer and the computers' hardware

Goals:
- Execute programs and make solving problems easier
- Making the computer easier to use
- Using the hardware efficiently

They turn *ugly* hardware into **`beautiful`** abstractions

- OS is a **`resource alocator`**
	- Manages all resources
	- Decides between conflicting request for efficient and fair resource use
- OS is a **`control program`**
	- Controls execution of programs to prevent errors and improper use of the computer

![[traffic_intersection_clipart.png| 400]]

## Computer Startup

### Bootstrap program

A **bootstrap program** is loaded at power-up or reboot.

- Stored in ROM (Read-Only-Memory) or EPROM (Electronically-Programmable-ROM)
	- Generally known as **firmware**
- Initializes all aspects of a system
- **Loads** operating system kernel and **starts** execution

Why is OS stored in hard disk and not in RAM?
- OS is huge nowadays

## CPU Interrupts

Interrupt is a signal or event that prompts the CPU to suspend its current activities and shift its focus to a specific task or event that requires immediate attention.

- I/O devices and the CPU can execute concurrently
- Each device controller is in charge of a particular device type
- Each device controller has a local buffer
- CPU moves data to and from the main memory and to and from local buffers
- I/O is from the device to local buffer of controller
- Device controller informs the CPU that it has finished its operation by causing an **interrupt**

![[CPU_IOdevice_interupt_graph.png | 600]]

## Storage Structure

### Main memory
Only Large storage media that the CPU can access directly
- Random Access Memory (**RAM**)
- Typically **volatile**
- Most common RAM sizes
	- 8, 16, 32, 64 GB

### Secondary storage
Extension of main memory that provides large nonvolatile storage capacity

### Hard Disks
rigid metal or glass platters covered with magnetic recorgin material

- Disk surface is logically divided into tracks, which are subdivided into sectors
- The disk controller determines the logical interaction between the device and the computer.

### Solid-state disks
Faster than hard disks, nonvolatile
- various technologies
- more popular

### Storage Hierarchy

Computer storage systems are organized in hierarchy
- Speed
- Cost
- Volatility

![[storage_hierarchy.png | 400]]

## Caching

**Caching** - copying information into faster storage system; main memory can be viewed as a cache for secondary storage

It is an important principle because it is performed at many levels. in a computer
- Hardware
- OS
- Software

The information that needs to be used is temporarily copied from slower storage to faster storage

Faster storage (cache) is checked first to determine if the information is there
- If the information is in the cache - information is used directly from the cache
- If the information is NOT in the cache - data is copied to cache and used there

When the cache capacity is smaller than the storage being cached
- cache management would become an important design principle
- cache size and replacement policy

## Computer-System Architecture

Most systems use a single general-purpose processor, and they have a special-purpose processors as well.

Multi-processor systems are growing in use and importance
- Also known as parallel systems, tightly-coupled systems.

Advantages:
1. Increased throughput
2. Economy of scale
3. Increased reliability (graceful degradation or fault tolerance)

Two types:
1. Asymmetric Multiprocessing - each processor is assigned a specific task.
2. Symmetric Multiprocessing - each processor performs all tasks

![[multi_processor_to_memory.png| 500]]

## Clustered Systems

Like multiprocessor systems, but multiple systems working together.
This is basically a large scale network of individual comptuters working together.

- Usually sharing storage via a **storage-area network (SAN)**
- Provides a **high-availability** service which survives failures
	- **Asymmetric clustering** has one machine in hot-standby mode
	- **Symmetric clustering** has multiple nodes running applications, monitoring each other
- Some clusters are for **high-performance computing (HPC)**
	- Application must be written to use **parallelization**
- Some clusters have **distributed lock manager (DLM)** to avoid conflicting operations

![[storage-area-network_clustered_system.png | 400]]

### Parallelization

breaks down a program or task into smaller components that can be executed simultaneously on different processes or units within the cluster

### Example - Video rendering

When creating high quality animations or videos, the rendering process can be **extremely complex** and **time consuming** because it handles a ton of complex computations. 

The video can be split up into multiple smaller parts so that the task can be divided into small segments, such as frame or scene, so that each computer individually will take care of that particular scene or frame, and they send back the result to the computer that is in charge of joining all these segments together to build the final output.

## Operating System Structure


### Multiprogramming
- **Multiprogramming (Batch System)** is needed for efficiency
	- Single user cannot keep CPU and I/O devices busy at all times
	- multiprogramming organizes jobs (code and data) so CPU always has one to execute
	- A subset of total jobs in system is kept in memory
	- One job is selected and run via job scheduling
	- When it has to wait (for I/O for example), the OS switches to another job

Example - Lawyer
A lawyer does not work for one client at a time. While one case is waiting to go to trial or have papers tied, the lawyer can work on another case. If the lawyer has enough clients, the lawyer will never be idle or be out of work to do.


### Timesharing
- **Timesharing (multitasking)** is the logical extension in which a CPU switches jobs so frequently that users can interact with each job while it is running, creating interactive computing
	- The **response time** should be less than 1 second
	- **process**: each user has at least one program executing in memory 
	- **cpu scheduling**: if several jobs ready to run at the same time
	- If processes don't fit in memory, **swapping** moves them in and out to run
	- **virtual memory** allows execution of processes not completely in memory

![[CPU_circular_process_queue.png| 500]]

## Operating System Operations

- **Interrupt driven** (hardware and software)
- Software interrupt (**exception** or **trap**)
	- Software error (division by zero, or invalid memory access) request for operating system service
- Other process problems include infinite loop, processes modifying each other or the operating system
- **Dual-mode** operation allows the OS to protect itself and other system components
	- **User mode** and **kernel mode**
	- **Mode bit** provided by hardware
		- Provides ability to distinguish when system is running user code or kernel code
		- Some instructions designated as **privileged** only executed in kernel mode
		- System call changes mode to kernel, return from call resets it to user


## Transition from User to Kernel Mode

A timer to prevent infinite loop / process hogging resources

- Timer is set to interrupt the computer after some time period
- Keep a counter that is decremented by the physical clock
- Operating system set the counter (a privileged instruction)
- When counter goes to zero it will generate an interrupt
- Set up before scheduling process to regain control or terminate the program that exceeds the allotted time

![[user_process_kernel_modebit.png| 600]]

## Process Management

- Process is a program in execution. It's a unit of work within the system. 
	- The program is a ***passive entity***
	- The process is an ***active entity***
- Process needs resources to accomplish its' task
	- CPU, memory, I/O, files
	- Initialization data
- Process termination requires reclaim of any reusable resources
- Single-threaded process has one **program counter** specifying the location of the next instruction to execute
	- The process executes the instructions sequentially (one at a time) until completion
- Multi-threaded processes has one program counter per thread
- These systems typically have many processes, some user, some OS running concurrently on one or more CPUs
	- Concurrency by multiplexing the CPUs among the processes / threads

- Context switch - `get a definition for this`
	- switch from one job to another
	- remember the current state or context
	- creates a snapshot
	- once a job is finished it goes back to the previous context

## Process Management Activities

The OS is responsible for the following activites in connection with process management
- Creating and deleting both user and system processes
- Suspending and resuming processes
- Providing mechanisms for...
	- Process synchronization
	- Process communication
	- deadlock handling

## Memory Management
- To execute a program all (or part) of the instructions must be in memory
- All (or part) of the data that is needed by the program must be in memory
- Memory management determines what is in memory and when something is in memory
	- Optimizing CPU utilization and computer response to users
- Memory management activties include:
	- Keeping track of which parts of memory are currently being used and by whom
	- Deciding which processes (or parts thereof) and what data to move into and out of memory
	- Allocating and deallocating memory space as needed

## Storage Management

- The OS provides a uniform and logical view of data storage
	- It abstracts physical properties into a logical storage unit - a **file**
	- Each medium is controlled by a device (disk drive, tape drive, etc)
	- Varying properties include:
		- Access speed
		- capacity
		- data transfer rate
		- access method
			- Sequential
			- Random
- File system management consists of
	- Files that are usually organized into directories
	- Access control on most systems to determine who can access what
	- Activities include:
		- Creating and deleting files and directories
		- Primitives to manipulate files and directories
		- Mapping files onto secondary storage
		- Backup files onto stable (non-volatile) storage media

## Mass-Storage Management

- Disks are usually used to store data that does not fit in main memory or data that must be kept for a *long* period of time
- Proper management very important
- Entire speed of computer poeration hinges on disk subsystem and its algorithms
- OS activities include:
	- Free-space management
	- Storage allocation
	- Disk scheduling
- Some storage does not need to be fast
	- Tertiary storage includes optical storage, magnetic tape
	- Still need to be managed - by OS or by applications
	- Varies between WORM (write-once, read many-times) and RW (read-write)

![[storage_level_performance.png]]

## Protection and Security

- **Protection** - is any mechanism for controlling access of processes or users to resources defined by the OS
- **Security** - defense of the system against internal and external attacks
	- Huge range, including denial-of-service, worms, viruses, identity theft, theft of service
- Systems generally first distinguish among users, to determine who can do what
	- User identities (**user IDs**, security IDs) include name and associated number, one per user
	- User ID then associated with all files, processes of that user to determine access control
	- Group identifier (**group ID**) allows a set of users to be defined and controls managed, then also associated with each process, file
	- **Privilege escalation** allows the user to change to an effective ID with more rights

## Distributed Computing

Collection of separate, possibly heterogeneous, systemsnetworked together

Network is a communications path, TCP/IP most common Local Area Network (LAN) Wide Area Network (WAN) Network Operating System provides features between systemsacross network Communication scheme allows systems to exchangemessages Illusion of a single system







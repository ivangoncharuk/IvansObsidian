---
tags:
  - COSC-439
  - spring2024
---

## What is it?
- CPU switches to another process, the sys must save the state of the old process and load the saved state for the new process through a **context switch**
- Context of a process represented in the PCB
- Context-switch time is overhead; the system does no useful work while switching
- The more complex the OS and the PCB $\rightarrow$ the longer the context switch
- Time dependent on hardware support
- Some hardware provides multiple sets of registers per CPU
	- multiple contexts loaded at once

![[process_switch.png| 600]]


## Process creation

- Parent process create children processes, which, in turn create other processes, forming a tree of processes
- Generally, process identified and managed via a **process identifier** (**pid**)
- Resource sharing options
	- Parent and children share all resources
	- Children share subset of parent’s resources
	- Parent and child share no resources
- Execution options
	- Parent and children execute concurrently
	- Parent waits until children terminate

![[linux_tree_of_processes.png | 600]]
![[pstree_linux.png | 600]]

- Address space (there are two possibilities in terms of the addressspace of the new process)
	- Child duplicate of parent (it has the same program and dataas the parent)
	- Child has a program loaded into it
- UNIX examples
	- `fork()` system call creates new process
	- `exec()` system call used after a `fork()` to replace the process’ memory space with a new program

![[fork_exec_exit_graph.png| 700]]

### C Program Forking Separate Process (linux)
```C
#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>

int main()
{
	pid t pid;
	
	/* fork a child process */
	pid = fork();
	
	if (pid < 0) { /* error occurred */
		fprintf(stderr, "Fork Failed");
		return 1;
	}
	else if (pid == 0) { /* child process */
		execlp("/bin/ls","ls", NULL);
	}
	else { /* parent process */
		/* parent will wait for the child to complete */
		wait (NULL);
		printf("Child Complete");
	}
	
	return 0;
}

```

### Creating a Separate Process via Windows API
```C
#include <stdio.h>
#include <windows.h>

int main(VOID) {
  STARTUPINFO si = {0};
  PROCESS_INFORMATION pi = {0};

  // Allocate memory and set cb field
  si.cb = sizeof(si);

  // Create child process for mspaint.exe
  if (!CreateProcess(NULL,
                    "C:\\WINDOWS\\system32\\mspaint.exe",
                    NULL,
                    NULL,
                    FALSE,
                    0,
                    NULL,
                    NULL,
                    &si,
                    &pi)) {
    fprintf(stderr, "Create Process Failed\n");
    return -1;
  }

  // Wait for child process to complete
  WaitForSingleObject(pi.hProcess, INFINITE);

  printf("Child Complete\n");

  // Close handles
  CloseHandle(pi.hProcess);
  CloseHandle(pi.hThread);

  return 0;
}

```


## Process Termination
- Process executes last statement and then asks the operating system to delete it using the `exit()` system call.
	- Returns status data from child to parent (via `wait()`)
	- Process’ resources are deallocated by operating system
- Parent may terminate the execution of children processes using the `abort()` system call. Some reasons for doing so:
	- Child has exceeded allocated resources
	- Task assigned to child is no longer required
	- The parent is exiting and the operating systems does not allow a child to continue if its parent terminates
		- cascading termination. All children, grandchildren, etc. are terminated.
		- The termination is initiated by the operating system.

## Assignment 0

- Install a virtual machine
	- Install Windows on my host macos machine
	- Install Ubuntu on host Windows
- Show that the guest machine is running
- Set up the environment
	- GCC or G++ (should be installed in ubuntu by default but re-check)
	- Windows: Set up you favourite C/C++ IDE
	- Run a simple C++ program
	- Take screenshots


## Multiprocess Architecture
- Many web browsers ran as single process (some still do)
- If one web site causes trouble, entire browser can hang or crash
- Google Chrome Browser is multiprocess with 3 different types of processes:
	- Browser process manages user interface, disk and network I/O
	- Renderer process renders web pages, deals with HTML,Javascript. A new renderer created for each website opened
		- Runs in sandbox restricting disk and network I/O, minimizing effect of security exploits
	- Plug-in process for each type of plug-in

![[googlechrome_tabs_sepprocesses.png]]

## Interprocess Communication

Processes within a system may be **independent** or **cooperating**

- **independent process**: They cannot affect or be affected by the other processes executing in the system.
- **cooperating process**:They can affect or be affected by the other processes executing in the system.

*Any process that shares data with other processes is a cooperating process.*

  
Reasons for cooperating processes:
- **Information sharing**: Shared files and resources require concurrent access.
- **Computation speedup**: Shared files and resources require concurrent access.
- **Modularity**: System functions divided into separate processes or threads to enhance system organization and management.
- **Convenience**: Provides multitasking

Cooperating processes need interprocess communication (**IPC**) mechanism that will allow them to <u>exchange data and information.</u>

Two models of IPC:
- **Shared memory**: a region of memory that is shared by cooperating processes.
	- Processes exchange information by reading and writing data to the shared region.
- **Message passing**: processes communicates through theexchange of messages.

## Communication Models

### Message Passing

![[message_passing_comm_model.png| 300]]

### Shared Memory

![[shared_memory_comm_model.png| 300]]

## Shared Memory

- To enable interprocess communication, processes need to establish a shared memory region.
- This shared memory region typically exists within the address space of the process that created it.
- Other processes wishing to communicate via this shared-memory segment must attach it to their address space.
- But the operating system restricts one process from accessing another process's memory.
- Shared memory requires mutual agreement among two or more processes to remove this restriction.

## Producer-Consumer Problem

Paradigm for cooperating processes, producer process produces information that is consumed by a consumer process.

- **Example**: Client-Server, Servers produce files like HTML, CSSand Clients consume these files.
- **Solution**: To allow producer and consumer processes to run concurrently, we must have available a buffer of items that can be filled by the producer and emptied by the consumer.
	- *unbounded-buffer* places no practical limit on the size of the buffer
	- *bounded-buffer* assumes that there is a fixed buffer size

### Bounded-buffer (shared memory)

```C
#define BUFFER_SIZE 10
typedef struct {
  . . .
} item;
item buffer[BUFFER_SIZE];
int in = 0;
int out = 0;
```

Solution is correct, but can only use BUFFER_SIZE-1 elements

### Bounded-buffer (producer)

```C
item next_produced;
while (true) {
	/* produce an item in next produced */
	while (((in + 1) % BUFFER_SIZE) == out)
			; /* do nothing as the buffer is full*/
	buffer[in] = next_produced;in = (in + 1) % BUFFER_SIZE;
}
```


### Bounded-buffer (consumer)

```C
item next_consumed;
while (true) {
	while (in == out)
		; /* do nothing because the buffer inempty*/
		next_consumed = buffer[out];
		out = (out + 1) % BUFFER_SIZE;
		/* consume the item in next consumed */
}
```


## Interprocess Communication

Mechanism to allow processes to **communicate** and to **synchronize** their actions <u>without sharing the same address space</u>.

Particularly useful is a distributed environment, where the communicating processes reside **on different computers** connected by a **network**.

- Chatting software (Client-Server)
- IPC facility provides two operations:
	- **send**(message)
	- **receive**(message)
- The message size is either fixed or variable

If processes P and Q wish to communicate, they need to:
- Establish a communication link between them
- Exchange messages via send/receive

Implementation of communication link
- Logical:
	- Direct or indirect
	- Synchronous or asynchronous
	- Automatic or explicit buffering

## Direct Communication

Processes must name each other explicitly:
- **send**(*P*, message) – send a message to process *P*
- **receive**(*Q*, message) – receive a message from process *Q*

Problem: Changing the identifier of a process may necessitate examining all other process definitions.

> In general, any such hard-coding techniques, where identifiers must be explicitly stated, are **less desirable**.

## Indirect Communication

Messages are directed and received from mailboxes (also referred to as ports)
- Each mailbox has a unique **id**
- Processes can communicate only if they **share a mailbox**

Operations:
- create a new mailbox (**port**)
- send and receive messages through mailbox
- destroy a mailbox

Primitives are defined as:
- **send**(*A*, message) – send a message to mailbox *A*
- **receive**(*A*, message) – receive a message from mailbox *A*

## Synchronization

Message passing may be either blocking or non-blocking



- Blocking is considered **synchronous**
	- **Blocking send** -- the sender is blocked until the message is received
	- **Blocking receive** -- the receiver is blocked until a message is available

- Non-blocking is considered **asynchronous**
	- Non-blocking send -- the sender sends the message and continue
	- Non-blocking receive -- the receiver receives:
		- A valid message, or
		- Null message




# General OS knowledge

The goal here is to get a general overview of how an OS works, and in particular how linux works under the hood.

## Overview

An Operating System (OS) is low-level collection of software that acts as an interface between a user and the hardware. It handles the basic computer functions, such as process management, memory management, task scheduling, controlling peripherals etc...

An operating system is usually writtent in lower-level languages such as Compiler or Assembler. This is opposed to application software which is software a user directly uses to perform different activities such as web browsing for example. Application software is usually written in higher-level languages such as C++, JAVA or Python.

There are plenty of operating systems, some of the most common include : 

* Windows
* Linux
* MacOS
* Android
* iOS

Operating systems have been existing since the 1950s/60s. Unix for example was developed in the mid 1960s by the MIT, AT&T Bell Labs and General Electric.

## Processing

There are different ways processing can happen in a OS, but modern OSs allow for running multiple tasks at the same time. This is called multi-tasking.

Multitasking is when multiple jobs are executed by the CPU simultaneously by switching between them. Those switches are so fast that a user doesn't feel them. He can interact with different programs on the same time. This is usually how a user is using his computer on a daily basis, for example Word, Email, Music all run in a multitasking fashion.
A similar technique to multitasking is multiprogramming which simply uses a different process scheduling method.

The load is split among the different CPU cores, this is called parrallelism. Each core handles a process and runs OS-related tasks in-between processes. The os-related tasks call a scheduler that plans what needs to be processed. A process only runs on one core at the time.

![](/Learning%20Path/Images/OS/os_process_scheduling.png)

A process is interrupted when the CPU receives a hardware interrupt signal. Then the process is interrupted and the progression is stored. The os scheduler then runs to plan what needs to be processed next. This is called pre-emptive multitasking. An interrupt is called on a regular basis (this is called a clocked system), for exemple every 10ms. This ensures that the CPU can change the running process at least several times per second. This mechanism is called concurrency.

The processes not only share the CPU cores but also the system memory. The OS ensures that each process only has access to its own memory portion and doesn't interfere with the memory allocated to other processes. The OS however can access any memory portion. There still is a possibility for processes to access specific fixed OS memory places such as reading/writing files or network communication. To do this a process needs to invoque a specific CPU instruction called a syscall.

The CPU runs in two different privilege levels. A first privilege level for the OS, and another one for processes. The second privilege level triggers exceptions if the processes try to access memory portions they aren't allowed to.

## Process memory

A process stores the elements it needs in three different memory sections : 
* Text section for the code (stored as binary code in a contiguous chunk of memory.)
* Call stack for the local variables
* Heap for everything else

The stack stores the variables for each process in a contiguous chunk called a frame. Additionnaly the memory address to return to after the process returns as well as the frame size are also stored. There also usually is an additionnal pointer tracing the top of the stack that is stored in a CPU register.
The size of the stack space is often kept track of using a stack boundary pointer also stored in a CPU register. If the stack grows bigger than the stack boundary allows, this boundary is first increased up to a certain point until the system triggers an error called a stack overflow. Such an error is often caused by programms that don't run correctly, for example by habing too many nested recursive calls.
In simpler systems there might not be this monitoring. A growing stack space might bump into memory addresses where it wasn't supposed to be creating bugs.

![](/Learning%20Path/Images/OS/os_process_stack.png)

No heap space exists when the process starts executing. The process explicitly needs to ask for it. The OS decides where it is placed, but the process determines the size. When the process is done with a chunk of heap, it is deallocated. Repeatadly allocating/deallocation heap space creates fragmentation. This means that the heap space that can be allocated to a single block shrinks even if the total heap space is bigger. If a process doesn't properly deallocate heap memory, the heap will run out of memory at some point. This is called a memory leak.
![](/Learning%20Path/Images/OS/os_process_heap.png)

The memory addresses are not refering directly to physical memory but it is mapped by the OS. It doens't have to be contiguous. A process can have memory located on any part of RAM and can only access its own parts. If a process tries to access part of its address space that is not mapped to actual RAM, an exception called a page fault is triggered. The mapped chunks in memory are called pages, and they are fixed length.

To free up RAM, the OS might decide to swap out a page from RAM to storage, usually a hard drive. For example pages of heap memory for which the pages have been swapped are marked swapped in the process memory table.
An attempt to access a swapped page will trigger an error and will trigger the OS swap the page back into RAM. Swapping is relatively slow but this way the total process memory can exceed system RAM.
This memory management technique is called virtual memory.

![](/Learning%20Path/Images/OS/os_process_mapping.png)

## Threads

A thread is a unit of execution within a process. A process has at least one thred but can have any amount. Multi-threaded processes contain more than one thread. All the threads share the process memory and resources. Each thread has its own stack but they will share the heap. Since threads share the same address space it is easy to communicate between them.

## Interprocess communication (IPC)

Two running processes can either be independent or cooperating. Independent processes cannot be affected nor do they affect other processes. Cooperating on the other hand can (be) afftect(ed) (by) other processes. Any process that shares data with other processes is a cooperating process.

There are several reasons for providing an environment that allows process cooperation:

* Information sharing. For example if several users are interested in a single piece of information.
* Computation speedup. A big task can be split up into subtasks and these can be split out to different processes.
* Modularity. A system is usually divided into different modules. These modules will later work together to achieve a same goal.
* Convenience. For example a user might be doing different things at the same time. The different processes need therefore to communicate with each other in order to avoid clashes.

There are two fundamental models of IPC:

**Shared memory**
Here a region of memory that is shared by cooperating processes is established. Processes can then exchange information by reading/writing data to the shared region.

**Message passing**
Here communication takes place by means of messages exchanged between the cooperating processes (think networking for example). These messages pass through the OS.
Message passing is also often used for process synchronization where no explicit data needs to be sent. Here often just messages are just signals.

# Resources

* [tutorials point - OS tutorial](https://www.tutorialspoint.com/operating_system/index.htm)
* [Brian Will - Operating System Basics](https://www.youtube.com/watch?v=9GDX-IyZ_C8)
* [backblaze.com - What’s the Diff: Programs, Processes, and Threads](https://www.backblaze.com/blog/whats-the-diff-programs-processes-and-threads/)
* [Neso Acamedy - Interprocess Communication](https://www.youtube.com/watch?v=dJuYKfR8vec)
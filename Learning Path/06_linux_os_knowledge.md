# General OS knowledge

The goal here is to get a general overview of how an OS works, and in particular how linux works under the hood.
These notes are based on the [tutorials point OS tutorial](https://www.tutorialspoint.com/operating_system/index.htm).

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

There are different ways processing can happen in a OS.

**Batch processing**

When doing batch processing, the OS collects programs and data together in a batch before processing starts. This is usually done to periodically complete high-volume, repetitive data jobs. Instead of running the tasks on individual bits of data, data is grouped into larger batches to optimize efficiency.

**Multitasking**

Multitasking is when multiple jobs are executed by the CPU simultaneously by switching between them. Those switches are so fast that a user doesn't feel them. He can interact with different programs on the same time. This is usually how a user is using his computer on a daily basis, for example Word, Email, Music all run in a multitasking fashion.
A similar technique to multitasking is multiprogramming which simply uses a different process scheduling method.

# 📅 Date: 2025-08-16
## 📖 Pages Covered
From page: 1  To page: ___

---

## 📝 Key Points (in my own words)
-  **Abstraction** - Focus on what a component while ignoring the low-level details
-  **Components** - Subsystems / modules / packages that make up Linux
- A Linux system can be divided into three main levels: Hardware, Kernel, and Processes
- Hardware resides at the bottom and includes Memory, Network Interface, CPU, Disks etc.
- Kernel lives in between Hardware and the user space and is the core of the OS. The main job of the kernel is to manage tasks and tell the CPU what it's next task is.
- User processes are the applications that a user can see or run. For example, GUI, Servers, Shell
- A Kernel runs the processes in Kernel mode. Kernel mode has unrestricted access to processor and memory and can crash the entire system.
- User processes run in user mode. User mode has a restricted access to memory
- The memory area only kernel can access is called kernel space. 
- User space means the parts of main memory that the user processes can access.
- Kernel also runs threads that look like processes but have access to Kernel space. For example kthread, kblockd
- Main memory is the most important hardware on a computer system.
- It contains 0s and 1s. Each slot of 0 or 1 is called a bit. 
- The input and output from the peripheral devices flow through the memory
- CPU is just an operator on the memory. It runs the instructions and writes the data back to the memory. 
- A state is an arrangement of bits. For example if you have 4 bits in the memory, 0010, 0100, 1000 represent three different states.
- Image refers to a particular physical arrangement of bits.
- One of the most important kernel's job is to split the memory into many subdivisions and maintain the state of these subdivisions. It should also ensure that each process keeps to its own share of memory
- Kernel is in charge of managing tasks in these four general areas
	- Process Management
	- Memory Management
	- Device Drivers
	- System calls

## Process Management
- Process Management involves in starting, pausing, resuming, scheduling and terminating the process. 
- Only one process can run on a CPU core at a time, even if it looks like many are running
- OS uses time slices, each process runs briefly, then yields to the next.
- Multitasking means rapid context switching, so human perceive tasks as simulataneous.

### Context Switching
- CPU Interrupts the running process after it's time slice and hands the control to kernel who's job is to 
	- Switches to kernel mode and saves the process state
	- Finish the tasks that might have come in the preceding time slice
	- Choose a process from the running processes in the queue
	- Prepares memory & CPU for the new process
	- Defines the time slice length for the next process to finish the computation
	- Hands CPU to the next process and switches to user mode
- This process of switching between one process to another process is called context-switching
### Multi-core difference
- Multiple processes can run at the same time
- Kernel still manages context switches to maximize CPU usage

## Memory Management
- Kernel must manage the memory with the following conditions
	- Kernel must have it's own memory that the processes cannot access
	- Each user process needs its own share of the memory
	- One user process may not access the private memory of another process
	- User processes can share memory
	- Some memory in the user processes can be read-only
	- The system can use more memory than is physically present by using disk space as **_auxiliary_** 
### Memory Management Unit (MMU)
-  Modern computers come with Memory Management Unit
- Job of MMU is to create a virtual memory where each process assumes that it owns the entire machine to itself
- This virtual machine is translated by actual physical memory on the machine by MMU which is called **_Memory address Mapping_**
- Kernel must maintain the Memory Address Map
- During context switching kernel swaps the memory map from the old process to a new process

## Device Drivers and Management
- Device drivers must run in Kernel mode to prevent improper access that leads to crashing of a machine
- Devices rarely have the same programming interface
- So device drivers are there to put an uniform interface between the devices

## System Calls and Support
- Almost every user process uses system calls to talk to the kernel
	- Examples of these are opening, writing and reading files
- Important system calls for processes:
	- `fork()` - Creates a nearly identical copy of the process
	- `exec(program)` - replaces the current process with `program` 
	- 


---

## ❓ Flashcards
<!--ID: 20250816100350-->
Q:  What term is commonly used for subdivisions of software in Linux?
A:  Components (also called subsystems, modules, or packages)
<!--ID: 20250816100350-->
Q:  How many levels does a Linux system has and what are they?
A:  Three levels. From Bottom - Hardware, Kernel, User Processes
<!--ID: 20250816100350-->
Q:  What is the main job of kernel?
A:  The main job of the kernel is to allocate tasks to CPU
<!--ID: 20250816100350-->
Q:  What does a Hardware layer consist of?
A:  Hardware mostly consists of one or more CPU s, Memory, Disks, Network Interface.
<!--ID: 20250816100350-->
Q:  What does a kernel consist of or do?
A:  System calls, Process Management, Memory Management, Device Drivers.
<!--ID: 20250816100350-->
Q:  What does a user processes or processes consist of?
A:  Applications, server, GUI.
<!--ID: 20250816100350-->
Q: Kernel runs the processes in what mode?
A:   Kernel mode 
<!--ID: 20250816100350-->
Q:  User runs the processes in what mode?
A: User mode
<!--ID: 20250816100350-->
Q:  Memory to which kernel has access to is called?
A: Kernel space
<!--ID: 20250816100350-->
Q:  What is the problem of running processes in kernel mode?
A: Processes in kernel mode has unrestricted access and can wreak havoc.
<!--ID: 20250816100350-->
Q:  Provide two examples of kernel threads that look like processes?
A: kthread, kblockd
<!--ID: 20250816100350-->
Q:  What does the term state mean
A: State means particular arrangement of bits. State can also be referred to what the process is doing at the particular moment. For example, waiting for the input etc.
<!--ID: 20250816100350-->
Q:  What does the term image mean
A: Image refers to a particular physical arrangement of bits. 
<!--ID: 20250816100350-->
Q:  Kernel is in charge of managing tasks in four general areas, what are they?
A: Process management, Memory Management, Device Drivers, System Calls
<!--ID: 20250816100350-->
Q:  What is the act of one process giving CPU control to another process called?
A: Context Switching
<!--ID: 20250816100350-->
Q: The time in which one process runs before handing the control to another process is called?  
A: Time slice
<!--ID: 20250816100350-->
Q:  What are kernel's main requirements for memory management?
A: 
1. Private Kernel Memory
2. Each process has it's own memory
3. No cross-access between processes
4. Processes can share the memory
5. Some memory can be read-only
6. Use disk space as an extra space (swap)
<!--ID: 20250816100350-->
Q:  What hardware feature enables virtual memory?
A: Memory Management Unit (MMU)
<!--ID: 20250816100350-->
Q:  What is a virtual memory?
A: A memory scheme where each process acts as if it has its own machine
<!--ID: 20250816100350-->
Q:  What role does kernel play in virtual memory?
A: It maintains the memory address map, switching it between the processes during the context switch
<!--ID: 20250816100350-->
Q:  Why is virtual memory important?
A: It separates the processes, allows flexible memory use (including sharing and read-only regions), and enables more memory than physically installed via swap
<!--ID: 20250816100350-->
Q:  What is the implementation of memory address map called?
A: Page table
<!--ID: 20250816100350-->
Q:  Why are devices usually only accessible in kernel mode?
A: To prevent improper access (e.g., user process shutting down power)
<!--ID: 20250816100350-->
Q:  How does kernel solve the problem of device differences?
A: By using device drivers that provide a uniform interface to user processes
<!--ID: 20250816100350-->
Q:  
A: 

---

## 💻 Commands Practiced
- Command: `____`
  - What it does:  
  - Example output:  

---

## 🔄 Review Log
- [ ] Day 2: {{date+1d}}
- [ ] Day 4: {{date+3d}}
- [ ] Day 8: {{date+7d}}
- [ ] Day 15: {{date+14d}}

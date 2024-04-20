# Syllabus Class
Free online textbook!: http://pages.cs.wisc.edu/~remzi/OSTEP/
Three Sections of text:
1. Virtualization (first half of course, ==lots of notes==)
	1. Architecture, process scheduling, memory management
2. Concurrency(second half of course, ==lots of programming==)
	1. Threads, deadlock, critical sections, mutual exclusion, etc.
3. Persistence
	1. I/O

## Evaluation
- Multiple projects
	- 1 is C++ acquaintance
	- 1 is process scheduling
	- rest is multithreading
- 2 midterms
- 1 finals (cumulative)

# [[Homework for Operating Systems]]

# Computer System Overview
## Topics
- Basic Elements
- Microprocessors
- Instructions
- Interrupts
- Memory
- I/O Techniques
- Symmetric multi-processors

## [[Basic elements]]

## [[Microprocessors]]

A number of different devices are considered microprocessors as well as some devices you wouldn't have expected to be real!

## Instructions
- A program is a set of instructions stored in memory
- CPU instruction cycle (fetch & execute)
	- program counter (PC) has address of next instruction
	- processor reads (fetches) an instruction from memory
	- instruction stored in instruction register (IR)
	- program counter increments address
	- processor executes instruction; repeat until done
![[Pasted image 20240111101405.png]]

Here's a little more of the [[Fetch & Execute]] cycle.

### Example
1. load AC from memory
2. store store AC to memory
5. add to AC from memory
![[Pasted image 20240111101509.png]]


## Interrupts
- Interrupts normal sequencing of the processor
- Provided to improve processor utilization
	- I/O devices are slower than CPU
	- Without interrupts, CPU must pause to wait for I/O device (wastes its time)
- Interrupts ensure timely process switches
- Interrupts provide safe user access to potentially dangerous instructions (like file read/write)

Where in the instruction cycle is this?
![[Pasted image 20240111102340.png]]
Fetch & Execute & Interrupt
- Same as before, plus an interrupt stage

### Why?
![[Pasted image 20240111102448.png]]
- Polling (left side) CPU periodically checks device to see if it needs attention. Almost always a huge waste of time.
- Instead, start operation, have CPU do other work until notified by interrupt that operation is finished
### Example - why we need interrupts (or why polling is often bad)
- CPU clock 2.5 Ghz or 4x10** -10 seconds per instruction
- Hard Drive 4 x 10**-3 seconds per access

- CPU is 10 million times faster than HD
- Or, if 1 CPU instruction took 1 second, 1 HD access would take 16.5 weeks

**Don't want CPU to wait on HD**

### What happens when CPU is disrupted by an interrupt?
- Finish executing instruction N
- {interrupt}
- store registers, PC (size M) in control stack @ T
- update stack pointer to T-M
- execute interrupt instruction @ Y until finishing @ Y+L
- load back top of control stack
- continue executing @ N+1
![[Pasted image 20240111103037.png]]

A little more on [[Interrupts and Control Stack]].

### Multiple overlapping interrupts
 - An interrupt happens when another is being handled 
 1. Disable interrupts (when handling an interrupt)  
	 2. nd interrupt waits until 1st interrupt is handled  Strictly sequential  2. Use a priority scheme  Interrupts can interrupt interrupt-handling…  …but only if they have a higher priority; otherwise they wait  Hierarchical (by priority)



- (approach 1) Interrupts disabled
![[Pasted image 20240111103543.png]]

- (approach 2) Priority Scheme
![[Pasted image 20240111103623.png]]

## Memory
- Speed (access time), amount, cost
- Memory must keep up with CPU (speed)
	- Faster access time = greater cost
- Memory must satisfy data volumes (amount)
	- Greater capacity = smaller cost = slower access speed
Here is [[Memory Hierarchy]] to see how things are structured in terms of what's important and faster.

### Memory Hierarchy
- cost decreases
- capacity increases
- access time increases
- frequency of access by CPU decreases
	- really? how does it happen?
![[Pasted image 20240116094648.png]]

### Principle of Locality
- Memory references (i.e., data) needed by CPU tend to cluster
- Temporal locality -- near in time. we need the same data soon. For example often go back and execute the same function
- Spatial locality -- near in space/distance, our next access is often very close to our last. For example an array "a" being read in a loop
- Eventually a set of data is replaced by another, but it's less frequent proportionally to the use within a set, which makes overhead bearable

### Performance Example
- 2 levels of memory (L1, L2)
	- T1 @ 0.1 $\mu$s (1kb total) faster but scarce
	- T2 @ 1 $\mu$s (100kb total) slower but plenty
- CPU checks L1 first then L2
- What's the average access time if...
	- 95% of data in L1 and 5% in L2?
		- 0.95 * 0.1$\mu$s + 0.05 * (0.1$\mu$s + 1$\mu$s) = 0.15$\mu$s
	- 5% of data in L1 and 95% in L2?
		- 0.05 * 0.1$\mu$s + 0.95 * (0.1$\mu$s + 1$\mu$s) = 1.05$\mu$s
	- It's to our advantage to have frequently accessed data in faster memory locations
But, what is the [[Reason why caches exist]]?

### Cache
- Exploits the Principle of Locality
- Controlled by hardware (i.e., it is invisible to OS)
- How it's used
	- Contains a copy of a portion of main memory
	- CPU checks cache for data
		- *if found* use data
		- *if not found* reads block of data from memory (where data is) and copies it into cache
![[Pasted image 20240116100524.png]]

## I/O Techniques
More on [[I_O techniques]] 
When the processor encounters an instruction relating to I/O, it executes that instruction by issuing a command to the appropriate I/O module
![[Pasted image 20240116100654.png]]
### What does the CPU do during I/O (read/write) instruction?
A little more on [[What does the CPU do doing I_O instruction]] if wanted.
1. Programmed I/O
	1. CPU waits for completion of command and periodically checks the status of the I/O module until it determines the instruction is complete
		1. CPU sends I/O command to I/O module. If write data is placed in buffer for I/O device.
		2. CPU waits until I/O module completes command.
		3. CPU resumes execution. If read it gets data from buffer
	2. Extreme inefficiency!
2. Interrupt-driven I/O
	1. CPU keeps executing while I/O command is completed
		1. CPU sends I/O command to I/O module. If write data is placed in buffer for IO device.
		2. CPU resumes execution
		3. I/O module triggers an interrupt when command is done.
		4. CPU resumes execution. If read it gets data from buffer.
	2. No wait, but CPU still heavily involved in data transfer
	3. Drawbacks
		1. Transfer rate is limited by the speed with which the processor can service a device
		2. The processor is tied up in managing an I/O transfer since a number of instructions must be executed for each I/O transfer
3. Direct Memory Address (DMA)
	1. Performed by a separate module on the system bus (DMA)
	2. CPU keeps executing while I/O command is completed by DMA module
		1. CPU sends I/O command, memory address (where data is read or written), data size and I/O module to DMA
		2. CPU resumes execution.
		3. I/O module triggers an interrupt when command is done (including data transfer)
		4. CPU resumes execution
	3. No wait & CPU doesn't transfer data (may have bus contention though)
## [[Symmetric Multi-Processors]]
- A stand alone computer system with:
	- 2+ similar processors:
		- Capable of performing the same functions
	- which (physically):
		- are interconnected by a bus
		- share memory & I/O devices
	- are controlled by an OS that
		- provides instructions between processors and their programs (at the job, task, file, and data levels)

- Advantages
	- Performance
		- can yield greater performance (if OS can handle work in parallel)
	- Availability
		- failure of one processor does not halt the machine
	- Scaling
		- additional processors result in a range of products of different price and performance

- Multi-core
	- 2+ processors (core) in 1 micro-chip
		- each core has all components of an independent processor (including 2 or 3 cache levels)
	- Intel Core i7
		- 4-8 cores
		- 8 Mb L3 cache
	- ![[Pasted image 20240116101649.png]]

# [[Computer Boot Sequence]]
1. The processor on the motherboard starts executing instructions at a predetermined address (0xFFFFFFF0) for the x86).
2. This address range contains the BIOS, a discrete chip on the motherboard
The BIOS is flash memory, which means you can update it without removing the chip. The BIOS conducts POST (Power-On-Self-Test), then finds the boot disk and attempts to find the bootloader which starts on the first sector.

# OS Evolution
- Reasons for OS to evolve
	- Hardware & Services
		- New | Upgrades | Fixes

## [[Simple Batch Systems]]
- Improving computer utilization
	- programmer has no direct access to computer
	- operator batches jobs, feeds them to an input device, then...
- Monitor (aka Batch OS)
	- program controlling the execution of jobs
	1. monitor reads next job & yields control of CPU to the job
		1. "control is passed to a job" : CPU starts running user program
	2. user program ends & monitor continues running again
		- "control is returned to the monitor" : CPU runs monitor
## Simple Batch Systems (II)
- Job Control Language ([[JCL]])
	- Instructions meant for the monitor (like pre-processing)
		- (On slide 5)
	- Memory protection
		- Memory where monitor resides is out-of-bounds for jobs
	- Timer
		- Notifies when jobs run longer than anticipated
	- Privileged instructions
		- Instructions that only the monitor can execute (e.g., load job)
	- Interrupts
		- Signals giving CPU a degree of flexibility

# [[Multiprogramming]]
- also known as multitasking
- memory is expanded to hold three, four, or more programs and switch among all of them.

# [[Utilization Histograms]]
## Example
#Important
![[Pasted image 20240118100943.png]]
Job1 uses 70% of the CPU, Job2 and Job3 use 10% each

![[Pasted image 20240118101151.png]]
CPU Utilization:
- Uniprogramming=(.7* 5 + .1 * 25)/30 = 20%
- Multiprogramming = (.9 * 5 + .2 * 5 + .1 * 5)/15 = 40%
==Know how to calculate utilization!== 

# [[Time Sharing Systems]]
- Users access system simultaneously using terminals
- Time Slicing
	- Timer generates interrupts every 0.x seconds (small number)
	- OS preempts current program and loads in another
	- Preempted program & data are stored in memory
	- If memory is full kick victim program to disk
		- *This is a time consuming operation, choose victim wisely*
	- Multiprogramming vs Time sharing
![[Pasted image 20240118101440.png]]

# Achievements
- Major advances in OS development
	- Processes
		- Definition, Errors, Components
	- Memory management
		- OS responsibilities, Virtual memory
	- Scheduling & resource management
	- System structure
# [[Process]]
A *process* is just an instance of a running program

## Cause of Errors
- Improper synchronization
	- a program must wait until the data is available in a buffer
	- improper design of the signaling mechanism can result in loss or duplication
- Nondeterminate program operation
	- program execution is interleaved by the processor when memory is shared
	- the order in which programs are scheduled may affect their outcome
- Failed mutual exclusion
	- more than one user or program attempts to make use of a shared resource at the same time
- Deadlocks
	- it is possible for two or more programs to be hung, waiting for each other
	- may depend on the chance timing of resource allocation and release

## [[Process Management]]
- Process (components)
	- Executable code
	- Data
		- e.g., variables, buffers, ...
	- Execution context (aka "process state")
		- internal data used by the OS to control the process
			- e.g., registers, priority, whether it is waiting for an I/O event
![[Pasted image 20240118103833.png]]
## [[Memory Management]] (Virtual Memory)
- Handling many processes with limited memory
- [[Paging]]
	- Processes are broken into blocks (aka pages)
		- Pages can be anywhere in main memory
	- CPU uses virtual addresses to find instructions/data
		- Addresses are page numbers + offset within page

## [[Scheduling & Resource Management]]
- OS manages resources (main memory, I/O devices, processors) and schedules their use by process
- Fairness
	- Equal processes given equal and fair access to resources
- Differential responsiveness
	- Different processes treated differently according to their needs
- Efficiency
	- Overall performance is a goal
		- [[Maximize Throughput]]
		- [[Minimize Response Time]]
		- accommodate as many users as possible
==These criteria conflict(what's the right balance?)==

## System Structure
- Until recently
	- OS are monolithic programs
	- processes are linearly executed
- Now Microkernel Architecture
	- Keep essential functions in kernel
		- memory addressing, scheduling, ...
	- Modularize the rest (towards object oriented approach)
		- modules dynamically linked, easier to replace
	- Advantages
		- low coupling - dynamically load modules when needed, encourages flexible API design - need new scheduler? Provide library that meets scheduler API, load at runtime
		- Works well with distributed OS - illusion of unified memory & resources
	- Symmetric multiprocessing (add CPUs)
		- 2+ CPU run in parallel (hardware + OS exploiting it)
		- Processes scheduled to separate CPU (but share resources)
	- Multi-threading (divide processes)
		- Process broken into parts that run concurrently (own thread)
		- Process = $\sum$ (threads = concurrent unit of work)
		- Programmers control scope & timing of concurrency
![[Pasted image 20240123100757.png]]

## Symmetric Multiprocessing

**Challenges**
- Scheduling: Scheduling across [[CPU]] cores must be coordinated
- Synchronization: Access to resources must be synchronized
- [[Memory Management]]: Page reuse
- [[Fault Tolerance]]: Graceful degradation
**Parallelism opportunities**
- [[Multiprogramming]] & [[Multi-Threading]] in each processor
- A process could and probably does have its thread executed in different CPUs

# Interrupts
## Motivation
- When a user process is running on the CPU, how does OS stop it?
- When a user process accesses disk, how does OS verify that user has permission?
- When a user process crashes, how does OS regain control?
## Kernel Mode verses User Mode
- Kernel Mode
	- Most privileged
	- Access to entire file system, memory space, all hardware
	- OS runs in this mode
- User Mode
	- Least privileged
	- Access to resources (like files and memory) that belong to current user
	- User processes run in this mode
- Can be implemented with 1 bit in a CPU register, register is only accessible in Kernel mode (means user mode programs cannot modify this bit)
- What mode is [[Process]] in?
	- 0=Kernel
	- 1=User
- Set/Reset when handling interrupts
## [[Interrupt Types]]
- Hardware
	- Raised by hardware devices
	- Can occur at any time (Asynchronous)
	- Examples: timer (process switch), I/O signals
- System calls:
	- [[Software Interrupts]] (Synchronous)
	- Raised by user programs to invoke OS functionality
- Exceptions
	- Generated by processor as a result of illegal action (Synchronous)
	- Faults recoverable (page fault)
	- Aborts difficult to recover (divide by 0)
## Interrupt Servicing
- Remember this cycle is for 1 machine instruction (assembly)
- Not a high level language (like C++)
- Uses lookup table to find correct interrupt handler (coming soon!)
- Works for both synchronous and asynchronous interrupts
- Part of the [[Fetch & Execute]] cycle
![[Pasted image 20240123103932.png]]
#Important 

### Pseudo Code
```pseudo
while (fetch next instruction) {
	run instruction;
	if (interrupt occurred) {
		save process state   //user mode
		find and jump to OS-provided interrupt handler //kernel mode
		restore original process state from kernel stack
	}
	//user mode
}
```
[[Kernel Stack]]

### Better Pseudo Code
```pseudo
while (fetch next instruction) {
	run instruction;
	if (interrupt occurred) {
		save process state //user mode
		find and jump to OS-provided interrupt handler //kernel mode
		OS chooses next process to run
		if new process
			load its state from mem
		else
			restore original process state from kernel stack
	}
	//user mode
}
```

## [[Interrupt Descriptor Table]] (IDT) setup
- OS sets up IDT at boot, its base pointed to by IDT register (IDTR) in CPU
- Each entry is address of an interrupt handler (known as [[Interrupt Service Routine]] (ISR))
- Each ISR handles a particular type of interrupt
![[Pasted image 20240125095329.png]]

## [[Hardware Interrupt]]
**Asynchronous interrupt, can happen anytime**
- Intr# generated by CPU
- Save current process state
- In kernel mode - look up Intr# in IDT
- Jump to, and run [[Interrupt Service Routine]]
- Either return to running process (reload its state including Instruction Pointer (IP) or load and run a new one)
![[Pasted image 20240125095546.png]]

## [[System Calls]]
- Applications cannot perform privileged operations themselves
	- Otherwise they could access devices they should not (DMA controller to access other processes memory), write files they don't have permission too, elevate their privileges, etc.
- Instead, they ask OS  to do so on their behalf by issuing system calls
- OS verifies permissions, then parameters then fulfills request

### System Call Types
1. **Process Control** - process creation, process termination etc.
	1. Ex. fork(), exit(), wait()
2. **File Management** - file manipulation such as creating a file, reading a file, writing into a file etc.
	1. Ex. open(), read(), write(), close() //to file
3. **Device Management** - device manipulation such as reading from device buffers, writing into device buffer etc.
	1. Ex. read(), write()  //to console
4. **Information Maintenance** - handle information and its transfer between the operating system and the user program.
	1. Ex. getpid(), alarm(), sleep()
5. **Communication** - interprocess communication. They also deal with creating and deleting a communication connection
	1. Ex pipe()

## System Call
![[Pasted image 20240125101010.png]]

## Exceptions
- Divide by 0, dereference Null pointer, page fault
- Throws exception interrupt
- Transition to Kernel mode to handle interrupt type as defined in IDT

- Some are recoverable
	- [[Page fault]] - OS blocks current process, request page from mem, loads another process. When page available OS interrupted again and page is loaded and page faulting process can run again
- Some are not
	- Divide by zero, OS logs error, terminates current process, loads a new process.

## System Operation with Interrupts
![[Pasted image 20240125101337.png]]

## Example - 2 programs, HW and system call interrupts
![[Pasted image 20240125101825.png]]

# Processes
## [[Control Block]]
- data structure created & managed by OS
	- Identifier: unique ID
	- State: (e.g., running, blocked)
	- Priority: relative to other processes
	- Program Counter: address of next instruction
	- Memory Pointers: to code & data
	- I/O Status: I/O in use/pending
	- Accounting: CPU time used, IDs, ...
- Data to hold/restore process state on interrupt/resume
	- Key to support multiprocessing

## [[Dispatcher]]
- Program that switches processes in/out of the CPU

```pseudo
OS dispatching loop:
	while(1){
		run process for a while;
		save process state;
		next process = schedule(ready process);
		load next process state;
	}
```
Q1: How to gain control?
Q2: What state must be saved?
Q3: Where to find processes?

## States
- Trace
	- Instructions executed by a process
	- In multiprogramming:
		- interleaving of instructions as processes alternate using the CPU
- Process switches because of interrupts (timer, I/O)

- One CPU
- [[Round-Robin]] (timeout)
- Running: CPU time!
- Not running: or not

- Where do processes come from?
- When do they stop?

## Swapping Processes
![[Pasted image 20240130101648.png]]

![[Pasted image 20240130101729.png]]


## 5 [[Process States|States]]
- New: not yet in memory
- Ready: awaiting its turn
- Running: CPU time!
- Blocked: waiting for I/O
- Exit: done & gone

![[Pasted image 20240130102039.png]]

## 7 States
- What if running I/O intensive processes and all are waiting for I/O?
	- Solution: suspend blocked processes to disk, bring in new (from new or ready/suspend)

## [[Process Tables]]
- OS keeps list of processes. Each entry tracks data about each process (process image)
	- Heap:
	- Globals:
	- Code: program to execute
	- Stack: method call stack frames
	- [[Process Control Block]] (PCB): data OS uses to control process
		- process identification: process/parent/user ID
			- Each process has a unique ID
			- IDs are used for reference:
			- in other tables
			- in inter-process communication
			- when a parent spawns a child process
		- processor state information: user/control registers, stack pointers
		- process control information: scheduling, inter-process comms, ...
	- reference (directly/indirectly) memory, I/O & file tables

# CPU Virtualization
## [[Dispatcher]]
- Low-level mechanism
- Performs context-switch
	- Switch from user mode to kernel mode
	- Save execution state (registers) of old process in Process Control Block (PCB)
	- Insert process in ready queue
	- Load state of next process to run from PCB to registers
	- Switch from kernel to user mode
	- Jump to instruction in new user process
## [[Scheduler]]
- Policy to determine which process gets CPU when

## Vocabulary
- Workload: set of **job** descriptions (arrival time, run_time)
	- Job: view as current CPU burst of a process
	- Process alternates between CPU and I/O, so process moves between ready and blocked queues
- Scheduler: logic that decides which ready jo to run
- Metric: measurement of scheduling quality

## Scheduling Performance Metrics
### Minimize turnaround time
- Do not want to wait long for job to complete
- Completion_time - arrival_time
### Minimize response time
- Schedule interactive jobs promptly so users see output quickly
- Initial_schedule_time - arrival_time
### Minimize waiting time
- Do not want to spend much time in Ready queue
### Maximize throughput
- Want many jobs to complete per unit of time
### Maximize resource utilization
- Keep expensive devices busy
### Minimize overhead
- Reduce number of context switches
### Maximize fairness
- All jobs get same amount of CPU over some time interval

## Workload Assumptions
1. Each job runs for the same amount of time
2. All jobs arrive at the same time
3. All jobs only use the CPU (I/O)
4. Run-time of each job is known

## Example: Workload, scheduler, metric
| JOB | arrival_time(s) | run_time(s) |
| ---- | ---- | ---- |
| A | ~0 | 10 |
| B | ~0 | 10 |
| C | ~0 | 10 |
FIFO: First In, First Out
- Also called FCFS (first come first served)
- run jobs in arrival_time order

## [[FIFO_FCFS|FIFO]]

### [[Gantt chart]]
Illustrates how jobs are scheduled over time on a CPU

## Average Turnaround time
What is the averge turnaround time?
*Def: turnaround_time = completion_time - arrival_time* #Important 

### Example: IDENTICAL Jobs
![[Pasted image 20240201101616.png]]

$$(10 + 20 + 30) / 3 = 20s$$

### Example: A Big Job Last
![[Pasted image 20240201101753.png]]
$$(10 + (10 + 10) + (10+10+60))/3 = 36.67s$$
## [[Convoy Effect]]
When a long job early on slows all jobs (Tractor on road)

### Passing the Tractor
- FIFO: Turnaround time can suffer when short jobs must wait for longs jobs
- SJF: (Shortest Job First) Choose job with smallest run_time

## [[Shortest Job First]]
![[Pasted image 20240201102209.png]]
$$(80+10+20)/3 = ~36.7s$$
Average turnaround time with FIFO: 70s

![[Pasted image 20240201102307.png]]

## Preemptive Scheduling
**Prev Schedulers:** FIFO and SJF are non-preemptive
- Only schedule new job when previous job voluntarily relinquishes CPU (performs I/O or exits)
**New scheduler:** 
- Preemptive: Potentially schedule different job at any point by taking CPU away from running job
- STCF (Shortest Time-to-Completion First)
- Always run job that will complete the quickest

## NON-PREEMPTIVE vs. PREEMPTIVE

- Average turnaround time with STCF? 36.6s
- Average turnaround time with SJF? 63.3s

## Response Time
Sometimes you care about when a job starts instead of when it finishes
New metric:
*response_time = first_run_time - arrival_time* #Important 

## [[Round-Robin|Round-Robin Scheduler]]
**Prev schedulers:** FIFO, SJF, and STCF can have poor response time
**New scheduler:** RR (Round Robin)
Alternate ready processes every fixed-length time-slice

### Response Time
![[Pasted image 20240201103344.png]]

### Turnaround Time
![[Pasted image 20240201103438.png]]

Round Robin has the worst turnaround time.
## Not I/O Aware
Don't let Job A hold on to CPU while blocked waiting for disk!

## I/O Aware (Overlap)
Treat Job A as 3 separate CPU bursts When Job A completes I/O, another Job A is ready 

Each CPU burst is shorter than Job B, so with STCF, Job A preempts Job B

## [[MLFQ|MLFQ (Multi-Level Feedback Queue)]]
Goal: general-purpose scheduling
Must support two job types with distinct goals
- "interactive" programs care about response time
- "batch" programs care about turnaround time
Approach: multiple levels of round-robin; each level has higher priority than lower levels and preempts them

### Priorities
Rule 1: If priority(A) > priority(B), A runs (B doesn't)
Rule 2: If priority(A) == priority(B), A & B run in RR

### History
- Use past behavior of process to predict future behavior
	- Common technique in systems
- Processes alternate between I/O and CPU work
- Guess how CPU burst (job) will behave based on past CPU bursts (jobs) of this process

### More Rules
- Rule 3: Processes start at top priority
- ~~Rule 4: If job uses whole slice, demote process (longer time slices at lower prioritites)~~
- Rule 4: Once a job uses up its time allotment at at given level (regardless of how many times it has given up the CPU), its priority is reduced
- Rule 5: After some time period S, move all the jobs in the system to the topmost queue

# [[Lottery Scheduling]]
- Goal: proportional (fair) share
- Approach:
	- give processes lottery tickets
	- whoever wins runs
	- higher priority => get more tickets

Simple to implement

## Other Lottery Ideas
Ticket transfers
Ticket currencies
Ticket inflation

#todo Slides 1 - 22 in Memory Virtualization

# [[How to Virtualize Memory]]
Problem: How to run multiple processes simultaneously?
Addresses are "hardcoded" into process binaries
How to avoid collisions?
1. Time Sharing
2. Static Relocation
3. Base
4. Base+Bounds
5. Segmentation

## [[Time Sharing of Memory]]
Try similar approach to how OS virtualizes CPU
Observation:
OS gives illusion of many virtual CPUs by saving CPU registers to memory when a process isn’t running
Could give illusion of many virtual memories by saving memory to disk when process isn’t running
### Problem
Ridiculously poor performance, so its not used
Better Alternative: Space Sharing
	At same time, space of memory is divided across processes

## [[Static Relocation]]

Never use absolute address, always use relative address
## [[Base]]

## [[Base and Bounds]]

## [[Segmentation]]

### [[Address Translation with Segmentation]]

### Example
![[Pasted image 20240213095818.png]]

### Advantages of Segmentation
- Enables sparse allocation of address space
- Different protection for different segments
- Enables sharing of selected segments
- Supports dynamic relocation of each segments
### Disadvantages of Segmentation
- Each segment must be allocated contiguously
- Fix with paging
## ^ But none of these actually work ^
It doesn't work because of the contiguous requirement

# [[Fragmentation]]
Free memory that can't be usefully allocated
Why?
- Free memory is too small and scattered
Types of fragmentation
- External
- Internal

# [[Paging]]
**Goal:** Elimante requirement that address space is contiguous
- Elim. external fragmentation
- Grow segments as needed
**Idea:** Divide address spaces and physical memory into fixed-sized pages
- Size $2^n$, Example 4KD (n=12)
- Physical page: page frame
## Translation of Page Addresses
- How to translate logical address to physical address?
	- High order bits of address designate page number
	- Low-order bits of address designate offset within page

## Virtual => [[Virtual-to-Physical Page Mapping|Physical Page Mapping]]
Number of bits in virtual address format does not need to equal number of bits in physical address format

[[How should OS translate VPN to PPN|How should OS translate VPN to PPN?]]
For segmentation, OS used a formula (e.g., phys addr = virt_offset + base_reg)
For paging, OS needs more general mapping mechanism
What data structure is good?

**Have to know**
_#_ of bits (System Size Bits (SSbits)) = 14
Page size = offset => offset bits = $2^8$ = $256$ 
VPN_bits == SS_bits - Offset

(In the example on the board) $VPN_b = 14 - 3 = 11$
Page size = $2^3 = 8$ bytes

## Where are [[Page Table|Page Tables]] Stored?
How big is a typical page table?
- Assume **32- bit** address space
- Assume 4 KB pages
- Assume 4 byte entries per page table row

Final answer: $2^{(32 -log(4\text{KB}))} * 4 = 4\text{MB}$
- Page table size = Num entires * size of each entry
- Num entries = num virtual pages = 2^(bits for vpn)
- Bits for vpn = 32 - number of bits for page offset = 32 - log(4KB) = 32 - 12 = 20
- Num entires = 2^20 = 1MB
- Page table size = Num entries * 4 bytes = 4MB

Implication: Store each page table in memory
	Hardware finds page table base with register (e.g., CR3 on x86)
What happens on a context switch?
	Change page table register to point to new page table

## Other PT info
What other info is in pagetable entries besides translation?
- Valid bit
- Protection bits (R/W)
- Present bits (is it memory or on disk?)
- Reference bit (used for page eviction algorithms)
- Dirty bit (has a page changed and thus needs to be rewritten to disk)

Pagetable entries are just bits stored in memory
	Agreement between hw and OS about interpretation

## Advantages of Paging
No external fragmentation
- Any page can be placed in any frame in physical memory
Fast to allocate and free
- Alloc: No searching for suitable free space
- Free: Doesn't have to coallesce with adjacent free space
- Just use bitmap to show free/allocated page frames
Simple to swap-out portions of memory to disk (later lecture)
- Page size matches disk block size
- Can run process when some pages are on disk
- Add "present" bit to PTE

## Disadvantages of Paging
Internal fragmentation: Page size may not match size needed by process
	Wasted memory grows with larger pages
Additional memory reference to page -> very inefficient
	Page table must be stored in memory
	MMU stores only base address of page table
	Solution: Add TLBs (a fast cahce... and a future lecture)
Storage for page tables may be substantial
1. Additional memory reference to look up in page table
	- Very inefficient
	- page table must be stored in memory
	- MMU stores only base address of page table (processor tells it which page table to use)
	- Avoid extra memory reference for lookup with TLBs (previous lecture)
2. Storage for page tables may be substantial
	- Simple page table: requires PTE for all pages in address space
		- Entry needed even if page not allocated
	- Problematic with dynamic stack and heap within address space

## Quiz: How big are page tables 
#study
1. PTE's are 2 bytes, and 32 possible virtual page numbers            -> 32 * 2 bytes = 64 bytes
2. PTE's are 2 bytes, virtual addrs are 24 bits, pages are 16 bytes  -> 2 bytes * 2^(24-lg16) = 2 * 2^20 bytes = 2 MB / 2^17 pages
3. PTE's are 4 bytes, virutal addrs are 32 bits, and pages are 4 KB -> 4 bytes * 2^(32 - lg 4k) = 4 * 2^20 bytes = 4 MB
	- Page size = 4KB = 2^12
	- 32 bits - 12 bits for the offset = 20 page numbers
4. PTE's are 8 bytes, virtual addrs are 64 bits, and pages are 4 KB -> 8 bytes * 2 ^ (64 - lg 4K) = 8 * 2^52 = a big number

## Avoid simple linear Page Tables
Use more complex page tables, instead of just big array
Any data structure is possible with software-managed TLB
- Hardware looks for vpn in TLB on every memory access
- If TLB does not contain vpn, TLB miss
	- Trap into OS and let OS find vpn->ppn translation
	- OS notifies TLB of vpn -> ppn for future access

## Multilevel Page Tables
Goal: Allow page tables to be allocated non-contiguosuly
Idea: Page the page tables
- Creates multiple levels of pages tables; outer level "page directory"
- Only allocate page tables for pages in use
- Used in x86 architectures (hardware can walk known structure)

Instead of having a ton of bits pointing to some random point in a massive page table, break the virtual address into multiple address to reference multiple page tables
Instead of <mark style="background: #ABF7F7A6;"> 0000</mark><mark style="background: #D2B3FFA6;">001</mark> it will now be <mark style="background: #FFB86CA6;">00</mark><mark style="background: #ABF7F7A6;">00</mark><mark style="background: #D2B3FFA6;">001</mark>

### Quiz: Multilevel
![[Pasted image 20240222101932.png]]

1. Translate 0x01ABC -> 
	1. 0x denotes we are in [[hex]], does not affect address (directly)
	2. 0 is the first four bits, the outer page table. Start at the 0th entry in the outer page table and follow to inner page table
	3. 1 is the next four bits, which says the second entry, 0x23, and then append the offset which is 12 bits or 3 hex characters
	4. Answer is 0x23ABC
2. Translate 0x00000
	1. Same steps as before
	2. Answer is 0x10000
3. Translate 0xFEED0
	1. Same steps as before
	2. Answer is 0x55EDO

### Quiz: Address format for multilevel Paging
30-bit address:
- Page offset is 12 bits

How should logical address be structured
- How many bits for each paging level?
Goal?
- Each page table fits within a page
- PTE size * number PTE = page size
	- Assume PTE size = 4 bytes
	- Page size = 2^12 bytes = 4KB
		- $4 \text{bytes} \cdot X = 4\text{KB}$
		- $X = \frac{2^{12}}{2^2} = 2^{10}$
	- number PTE = 2^10
- number of bits for selecting inner page = 10
Remaining bits for outer page:
30 - 12 - 10 = 8 bits


**24 bit system**
6 bits offset
- Max page size = 2^6 = 64 bytes

24-6 = 18 vpn

## Quiz: Full System with TLBS
Assume 3-level page table
Assume 256-byte pages (8 bits)
Assume 16-bit addresses (so 8 bits for 3 levels)
Assume ASID of current process is 211

How many physical accesses for each instruction
1. 0xAA10: movl 0x1111, %edi
0xaa: (TLB miss -- 3 for addr trans) + 1 instr fetch
0x11: (TLB miss -- 3 for addr trans) + 1 movl
Total: 8

2. 0xBB13: addl $0x3, %edi
0xbb: (TLB hit -- 0 for addr trans) + 1 instr fetch from 0x9113
Total: 1

3. 0x0519: movl %edi, 0xFF10
0x05: (TLB hit -- 0 for addr trans) + 1 instr fetch 

## Summary: Better PAGE TABLES
Problem: Simple linear page tables require too much contiguous memory


## Practice
**What you need:**
- Size of address
- Size of each row in PT in bytes
- Page size (4 bits)

## [[Flat Page Table]]

---

# Midterm 1 - 2/29/24

---
# [[Concurrency]]: [[Threads]]
## Motivation
CPU trend: same speed, but multiple
Goal: write applications that fully utilize many cores

### Option 1: build apps from many communicating processes
- Example: chrome (process per tab)
- communicate via pipe() or similar

Pros?
- Don't need new abstractions; good for security

Cons?
- Cumbersome programming
- High communicatoin overheads
- Expensive context switching

### Option 2: new abstraction -> thread

threads are like processes, except: multiple threads of same process share an address space

divide large task across several cooperative threads, communicate through shared address space

## Common Programming Models
Multi-threaded programs tend to be structured as:
- Producer/consumer: Multiple producer threads create data (or work) that is handled by one of the multiple consumer threads
- Pipeline: Task is divided into series of subtasks, each of which is handled in series by a different thread
- Defer work with background thread: One thread performs non-critical work in the background (when CPU idle)

## What state do threads share?
They share the page table of their host process

Do threads share instruction pointer?

Show process address space and how a thread fits in

Share code, but each thread may be executing different code at the same time
So, different instruction pointers

Do threads share stack pointers?
No... threads executing different functions need different stacks

## Thread VS. Process
Multiple threads within a single process share:
- Process ID (PID)
- Address space
	- Code (instructions)
	- Most data (heap)
- Open file descriptors
- Current working directory
- User and group ID
Each thread has its own
- Thread ID (TID)
- Set of registers, including Program counter and Stack pointer
- Stack for local variables and return addresses (in same address space)

## Thread API
Variety of thread systems exist
- POSIX Pthreads

Common thread operations
- Create
- Exit
- Join (instead of wait() for processes)

## OS Support: Approach 1
**User-level threads: Many-to-one thread mapping**
- Implemented by user-level threads
	- Create, schedule, synchronize threads at user-level
- OS is not aware of user-level threads
	- OS thinks each process contains only a single thread of control
Advantages
- Does not require OS support; Portable
- Can tune scheduling policy to meet application demands
- Lower overhead thread operations since no system call
Disadvantages
- Cannot leverage multiprocessors
- Entire process blocks when one thread blocks

## OS Support: Approach 2
**Kernel-level threads: One-to-one thread mapping**
- OS provides each user-level thread with a kernel thread
- Each kernel thread scheduled independently
- Thread operations (creation, scheduling, synchronization) performed by OS
Advantages
- Each kernel-level thread can run in parallel on a multiprocessor
- When one thread blocks, other threads from process can be scheduled
Disadvantages
- Higher overhead for thread operations
- OS must scale well with increasing number of threads


## Non-Determinism
Concurrency leads to non-deterministic results
- Not deterministic result: different results even with same inputs
- race conditions

Whether bug manifests depends on CPU schedule!

Passing tests means little

How to program: imagine scheduler is malicious
Assume scheduler will pick bad ordering at some point...

## Conclusions
Concurrency is needed to obtain high performance by utilizing multiple cores

Threads are muliple execution streams within a single process or address space (share PID and address space, own registers and stack)

Context switches within a critical section can lead to non-determinisitic bugs (race conditions)

Use locks to provide mutual exclusion

# Threads

### Advice
A multithreaded introduction  
Takeaways:  
- Threads - know how to set up your C++ project to use threads (compiler set to use C++ 11 minimum, add the pthread library). See [Eclipse Customizations](https://github.com/CNUClasses/CPSC327/blob/master/content/Lectures/Eclipse_Customizations.pdf) for more info.
Threaded applications can be proven incorrect, but not correct since you cant control the scheduler. Therefore testing is not as helpful. Your only defense is to write perfect code, to do this there are some rules to follow;  

- If you start a thread (thread t1(fun)) you must wait for it to finish (t1.join())!
- Never, ever rely on knowledge of system behavior to predict thread run order! You cant tell! (see [Thread_Race_Condition](https://github.com/CNUClasses/Thread_Race_Condition.git))
- Learn to identify minimal critical sections. You want them to be as small as possible since only 1 thread can be in the critical section at a time, the others block and wait.
- To identify critical sections, start by finding all variables that multiple threads can access. This includes all globals, heap based variables that multiple threads are aware of, and all non-threadsafe API's used (like cout)
- Are these globals accessed by more than 1 thread? You probably have critical sections that need protection (synchronization).
- the exception to this rule is a shared variable that is only read, never written. BUT the very first time it's written it needs protection (synchronization) on every read and write
- Atomic classes are great, IFF you have a single line critical section. For multiple lines, you need a mutex (coming next)

## Race Conditions
- Launch 2 threads, the outcome depends on which finishes first
	- Spurious, tough to reproduce (may need exacting set of conditions)
	- Because of this non-determinism they are **tough to debug**

**Imagine these 3 things**
```C++
 int i = 0; //A global int
 i++; // Thread 1
 i--; // Thread 2
```

Each of these instructions are really 3 assembly instructions

The problem is you can't guarantee that all three will run to completion without being interrupted.

Want an atomic operation; a sequence of 1 or more operations that appear indivisible. No other process can see an intermediate state, once started cannot be interrupted.

**So is this atomic?**
```C++
global2++;
--global2;
```
No, it is 3, interruptible, machine instruction
See https://github.com/CNUClasses/thread_problem_atomic_solution.git for project and demo on non-deterministic behaviour

## Ok, make it atomic
**Go from this**
```C++
#include <thread>

using namespace std;
const int NUMB_TIMES = 100000;

// global variable
int global2 = 0;
```

**To this**
```C++
#include <thread>
#include <atomic>

using namespace std;
const int NUMB_TIMES = 100000;

// atomic variable
std::atomic<int> global2(0);
```

<mark style="background: #FF5582A6;">Atomic types are types that encapsulate a value whose access is guaranteed to not cause data races and can be used to synchronize memory accesses among different threads.</mark>

Go to https://github.com/CNUClasses/thread_problem_atomic_solution.git for atomic project and demo solution

## But...
- Atomic protect single lines of code only
- What if you have 3 lines that must be interruptable? Like this
```C++
int bal = 50;

void withdrawmoney(int amt) {
	if (bal > amt) {
		cout<<"approved!"<<endl;
		bal -= amt;
	}
	else {
		cout << "denied!";
	}
}

int main() {
	thread t1 (withdraw, 40);
	thread t2 (withdraw, 25);
}
```

What happens if the `if` statement is interrupted? Not good things! This is called a *critical section* 
	Critical Section: Code that accesses a shared resource, that must complete without interruption. BTW make them as small as possible

*Question: Can you have a critical section in a single threaded environment?* **No** #important

## Critical Section
- Critical Section: Code that accesses a shared resource, where only 1 thread can be at a time. 
- Make them as small as possible! Why? Because in the critical section you potentially go from a multithreaded application, to a single threaded application where the other threads are blocked waiting to get in.

### Critical Sections in this code?
```C++
int g=0;

void fun(){
	g++
}

int main(){
	thread t1(fun);
	int i = g;
	i++;
	g=i;
	t1.join();
}
```

# [[Study for Test 2 410]]

# [[Final Exam Review 410]]

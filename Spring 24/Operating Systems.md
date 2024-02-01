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

## [[Basic Elements]]

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

# [[Process Management]]
- Process (components)
	- Executable code
	- Data
		- e.g., variables, buffers, ...
	- Execution context (aka "process state")
		- internal data used by the OS to control the process
			- e.g., registers, priority, whether it is waiting for an I/O event
![[Pasted image 20240118103833.png]]
# [[Memory Management]] (Virtual Memory)
- Handling many processes with limited memory
- [[Paging]]
	- Processes are broken into blocks (aka pages)
		- Pages can be anywhere in main memory
	- CPU uses virtual addresses to find instructions/data
		- Addresses are page numbers + offset within page

# [[Scheduling & Resource Management]]
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

# System Structure
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

# Symmetric Multiprocessing

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
Rule 1: If priority(A) > priority(B), A runs
Rule 2: If priority(A) == priority(B), A & B run in RR

### History
- Use past behavior of process to predict future behavior
	- Common technique in systems
- Processes alternate between I/O and CPU work
- Guess how CPU burst (job) will behave based on past CPU bursts (jobs) of this process

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

# Homework for Operating Systems
[[Homework for Operating Systems]]

# Computer System Overview
## Topics
- Basic Elements
- Microprocessors
- Instructions
- Interrupts
- Memory
- I/O Techniques
- Symmetric multi-processors

## Basic Elements
What are some [[Basic elements]]?

## Microprocessors
How about some information on [[Microprocessors]]?

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
## Symmetric Multi-Processors
A lot about [[Symmetric Multi-Processors]].
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

# Computer Boot Sequence
A good bit on the [[Computer Boot Sequence]].
1. The processor on the motherboard starts executing instructions at a predetermined address (0xFFFFFFF0) for the x86).
2. This address range contains the BIOS, a discrete chip on the motherboard
The BIOS is flash memory, which means you can update it without removing the chip. The BIOS conducts POST (Power-On-Self-Test), then finds the boot disk and attempts to find the bootloader which starts on the first sector.


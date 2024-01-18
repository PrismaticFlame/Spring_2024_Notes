# Processor
- aka CPU
	- Central Processing Unit
- Controls execution of instructions
- Performs data processing
![[Pasted image 20240109101229.png]]

[[The benefits of smaller microprocessors]] 


# Memory
- aka primary/main memory, RAM
	- Random Access Memory
- Stores instructions & data
- Volatile
	- Contents are lost when the computer is shut down

![[Pasted image 20240109102407.png]]

Not necessary to know, but if you're wondering [[Why put memory in alternating slots]], then its right there

# I/O Modules
- aka device drivers
- Move data between the computer and external devices
	- storage (e.g. hard drive)
	- communications equipment
	- terminals
- Have buffers to push/pull data
![[Pasted image 20240109102855.png]]

The reason all these different brand hard disks/ssd's (samsung, wd) work on the same motherboard is because of [[Device Driver]].

There is also this system to help overall system performance by minimizing the need to repeatedly access slower external storage or devices, and it is called [[Device Driver Caching]].
# System bus
- Means of communication among processors, memory & I/O modules
- Its speed limits computer performance
	- Known as the... [[von Neumman Bottleneck]]
	- Data & Code must pass through the bus (the bottleneck)
	- Physical & Intellectual barrier*
![[Pasted image 20240109103438.png]]

Companies are working on solutions to the von Neumman Bottleneck by adding multiple buses, fast buses between high demand areas like CPU and GPU, but it won't be solved any time soon. ==This is the main "hold up" in computer systems==.

Bus is the slow part, bad. Not a great way to solve this issue yet, but one way is to give each core in the CPU its own cache to store some things in the cache so that it can pull from the memory right next to it instead of going out on the bus and going all the way to memory.
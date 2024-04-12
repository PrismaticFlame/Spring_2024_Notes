**Test 2, 4/16/24. Includes everything from week 6 thru week 13 and project 3. The test will be given to you on paper.  
You may bring 1 sheet of paper with notes on both sides. No other resources are allowed.  
You should know;  
-how to identify and protect critical sections in a multi threaded program  
-how to maximize concurrency in a multithreaded program. For examaple, given 2 unrelated critical sections, you can protect each with a different mutex, and thus have 2 different threads executing in each critical section at the same time.  
-how to recognize and prevent deadlock  
-how to use mutexes in an exception prone environment (use a lock_guard that automatically unlocks)**



# Week 6
## Virtualizing Memory: Faster with TLB
### Reviewing Paging


#### Pros and Cons
Pros:
- No external fragmentation
	- Don't eed to find contiguous RAM
- All free pages are equivalent
	- Easy to manage, allocate, and free pages
Cons:
- Page tables are too big
	- Must have one entry for every page of address space
- Accessing page tables is too slow
	- Doubles number of memory references per instruction

### Translation Steps
1. extract VPN (virt page num) from VA (virt addr)                   (cheap)
2. calculate addr of PTE (page table entry = PTBR + VPN)     (cheap)
3. read PTE from memory                                                            (expensive)
4. extract PFN (page frame num)                                                (cheap)
5. build PA (phys addr)                                                                (cheap)
6. read contents of PA from memory into register                     (expensive)

#### Example: Array Iterator






Test, Test, test
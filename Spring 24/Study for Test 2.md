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
![[array_iterator.png]]


#### Strategy: Cache Page Translations
TLB: Translation Lookaside Buffer

##### Array Iterator w/ TLB
```C++
int sum = 0;
for (i = 0; i < 2048; i++) {
	sum += a[i];
}
```
Assume following virtual address stream:
load 0x1000
load 0x1004
load 0x1008
load 0x100C

Answer:
![[TLBAccess_sequential_example.png]]

#### Performance of TLB?
```C++
int sum = 0;
for (i = 0; i < 2048; i++) {
	sum += a[i];
}
```

As integer is 4 bytes, a[] is an array, its allocated contiguosly in memory. It takes up 2048 * 4 = 8192 bytes <mark style="background: #FFB86CA6;">which takes a min of two and a max of 3 4k pages (assume 2)</mark>

Calculate miss rate of TLB for data:
number of TLB miss / number of TLB look ups (makes sense)

number of TLB lookups? = number of accesses to a = 2048

number of TLB misses?
	= number of unique pages accessed
	= 2048 / (elements of 'a' per 4K page)
	= 2K / (4K / sizeof(int)) = 2K / 1K
	= 2

Miss rate?
	2 / 2048 = 0.1%

Hit rate? ( 1 - miss rate )
	99.9%
would hit rate get better or worse with smaller pages?
<mark style="background: #BBFABBA6;">Worse, still have 2048 lookups but would have to access more pages</mark>

#### TLB Performance
How can system improve TLB performance (hit rate) given fixed number of TLB entries?

Increase page size
	Fewer unique page translations needed to access same amount of memory

TLB Reach: The amount of memory accessible from the TLB.
	TLB Reach = (TLB Size) X (Page Size)

#### TLB Performance with Workloads
Sequential array access almost always hit in TLB
	Very fast!
What access pattern will be slow?
	Highly random to many different pages, with no repeat access

```C++
int sum = 0;
for (i = 0; i < 2048; i++) {
	sum += a[i];
}
```

```C++
int sum = 0;
srand(1234);
for (i = 0; i < 1000; i++) {
	sum += a[rand() % N];
}
srand(1234);
for (i = 0; i < 1000; i++) {
	sum += a[rand() % N];
}
```

#### Workload Locality
**Spatial Locality**: future access will be to nearby addresses
**Temporal Locality**: future access will be repeats to the same data
What TLB characteristics are best for each type?
Spatial:
	Access same page repeatedely; need same vpn -> ppn translation
	Same TLB entry re-used
Temporal:
	Access same address near in future
	Same TLB entry re-used in near future

#### Replacement Policies
**LRU**: evict Least- Recently Use TLB slot when needed
**Random**: Evict randomly chosen entry
Which is better?

LRU troubles: Workload repeatedly accesses same offest across 5 pages (strided access), but only 4 TLB entries

Several slides showing that random is better than "smart" policy

#### Context Switches
What happens if a process uses cached TLB entries from another process?
Solutions?
1. Flush TLB on each switch
	1. Costly; lose all recently cached translations
2. Track which entries are for which process
	1. Address Space Identifier
	2. Tag each TLB entry with an 8-bit ASID
		1. how many unique ASIDs? 2 ** 8 = 256
		2. Why not use PIDs? PID is 32 bits, TLB is small, cannot hold 2 ** 32 processes page table entries.

![[TLBexample_with_asid.png]]

Who Handles TLB MISS? H/W or OS? 
H/W: CPU must know where pagetables are 
	CR3 register on x86 
	Pagetable structure fixed and agreed upon between HW and OS 
	HW “walks” the pagetable and fills TLB 
OS: CPU traps into OS upon TLB miss 
	“Software-managed TLB” 
	OS interprets pagetables as it chooses 
	Modifying TLB entries is privileged 
	- otherwise what could process do? 
Need same protection bits in TLB as pagetable 
- rwx

# Week 8, 9


## Atomics
Atomic types are types that encapsulate a value whose access is guaranteed to not cause data races and can be used to synchronize memory accesses among different threads.  
  
This header declares two C++ classes, [atomic](https://cplusplus.com/atomic) and [atomic_flag](https://cplusplus.com/atomic_flag), that implement all the features of atomic types in self-contained classes. The header also declares an entire set of _C-style_ types and functions compatible with the atomic support in C.

### Types

|contained type|atomic type|description|
|---|---|---|
|`bool`|atomic_bool||
|`char`|atomic_char|atomics for _[fundamental integral types](https://cplusplus.com/is_fundamental)_.  <br>These are either typedefs of the corresponding full specialization of the [atomic](https://cplusplus.com/atomic) class template or a base class of such specialization.|
|`signed char`|atomic_schar|
|`unsigned char`|atomic_uchar|
|`short`|atomic_short|
|`unsigned short`|atomic_ushort|
|`int`|atomic_int|
|`unsigned int`|atomic_uint|
|`long`|atomic_long|
|`unsigned long`|atomic_ulong|
|`long long`|atomic_llong|
|`unsigned long long`|atomic_ullong|
|`wchar_t`|atomic_wchar_t|
|`char16_t`|atomic_char16_t|
|`char32_t`|atomic_char32_t|
|intmax_t|atomic_intmax_t|atomics for _[width-based integrals](https://cplusplus.com/cinttypes)_ (those defined in [<cinttypes>](https://cplusplus.com/%3Ccinttypes%3E)).  <br>Each of these is either an alias of one of the above _atomics for fundamental integral types_ or of a full specialization of the [atomic](https://cplusplus.com/atomic) class template with an _extended integral type_.  <br>  <br>Where _N_ is one in 8, 16, 32, 64, or any other type width supported by the library.|
|uintmax_t|atomic_uintmax_t|
|`int_least`_N_`_t`|`atomic_int_least`_N_`_t`|
|`uint_least`_N_`_t`|`atomic_uint_least`_N_`_t`|
|`int_fast`_N_`_t`|`atomic_int_fast`_N_`_t`|
|`uint_fast`_N_`_t`|`atomic_uint_fast`_N_`_t`|
|intptr_t|atomic_intptr_t|
|uintptr_t|atomic_uintptr_t|
|size_t|atomic_size_t|
|ptrdiff_t|atomic_ptrdiff_t|

## Threads
### Motivation
CPU Trend: Same speed, but multiple cores

Goal: Write applications that fully utilize many cores

Option 1: Build apps from many communicating processes
	Example: Chrome (process per tab)
	Communicate via pipe() or similar

Pros?
	Don't need new abstractions; good for security

Cons?
	Cumbersome programming
	High communication overheads
	Expensive context switching (why expensive?)

Options 2: Thread

Threads are like processes, except: multiple threads of same process share an address space
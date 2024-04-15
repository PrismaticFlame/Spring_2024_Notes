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

Divide large task across several cooperative threads

Communicate through shared address space

### Common Programming Models
Multi-threaded programs tend to be structured as:
- **Producer/Consumer**: multiple producer threads create data (or work) that is handled by one of the multiple consumer threads
- **Pipeline**: Task is divided into series of subtasks, each of which is handled in series by a different thread
- **Defer work with background thread**: one thread performs non-critical work in the background (when CPU idle)

![[threads_stack_pointers.png]]


### Thread vs. Process
Multiple threads within a single process share:
- Thread Group ID (TGID)
- Address space
	- Code (instructions)
	- Most data (heap)
- Open file descriptors
- current working directory
- user and group id

Each thread has its own
- Process ID (PID)
- Set of registers, including Program counter and stack pointer
- Stack for local variables and return addresses (in same address space)

### Thread API
Variety of thread systems exist
- POSIX Pthreads
Common thread operations
- Create
- Exit
- Join (instead of wait() for processes)

### OS Support: Approach 1
User-level threads: Many-to-one thread mapping 
• Implemented by user-level runtime libraries 
	• Create, schedule, synchronize threads at user-level 
• OS is not aware of user-level threads 
	• OS thinks each process contains only a single thread of control 
Advantages 
• Does not require OS support; Portable 
• Can tune scheduling policy to meet application demands 
• Lower overhead thread operations since no system call 
Disadvantages? 
• Cannot leverage multiprocessors 
• If one thread blocks they all block 

### OS Support: Approach 2
Kernel-level threads: One-to-one thread mapping 
• OS provides each user-level thread with a kernel thread 
• Each kernel thread scheduled independently 
• Thread operations (creation, scheduling, synchronization) performed by OS Advantages 
• Each kernel-level thread can run in parallel on a multiprocessor 
• When one thread blocks, other threads from process can be scheduled 

### Aside: Linux Processes and Threads
Linux treats threads as processes
	Parent process pid == tgid
	Launched threads have new pid and **Parents** tigd
	So scheduler sees different pids (for scheduling)
	But same tgid means don't swap memory if swapping to same tgid

### Aside: HTOP
Also means you can just show processes (not their internal threads) by displaying tgid only
Show how HTOP tracks processes and threads
	F2 to setup columns (PID, TGID)
	Show tree view (display options -> to see parent process)

### [[Timeline View (of Thread SchedulE #2)]]

### Non-Determinism
Concurrency leads to non-deterministic results
- Not deterministic result: different results even with same inputs
- race conditions

Whether bug manifests depends on CPU schedule!

Passing test means little

How to program: imagine scheduler is malicious
Assume scheduler will pick bad ordering at some point...


### Conclusions
Concurrency is needed to obtain high performance by utilizing multiple cores

Threads are multiple execution streams within a single process or address space (share PID and address space, own registers and stack)

Context switches within a critical section can lead to non-deterministic bugs (race conditions)

Use locks to provide mutual exclusion

## Threads (pt 2)
Race conditions, atomic variables, critical sections

### Race Conditions
- Launch 2 threads, the outcome depends on which finishes first
	- Spurious, tough to reproduce (may need exacting set of conditions)
	- Because of this non-determinism they are Tough to debug
![[race_conditions_1.png]]

```C++
global2++;
--global2;
```
So, is this atomic?

==No, it's three interruptible machine instructions==
![[race_conditions_2.png]]

**Ok make it atomic**

Go from this
```C++
#include <thread>

using namespace std;
const int NUMB_TIMES = 100000;

//global variable
int global2 = 0;
```

To this
```C++
#include <thread>
#include <atomic>

using namespace std;
const int NUMB_TIMES = 100000;

//atomic variable
std::atomic<int> global2(0);
```

==Atomic types are types that encapsulate a value whose access is guaranteed to not cause data races and can be used to synchronize memory accesses among different threads.==

**But...**
- Atomic protect single lines of code only.
- What if you have 3 lines that must be uninterruptable?

```C++
//starting balance
int bal = 50;

void withdrawmoney(int amt) {
	if (bal>amt) {
		//What happens if you are interrupted right after the if
		//conditional 
		
		//check
		
		//Will not help to make bal an atomic (why?)
		cout<<"approved!"<<endl;
		bal -= amt;
		//What is needed is to make these three lines uninterruptable
		//We call this a "critical section"
	}
	else
		cout<<"denied!";
}

int main() {
	thread t1(withdraw, 40);
	thread t2(withdraw, 25);
}
```

Critical Section: Code that accesses a shared resource, that must complete without interruption. BTW make them as small as possible
Question: Can you have a critical section in a single threaded environment? ==No==

### Critical Section
- Critical Section: Code that accesses a shared resource, where only 1 thread can be at at time.
- Make them as small as possible! Why? Because in the critical section you potentially go from a multithreaded application, to a single threaded application where the other threads are blocked waiting to get in.

Where are critical sections in the following code?
```C++
int g=0;

void fun(){
	g++;
}

int main(){
	thread t1(fun);
	
	int i =g;
	
	i++;
	
	g = i;
	
	t1.join();
}
```

```C++
int g=0;

void fun(){
	g++;
}

int main(){
	//thread t1(fun); What about if no threads?
	
	int i =g;
	
	i++;
	
	g = i;
	
	//t1.join();
}
``` 
*If no threads, then single threaded. no critical sections*

```C++
int g=0;

void fun(){
	int a = g;
}

int main(){
	thread t1(fun);
	
	int i =g;
	
	i++;
	
	g = i; //1
	
	t1.join();
}
```
If fun() just reads g?
g is being written at *1* If 1 write then all reads and writes need protection
These are the critical sections

```C++
int a = g;
```

&

```C++
int i = g;

i++;

g=i;
```

Will these smaller critical sections work (note fun changes)?

```C++
int g = 0;

void fun() {
	g++;//<---
}

int main(){
	thread t1(fun);
	
	int i = g;//<---
	
	i++;
	
	g = i;//<---
	
	t1.join();
}
```

==NO==
In main thread, if *i* receives *g*, then increment *i*, then *t1* changes g, then main thread writes *i* back to *g*? Answer: you overwrite *t1*s changes

![[threads_starts_diff.pdf]]

**BTW... When only reading global variables**
- If all you do is read a global variable, then there is no critical section and no need to protect access to the global variable
- BUT, if you write a global variable at all. Even if just 1 write and 10000 reads.
- Then all 10001 operations are critical and all 10001 must be protected.
```C++
//A global int
int i = 0;

//Thread 1
int j = i ;

//Thread 2
int k = i;
```

### [[Race Condition again - what happens here]]
```C++
#include <iostream>
#include <thread>

void doZero(){}
void doNotZero(){}

int global=2;
void fun(){
	if(global==0)
		doZero();
	else
		doNotZero();
}

int main(){
	std::thread t1(fun);
	global=0;
	t1.join();
	return 0;
}
```

### Summary
- Race conditions - where they occur, learn to recognize them
- Atomics and problems they solve (single line only)
- Critical Sections - an area of code where only 1 thread can be at a time. Learn how to recognize them, make them small (since only one thread should be in them at a time)
	- Question - if you launch no threads, can you have critical sections?
	- Question - if you only read global variables, can you have critical sections?

# Week 10, 11

## Mutual Exclusion (Mutex)
Protects critical sections that are longer than 1 line

- Enforcement
	- Only 1 thread in a critical section at a time
- Availability
	- If no thread in critical section, then any thread can enter
- Minimal Stay
	- Threads stay in critical section for minimal time
- Consistency
	- If resource must be protected anywhere, then it must be protected everywhere

### What it does
```C++
int balance = 60;

void withdraw(int amt) {

	if(balance > amt) { //64
		cout<<"approved"<<endl;
		balance -= amount; //66
	}
}

int main(){
	thread t1(withdraw, 40);
	thread t2(withdraw, 25);
	t1.join();
	t2.join();
}
```

As written, there is a chance that a thread will be interrupted After line 64 but before line 66 executes.
In this case the result will likely be an overdrawn account

We want to ensure that doesn't happen!

First: Identify minimal critical section(s)
```C++
if(balance > amt) {
		cout<<"approved"<<endl;
		balance -= amount;
	}
```

Next: protect critical section(s) with a mutex
```C++
mutex m;
void withdraw(int amt) {
	m.lock();//63, t2 is blocked here
	if(balance > amt) {
		cout<<"approved"<<endl; //<--- t1, line 65
		balance -= amount;
	}
	m.unlock();//68
}
```

Only 1 thread can be executing code between lines 63 and 68 at a time.

Assume t1 is executing line 65
t2 is likely blocked at line 63, waiting for t1 to finish executing line 68.
Once t1 executes line 68, t2 is free to acquire the mutex and proceed

### How to implement
- Hardware enforced
	- Disable interrupts
	- Guarantees atomic code because your code cannot be interrupted
- But...
	- Cannot have overlapping critical sections
	- Cannot switch to other, non-related, processes
	- Will not work on multi-core system unless you disable interrupts on all cores (big performance hit)
	- Kills performance on core
- So... cannot use disabled interrupts solution

```C++
//a special atomic function
int compare_and_swap(int *word, int notlockedval, int lockedval){
	//save original
	int oldval=*word;

	if(oldval==notlockedval){ //if we can
		*word=lockedval;      //then do
	}
	return oldval;
}

const int notlockedval=0;
const int lockedval=1;

int word=notlockedval; //start unlocked

void withdraw(int amt){

	//stay in below loop until compare_and_swap returns lockedval
	while(compare_and_swap(&word,notlockedval, lockedval ) == lockedval{}
	if(balance > amt){
		cout<<"approved"<<endl;
		balance-=amount;
	}
	word=notlockedval;
}
```

Compare and Swap - an atomic operation (once started cannot be interrupted)
1. 1st thread => `word=notlockedval` => line 19 returns false, go to 20
2. 1st thread => interrupted at line 21
3. 2nd thread => line 19 returns true, so it busy waits (spins) burning CPU time
4. 1st thread swapped back and finishes, line 24 set word=notlockedval
5. 2nd thread swapped back, line 19 returns false, goes to 20 and finishes

Compare and Swap
- Good
	- Simple
	- Easily verified
	- Multiprocessor/multiprocess as long as can share memory
- Bad
	- Busy wait (line 19) must keep checking until available, CPU usage spikes, see Spinlock project
	- Starvation and Deadlock both possible
	- Compare_and_swap has to be atomic, this C++ code is not

### Using implementation in C++ 11
- Mutexes are thread based in C++ 11, not process based!
```C++
#include <mutex>
std::mutex g_mutex;        //generally a global value

g_mutex.lock();            //if available then proceed, otherwise thread blocks
g_mutex.unlock();          //unlocks the mutex, other waiting threads can acquire
```

General rules
- Unlock a mutex when you are done (else waiting threads will wait forever)
- Do not lock() a mutex twice from same thread without intermediate unlock(). Otherwise thread will block waiting to acquire a mutex that it has.

### Solve withdrawal problem
```C++
std::mutex mymutex;
void withdraw(int amt){

	mymutex.lock();
	if(balance > amt) {
		cout<<"approved"<<endl;
		//what if an exception is thrown in here?
		balance-=amount;
	}
	mymutex.unlock();
}
```

If at the commented line an exception is thrown
- You will never unlock the mutex
- All threads waiting to enter the critical section will be blocked forever
- Process will never join() those threads
- Process will be blocked forever
- Have to kill and restart process

### A better idea
- Use a self unlocking mutex - as soon as the mutex goes out of scope it unlocks.
```C++
std::mutex mymutex;
void withdraw(int amt){

	lock_guard<std::mutex> lock(mymutex); //locks mymutex here
	if(balance > amt) {
		cout<<"approved"<<endl;
		//BUT WAIT - what if an exception is thrown in here?
		balance-=amount;
	}
	//unlocks mymutex here when the lock_guard goes out of scope
}

lock_guard<std::mutex> lock(mymutex);
```

No worries! the `lock_guard` will unlock as soon as it goes out of scope

### Summary
- Mutexes function as a traffic cop, they allow 1 thread in a critical section at a time, other threads are blocked.
- Prefer a lock_guard over a raw mutex since it automatically unlocks when it goes out of scope
- To use: Identify minimal critical sections, then wrap critical section with an auto unlocking lock_guard
- Mutexes are going to be global variables, they will NOT be local variables

## [[Thread Ticket Agent Slides]]


## Deadlock
(and how you will likely encounter it)

- Classic Deadlock Definition
	- 2 threads - each have a resource that the other wants

```C++
mutex m1;
mutex m2;
void f1(int i) {
	while(i > 0){
		lock_guard<mutex> lg1(m1);
		//if t1 is interrupted here
		lock_guard<mutex> lg2(m2);
	}
}

void f2(int i){
	while(i > 0){
		lock_guard<mutex> lg1(m2); //mutexes acquired out of order
		//then t2 runs and is interrupted here
		lock_guard<mutex> lg2(m1);
	}
}

int main(){
	//the threaded way with 2 mutexes
	thread t1(f1, NUMB_TIMES);
	thread t2(f2, NUMB_TIMES);
	t1.join();
	t2.join();
}
```

After the two interrupts, the program will stop making forward progress
*Demo: simple_deadlock project*

To fix: always acquire lock objects in same order

### Possible Solution
```C++
//the prevention lock is used to protect
//critical sections wehre locks are being acquired
prevention.lock();

//then acquire all necessary locks
//knowing that no other thread can be
//in a critical section protected by
//the prevention lock
l1.lock();
l2.lock();

prevention.unlock();

//grab this lock first
prevention.lock();

l2.lock(); //ordering does not matter now
l1.lock(); //given the prevention lock

prevention.unlock();
```

- Put all lock acquisition in critical sections
- Good
	- Cannot be interrupted while acquiring locks

- Bad
	- Additional lock (prevention) to manage
	- Have to know ahead of time what locks we need
	- Decreases concurrency as we are likely acquiring locks early. Critical sections are larger than needed

- But probably about as good as it will get

### Things that act like deadlock
```C++
mutex m;
void fun2(){
	m.lock();
}
void fun1(){
	m.lock();
	fun2();
}
int main(){
	//superficial blocking? Its actually undefined
	//from the C++ 11 standard
	//30.4.1.2.1/4 [Note: A program may deadlock if the thread that owns
	// a mutex object calls lock() on that object.]
	//it MAY, or it may not block. It may work on 1 compiler and not another
	m.lock();
	m.lock(); //This causes thread to block and wait to acquire a lock that it
			  //already owns
	//the way locking twice without really happens
	fun1(); //This is how it happens in real code
}
```

- Locking twice on the same thread without an intervening unlock

### Deadlock - the real world
- Locking is not so simple, especially if you have more than 1 lock
- Locks are spread out among classes, functions and libraries with many conditional satements
- Its often hard to see what the lock ordering will be
- Once a program deadlocks it stops, it does not consume processor cycles, or any more memory than it had when the deadlock occurred. But it will never exit. It must be killed and restarted


# Week 12, 13

## Condition Variable - Website
`std::condition_variable` is a synchronization primitive used with a [std::mutex](https://en.cppreference.com/w/cpp/thread/mutex "cpp/thread/mutex") to block one or more threads until another thread both modifies a shared variable (the _condition_) and notifies the `std::condition_variable`.

The thread that intends to modify the shared variable must:

1. Acquire a [std::mutex](https://en.cppreference.com/w/cpp/thread/mutex "cpp/thread/mutex") (typically via [std::lock_guard](https://en.cppreference.com/w/cpp/thread/lock_guard "cpp/thread/lock guard")).
2. Modify the shared variable while the lock is owned.
3. Call [notify_one](https://en.cppreference.com/w/cpp/thread/condition_variable/notify_one "cpp/thread/condition variable/notify one") or [notify_all](https://en.cppreference.com/w/cpp/thread/condition_variable/notify_all "cpp/thread/condition variable/notify all") on the `std::condition_variable` (can be done after releasing the lock).

Even if the shared variable is atomic, it must be modified while owning the mutex to [correctly](https://stackoverflow.com/questions/38147825/) publish the modification to the waiting thread.

Any thread that intends to wait on a `std::condition_variable` must:

1. Acquire a [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock)<[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)> on the mutex used to protect the shared variable.
2. Do one of the following:

1. Check the condition, in case it was already updated and notified.
2. Call [wait](https://en.cppreference.com/w/cpp/thread/condition_variable/wait "cpp/thread/condition variable/wait"), [wait_for](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_for "cpp/thread/condition variable/wait for"), or [wait_until](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_until "cpp/thread/condition variable/wait until") on the `std::condition_variable` (atomically releases the mutex and suspends thread execution until the condition variable is notified, a timeout expires, or a [spurious wakeup](https://en.wikipedia.org/wiki/Spurious_wakeup "enwiki:Spurious wakeup") occurs, then atomically acquires the mutex before returning).
3. Check the condition and resume waiting if not satisfied.

or:

1. Use the predicated overload of [wait](https://en.cppreference.com/w/cpp/thread/condition_variable/wait "cpp/thread/condition variable/wait"), [wait_for](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_for "cpp/thread/condition variable/wait for"), and [wait_until](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_until "cpp/thread/condition variable/wait until"), which performs the same three steps.

`std::condition_variable` works only with [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock)<[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)>, which allows for maximal efficiency on some platforms. [std::condition_variable_any](https://en.cppreference.com/w/cpp/thread/condition_variable_any "cpp/thread/condition variable any") provides a condition variable that works with any [BasicLockable](https://en.cppreference.com/w/cpp/named_req/BasicLockable "cpp/named req/BasicLockable") object, such as [std::shared_lock](https://en.cppreference.com/w/cpp/thread/shared_lock "cpp/thread/shared lock").

Condition variables permit concurrent invocation of the [wait](https://en.cppreference.com/w/cpp/thread/condition_variable/wait "cpp/thread/condition variable/wait"), [wait_for](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_for "cpp/thread/condition variable/wait for"), [wait_until](https://en.cppreference.com/w/cpp/thread/condition_variable/wait_until "cpp/thread/condition variable/wait until"), [notify_one](https://en.cppreference.com/w/cpp/thread/condition_variable/notify_one "cpp/thread/condition variable/notify one") and [notify_all](https://en.cppreference.com/w/cpp/thread/condition_variable/notify_all "cpp/thread/condition variable/notify all") member functions.

The class `std::condition_variable` is a [StandardLayoutType](https://en.cppreference.com/w/cpp/named_req/StandardLayoutType "cpp/named req/StandardLayoutType"). It is not [CopyConstructible](https://en.cppreference.com/w/cpp/named_req/CopyConstructible "cpp/named req/CopyConstructible"), [MoveConstructible](https://en.cppreference.com/w/cpp/named_req/MoveConstructible "cpp/named req/MoveConstructible"), [CopyAssignable](https://en.cppreference.com/w/cpp/named_req/CopyAssignable "cpp/named req/CopyAssignable"), or [MoveAssignable](https://en.cppreference.com/w/cpp/named_req/MoveAssignable "cpp/named req/MoveAssignable")

### Example
`std::condition_variable` is used in combination with a `std::mutex` to facilitate inter-thread communication
```C++
#include <condition_variable>
#include <iostream>
#include <mutex>
#include <string>
#include <thread>
 
[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex) m;
std::condition_variable cv;
[std::string](http://en.cppreference.com/w/cpp/string/basic_string) data;
bool ready = false;
bool processed = false;
 
void worker_thread()
{
    // wait until main() sends data
    [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock) lk(m);
    cv.wait(lk, []{ return ready; });
 
    // after the wait, we own the lock
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Worker thread is processing data\n";
    data += " after processing";
 
    // send data back to main()
    processed = true;
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Worker thread signals data processing completed\n";
 
    // manual unlocking is done before notifying, to avoid waking up
    // the waiting thread only to block again (see notify_one for details)
    lk.unlock();
    cv.notify_one();
}
 
int main()
{
    [std::thread](http://en.cppreference.com/w/cpp/thread/thread) worker(worker_thread);
 
    data = "Example data";
    // send data to the worker thread
    {
        [std::lock_guard](http://en.cppreference.com/w/cpp/thread/lock_guard) lk(m);
        ready = true;
        [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "main() signals data ready for processing\n";
    }
    cv.notify_one();
 
    // wait for the worker
    {
        [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock) lk(m);
        cv.wait(lk, []{ return processed; });
    }
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Back in main(), data = " << data << '\n';
 
    worker.join();
}
```

Output:
```C++
main() signals data ready for processing
Worker thread is processing data
Worker thread signals data processing completed
Back in main(), data = Example data after processing
```

## Condition Variables - Slides
**How do you signal between threads?**
- What if you want to ensure that one thread starts before another (1 thread waits until another thread says go)
- Or to check if a condition is true before proceeding?

What we want:
```C++
//a global
bool isReady=false;

//Thread 1
# efficiently waiting on isReady == True

//Thread 2
# sets isReady==True and then wakes up Thread 1
```

### How do you signal between threads?
- As an example, if I launch 2 threads;
	- 1 to deposit $100
	- 1 to withdraw $90
- I want to deposit to finish first (otherwise overdraft)
- How to do this?
```C++
//how do you ensure you deposit before withdraw?
thread thread1(withdraw, 50);
thread thread2(deposit, 90);
```

- Start with this code (BTW, it does not ensure the deposit occurs first)
Thread 1
```C++
mutex m;
int balance = 0;

void withdraw(int amount){

	lock_guard<mutex> lck(m);
	balance -= amount;
	if(balance < 0){
		cout<<"You are overdrawn"<<endl;
	} else {
		cout<<"no worries"<<endl;
	}
}
``` 

Thread 2
```C++
void deposit(int amount){
	//deposit is delayed!
	std::this_thread::slee_for(std::chrono::milliseconds)//...

	lock_guard<mutex> lck(m); //waiting for mutex
	balance += amount;
}
```

### Can use a spin lock
- Works but at a cost!
- High CPU usage!
- See [Simple_Condition_Variable](https://github.com/CNUClasses/Simple_Condition_Variable) project, call up System Monitor and watch one cores usages spike
```C++
mutex m;
int balance = 0;
bool deposit_made = false;

void withdraw(int amount){
	//the bad idea, a busy wait
	while (!deposit_made){}

	lock_guard<mutex> lck(m);
	balance -= amount;
	if(balance < 0){
		cout<<"You are overdrawn"<<endl;
	} else {
		cout<<"no worries"<<endl;
	}
}
```

```C++
void deposit(int amount){
	//deposit is delayed!
	std::this_thread::slee_for(std::chrono::milliseconds)//...

	lock_guard<mutex> lck(m); //waiting for mutex
	balance += amount;
	deposit_made = true;
}
```

### Get ride of that spinning
- Instead would like to put the waiting thread to sleep until the event occurs...
- And then wake it up
- No more spiking CPU core usage!

### Use condition variables
- First the proper include (works with C++ 11 and above)
`#include <condition_variable>`
- And a new kind of lock object
```C++
//just like a lock_guard
//PLUS you can manually unlock it!
unique_locK<mutex> lck(m);
```
- Works just like a lock guard
- Except you can manually unlock it
- AND IT'S THE ONLY KIND OF LOCK A CONDITION_VARIABLE CAN WAIT ON!

### Use condition variables
Thread 1
```C++
mutex m;
int balance = 0;
bool deposit_made = false;
condition_variable cv;

void withdraw(int amount){
	//just like a lock_guard
	//PLUS you can manually unlock it!
	unique_lock<mutex> lck(m); //Note the unique lock
	
	//MUST be a loop to handle
	//spurious wakeups
	while(!deposit_made){
		cv.wait(lck);    //if here, release lock
						 //and then sleep until
						 //awakened
	}

	balance -= amount;
	if(balance < 0){
		cout<<"You are overdrawn"<<endl;
	} else {
		cout<<"no worries"<<endl;
	}
}
```

- Note the unique lock `unique_lock<mutex> lck(m);`
- `while(!deposit_made)` This MUST be a while loop so Thread can go back to sleep if it wakes and the condition evaluates to false
	- Can be any expression that evaluates to a bool 
		- for instance: `(!deposit_made && !likes_dogs)`
- `balance -= amount;` If you get here thread has awakened, acquired lock, checked condition (!deposit_made) and broken out of while loop. Code owns lck at this point


Thread 2
```C++
void deposit(int amount){
	//deposit is delayed!
	std::this_thread::slee_for(std::chrono::milliseconds)//...
	{
		lock_guard<mutex> lck(m);
		balance += amount;
		
		//must change condition while locked!
		deposit_made = true;
	}
	//must release lock before notify notify_all wakes ALL threads
	//waiting on this cv. One will acquire the mutex, check condition
	//in while and move forward the other go back to sleep
	cv.notify_all();
}
```

```C++
lock_guard<mutex> lck(m);
balance += amount;
```
- Lock_guard, unique_lock... Whatever, just lock it!
- `deposit_made = true;` Boolean used in waiting threads while loop
	- Change value to indicate waiting thread should wake
- (End of sleep_for) Lock_guard goes out of scope here, make sure you release mutex before signaling!
- `cv.notify_all();` Wake up every thread waiting on condition_variable cv

### Problem - Spurious wakeup
- **Spurious wakeup** - sometimes the receiver wakes up, although notification happened. POSIX Threads and the Windows API are vulnerable to this.
- That's why we have the while loop
- If thread awakes without condition being changed it just goes back to sleep

### Problem - Lost Wakeup
- **Lost wakeup** - the sender sends its notification before the receiver waits on the cv. So the notification is lost (but not in this code)
- What happens if Thread2 notifies when Thread1 is at any arrow below?
- (Keep in mind who holds the lock)
- No worries here
```C++
void withdraw(int amount){
	//just like a lock_guard
	//PLUS you can manually unlock it!                   <--
	unique_lock<mutex> lck(m); //Note the unique lock
	
	//MUST be a loop to handle
	//spurious wakeups
	while(!deposit_made){
		cv.wait(lck);    //if here, release lock          <--
						 //and then sleep until
						 //awakened
	}

	balance -= amount;
	if(balance < 0){
		cout<<"You are overdrawn"<<endl;
	} else {
		cout<<"no worries"<<endl;
	}
}
```

### Condition variables - notifying
- **notify_one();**   
	- wake just 1 thread waiting
- **notify_all();**
	- wake them all, 1 will acquire the mutex, go about its business, then the next acquires mutex etc

- I use notify_all for convenience in this class because I often have more than 1 thread waiting on the condition_variable and I want them all to awake
- If I used notify_one instead and had multiple threads, one would wake up and the rest would sleep, possibly never awakening and blocking my program

### Condition variables - waiting
- **'wait'** releases the mutex until condition_variable is signaled


- **cv.wait**           wait until notified
- **cv.wait_for**    timed version of wait
- **cv.wait_until**  ''

## Producer Consumer
- One thread produces widget
- One thread consumes widgets

- Producer thread is in charge - tells consumer to get to work
- Consumer thread waits until told to work and then does so

Can do it 2 ways;
- Partially coordinated: No confirmation from consumer
![[prod_cons_1.png]]
- Coordinated: lockstep coordination between producer and consumer
![[prod_cons_2.png]]

### Producer Consumer  - Outline
(partially coordinated)
```C++
//globals
gCount = 0; //tracks widgets
bDone = false; //is producer finished?
```
![[prod_cons_3.png]]
![[prod_cons_4.png]]

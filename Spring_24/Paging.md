---
aliases:
  - Paging
  - Memory Management
  - Memory
---
Paging is a memory management scheme used in computer operating systems to implement virtual memory. It allows processes to use memory addresses that are independent of the physical memory layout. In a paged memory system, both physical and virtual memory are divided into fixed-size blocks called pages. These pages serve as the basic unit of data transfer between physical and virtual memory. Let's explore the key concepts and mechanisms of paging:

### Key Concepts of Paging:

1. **Page Size:**
   - The operating system divides both physical and virtual memory into fixed-size pages. The page size is determined by the hardware architecture and operating system design. Common page sizes include 4 KB or 8 KB.

2. **[[Page Table]]:**
   - To keep track of the mapping between virtual and physical pages, the operating system maintains a data structure called the page table. The page table contains entries that map virtual page numbers to corresponding physical page numbers.

3. **Page Number and [[Offset]]:**
   - In the virtual address space, an address is divided into two parts: the page number and the offset within the page. The page number is used to index the page table, while the offset determines the specific location within the page.

4. **[[Page fault]]:**
   - A page fault occurs when a process attempts to access a virtual page that is not currently in physical memory. The operating system must then bring the required page into memory from secondary storage.

5. **Backing Store (Swap Space):**
   - When a page is not in physical memory, it is stored in a backing store (e.g., a disk). The operating system swaps pages in and out of physical memory as needed.

6. **Page Replacement Algorithm:**
   - When physical memory is full and a new page needs to be brought in, the operating system must decide which existing page to remove. This decision is made by a page replacement algorithm, such as Least Recently Used (LRU) or First-In-First-Out (FIFO).

7. **[[TLB]] (Translation Lookaside Buffer):**
   - The Translation Lookaside Buffer is a cache that stores a subset of page table entries to accelerate address translation. It reduces the need to access the full page table for frequently used pages.

### Paging Mechanism:

1. **Virtual to Physical Address Translation:**
   - When a process generates a virtual address, the operating system extracts the page number and offset. The page number is used to index the page table, obtaining the corresponding physical page number. The offset determines the location within the physical page.

2. **Page Fault Handling:**
   - If a page fault occurs (i.e., the required page is not in physical memory), the operating system initiates a page fault handler. The handler retrieves the required page from the backing store, updates the page table, and restarts the interrupted instruction.

3. **Page Replacement:**
   - When physical memory is full and a new page must be brought in, the operating system selects a victim page for replacement using a page replacement algorithm. The victim page is then swapped out to the backing store, and the new page is brought in.

4. **Benefits of Paging:**
   - **Simplified Memory Management:** Paging simplifies memory management by breaking physical and virtual memory into fixed-size blocks, allowing for more straightforward allocation and deallocation.
   - **Isolation:** Each process has its own page table, ensuring isolation and preventing one process from accessing the memory of another.

5. **Challenges of Paging:**
   - **[[Fragmentation]]:** Paging helps reduce external fragmentation but can still lead to internal fragmentation within pages.
   - **Overhead:** Maintaining and updating the page table incurs overhead, and frequent page faults may impact performance.

### [[TLB]] (Translation Lookaside Buffer):

1. **TLB Function:**
   - The TLB caches a subset of page table entries to accelerate virtual-to-physical address translation.

2. **TLB Miss:**
   - If the TLB does not contain the required entry (TLB miss), the operating system performs a full page table lookup and updates the TLB.

3. **TLB Replacement:**
   - Similar to page replacement, the TLB may use replacement algorithms to determine which entry to evict when the TLB is full.

Paging is a fundamental technique in virtual memory systems, allowing for efficient utilization of physical memory resources and providing an abstraction layer between the virtual and physical address spaces. It plays a crucial role in modern operating systems, enabling processes to utilize more memory than physically available and facilitating dynamic memory allocation and deallocation.


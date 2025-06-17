# Heap-Management : Virtual Memory Allocation using Buddy System
This project implements a virtual heap-memory management system in C, designed to simulate dynamic memory allocation and deallocation.

## Project Overview
This system aims to provide a low-level understanding of memory management by simulating a "heap" region where memory of a particular size can be requested and freed. At its core, it utilizes the efficient **Buddy System** algorithm to manage memory blocks, providing a practical demonstration of how a programming language might handle dynamic memory allocation requests.

## Features

* **Virtual Heap Creation:** Initialize a contiguous block of memory to act as the virtual heap. (An array of 1024 bytes used in this case)
* **Memory Allocation (`malloc` simulation):** Request memory blocks of specified sizes. The system will find and allocate the most suitable block using the Buddy System.
* **Memory Deallocation (`free` simulation):** Release previously allocated memory blocks, which are then reintegrated into the available memory pool.
* **Buddy System Implementation:** Efficiently manages free and allocated memory blocks by dividing and merging them in powers of two.
* **Memory Visualization:** The underlying structure allows for conceptual visualization of memory fragmentation and allocation patterns.

## The Buddy System Explained

The Buddy System is a memory allocation algorithm that efficiently manages memory by dividing it into blocks of sizes that are powers of two. It's particularly effective at minimizing external fragmentation (unused memory between allocated blocks) and allowing for fast allocation and deallocation.

### How it Works

1.  **Initial State:** The entire memory heap is treated as one large block, typically a power of two in size (e.g., 256KB, 1MB).

2.  **Allocation:**
    * When a request for `N` bytes is made, the system finds the smallest power-of-two block size (`S`) that is greater than or equal to `N`.
    * If a free block of size `S` is available, it's allocated.
    * If no free block of size `S` is available, but a larger free block (e.g., `2S`) exists, that larger block is recursively split into two equal-sized "buddy" blocks of size `S`. One of these `S`-sized blocks is then allocated, and the other remains free.
    * This splitting continues until a block of the exact requested or next-power-of-two size is found and allocated, or until the smallest possible block size is reached.

3.  **Deallocation:**
    * When a block is freed, the system checks its "buddy." A buddy is another block of the same size that, if combined with the freed block, would form a larger power-of-two block.
    * If the buddy is also free, the two blocks are merged to form a larger block (e.g., two 16KB blocks merge to form one 32KB block).
    * This merging process continues recursively. If the newly merged block's buddy is also free, they too are merged, and so on, until an allocated buddy is encountered or the entire heap is reassembled.

### Advantages of the Buddy System

* **Fast Allocation/Deallocation:** Operations involve simple arithmetic (finding powers of two, calculating addresses) and bitwise operations, leading to quick performance.
* **Reduced External Fragmentation:** The merging of free buddy blocks helps to consolidate small free blocks into larger ones, making more contiguous memory available for larger requests.
* **Simplicity:** The underlying logic is relatively straightforward compared to some other complex memory management schemes.

The allocation and freeing have been done using the Buddy-system. 
This project implements the core logic of the Buddy System using C. It manages a data structure (An array of linked-lists of Free Blocks of sizes with different powers of 2) to keep track of available memory. When a `malloc` equivalent is called, the system traverses these structures, performs necessary splits, and updates the free list. Conversely, a `free` equivalent triggers the merging process, returning blocks to larger available chunks.

### Installation
**Clone the repository:**

    
    git clone https://github.com/Cpt-Shaan/Heap-Management.git
    cd Heap-Management
    

   

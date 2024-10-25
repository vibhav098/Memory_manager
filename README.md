# Memory Manager

This project implements a memory management system simulating virtual memory with FIFO and LRU page replacement algorithms. The manager handles page requests in both main memory and virtual memory, allowing you to specify main memory size, virtual memory size, and page size. It supports both **First-In-First-Out (FIFO)** and **Least Recently Used (LRU)** replacement policies.

## Features

- **FIFO (First-In-First-Out)** page replacement
- **LRU (Least Recently Used)** page replacement
- Configurable main and virtual memory sizes with adjustable page sizes
- Supports multiple processes, each with its own set of pages

## Installation

To compile the program, use `make`:

```bash
make
```
This will create two executables: `fifo` and `lru`, each corresponding to its respective page replacement algorithm.

## Usage

Run the memory manager using either FIFO or LRU algorithms with the following command-line options:

- `-M`: Size of the main memory in KB
- `-V`: Size of the virtual memory in KB
- `-P`: Size of each page in B
### Commands

#### FIFO Page Replacement

```bash
./fifo -M <main_memory_size> -V <virtual_memory_size> -P <page_size>
```
#### LRU Page Replacement
```bash
./lru -M <main_memory_size> -V <virtual_memory_size> -P <page_size>
```
## Example
```bash
./fifo -M 1024 -V 2048 -P 256
```
## Project Structure

The code uses several classes to manage processes, pages, and memory.

### Classes

* **`Pages`**: Represents an individual page with properties like process ID (`pid`), virtual ID (`vid`), a flag `inmain` to indicate if it's in main memory, and a data vector representing page content.
* **`Process`**: Manages process-level information, including process ID (`pid`), total pages (`totalpages`), process size (`size`), and an optional filename (`filename`) for process-specific data.
* **`Memory`**: Manages main memory and virtual memory spaces, with attributes such as:
    * **`mainsize`** and **`virtualsize`**: Define the sizes of main and virtual memory.
    * **`pagesize`**: Defines the size of each page.
    * **`mainpages`** and **`virtualpages`**: Track the number of pages in main and virtual memory.
    * **`emptyslots`** and **`virtualslots`**: Sets to track available and occupied slots in memory.
    * **`fullslots`**: A queue used for the FIFO replacement algorithm.
    * **`mainmem`** and **`virtualmem`**: Vectors that store the pages in main and virtual memory.
    * **`processes`**: A map that stores all active processes.
## Algorithms

### FIFO

The **First-In-First-Out (FIFO)** algorithm replaces the oldest page in main memory first. A `queue<int> fullslots` is used to track the page order for replacement.

### LRU

The **Least Recently Used (LRU)** algorithm replaces the page that has not been accessed for the longest time. The LRU replacement policy would use a doubly linked list (unimplemented in this code) to keep track of page access order.

## Makefile

To compile the code, Run `Makefile`

Run `make clean` to remove compiled files.

### Note:
1. When replacing pages in swap space with empty pages in main memory data from pages in swap space is copied to main memory pages, not swapped.
2. Instructions should be of the form add a, b, c ( spaces after ',' is necessary and there should not be space before ',' )

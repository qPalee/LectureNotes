# Memory Management

Memory is a limited resource 
- It must be arranged to optimise performance

Programs view memory as a set of memory cells starting at 0x0 and finishing at some value

We want to be able to store multiple programs in memory at the same time

## Address mapping 
Maps logical address to physical address

At compile time
- Absolute references generated (MS-DOS .com-files)

At load time
- Done by special program

At execution time
- Needs hardware support

Dynamic Linking
- Use only one copy of system library

## Swapping

If memory demand is too high, some processes' memory is swapped to disk, with low priority processes being swapped first

#### Problems
- Big transfer time
- What about pending I/O
- Swapping causes fragmentation

## Fragmentation
There are two types of fragmentation

External fragmentation
- Over time small holes appear in memory 

Internal fragmentation
- Program is small than hole and leftover is too small to qualify as a hole

Strategies for choosing holes

<span style="color:#00bfff">First-fit</span>
- Use first available hole

<span style="color:#00bfff">Rotating first-fit</span>
- Start after last assigned part of memory

<span style="color:#00bfff">Best fit</span>
- Find smallest available hole

<span style="color:#00bfff">Buddy System</span>
- Have holes in sizes of powers of 2
- Smallest possible hole used
- Split hole in 2 if necessary
- Recombine adjacent holes of same size

## Paging
Paging is when you assign memory of a fixed size
- It avoids external fragmentation
- Translation done via page table

<span style="color:#ff0000">Hardware support mandatory for paging</span>


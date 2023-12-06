# File Systems

The main function of a file system is to be main permanent storage of data.
However, due to it being a permanent data source, it leads to <span style="color:#ff0000">speed bottlenecks</span>

In the modern day, capacity is no longer a major problem, however backing up data is becoming an issue

In a logical view, there is a <span style="color:#00bfff">tree structure of files</span> starting at the root, together with read write operations and creating of directories

In a physical view, there is a <span style="color:#00bfff">sequence of blocks</span> which can be read and written

The OS must map the logical view to the physical view by imposing the tree structure and assigning blocks for each file

There are two possibilities to realise the filesystem:
<span style="color:#00bfff">Linked List</span>
- Each block contains a pointer to the next block
- <span style="color:#ff0000">Very inefficient</span>

<span style="color:#00bfff">Indexed Allocation</span>
- Store pointers in one central location, an <span style="color:#00fc00">index block</span>
	- Index blocks are called inodes in Unix
	- Inodes store additional information about each file

### File Allocation Table (FAT)
Useful for explaining filesystem concepts, but modern filesystems are more complicated

Different variants define number of bits per entry

Sector - disk unit (block)
Cluster - Multiple sectors

Uses linked list to group clusters
##### Structure of FAT16
![[Pasted image 20231127112344.png]]

#### FAT Limits
Max volume size - 2 GB ($2^{16} \times 32 kB$)
Max file size - 2 GB
Max number of files - 65460
Max filename length - 8 + 3

FAT32/exFAT have higher limits
Other filesystems overcome these limits by using other data structures (B-Trees/bitmaps)

### Caching
Disk blocks used for storing directories or recently used files cached in main memory

Blocks periodically written to disk - big efficiency gain

<span style="color:#ff0000">Inconsistency arises when system crashes</span> - reason why computer must be shutdown properly

##### Minimise data loss from system crash
Idead from databases are used:
Define <span style="color:#00bfff">Transaction points</span>: points where cache is written to disk
- Consistent state

Keep log-file for each write operation
- Log enough info to unravel any changes done after latest transaction point

### Disk Access
Disk access contains three parts
- <span style="color:#00bfff">Seek</span> - head moves to appropriate track
- <span style="color:#00bfff">Latency</span> - correct block is under head
- <span style="color:#00bfff">Transfer</span> - data transfer

For HDDs, the time necessary for seek and latency dwarfs transfer time
- Distribution of data and scheduling algoirthms have major impact of performance for HDDs, less so for SSDs

#### Disk Scheduling Algorithms
Standard scheduling algorithms apply
1. <span style="color:#00bfff">First Come First Serve</span> - Easiest to implement, requires lots of head movement
2. <span style="color:#00bfff">Shortest Seek Time First</span> - Select job with minimal head movement

Problems:
- May cause starvation
- Tracks in the middle of the disk preferred
- Increases mechanical wear

Algorithms doesn't minimise the number of head movements

3. <span style="color:#00bfff">SCAN-scheduling</span> - head continuously scans the disk from end to end
- solves fairness and starvation problem of SSTF

4. <span style="color:#00bfff">LOOK-scheduling</span> - head only moves as far as last request
- improvement on SCAN-scheduling

Particular tasks may require different disk access algorithms

Example: Swap space management
if speed is crucial, it gets different treatment
- Swap space stored on separate partition
- Indirect access methods not used

- Special algorithms used for access of blocks
- Optimised for speed at the cost of space
- Increased internal fragmentation

##### Linux Implementation
Interoperability with Windows and Mac requires support of different file systems (vfat)

Linux implements common interface for all filesystems - <span style="color:#00bfff">virtual file system</span>

The VFS maintains:
- Indoes for files and directories
- Caches, in particular for directories
- Superblocks for file systems

All syscalls first go to VFS
If necessary, VFS selects appropriate operation from real file system

Kernel makes it possible to have different schedulers for different file systems
Default scheduler based on lift strategy with a seperate queue for disk requests for each process
- Queues served in Round-Robin fashion

In addition it has a <span style="color:#00bfff">no-op scheduler</span>
- Implements FIFO
- Suitable for SSDs where access time is equal for all sectors
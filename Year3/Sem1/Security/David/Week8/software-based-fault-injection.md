# Software-based fault injection
You can't do physical attacks on a general purpose PC
What can we do with just code execution
- we can run 'magic' instruction sequences that can be ran in user mode

### Rowhammer
- If you access the 2 rows around the target row it can modify the data in the target row before the refresh interval, leading to bit-flips

To do this, we need to have:
- uncached memory access
	- various techniques for this such as `clflush`
- fast memory access
- target specific row
	- reverse-engineer mapping functions

Rowhammer essentially lets you flip a specific bit of memory
If a user page can change the memory in its page table, then it can point anywhere and modify any values in memory

### Power Management
Modern CPUs continuously adjust their clock frequency and supply voltage to run at minimum power consumption/temp
Dynamic Voltage and Frequency Scaling (DVFS)
Overlocking/Undervolting can result in faults
DVFS is often software-exposed

Smartphones allow clock and voltage control if you are root
This can be used to inject controlled faults from privileged software

Basically you can undervolt a cpu by changing the RAM which can lead to a machine miscomputing values
- This can then let us fault RSA and AES in the same way as hardware faults

Intel fixed this in 2019 :(


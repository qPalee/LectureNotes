# Firmware Analysis

### Black-box analysis
Similar to pentesting a network/website/etc
- You can use standard techniques without firmware
	- port scans
	- looking at network traffic
	- web vulnerabilities
- Can be combined with analysis of actual firmware, or simplify some steps

### White-box firmware analysis
1. Convert dump into appropriate form
2. Identify device and CPU architecture
3. Analyse structure
4. Decrypt (if needed)
5. Unpack (if needed)
6. Load into IDA/Ghidra if bare metal
7. If not mount filesystem and load into forensics tool
8. Analyse files of interest

#### Bare-metal firmware

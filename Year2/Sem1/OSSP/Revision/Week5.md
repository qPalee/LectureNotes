# Week 5

### System Calls
- System calls are a programming interface to the services provided by the OS
- Typically written in C
- Mostly accessed via API calls
- Most common APIs: Win32 and POSIX API
- APIs allow application code to access kernel without root privileges

### Virtual Machines
A virtual machine allows you to run one OS on another OS
A VM provides an interface identical to the underlying bare hardware
The operating system host creates the illusion that a process has its own processor and virtual memory
Each guest is provided with a copy of the underlying computer, so it is possible to install Windows 10 as a guest operating system on Linux

### Device Drivers
A device driver is software that allows other programs to interface with external devices through the device controllers

Device drivers run in kernel mode

From user space, device drivers have 5 system calls:
- <span style="color:#00bfff">open</span>: make device available
- <span style="color:#00bfff">read</span>: read from device
- <span style="color:#00bfff">write</span>: write to device
- <span style="color:#00bfff">ioctl</span>: perform operations on device (optional)
- <span style="color:#00bfff">close</span>: make device unavailable

From kernel space, each file has functions associated with them which are called when the corresponding system call is made

#### Interrupts in Device Drivers
The normal cycle of interrupt handling for devices is:
- Device sends interrupt
- CPU selects appropriate interrupt handler
- Interrupt handler processes interrupt
	- Data to be transferred to/from device
	- Waking up processes which wait for data transfer to be finished
- Interrupt handler clears interrupt bit of device

Interrupt processing time must be as short as possible

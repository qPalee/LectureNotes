# Device Drivers
A device driver is a software that allows other programs to interface with external devices through device controllers

Device drivers run in kernel mode

They have five system calls
- <span style="color:#00bfff">open</span> - make device available
- <span style="color:#00bfff">read</span> - read from device
- <span style="color:#00bfff">write</span> - write to device
- <span style="color:#00bfff">ioctl</span> - performs operations on device
- <span style="color:#00bfff">close</span> - make device unavailable

### Automatic recognition of devices
Nowadays, automatic HW recognition and insertion and removal of devices is important

Requires suitable HW support: Each device responds with unique vendor ID and product ID when probed

For certain devices, they also respond with what type of device they are (eg usb-storage

Each device driver keeps a list for all devices and types it is responsible for

Special program goes at installation time through all device drivers and records device ID's and type

Steps:
- At boot time, kernel probes devices, which respond with unique ID indicating vendor and device type
- For each device found, kernel sends info to userspace
- Special program in userspace (<span style="color:#00bfff">udev</span>) generates entry in /dev and loads appropriate module

#### Categorising devices
Kernel also keeps track of 
- <span style="color:#00bfff">Physical dependencies</span> between devices - such as devices connected to a USB-hub
- <span style="color:#00bfff">Buses</span> - Channels between processor and one or more devices
			 - Can be physical or logical
- <span style="color:#00bfff">Classes</span> - Sets of devices of the same type (keyboards/mice)

#### Handling interrupts in Device Drivers
Normal cycle of interrupt handling for devices is such:
- Device sends interrupt
- CPU selects appropriate interrupt handler
- Interrupt handler processes interrupt
	- Data to be transferred to/from device
	- Waking up processes which wait for data transfer to finish
- Interrupt handler clears interrupt bit of device
	- Necessary for next interrupt to arrive

Interrupt processing time must be as short as possible

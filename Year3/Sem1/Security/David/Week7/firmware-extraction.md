# Firmware Extraction

Firmware is the OS and application logic for embedded devices, sometimes without an OS which is known as 'bare metal'

Nearly all modern embedded devices are programmable with firmware (not hardwired)

Embedded systems can contain multiple processors each with their own firmware binary

#### Why is this relevant?
- Finding vulnerabilities
- Extraction of secret data
- Reverse-engineering of proprietary protocols, interfaces, crypto etc
- Forensics and failure analysis
- Re-purposing of end-of-life devices
- Developing replacement firmware

#### Firmware extraction from 'complex' devices
1. Check manufacturer website
2. Check network traffic for firmware upgrades
	1. plain HTTP is often still used (apt-get)
3. Check for running services
4. Go to hardware methods
The more complex device the easier it is

### UART
UART is a serial communication interface frmo the stone age of computing but still going strong today

It has minimal pins:
- RX = Receive
- TX = Transmit
- Ground
- Supply Voltage

#### UART firmware extraction
- Get access via rootshell + dump
	- user + pw are often trivial
	- often things like `root/root`
- Use the boot loader (often U-Boot)
	- Interrupt boot process
	- Enter bootloader shell
	- U-boot: `nand dump 0x0` etc

### JTAG
Processors and flash chips can support a range of programming interfaces such as:
- JTAG
- ARM SWD
- various other obscure ones

Similar to UART, pin headers are often present and the interface left active

### Reading flash memories
Firmware is stored in external flash chips
These can be read out (either on the board or after desoldering)
### eMMC
These are common in modern devices
Basically a glorified an SD card
You can sometimes use a standard SD card reader
In-circuit operation often requires temporarily disabling the main CPU
Firmware modification is also possible

#### Direct eMMC access
Tools like easyJTAG give R/W access
Wires can stay connected permanently
Many devices use standard android/linux partition layout

<span style="color:#ff0000">NEVER</span> rely on firmware secrecy to protect your products
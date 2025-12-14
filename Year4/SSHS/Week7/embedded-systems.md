# Embedded Systems

Embedded systems often have vastly different characteristics to standard desktop computers

### Core Components
- Memory
- Processing Unit
- Peripherals

#### Memory

##### Non-volatile
Holds code, Static Data and Config info

Often implemented as ROM

##### Volatile
Holds runtime data and code

Implemented as either DRAM or SRAM
- SRAM is more expensive but has less power consumption

#### Peripherals
I/O Devices
Interfaced via:
- MMIO
- Interrupts
- DMA

##### On-chip peripherals
- Shares chip with cpu
- Directly interfaced
- Usually simple but essential

##### Off-chip peripherals
Physical separation from cpu
Connected via bus
May be embedded system on its own

#### Processing Unit
Microprocessor which is an integrated circuit which holds CPU and Peripheral/Memory interfaces
- Low complexity
- Low power consumption

### Protocols
#### UART
Used for serial communication between 2 devices
Separate receive and transmit lines
- TX -> RX
- RX -> TX

##### Configuration
- Baud Rate
	- 2400 - 4800 - 9600 - 19200 - 36400 - 56700 - 115200
- Data bits
	- 5 - 6 - 7 - 8
- Parity bit
	- None - Even - Odd
- Stop bit
	- 1 - 1.5 - 2
- Bit order
	- LSB first - MSB first


Baud rate determines the transmission speed for UART communication
Example: 115200 baud, 8 data bits, 1 stop bit, no parity (8N1)
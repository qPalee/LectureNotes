# Main Modern Network
Historically, LANs and WANs were different in technology protocols

In Europe, telco monopolies limited what WANs can do

The main difference between LAN and WAN these days is how easy it is to put together
- You can plug a LAN together and it will just work
- A WAN requires planning

WANs were mostly used for mass file transfer between buildings

#### Workstations
The game changer for LANs was the arrival of workstations

Ethernet came from Xerox
- It was originally 3Mbps, and now you can get 100Gbps 

#### WAN Technology
WAN has been very slow and reliable for most of history
- cs.bham.ac.uk had only 9.6 kbps in 1987
- The US/UK ARPAnet connection was 2.4 kbps in 1986

This makes efficiency very important

### Ethernet
Developed my Xerox in the 1970s
Named after the 'ether' which supposedly carried light until it was disproved

The topology was originally a bus, a single cable with computers connected to it
There was a single yellow cable which was always 10Mbps
- Originally was 3Mbps but upgraded to 10 within a couple months
The maximum length for ethernet was 500m but could be amplified

#### Format
<span style="color:#ff0000">Do this later</span>

##### Finding the end of the packet

#### Basic Logic
Only one station can talk at a time
Each station waits until no-one else is talking

##### Collisions
Ethernet is formally known as <span style="color:#00bfff">CSMA/CD</span> - Carrier Sense Multiple Access Collision Detection

To stop collisions the station listens to the ether and checks if it only contains the signals that are being sent
- This is why there is a limit on the length of the cable

If there is a mismatch, someone else is transmitting at the same time

When a collision happens, the first action is to 'jam' the network
- This is done by sending a pattern of 0x55 followed by an invalid checksum

Its critical that the whole ether known about the collision before the packet has finished being sent
- This makes a minimum packet size of 64 bytes

To recover, the system chooses a random number k from {0..$2^n$} and delay $k \times 512$ bit periods before trying again
- It gives up after 10 attempts
- The random numbers aren't very random, often coming from things like serial numbers

#### Sizes
- Maximum frame size is 1500 bytes plus payload plus 22 packets of header
- Minimum frame size is 64 bytes
- Maximum 'diameter' is 1500m 
- 500m and 10Mbps gives name: 10Base5





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
![[Pasted image 20241022121713.png]]

##### Why 0x55?
- 0x55 is 01010101, so a stream of 0x55 is a stream of alternating 1s and 0s
- Ethernet doesn't have a central clock, so everyone is responsible for clocking the data at the correct speed
- Two stations can easily be >100ppm out of sync, which is a bit period every 10,000 bits
	- A packet is ~1500 bytes, or 12,000 bits
	- This would mean to stations would not be able to track each others data
	- The 0x55 patters allows receivers to lock the current speed of the transmitter
##### Finding the end of the packet
- To find the end, a checksum is continuously computed
- If the last 4 bytes are the correct checksum for the whole packet, you know you have reached the end
- CRC calculation generated the magic number 0xC704DD7B
- You can also wait for the inter-packet gap

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

#### Problems
- Cable is heavy, spenny and difficult to install
- Installing taps for receivers involves drills, and risks damaging the cable
- Need for transceivers adds cost and complexity
- Performance issues lurking in the background

##### 10Base2
- Instead of using thick, co-ax, use thin coax
- It has a higher resistance, so limited to 185m
- Instead of using transceivers, bring the coax to the computer
- Cut the cable instead of drilling into it
- Can be mixed electrically and logically with 10Base5
- Dominant networking of the 80s and early 90s
	- Older building are still full of it

##### BaseT
- Coax cable is still a pain
	- Expensive, hard to install, easily damaged
- This is the modern ethernet
- Up to 95m of twisted pairs using RJ45 connectors to a hub
- Was originally Cat 3 but now we have Cat 6E

#### Repeaters
- A repeater is just an analogue amplifier
	- Collisions are seen on both sides
- A bridge receives, buffers and transmits frames
	- This helps reduce collisions
	- <span style="color:#00bfff">dumb</span> bridges just propagate everything
- Ether hubs are repeaters, not bridges

#### Switches
- A switch is a set of learning bridges in a box
- Each interface is its own collision domain
- Packets to unknown destinations are sent out of all ports
	- Otherwise only traffic for devices plugged into the port is sent
- <span style="color:#00bfff">Full Duplex</span> means traffic can go in and out without colliding
	- Each direction is a separate collision domain
- Large buffers internally deal with congestion
- This results in no collisions
	- A switch may fake a collision if it runs out of buffer space though

#### Token Ring
- Ethernet was argued to behave badly under heavy load
- Token Rings pass a 'token' from station to station
- These can also be referred to as a '<span style="color:#00bfff">Token Bus</span>'

##### Problems
- In theory, Token Rings offer bounded latency
- The token will always circulate in n_stations \* max_packet_period \* fudge
- In practice, it is very complicated to get right
	- Token loss/creation
	- Station failure

#### Slotted Rings
Knows as Cambridge Rings from their place of development
 ![[Pasted image 20241022132527.png]]
Picture unrelated

Instead of circulating a token, empty data frames circulate
###### Todays lecture

ATM didn't deliver what it promised
If you have lots of bandwidth available and the clients aren't too fussy, you can just assume you can send packets and they'll get there eventually
- If the network fills up you can just throw away some packets

Most ISPs hard-drop policing, either deliberately to save costs or as a consequence on the hardware they're using
	Often the upload speed id only 10% of the download speed

The issues with switching is the same as crashing an f1 car apparently

Its possible that equipment isn't sufficiently fast to cause problems

Ian doesn't think we will ever upgrade a PC (wrong)

The gigabit standard has changed over time
- these days the pc just wouldn't work
- gigabit flow control is very bad
	- If buffer is about to fill up, send a signal to tell the client to shush

Packets per second is much more often the limit than the actual bandwidth
All of these problems are a nightmare to debug

Traffic shaping is like a leaky bucket
- Stuff comes in
- We siphon bits out at a predetermined speed
- Anything which overflows just gets thrown out

Traffic Policing is the same but with a tiny buffer
- Like using a plate instead of a bucket

### MPLS
- Multi Protocol Label Switching
- Basically ATM with larger packets
	- As networks get faster, the benefits of smaller packets are outweighed by the additional switching overhead
- I need to know it exists

### Wave Division Multiplexing
- Uses different colour light to transmit multiple streams down a single fibre
	- Cool kids call it 'lambda' instead of colour
		- Giving PLPDI flashbacks
- You can get over 1000 channels down a single fibre

### Random Early Drop
- Always turn it on if you can
- Current State-of-the-art
Strategy is to randomly drop packets with a probability which increases as the buffer fills up
- This reduces speed before the real loss starts to happen

This loss of packets is seen by the sender when the acknowledgements stop, and is a signal to the sender to send less packets (hopefully)

With leaky bucket everything is fine until it isn't
- Once the buffer fills up all hell breaks loose
	- Either a huge break in traffic
	- Or fragmented data is sent


### Takeaway
- Ethernet switching is robust under load, and networks these days have substantial excess performance
- Finding the performance handicap is hard, but once it is hit it can be dramatic and break down quickly
- Debugging these problems are very hard
- Over-engineering the problem can be cheaper than solving it properly
- Be very careful of buffering
- You can just pay your way out of trouble

# IP
IP has been the biggest protocol for about 30-40 years

You can do so many things with it since its so basic

IP is a network layer which makes no promises
- No order guaranteed
- No reliability guaranteed
	- If you lose a packet you will most likely not get an error message
- There is no checksum covering the data

Its hard to image something which offers less

##### History
- Proposed in 1974
- ipv0-3 were experimental versions
- Updated by RFC791 in 1981 which is still current

#### Why IP?
- Easy to implement
- Works over anything
- Has had support from US DoD, ARPA and NSF
- Its kinda good aswell ig

#### Packet Format
![[Pasted image 20241025091312.png]]
##### Version
The first 4 bits of the packet tells you the ip version being used
- We just need to hope 16 versions of ip aren't used at the same time
##### IHL
This is the length of the header in 32-bit words
- Typical header is 5
- If >5 then theres other options present
	- These are mostly obsolete/useless
	- Its standard for extra options to be stripped off by devices
##### Type of Service
- Used to be used for security labels, precedence, etc
- Not stable, standard, widely used by application
	- Very difficult to set
- Might be used in enterprise networks to tag voice packets for special treatment
	- Easier to buy some modern switches though
##### Total Length
- This is measured in bytes
	- This makes sense as it means packets dont need to be padded to a multiple of 4 bytes
##### Flags and Fragments
- IP has support for splitting packets into fragments so that a large packet can travel over a network which only supports smaller packets
	- Possibly the old 576 byte limit (512+64)
- This is inefficient and unreliable
	- The packets are only reassembled by the receiver
	- If one fragment is lost the whole packet must be resent
	- If someone is trying to do this, fuck them off
- Fragmentation is strongly deprecated
	- Later fragments contain no info about TCP/UDP ports
	- IPv6 doesn't support it
##### Time to Live
- How many hops the packet is valid for
- Decremented on each passage through a router
- Initial value sets max diameter of the internet
	- Recommended 64
	- If the number is too much
	- Old versions of windows set it at 30
		- This was too low and packets couldn't reach some places
- Generates ICMP Time Exceeded errors when it reaches 0
##### Protocol Numbers
- 1 is ICMP
	- Only really used for error messages
- 6 is TCP
	- Streams of data
- 17 is UDP
	- Thin datagram over IP
##### Header Checksum
- This is NOT a secure hash
	- You can change one byte in the header and alter the checksum based on the old checksum
- Only guards against accidental corruption
##### Source + Destination Address
- 32-bit addresses
- Identifies hosts, NOT applications
- No way to determining the purpose of the packet
	- IP just sends a packet from one place to another
##### Flags
- Bit 0: reserved, must be 0
- Bit 1: Don't Fragment
- Bit 2: More fragments
	- tells the person that this is part of a fragmented sequence
#### Fragmentation
If a packet is too large for a link
- Put the IP header and as much data as possible in the first fragment
- Set the MF bit to 1 (More Fragments)
- For all fragments but the last
	- Use the same header
	- Same ID
	- MF=1
	- Fragment Offset = offset in bytes in the original packet
- For the last fragment
	- The same but MF=0
- Fragments other than the first do not contain a TCP, UDP or other header
	- This gives firewalls very little information to work with
	- Firewalls will often just block fragmented packets
##### Example
![[Pasted image 20241025102205.png]]
##### Reassembly
- Fragments are NOT reassembled when they pass from a network with a small MTU to one with a large MTU
	- Routers don't have enough RAM for this
	- Fragments may travel through different routes
- They are only reassembled by the destination system
- Fragments are buffered until the destination has the complete set, the processed after reassembly
- This has many problems
	- DoS attack: Just send a constant stream of fake fragments which never form a complete packet
	- Reassembly timers are not well defined
	- Firewalls often drop anything with MF=1 of offset>0
	- IPv6 has no concept of fragmentation
##### Path MTU Discovery
Instead of fragmenting, discover the minimum MTU along the route packets
- Send the packet with DF=1 (Do not fragment)
- If you get a "Fragmentation Needed" error, reduce the size of packets to that destination
- Periodically re-probe, in case the route has changed
- Some dumbass firewalls drop all ICMP
	- If Fragmentation Needed ICMP messages are dropped then shit goes bad
#### 32-bit Addresses
- At the time, this was insanely large
- Arpanet reached a peak of 113 nodes by 1983
- Originally, there was 8 bits for the site, and 24 bits to specify a machine at that site
	- This was seen as wrong very quickly, 256 sites was simply not enough, even in the early 80s
#### Notation
- Conventionally written as 4 decimal numbers, each encoding one byte, separated by dots
- Typically not zero-padded
- Hexadecimal would have been better, but it wasn't used much in the 70s
#### Routing Decisions
- All IP addresses identify a network and the host on that network
- A router ignores the host on network part for all non-local addresses
	- It looks up the network in a routing table
	- Then chooses which interface to send the packet through
	- A router close to the centre of the network needs to know about a lot of networks
- At the time IP was designed, 65 KB was A LOT of RAM.
##### Performance on limited hardware
Back in the day, building large distributed routing tables was hard
- It was essential to keep the number of networks with information exchange to a minimum
Limiting it to 256 was unreasonable, but there had to be a low limit
It was decided that 32 bits would be used, which gives ~4 billion addresses
- This was decided in a time when a few thousand computers were seen as an upper bound
- Efficient allocation of addresses did not matter
- They expected a fraction of a percent of utilisation
The priority was being able to make routing decisions quickly on slow hardware
- This is still affecting us today

### Classful Addresses
This lead to lots of wasted addresses
##### Wasteful Allocation
Total reachable space is only ~87% of available addresses
Class A space is very sparsely occupied since no-one has 16 million hosts
Very few universities have 65536 hosts, so class B space is also sparsely occupied
Class C space, was initially available in bulk

Estimates these days say that around 25% of address space is usefully deployed
There are huge shortages outside of Cold War era NATO countries

This is bad, but it was done since it is very easy for routers
- Back in the day most of the internet was only Class A addresses
- Routers would check if it was 'local' first
- Then they checked where to send the packet to by looking at the first bit of an address
- This was easy even in 1980
#### Sub-Netting
You can split up the large network into smaller sub-networks
- Birmingham has 256 networks each with 256 hosts
![[Pasted image 20241029111208.png]]
##### Netmasks
A bit pattern which can be & with an address to get a network number
- Class A (/8) is 255.0.0.0
- Class B (/16) is 255.255.0.0
- Class C (/24) is 255.255.255.0

##### CIDR and Slash Notation
Classless Inter-domain Routing gave each network a net-mask which describes how much of the ip is network and how much of it is host
These are notated using a Slash

#### RFC1918
- Class A Network 10 became free when the Arpanet backbone was closed down


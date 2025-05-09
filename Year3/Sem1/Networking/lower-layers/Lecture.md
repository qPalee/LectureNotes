# Lower Layers

### Volume
Bandwidth will tend to infinity
### Latency
How much delay does the network have

The speed of light imposes a floor, which is a lower bound
It will take at least a ms to send a light from London to Birmingham, not thinking about any other factors

Twitter had football goals before the trial BT 4K Service
### Error Rate
In large networks, we will transfer it through ram in every step

Non-ECC RAM has an error rate of 1 bit per gigabit per day - often by cosmic rays
If you are moving a lot of data around, this error will be encounter quite often
- slap a sha256/sha3 hash on it
- slap both on if you really want to

CPU power is cheap so isn't too bad to add error checking

If you move one terabyte of data, the error rate after checksums would be about 1 bit

Long haul networks are in volume of over a terabit per second
Petabits per second will be done in the near future

### Circuit Switching
Telephones magically allocated you a frequency

Fun Fact! Lots of the atomic bomb research was done in this lecture hall

### Packet Switching
We can divide the data stream up into small units, called 'packets'
Each packet is given some identifying information

#### Advantages
- You are now in the time domain
- Its easier to build
- When no data is being sent, no resources are consumed
- You can re-route data around failed switched

#### Virtual Circuits
A virtual circuit is a network which is able to understand the concept of a link between two points
It gives a connection a token, and you give your packets said token and the network will send it to the correct place
The virtual circuit is torn down when the endpoint has finished with it
The network has to know about every connection in the network
Every packet follows the same route
- What if a part of the connection fails?
#### Datagrams
Each packet contains complete addressing information
Datagram just sends data through a wire and lets the user deal with the rest of it

'Networks are kinda good'

#### Layering
Applications in general want something with guarantees: you send a file and it gets there undamaged, or it tells you if something goes wrong
You also want your programs to operate over different sorts of network

Layering id thinking of a network in terms of layers or a 'stack'

Each layer provides services to those above it, and makes use of services from those below it

Layering gives a clean, undefined interface between components in the system
It also allows the OS to swap implementations, and the ability to swap interface-equivalent things which do different jobs

##### OSI
Ian doesn't like OSI

This model was produced out of thin air and came long before any successful implementation

Developed based on how people thought a network should work
##### DoD
This was based on things that were already working

###### Applications
- Applications are running code that do real, useful work, and the protocols that they use
- They need services to move data from computer to computer
###### Transport
- A Transport layer moves bytes between two end systems via a network whose topology and other properties the transport layer doesn't need to know much about
	- TCP is used for streams of data where reliability is needed
	- UDP is for packets
- The transport layer will guarantee various properties such as reliability and sequenced delivery
	- If not it will disclaim responsibility for these properties
- It permits communication between multiple entities (applications) running on the same end systems
- It is unconcerned with what the bytes mean, it just moves them
###### Network
- This layer moves packets between end systems, but doesn't offer any guarantees on reliability
- It handles choosing which link to use to get the data closer to its destination
- It also doesn't deal with any concept of multiple applications
	- This is the responsibility for the layer above
###### Link
- This layer moves data between one network element and the 'next' element
- It is concerned with packetisation, addressing etc
- There may be a variety of protocols in use
	- Ethernet will be the main focus, but ATM will sometimes appear
###### Physical
- This is the actual encoding used to shift bits over a distance
- Data can move over: co-axial cable, twisted pair, fibre optics, radio etc

![[Pasted image 20241011091941.png]]

#### TCP/IP won
There is only one transport service for connections and one transport service for datagrams

It is the responsibility of the implementor to make TCP and UDP work
It wins because there is only one network layer, IP
- IPv4 and IPv6 only differ in address length
- The tcp implementation can be exactly the same and it'll still work

#### Why OSI lost
It tried to be 'efficient' and provided multiple transport services
It was about telcos protecting business models and capital plant
There were 2 different network layers
- CONS for connection-orientated (virtual circuit)
- CLNS for connection-less (datagram) services

None of it interworked

### Different Hardware
<span style="color:#00bfff">Switches</span> understand the link layer
- An ethernet switch switches ethernet packets between links

<span style="color:#00bfff">Routers</span> understand the IP layer
- They move packets between potentially very different links
- A router may have ethernet on one side, and a long-haul serial link on the other
	- These days a long-haul link is just ethernet

<span style="color:#00bfff">Hosts</span> understand the transport layer and application layer
- Usually general purpose computers
### Blurring
- These days hosts understand everything, and they also make pretty good routers
- Routers tend to have a switch integrated into them
- Switches are increasingly 'L3 aware' and make switching decisions based in part on the contents of IP headers

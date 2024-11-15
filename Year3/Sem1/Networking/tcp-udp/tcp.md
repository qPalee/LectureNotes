# TCP
Sending reliable data through an unreliable service

In theory, it is quite simple
TCP is designed around having an underlying channel which pretty much works
- Assumes the packets arrive in order and correct
- It then deals with the unreliable parts after

TCP is split up into 4 chunks
1. Bundle up data in userspace and slap it in the kernel
2. Kernel sends it all over through an unreliable channel
3. The other kernel receives the data and unpacks it
4. The data goes into userspace

TCP does no error correcting
- It will just retransmit data
- It something is corrupted it will bin it

#### Acknowledgement Mechanisms
Let us assume that the channel may introduce errors but packets are not lost
- Underlying channel may flip bits in the packet
- Checksum is used to detect this

There are 2 mechanisms to deal with this
- Send an ACK to tell the sender that the packet has been received correctly
	- Sender retransmits if it takes too long
- Negative acknowledgement (NAK): receiver tells sender that the packet has errors
	- This is silly and not used

##### What if ACK/NAK gets corrupted
You can have errors in packet transmission in ACK/NAK transmission
- One solution is to just retransmit the data since we don't know what happened
- We now need to handle duplicate packets

##### Handling Duplicates
To handle duplicates, every packet should have a sequence number that uniquely identifies the packet
- The receiver discards duplicate packets

#### Time-outs in action
![[Pasted image 20241115092716.png]]![[Pasted image 20241115092739.png]]
Delayed ACK looks like a big fucking mess

##### Latency kills this
The speed of light is $3 \times 10^8 ms^{-1}$
There are plenty of paths which are $3 \times 10^6 m$ (west europe to east cost america)
This causes a 20ms round trip time - assuming infinitely fast routers and computers
50 packets per second @ 1500 bytes/packet = 600Kb/s maximum

This is not good

#### Pipelining
Sender allows multiple 'in-flight', yet-to-be-acknowledged packets
- range of sequence numbers must be increased
- Buffering at sender and/or receiver

Sender can have up to N un-acked packets in pipeline
Receiver only sends <span style="color:#00bfff">cumulative ack</span>
- Doesn't ack packet if there is a gap
Sender has time for older un-acked packet
- When timer expires, sender retransmits all un-acked packets

##### Pipelined Sender
![[Pasted image 20241115093422.png]]

##### Pipelined receiver
- Ack-only: always send ACK for correctly-received packet with highest in-order sequence number
- May generate duplicate ACKs

Discard out of order packets
re-ACK packets with highest in-order sequence number

##### Selective Repeat
This is an alternative to pipelining
This is not better

Receiver acknowledges all correctly received packets
- Buffers packets for eventual in-order delivery to upper layer
Sender only resends packets for which ACK not received
- Sender timer for each unACKed packet
	- Separate timer for each packet sent

![[Pasted image 20241115094206.png]]
This is a big fucking mess

### TCP Overview
<span style="color:#00bfff">Point-to-point</span>
- One sender, one reciever

<span style="color:#00bfff">Reliable, in-order byte stream</span>
- No 'message boundaries'

<span style="color:#00bfff">Pipelined</span>
- TCP congestion and flow control and window size

<span style="color:#00bfff">Full duplex data</span>
- Bi-directional data flow in same connection

<span style="color:#00bfff">Connection-oriented</span>
- Handshaking inits sender, receiver state before data exchange

<span style="color:#00bfff">Flow controlled</span>
- Sender will not overwhelm receiver


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
- If something is corrupted it will bin it

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
- One sender, one receiver

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

RFC9293 is the most modern one and unifies all older ones
- I think Ian think we are gonna read the spec for some reason

TCP uses the same header between both IPv4 and IPv6
![[Pasted image 20241119090558.png]]
Sequence number allows us to identify each bit with a unique identifier
This tells us which bytes have been send and which ones haven't

the urgent bit is bad, kill it when you find it
- it was designed for some data to be delivered quicker than other data
- It is also now a security risk due to malware using it
- You are supposed to support it but realistically no one does

The 'push bit' is also pretty much obsolete now
- The idea is that data is sent then the OS sets the push bit to send it to the application
- There is no API for this on unix or windows
- You can't tell if data has had the push bit has been added or not

The receive window is 16 bit
- If you go back in time you get rid of this and make it 32 bits long

#### Sequence Numbers
TCP sequence numbers denote bytes
Acknowledgements indicate the next expected byte

Suppose we have a packet with 10 bytes with the sequence number 1234
- Starts 1234
- Ends 1243
- ACK Trigger = 1244, the next expected byte
#### TCP timeouts
The timer is longer than RTT (idk what this is)

If you set the timer too short you will get too many duplicates
- This just wastes data, especially on slow networks
On the other hand, if it is too long, one packet can get lost and the timeout will just sit there doing nothing 

The timer is calculated by checking how long the round trip time is for data you are sending then estimating a good timer
- Don't want to do floating-point arithmetic in the kernel
- There is algorithms for this

#### Reliable data transfer
TCP created reliable data service on top of IPs unreliable service
It does this through
- Pipelined segments
- Cumulative ACKs
- Single retransmission timer

Retransmissions are triggered by:
- Timeout events
- Duplicate ACKs

#### Sender Events
<span style="color:#ff0000">When data is received from the app:</span>
- Create segments each with seq number
- Send the segments
- Start timer if not already running
	- Timer is for the oldest unacked segment
	- Expiration Interval: <span style="color:#00bfff">TimeOutInterval</span>

<span style="color:#ff0000">Timeout:</span>
- Retransmit segment that caused timeout
- Restart timer

<span style="color:#ff0000">ACK received</span>
- If ack acknowledges previously unacked segment
	- Update what is known to be ACKed
	- Start timer if there is still unacked segments

##### Ian yap session
In reality the TCP spec is a bit silly
- It's silly to ACK every single packet
- ACK quickly enough so the timeout doesn't go off

If using something like ssh
- Set ack field in the next packet to send and then you have one less packet to send

If you have recently ACKed a packet and receive another then don't bother sending another one
- Send delayed acknowledgement

'2024 we've got enough RAM'
 - sounds like a political campaign

512gb of ram is a reasonable amount now apparently
- Might be enough to run google chrome on windows 11

If there is lots of data being send, ACKs may only be sent once every 16 or 32 packets

#### TCP 3-way handshake
In some mysterious world it's possible to do this in only 1 message but it requires some magic

Setting the SYNbit to 1 on the first packets tells the server that it is the first packet and tells the server your seq number

Make sure the seq number is actually truly random otherwise security goes brrr
- If it is predicable bad things will happen
- "Don't do crimes"

The server responds with an ACK, as well as it's own SYN

Finally the client ACKs the servers SYN
![[Pasted image 20241119094924.png]]

There is no reason why you can't put some data in these packets
The only reason you can't is the API written in the 80s don't let you
- Why can't we fucking change that then
- 'There is no API for it' - fuck you write one 
- So many less packets will be sent

#### Closing a connection
This can be done in only 3 packets but sometimes 4 if the code is shit

### TCP Summary
- a connection established by exchange of initial sequence numbers, and acknowledging them
- Each side advertises a current receive window in every segment it sends
- Acknowledgements acknowledge the last contiguous byte plus one (first expected byte)
- Timeout triggers retransmission of some or all outstanding data
- Receiver can buffer out-of order packets
	- Most implementations do this in 2024
- Connection is closed in an orderly fashion by the exchange of FINs and acknowledging them
	- All data has been acknowledged after this is complete
- Connections can be terminated at any time with an RST reset
	- These can be done on either end
- There are no guarantees of how much data has been successfully received after this happens


Luckily don't need to understand TCP State Diagram bc this looks ass

#### TCP Options
The header length field is usually 5, measured in 32-bit words, if this is bigger than 5 than there are options.
- SACK - Selective acknowledgement
- Window Scaling - deals with bandwidth delay > 64K
- Timestamping for PAWS and RTTM 
	- Protection against wrapped sequence numbers
	- Round trip time measurement
##### Selective Acknowledgement
Instead of acknowleding the most recent packet, you can acknowledge any packets, even those which are meant to be received in the future
- matey boy kernel can you gives us the bytes lad

##### Window Scaling
This is actually good

Ian gets 400 Mb/s at home 

Window Scaling lets you send more data at long distance
It does this to negotiate a scaling factor for the receive window
'In an ideal world' - Ian's favourite sentence
Ideally we would recreate the TCP header but we cant do that since computers from 1243 wouldn't be able to be used anymore

Window Scaling increases the effective window size to $2^{30}$ (Shifts window left by 14 bits)
This gives GigE up to 10s RRT

##### PAWS
Protection against wrapped sequence numbers
- If you have a receive window that is approaching 1GB, you can have duplicate sequence numbers on packets which are 4GB apart in the sequence space
- Sequence numbers can wrap around and give you 2 packets with the same sequence number
	- This is very very bad
- There is a 'time'stamp in header which is always increasing
- This allows us to distinguish between 'new' and 'old' packets with the same sequence number
- 32 bit counter running at 1000 Hz takes 50 days to wrap around

##### RTTM
- Round Trip Time Measurement
- Measuring RTT can be difficult in the face of retransmissions
- Instead we can place timestamp in header of data segments and reflect that timestamp back in an ACK
- Subtract the ACK timestamp from current value of counter to get RTT
- Free calculation

##### Slow Start
This shit IS compulsory
- It's not enforceable but technically a requirement
- Dont do crimes
Its very difficult to see these days
My laptop is not as fast as the uni internet connection
However at home this is not the same

If both you and your housemate want to upload a backup at the same time then data will be thrown away since the router doesn't have enough buffer space
You then keep retransmitting it and it keeps throwing it away

Once a connection is established, do not initially send the full amount of the receive window
Instead, only send one packet, and increase the number of packets sent until the window is full
This is meant to spread out the packets in the network
- There are many different algorithms for this (+1, x2, etc)
- All of them maintain a local congestion window, which is less than or equal to the receive window
- In general, modern implementations ramp up faster than older ones

You can choose the algorithm for this on unix but 'we shouldn't do this' - Ian is boring
- 'it has to be done by the kernel' - nuh uh
- Its my computer ill do what i want Ian fuck you

##### Fast Transmit
- Uses receipt of duplicate ACKs to infer that subsequent packets have been lost, and retransmits them early rather than waiting
- Avoids going into slow start
- Often just retransmits one segment on the assumption that was lost and the other end has buffered the following segments

Basically just says fuck you to slow start
This will show up in wireshark
- yap about this in the assignment
##### Silly Window Syndrome :3
Less important than it used to be 
Windows don't fill up with small packets as much

The buffer will empty one byte, then advertise that it has 1 byte available
Sender then sees that it can send a byte so makes a whole ass packet to send that one byte
- sender is very horny

###### Solutiong
Receiver:
- Do not advertise small increases in window
- Only advertises when we can accept one more segment, or half the buffer

Sender:
- Do not send small packets when there is outstanding unack'd data

Next tuesday is gonna be a good lecture
We have been good boys this time
# Introduction
Ian doesn't like networking theory

"You click on a link, what happens?"

Mostly focused on TCP/IP and ethernet since nothing else is ever used. Everything else is history

OSI 7 layer model is nonsense - Tim lied to me
### Week 1-2
- Packet vs Circuit Switching
- Layer Models

### Week 3
- Why IPv6 is needed - we have ran out
- Address translation

### Week 4 
- Transport mechanisms - UDP, RTSP
- NAT, how ipv6 fixes it, IoT
- The Chinese government can open Ians curtains

### Week 5
- Going over TCP in lots of detail
- Possible extra video lectures
- "one of the best achievements post war"

### Week 6 
- Consolidation Week
- Fancy reading week

### Week 7-8
- Higher level protocols
- HTTP, SMTP, ...., **DNS**
- Lots of issues with DNS
- Some security issues with these protocols aswell

### Week 9-11
- Routing in/out the enterprise

TCP/IP Illustrated is a really good book
Expected to read RFCs

# Introduction 2: Electric Boogaloo
Most networks have 3 sort of boxes
- <span style="color:#00bfff">Hosts, Systems, Computers</span> - Things which we run useful programs
- <span style="color:#00bfff">Switches</span> - Devices which move individual packets between in a LAN
- <span style="color:#00bfff">Routers</span> - things that move packets between networks
	- Make finer grain decisions about how data is sent between places

What does happen when you click on a link?
- Parse the URL
- Use DNS to find the IP address
- Make a TCP connection
- Some encryption for security
- Fetch content with http

<span style="color:#ff0000">We will NEVER write any of this ourselves, there are libraries for it all</span>

#### Parse the URL
<span style="color:#00bfff">scheme://host/path</span>

The <span style="color:#00bfff">scheme</span> is the protocol we are going to use - often http/https or file
The <span style="color:#00bfff">host</span> and <span style="color:#00bfff">path</span> are specific to the scheme, and it may have a different syntax

#### DNS
These protocols were written 35 years ago
They were not perfect and people just don't wanna change it

##### Why do we need DNS
We need a way of mapping human readable names into the address that the underlying protocol uses, which is often IP

#### UDP vs TCP
##### UDP (RFC768)
Sends an unreliable packet and hope it gets there
##### TCP (RFC9293/RFC793)
Does more work than UDP to guarantee reliability and error checking

UDP became popular at first because some machines couldn't afford to run tcp
TCP is like building a buffered stream

UDP has a checksum which is often set to 0 (very helpful)

#### Sending a packet
`ifconfig` shows what ip address the machine is running

If building a private network use the 172.16 network bc noone uses it

#### Ethernet
##### ARP is a very bad protocol
Very easy to hijack traffic by responding to the ARP 

Some ethernet protocols don't have a length value
To figure out the length of the packet you need to continuously run a checksum until it is correct

##### How does TCP work
This is a very basic description
![[Pasted image 20241004092726.png]]

We set up a TCP connection with 3 messages in a sequence
- SYN
- SYN, ACK
- ACK

After this we can send bytes whenever
When you send data back you also acknowledge you received their data
When the connection closes there is a final acknowledge

# Networking
### The start of the internet
In 1969, the US Defense Advanced Research Projects Agency gives research grants to universities to buy computers
They decided to link computers

### IP packet
![[Pasted image 20240212152145.png]]

### TCP
- In 1974, daily traffic was reaching $\gt$ 3 million packets a day. Many packets got lost
- TCP is a protocol that runs on top of IP, if an IP packet gets lost, it requests for it to be resent
- TCP/IP becomes standard and allows inter network connections

### Domain Name Servers (DNS)
- Remembering IP addresses is hard
- So people associated names with IP addresses -> news.bbc.com -> 212.58.226.141
- Hierarchy of servers handle requests
- The route for most of Europe is RIPE based in Amsterdam

### Ports
- To allow multiple connections to the same machine, TCP uses ports
- TCP “Socket” connection is defined by: (destination IP, destination port, source IP, source port)
- The destination port normally depends on the service: WWW -> 80, ssh -> 22, dns -> 53
- The source port is normally chosen at random
### Internet Protocol Stack
- Internet communication uses a stack of protocols
- Each protocol uses the protocol below it to sent data
![[Pasted image 20240212154504.png]]
![[Pasted image 20240212154551.png]]

### MAC and IP address
Every machine has a unique MAC address (Media Access Control)
Every computer on the internet has an IP address

#### DHCP and ARP
- Dynamic Host Configuration Protocol
	- Assigns an IP address to a new machine (not stored long term)
- Address Resolution Protocol
	- Lets router find out which IP address is being used by which machine
	- ARP Spoofing lets one machine steal the IP address of another on the same network

### Wireshark
- Wireshark is a network protocol analyser. Records all internet traffic so it can be viewed and analysed
- Excellent for debugging protocols and network problems
- tcpdump is another option which also writes traffic data to disk

### "The Attacker Owns the Network”
- The Internet was not designed with security in mind.  
- Traffic may be monitored or altered. 
- All good security products assume that the attacker has  complete control over the network (but can’t break encryption)





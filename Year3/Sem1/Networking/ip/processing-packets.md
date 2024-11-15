# Processing IP Packets
In operation:
- If the packet is local, process the packet locally
- If its for someone else, 
	- If we know where to send it we send it there
	- If not, throw it on the floor

### IPv4 uses ARP
- Sends out a message asking who has a certain ip
- Someone responds with a MAC address and you have to just trust that its the right person
	- 'trust me bro'

### Point-to-point link
If a link is point-to-point, you just send the packet down it

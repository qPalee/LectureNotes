# NAT
<span style="color:#ff0000">These slides are on a canvas announcement for some fucking reason</span>

Not enough IP addresses

RFC1918 reserved some addresses for private use
- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16

bad things happen if these addresses are used
- don't do crimes

### Proxying
Was the first thing used back in the day
- Custom app per protocol, supported by clients
	- Very resource intensive
- Client connects to proxy, tells it where to connect to and the proxy does it
- Fancy version of ssh to proxy

Proxying was seen as 'adding value' to HTTP before encryption

Bluecoat is evil and their product is shit

/* Eduroam rant inbound \*/
- When you connect to eduroam you have to accept a certificate
- This is done so your device which knows what domain to use
- 'The whole thing is madness'  - Ian
	- Asking users to accept a certificate they know nothing about is silly
- He really don't like eduroam that was a long ass yap

### Address translation
Mechanism to extend the limited amount of IP numbers
Accidentally provides some security - it was not deliberate
Breaks 'end to end principle'
Ian also really doesn't like this

#### Outbound NAT
Connection is modified so that connections from multiple source IP addresses are encoded into port number space of a smaller number of addresses

Source address is modified into a public address
Port number is used to distinguish from separate connections
#### Inbound NAT
Connection is modified so that connections to multiple ports on a small number of IP addresses are expanded out to a large number of addresses

Inbound NAT can be very useful for load balancing

Used for gaming sometimes
- Destiny doesn't do this lmao
- NL4P time :)


Each connection gets a distinct source port number
- Gives 65535 connections per IP address

### NAT for TCP
Maps after receiving TCP SYN packet and turns it off after FIN packets are done

### NAT for UDP
When it sees a packet, and makes a mapping
Deletes it after like 30 seconds 
Can impose a limited number of replies, such as DNS

Clock receivers are 50 quid
Ian has them in his house, no reason for data centres to not have them
He seemed VERY passionate about this
You could tell from his voice

### NAT for IPv6
IPv6 doesn't require NAT due to there being more than enough addresses for everyone

There are proposals for IPv6 NAT for 'security' but it's pointless

#### NAT 'Security'
NAT is basically a dodgy firewall

There is little to no security benefits from it whatsoever

UPnP (Universal Plug n Play) allows devices to communicate with a NAT point and request inbound NAT, bypassing any firewall
- Dream for malware
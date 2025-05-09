# Address Allocation

### Ethernet Addresses
MAC addresses are normally inherent to the machine
Has a length of 6 bytes
- 3 bytes to identify manufacturer
- 3 bytes to identify device

### Local IP numbers
Local IP numbers some from 4 different ways

#### Static Allocation
Don't do this

The end point is given an IP number in some config file or whatever
Each time the device boots, it gets given that IP number no matter what
- Even if its for the wrong network
- Even if it clashes with other devices

The machine might notice that it's a duplicate but it won't know what to do after that

Its only purpose is for routers that need to be up very early after a power failure
Its often used for servers that need to have fixed addresses

### bootp
Very old
- Kill it when you see it

### DHCP
Some DHCP servers offer bootp backwards compatibility
- Turn it off if it does

Provides a lease to a temporary IP number for a specified duration
Also obtains address mappings for routers, DNS, time servers etc

DHCP works very well up until it doesn't

##### Initial Operation
- Client broadcasts a request for an IP number, including its MAC address and other identifiers
	- DHCPDISCOVER
- Servers reserve an available IP number and broadcast an offer of it with a lease time
	- DHCPOFFER
- Client chooses an offer and broadcasts a reply containing the chosen IP number
	- DHCPREQUEST
- Server that offered the IP number locks it for the lease time and acknowledges
	- DHCPACK
- Other servers see that their offer has been declined and unreserve their offer

#### DHCP Relaying
- Relay agent on each network, usually embedded in router (but can be standalone)
	- Contains no state, can safely be replicated and have multiple running at the same time
- Operation is messy

- Relay agent hears a broadcast packet
- It is configured to send all requests to a known DHCP server, after filling in its own address
- DHCP server receives unicast DHCP packets
- Server sends responses back to the relay
- The relay then broadcasts them on the local network

- Relaying to a single server is the right solution in complex networks
	- DHCP servers can be industrial-strength in a secure data centre
- Makes complying with legal and regulatory requirements easier
- Nasty to debug

#### DHCP Security
- Obvious DoS: rapidly request leases, then abandon them so the servers have no more addresses to hand out
	- Some servers have no, or unrealistic, release periods
- They are un-authenticated, so running a rogue DHCP server on a network which provides addresses of hacked DNS and routers is powerful
	- This is very hard to stop
- Nothing is stopping you from ignoring the DHCP server and making up your own address

Dont do crimes
# IPv6 Address Allocation

### DHCPv6
- Broadcast your MAC address, get an IPv6 config
	- All the same problems as DHCP
- Preferred methods are static for servers and SLAAC (Stateless Address Auto Config)

### Router Advertisements
- In general, IPv4 routers are configured either statically or by DHCP
- IPv6 routers send router advertisements, 
	- announce their existence
	- provide basic information about connectivity
		- periodic broadcasts
		- in response to solicitation messages

### SLAAC for IPv6
- Routers broadcast router advertisement packets
- From these, a device can deduce the prefix, the /64 that identifies the network
- After this, they put their 48 bit MAC address, plus some other stuff, into the address and just use it

#### Problem 1
- The device now has an address, but no details on things like DNS servers
- In a dual-stack world, it can just use the IPv4 devices discovered with DHCP
- In a single-stack world, intention is that there will be standard multicast addresses for standard services
None of these are universally implemented

#### Problem 2
- In IPv4, your MAC address never leaves the local network
- In IPv6 with SLAAC, your MAC address is embedded in your IP number
- This allows an observer to track you from the network just by your temporary IP number
- Arguably a privacy risk
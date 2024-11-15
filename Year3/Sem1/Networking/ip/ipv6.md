# IPv6

#### Header
The header is a subset of IPv4, with one extra field
![[Pasted image 20241029093407.png]]
##### Version
Version = 6
##### Traffic Class
Same as IPv4 ToS
##### Flow Label
- Used for labelling related flows of data
- Idea is that routers can keep related flows on the same path to reduce reordering
##### Payload Length
Length of remaining data
##### Next Header
Type of the next header
Equivalent to IPv4 protocol field
##### Hop Limit
Counts the number of hops left before the packet is just killed
#### Address Layout
- Standard Format is a hex string
	- Broken into 16 chunks with colons
	- leading zeroes are suppressed
- `::` means 'fit an many zeros as possible'

IPv6 is really 64 bits
##### IPv6 Reservations
They learned some lessons from IPv4 when making reservations

##### IPv6 waste
- People who complain that IPv6 being wasteful are dumb
- If they compare it to IPv4 they are dumb
- There is $2^{28}$ addresses for every single human being on the planet
- We physically cannot get enough energy to power that many systems 

###### Consequences
- We can assign a separate IPv6 address to each service running on a computer
- We can assign a separate global IPv6 address to every device in a building, so no more local addresses
- IPv6 has local addresses

#### Routing Tables
- In the long term the same complexity as IPv4 will be required 
- $2^{61}$ would require $2^{21}$ TB, which isn't going to happen any time soon
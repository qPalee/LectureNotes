# UDP

#### Big Packets
UDP has no mechanism for large payloads
You can put an massive payload into UDP and it'll appear to work
- it does this through packet fragmentation which doesn't really work

If one packet gets lost the whole thing has to be resent
- This can cause issues where it works locally but not on WAN

Ian thinks anything more than 1200 bytes is risky
1k is mostly safe
512 meets the oldest standards

#### Checksum
This detects errors in transmitted segments
- You put 0's in the checksum field
- Calculate a sum
- Put that sum in the checksum field

##### Issues
This is a very 16-bit machine design
You don't have a carry bit in 32-bit

RFC1071 has lots of cool things about this
- all the goofy cpu architectures of the time
# Other random ass protocols

### RTP
Real-time Transport Protocol
- Used to transport voice and video in some applications
- Doesn't do anything you can't do with UDP

For voice and video you need consistent timing
A choice needs to be made between dropping data and catching up

For telephony, a large buffer is used to ensure data is there if it is needed, and there is backup is connection is partially lost
- This doesn't work for live radio/video
- You can't buffer data that doesn't exist yet

RTP includes a 32-bit timestamp in every packet
- this lets you skip packets if needed
- just miss out the data you don't have

There is no acknowledgements with RTP, but a good checksum
Receiver knows when packet was sent, and how many were sent

#### RTCP
Real time control protocol
Used to set up video replay and similar
SIP used to set up voice over IP telephony

### Multipath TCP
Allows multiple paths to be used by one TCP connection
- wifi and 4G/5G simultaneously

This is a new protocol
- Implemented in iOS 7
- Reference implementation in Linux
- Doesn't require major application changes
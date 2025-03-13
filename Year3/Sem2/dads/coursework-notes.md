# Coursework notes

Cloud Gaming for multiplayer games

Infrastructure issues
- currently 4 hops over the internet are needed instead of the usual 2
- to improve this we either need to:
	- reduce the number of hops
		- Put vm running game in same network as game server(s)
		- Reduces 4 hops to either 2 or 3
		- Forces company to support instead of a third party
	- make the 'extra' hops to the vm shorter
		- Need more data centers
- both require good upload and download latency
	- needs to be able to stream at least 1080p 60fps video

Packet loss is a big issue
- Losing a couple video packets isn't a big issue
- If you lose input packets it is though
- RTP is fine for video streaming - RTP 3350
- Need to have quick upload time without packet loss
	- Send multiple packets and hope that at least one of them gets through?
		- No ACK needed
		- Need to verify that they are the same packet
			- RFC 7198 - duplicate packet streams
			- Need to check if geforce now does this tonight


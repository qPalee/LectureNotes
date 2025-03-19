# Reliable Time Sources
If a Reliable Time Source (RTS) is available, it is easy to satisfy synchronisation requirements

An RTS distributes the correct time to all nodes when:
- Time is distributed frequently enough to bound skew
- No node is required to implement too much adjustment in a single resynchronisation action

### Implementation
We can use 2 functions for implementation
- Generate events that causes nodes to resynchronise clocks
- Provide a clock value to each correct node

### Single RTS algorithm
Universal Coordinated Time (UTC)
- I hate this but its also really funny

WWV is a shortwave radio station in the USA that broadcasts UTC

Suitable for distributed systems where one node has WWV

This doesn't work because can not go backwards or zoom forward in time
There is also latencies with requests and replies

Local clocks end up being a variation of UTC because of this

#### Cristian's Algorithm
- Each client node periodically asks WWV for UTC
- Server sends UTC to client
- When client receives UTV it sets its clock to UTC

### Berkeley Algorithm
1. Time server polls each client periodically
2. Server computes the average
3. Server gives client an amount to gradually add/subtract from its clock

No WWV server is needed but we might drift away from UTC

### Implementing RTS1 and RTS2

#### FIX
$FIX$ is a function from clock time at node $p$ to a correction for hardware clock $C_p$

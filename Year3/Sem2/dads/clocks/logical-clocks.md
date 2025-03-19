# Logical Clocks
The problem is that synchronous systems have poor coverage
- This makes clocks difficult to implement
- Asynchronous systems provide no assumptions on speeds/delays

### Synchronous Distributed Systems
Allows us to have synchronised clocks
- Can determine the order of events
- Important in applications such as mutual exclusion, broadcast etc
- Helps in networking protocols which require timestamps

Physical clocks have a quartz crystal clock which drift 1 microsecond per second

Measures global time but can be expensive to implement

### Ordering in Asynchronous Systems



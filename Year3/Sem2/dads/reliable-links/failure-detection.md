# Failure Detection

### Timing Assumptions
Timing assumptions relate to different:
- Processing speeds of processes
- Transmission speeds of messages

There are 3 basic types of system model
<span style="color:#00bfff">Synchronous</span>
- Processing 
	- Time it takes for a process to execute a step is bounded and known
- Delays
	- There is a known upper-bound on the time it takes for a message to be received
- Clocks
	- Drift between local clock and global clock is bounded and known
<span style="color:#00bfff">Partially synchronous</span>
- Timing bounds eventually hold
<span style="color:#00bfff">Asynchronous</span>
- No assumptions
- Challenging to design fault tolerant solutions


#### Synchronous Systems
While one process takes one step, another process can take at most a bounded number of steps
![[Pasted image 20250324163203.png]]

#### Asynchronous Systems
While one process takes one step, another process can take any unbounded finite number of steps
![[Pasted image 20250324163305.png]]

### Failure Detectors
A failure detector is a distributed oracle that provides processes with suspicions about crashed processes

It is implemented using timing assumptions

#### Perfect Failure Detectors
Indication event $<crash, p>$ is used to notify that process $p$ has crashed

Perfect failure detector properties:
<span style="color:#00bfff">Property 1</span>
- Eventually every process that crashes is permanently detected by every process
<span style="color:#00bfff">Property 2</span>
- No process is detected by any process before it crashes

##### Algorithm implementation
1. Processes periodically exchange heartbeat messages. 
2. A process sets a timeout basis on the worst case round trip of a message exchange
3. A process suspects another process if a timeout expires relating to that process
4. A process that delivers a message from a suspect's process revises its suspicion and increases the associated timeout

![[Pasted image 20250324163849.png]]

##### Correctness
Look at different cases
- Synchronous where initial timeout is accurate
- ![[Pasted image 20250324164042.png]]
- Synchronous where initial timeout is too small
- ![[Pasted image 20250324164051.png]]
- Partially synchronous, where the timeout is accurate
- ![[Pasted image 20250324164059.png]]
- Partially synchronous, where the timeout is too small
- ![[Pasted image 20250324164107.png]]
- Asynchronous
- ![[Pasted image 20250324164118.png]]

##### Perfect Failure Detector Properties

##### Eventually Perfect Failure Detector Properties
# Reliable Links and Failure Detectors

### Assumptions on Channels
A channel should ideally transport any message from its source to its destination

Real channels are unreliable

### Fair Loss
Fair loss is a realistic assumption on channels

It is a combination of assumptions that we make about the properties of communication links to provide an accurate modelling mechanism
- If you try enough, the message will eventually get through

#### Fair Loss Link Properties
<span style="color:#00bfff">Property 1</span> - If message $m$ is sent infinitely often by  $p_i$ to $p_j$ and neither $p_i$ or $p_j$ crash then $m$ is delivered infinitely often to $p_j$

<span style="color:#00bfff">Property 2</span> - if message $m$ is sent finitely often to by $p_i$ to $p_j$ then $m$ is delivered a finite number of times to $p_j$

<span style="color:#00bfff">Property 3</span> - No message is delivered unless it was sent

#### Fair Loss Links
Fair Loss links reflect the possibility for explicit retransmission

It has a well-defined interface:
- flp2pS (fair loss peer-to-peer send)
- flp2pD (fair loss peer-to-peer deliver)

### Stubborn Links
<span style="color:#00bfff">Property 1</span> - If a process $p_i$ sends a message $m$ to a correct process $p_j$ AND $p_i$ does not crash then $p_j$ takes delivery of $m$ an infinite number of times

<span style="color:#00bfff">Property 2</span> - No message is delivered unless it was sent


There is also a well-defined interface for stubborn channels
- sp2pS (stubborn peer-to-peer send)
- sp2pD (stubborn peer-to-peer deliver)

You also need to implement fair loss links since this builds on top of them

#### Stubborn Link Algorithm
![[Pasted image 20250320093831.png]]

#### Example Execution
![[Pasted image 20250320093858.png]]

A stubborn send is an infinite series of fair loss sends

### Reliable Links
Stubborn Links are a gateway to reliable links

Have the receiver check whether the message has been delivered before

They are also knows as perfect links
- At most one delivery
- Implemented on top of stubborn links

#### Properties
<span style="color:#00bfff">Property 1</span> - If $p_i$ and $p_j$ are correct then every message sent by $p_i$ to $p_j$ is eventually delivered to $p_j$

<span style="color:#00bfff">Property 2</span> - No message is delivered to a process more than once

<span style="color:#00bfff">Property 3</span> - Mo message is delivered unless it was sent

Reliable Link Property 1 is a liveness property
Property 2 and 3 are safety properties


#### Reliable Links Algorithm
![[Pasted image 20250320094347.png]]

#### Assumptions
We will assume reliable links for the development of future algorithms
- Messages are uniquely identified and the message identity is included in the senders identifier


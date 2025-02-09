# Dependability Attributes
People often use these terms intermittently

Different domains have different attributes
- Safety-critical domains need high reliability
- Internet Services need high availability

All attributes are equal but some attributes are more equal than others

### Reliability
Probability of a system to correct services over a specified time period
- For example, an aircraft needs high reliability during flights but you don't care quite so much when it is inactive on the ground

#### Formal Definition
Reliability is formally defined as the conditional probability that the system will provide correct service throughout the interval $[t_0, t]$ given that system was providing correct service at $t_0$

It is often assumed that $t_0$ is the current time, therefore $R(t)$ is conventionally used to denote reliability

The unreliability of a computer system is conventionally denoted by $Q(t) = 1-R(t)$, which is just 1 - reliability
#### Regimes
##### Fail-safe
Fail-safe systems become safe when they can not operate

For example:
- infusion pumps can fail but as long as the pump complains and stops pumping, it will not be a threat to life
- domestic burner controllers would be capable of exploding and poisoning humans if the were not designed to turn off when faults occur
##### Fail-operational
Fail-operational systems continue to operate when they fail

Examples include:
- train signals
- elevators
- gas thermostats
- passively safe nuclear reactors

Fail-operational systems can be unsafe sometimes. 
Nuclear weapons launch-on-loss-of-communication was rejected as a control protocol by the US due to it being too much of a risk to human life
##### Fail-secure
Fail-secure systems maintain maximum security when they can not operate

Examples include fail-secure electronic doors, which lock when power is removed
##### Fail-silent
Fail-silent systems either function correctly or stop functioning after an internal failure occurs

This eases the design of fault-tolerant systems

This can be implemented using commercial off-the-shelf components and well-established protocols
##### Fault-tolerant
Fault-tolerant systems continue to operate correctly when subsystems operate incorrectly

Examples include auto-pilot systems and nuclear reactor control systems

This is often implemented by having multiple computers continually test the part of a system, and switch in a spare for failing subsystems
### Availability
Availability is defined as a function of time representing the probability that a service provided a system is operating correctly and able to perform its designated function at a given time
- The higher the availability of a service provided by a computer system, the more likely that its available when requested

Generally availability is applicable to business-critical systems
- financial services, internet services, telecommunications

![[Pasted image 20250123181902.png]]

The availability $A(t)$ of a system at time $t$ is the probability that the system is functioning correctly at time $t$.

$A(t)$ is also referred to as <span style="color:#00bfff">point availability</span> or <span style="color:#00bfff">instantaneous availability</span>, such that it is necessary to determine the interval or mission availability, as defined by $\frac{1}{T}\int_{T}^{0} A(t) \ dt$


### Safety
The safety attribute of dependability reflects the extent to which a system can operate without damaging or endangering its environment

some systems have 'safe' statuses:
- Railway systems where all lights are red, such that all trains halt
- Fly-by-wire avionics are not inherently fail-safe, though it can be transformed to be fail-safe under a reasonable set of failure mode assumptions

### Confidentiality
The confidentiality attribute is concerned with the non-disclosure of undue information to unauthorised entities

Serves as a measure to the extent to which a computer system will allow those without sufficient privilege to obtain information that should not be made available

### Integrity
The capacity of a computer system to ensure the absence of improper system alterations, with regard to the with-holding, modification and deletion of information

This is typically interpreted such that "improper system alterations" relates only to information alterations performed by an unauthorised entity
- Also en-compasses acts where an unauthorised party prevents modifications or causes information corruption

### Maintainability
Defined as a function of time representing the probability that a failed computer system will be repaired in $t$ time or less

Maintainability is denoted by $M(t)$

When a constant rate of repair ($\mu$) can be assumed, the maintainability of a given system can be estimated as: $$M(t) = 1 - exp(-\mu t)$$
### Security
The composite of the availability, confidentiality and integrity attributes was traditionally considered to account for the computer system security aspect of computer system dependability
- Some argue that security considerations have outgrown this interpretation
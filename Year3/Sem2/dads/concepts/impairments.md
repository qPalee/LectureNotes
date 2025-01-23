# Impairments

### Failure
A system failure occurs when the services provided by a system deviate from its specification

Failures are <span style="color:#00bfff">observable</span>, for example:
- **Specification** - user must receive an update value every second
- **Problem** - At some point, more than one second elapses between successive sensor readings
- **Conclusion** - A failure occurred, since this is an observable derivation from specification

### Error
An error is an erroneous system state that can lead to a failure

It may or may not be detectable
- most of them are but not all

Not all errors lead to a failure
To prevent failure, we need to ensure no errors exist

### Fault
An error is the consequence of a fault
The are undesirable effect

Faults may or may not be observable

There are many different types of fault:
- software bugs
- noisy message loss
- bit-flips
- etc

Faults can be:
- <span style="color:#00bfff">Permanent</span> - remains until corrective action is taken
- <span style="color:#00bfff">Transient</span> - remains active for a short time period
- <span style="color:#00bfff">Intermittent</span> - becomes active periodically

Transient faults are often detected as errors that result from propagation
They are also the dominant type of fault in integrated circuits

## Fault-Error-Failure Cycle
Also known as The Fundamental Chain

Dependability attributes are impacted by the interplay of impairments at various levels of abstraction

It has a recursive structure
- Failure at one level can represent a fault at another
- Leads to the definition extended chains of causality to represent the error propagation

![[Pasted image 20250123104917.png]]

## The Dependability Tree
A taxonomy generalises and structures our consideration of dependability

- [[impairments]] - what endangers the dependability of a system
- [[means]] - what we can do to impart dependability
- [[attributes]] - what measures we use to establish the dependability of a system

![[Pasted image 20250123105354.png]]

# Correctors
A corrector is a class of program components that imposes a given predicate on a running program

In its simplest form, it can be represented as 
```
if(not safety)
	enforce predicate;
```

Predicate enforcement techniques ensure that invariant is satisfied again, after it has been violated.
- Invariant captures the safety notion for the program

Due to this, correctors try to reinstate the invariant again once it has been violated

This means the eventual program satisfies liveness, but not safety
- safety is eventually satisfied

### Example - Exception Handlers
Detectors raise exceptions using interrupt signals
- This is the interruption of normal operation to handle an event

There are three main classes:
#### Interface exception
Invalid service request detected by interface detectors and corrected by service requester

#### Local exception
Problems with own internal operations detected by local detectors and corrected by local correctors

#### Failure exception
When internal errors propagate to interface, and detected by interface detectors
- Global correction may be needed such as looking for another server


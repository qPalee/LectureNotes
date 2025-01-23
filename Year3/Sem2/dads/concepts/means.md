# Dependability Means
There are four dependability means that may be used to provide dependability attributes in the presence of dependability impairments

There is no silver bullet, so it is common to combine approaches
### Fault Prevention
Intention of fault prevention is to hinder and obstruct the occurrence
- Focus on eliminating the conditions for faults to be activated

Examples of fault prevention include:
- modular software design
- software development methodologies
- process quality assurance
### Fault Tolerance
Fault Tolerance is actively handling the occurrence of faults and errors to ensure that a system is able to meet its specification regardless of dependability impairments

Techniques generally focus on the recognition of an erroneous state in a system and restoring a suitably correct state, or at least a safe state, following the occurrence of an error

Widely used means for imparting dependability because we can never guarantee a fault-free system

### Fault Removal
Intention of fault removal techniques is to reduce the number, likelihood and wider consequences of faults in a system

It is a 3 stage process:
- <span style="color:#00bfff">Validation</span> - Determine whether a system adheres to a set of defined properties
- <span style="color:#00bfff">Diagnosis</span> - Identify problems (faults) preventing these properties from being fulfilled
- <span style="color:#00bfff">Correction</span> - Modify the system to allow the defined properties to be fulfilled

Examples of fault removal includes debugging and code reviews
### Fault Forecasting
Concerned with estimating the number, likelihood and consequences of faults in a system

Forecasting involves the identification, classification and analysis of modes by which a computer system can fail, as well as an evaluation of dependability attributes using probabilistic and analytical approaches

Fault injection analysis is a commonly adopted approach when attempting to establish dependability measures and forecast fault proneness

This can very often become physical as well as technical


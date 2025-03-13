# Hazards
A hazard is a set of conditions of a system that will lead to an accident, when combined with environmental conditions

Defined in terms of states to be avoided
- No two aircraft should share the same airspace
- Cars should not be within 2 seconds of each other at high speed

### Dealing with Hazards
We need to be able to rank hazards in order to address the most severe

We need to know:
- the <span style="color:#00bfff">severity</span> of the hazard
- the <span style="color:#00bfff">frequency</span> of occurrence

Different domains will have different interpretations of severity and frequency

### Hazard Analysis
Identification of way in which a system can cause harm

Consists of a set of techniques with distinctive attributes

#### FEMA 
Failure Modes and Effects Analysis

Considers the failure of a component with the effect of this failure being assessed at a system-level to detect hazardous situations

##### Advantages
- Can detect hazard situations arising as a result of single failures
##### Disadvantages
- Does not consider multiple failures
- Expensive to perform exhaustively

#### FMECA
Failure Modes, Effects and Criticality Analysis

Same thing as FMEA but with criticality

Permits meaningful cost-benefit analysis

#### HAZOP
Hazard and Operability studies

Focuses on answers to 'what if?' questions

Can effectively demonstrate the effects of parametric changes and out-of-range values

##### Advantages
- Effective for situations where 'what if?' questions are constrained
##### Disadvantages
- TIme consuming, especially for question generation

#### Event Trees
Starting from events that can affect system, tracking **forward** to determine their effects

Events can either be normal or faulty

They are made up of 3 parts:
- Root node - associated with event under scrutiny
- Other nodes - associates with other system events
- Edges - links two system events

##### Advantages
- Allows outcomes of events to be determined
##### Disadvantages
- Exponential complexity

#### Fault Trees
Commonly used for safety-critical systems

Tracks **backwards** instead of forward

Starts from hazardous situations and moves backwards to determine possible causes
##### Advantages
- Resultant trees are simplified
##### Disadvantages
- Identification of high-level hazards is challenging


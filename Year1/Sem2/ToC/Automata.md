Double circle is an accepting state
Single cirlce is a rejecting state

## DFA
DFA - Deterministc Finite Automaton
Deterministic - Follow algorithmically, we make no decisions
Finite - Restricted number of possible nodes

A DFA consists of the following data:
- A finite set X of states
- An initial state $p \in X$
- A transition state $\delta: X \times \Sigma \rightarrow X$
- A set of accepting states $Acc \subseteq X$

**Isomorphism** is when two automatons have one a one to one relation. They have the same shape but different set of states. 

It is a bijection that preserves the initial state, the accepting states and the transition function

If 2 automata are ismorphic then they're "essentially the same" so we can get away with omitting the filling of the circles. 

## Partial DFA
$\delta$ is now a partial function - it can now be undefined
If $\delta$ is undefined, it will be rejected
It also doesn't need an initial state - if so it will just be rejected

To turn a Partial DFA into a normal DFA, we just need to add an error state where the partial DFA would be undefined. 

## Nondeterministc DFA (NFA)
An NFA differs from a DFA since one input can have multiple different states available, aswell as multiple initial states. Thus $\delta$ is a relation but not a function

A word W i acceptable when there's some path following W that leads to an accepting state

### Determinizing an NFA into a DFA

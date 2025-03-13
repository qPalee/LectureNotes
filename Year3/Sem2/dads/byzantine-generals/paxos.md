# Paxos
'unlikely to show up on the exam'

Paxos is a consensus algorithm that can be used in a partially synchronous network

One or more clients proposes a value and we have consensus when a majority of systems running Paxos agrees on one of the proposed values

It was the first consensus algorithm to be proved to be correct
- Leslie Lamport is back!!!

### How does it work
Paxos selects a single value from a set of values that are proposed to it and lets everyone know

A single run of the Paxos protocol results in the selection of single proposed value

If we need to create a replicated log using Paxos then we need to run it repeatedly
- This is known as multi-Paxos

### Principles
We have <span style="color:#00bfff">proposers</span>, <span style="color:#00bfff">acceptors</span> and <span style="color:#00bfff">learners



</span>

You can have a situation where someone proposes, gets rejected and needs to learn

Its possible that a process needs to do all three
#### Proposer
Proposers are responsible for initiating the consensus process by suggesting a value

#### Aceptor


#### Learner


### Phases
#### Prepare Phase

#### Accept Phase

#### Learn Phase



### Abortability
Paxos provides abortable consensus
- Some processes will abort the consensus if there is contention while others decide on the value
- 

### Assumptions

### Algorithm
When you propose it needs to be unique

#### Pseudocode

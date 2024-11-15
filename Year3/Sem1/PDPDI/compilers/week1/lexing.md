# Lexing

### Regular Expressions
How can we specify all the lemexes that can occur in a program? Regular Expressions (REs)

Given an alphabet $\Sigma$, a regex $e$ is either:
- a symbol $a \in \Sigma$
- the empty string $\epsilon$
- an alternate/union $e_1 | e_2$
- a concatenation $e_1 e_2$
- a repetition $e^*$

#### Abbreviations
- We write $[a-z]$ for $a | ... | z$ and $[0-9]$ for $0 | ... | 9$
- We write $e^+$ for $ee^*$
- We write $e?$ for $e|\epsilon$

### Finite Automata
Regex's are not convenient to compute whether a word is part of a language
Instead, we will use Finite Automata

A finite automata is defined as a tuple: $M=<Q,\Sigma , \delta , q_0 , F>$ where
- $Q$: set of states
- $\Sigma$: alphabet
- $\delta$: transition relation
- $q_0 \in Q$: start state
- $F \subset Q$: set of final state

A <span style="color:#00bfff">dead</span> state is a state without outgoing transitions. We sometimes omit dead states when they are not final

A word is accepted by an FA if it finds a path from the start state to the final state

The language accepted by an FA is the set of words it accepts
![[Pasted image 20241114160351.png]]
![[Pasted image 20241114160439.png]]
![[Pasted image 20241114160621.png]]
Regex: $a(aa)^*$

It is easy to check if a word is accepted by a deterministic finite automata

A lexer has to find the longest match, which is harder.

We can keep track of the last time the FA was in a final state
We can track:
- the state $q$
- the word $w$ read at that time

When a dead state is reached, or the input is entirely read and the current state is a final state, $w$ is returned
![[Pasted image 20241114161044.png]]

#### Generating DFA from regex
Given a regex describing a language, we can convert it into an NFA as follows
![[Pasted image 20241114161304.png]]

![[Pasted image 20241114161554.png]]

#### Converting NFA to DFA
Read through this later
Also maybe look at first year ToC notes


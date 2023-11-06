The syntax of predicate logic is defined by the following grammar:
$t :== x | f(t, ...., t)$
$P :== p(t, ....., t) | \lnot P | P \land P | P \lor P | P \rightarrow P | \forall x.P | \exists x.P$

where:  
- $x$ ranges of variables  
- $f$ ranges over function symbols  
- $f(t_1, . . . , t_n)$ is a well-formed term only if f has arity n  
- $p$ ranges over predicate symbols  
- $p(t_1, . . . , t_n)$ is a well-formed formula only if p has arity n


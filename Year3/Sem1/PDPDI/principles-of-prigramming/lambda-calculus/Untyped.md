# Untyped $\lambda$-calculus
Its a small universal programming language
Introduced in the 1930s

It consists of:
- A set of $\lambda$-terms: 
- Several different notions of <span style="color:#00bfff">equivalence</span> and <span style="color:#00bfff">reduction</span> relations
$\lambda$-terms describe functions
It is a standard model of computation
Expresses the same computational functions as Turing machines

### Syntax
The pure $\lambda$-calculus has 3 constructs:
- <span style="color:#00bfff">Variables</span>
- <span style="color:#00bfff">Functions</span> called lambda abstractions
- Application

The following Backus-Naur form inductively defines the syntax of the λ-calculus:
$$M ::= x | \lambda x.M|\text{M M}$$

A variable is a name for something that has to be supplied by the environment
An abstraction stands for a function which, given an argument $x$, evaluates to the body M
An application means the result of passing an argument N to the function M

**Anything can be applied to anything**

#### Conventions
- Arguments can be functions
- Application is left associative
	- `xyz` stands for `(xy)z`
- The scope of a $\lambda$ extends as far right as brackets allow
	- $\lambda x.xx$ stands for $\lambda x.(xx)$

$\lambda x. \lambda y.xy$ = $(\lambda x. (\lambda y. (xy)))$

### Abstract Syntax Trees
The grammar can be seen as rules to derive trees where:
- leaves are variables
- nodes are either:
	- application nodes (@)
	- lambda nodes ($\lambda$)

![[Pasted image 20241007123115.png]]

### Free and Bound Variables
An occurrence of a variable `x` in a $\lambda$-term M is either
- <span style="color:#00bfff">bound</span> if it is in the scope of a $\lambda$-abstraction with argument `x`
- <span style="color:#00bfff">binding</span> if the occurrence is in the '$\lambda x$' of a $\lambda$-abstraction, or
- <span style="color:#00bfff">free</span> otherwise

Examples:
- `x` is bound in $\lambda x.x$
- `x` is free is $\lambda y.yx$
- `x` is both free and bound in $x(\lambda x.x)$
	- 3rd occurrence is bound and 1st occurrence is free
### $\alpha$-equivalence
Bound variable names are not important and can be renamed without changing the meaning of a term

Two terms, `M` and `N` are $\alpha$-equivalent if they only differ by their bound variables

#### Examples
$\textcolor{#00ff00}{\lambda x.x \equiv_{\alpha} \lambda y.y}$
$\textcolor{#ff0000}{\lambda x.xx \not\equiv_{\alpha} \lambda x.x}$ - not the same tree structure
$\textcolor{#00ff00}{x(\lambda x.yx) \equiv_{\alpha} x(\lambda z.yz)}$
$\textcolor{#ff0000}{x(\lambda x.yx) \not\equiv_{\alpha} x(\lambda.y.yy)}$ - not the same occurrences of free variables

### Capture-avoiding substitution
We want a <span style="color:#00bfff">substitution operation</span> - denoted $\textcolor{#00ffff}{M[x \backslash N]}$ - that substitutes the term $\textcolor{#00ffff}{N}$ into the free occurrences of the variable $\textcolor{#00ffff}{x}$ in $\textcolor{#00ffff}{M}$

This should be like running $\textcolor{#00ffff}{M}$ in an environment where $\textcolor{#00ffff}{x}$ is a name for the program $\textcolor{#00ffff}{N}$ 
- Straightforward substitution is not appropriate since free variables in $\textcolor{#00ffff}{N}$ could become captured
- Substitutions should be $\alpha$-equivalent

#### Examples
$\textcolor{#00ff00}{(xx)[x \backslash (\lambda y.y)] = (\lambda y.y)(\lambda y.y)}$
$\textcolor{#00ff00}{(\lambda y.x)[x \backslash (\lambda y.y)] = \lambda y . \lambda y.y}$
$\textcolor{#00ff00}{(\lambda y.yx)[x \backslash xx] = \lambda y. y(xx)}$
$\textcolor{#ff0000}{(\lambda y.yx)[x \backslash yy] \neq \lambda y.yy}$
- This is not correct since the the free $(yy)$ would be captured by the $\lambda y$ 
- To fix this we have to substitute the bound y to another variable
- We convert $\lambda y.yx$ into $\lambda w.wx$ before doing the substitution
- $\textcolor{#00ff00}{(\lambda y. yx)[x \backslash yy] = \lambda w. w(yy)}$
- We can do this since $\lambda y.yx \equiv_{\alpha} \lambda w.wx$

### $\beta$-equality
We can now use substitution to define the $\lambda$-calculus' main 'computation' rule called the $\textcolor{#00ffff}{\beta \text{-conversion}}$ rule

We say that if $\textcolor{#00ffff}{M}$ and $\textcolor{#00ffff}{N}$ are $\textcolor{#00ffff}{\beta \text{-equal}}$ - denoted $M =_{\beta} N$ - if the pair can be derived from the following rules:

$\textcolor{#00ffff}{\beta \text{-conversion}}$ - $(\lambda x.M) N =_{\beta} M[x \backslash N]$

$\textcolor{#00ffff}{\text{Reflexivity}}$ - $M =_{\beta} M$
$\textcolor{#00ffff}{\text{Symmetry}}$ - if $M =_{\beta} N$ then $N =_{\beta} M$
$\textcolor{#00ffff}{\text{Transivity}}$ - if ($M =_{\beta} N$ and $N =_{\beta} P$) then $M =_{\beta} P$

$\textcolor{#00ffff}{\text{Left-apply}}$ - if $M =_{\beta} N$ then $\text{M P} =_{\beta} \text{N P}$
$\textcolor{#00ffff}{\text{Right-apply}}$ - if $M =_{\beta} N$ then $\text{P M} =_{\beta} \text{P N}$
$\textcolor{#00ffff}{\text{Lambda}}$ - if $M =_{\beta} N$ then $(\lambda x.M) =_{\beta} (\lambda x.N)$

#### Example
$(\lambda f.\lambda x.fx)(\lambda y.y) =_{\beta} \lambda x.(\lambda y.y) =_{\beta} \lambda x.x$
### $\beta$-reduction
$\beta$-reduction is just $\beta$-conversion but only in one direction

$(\lambda f.\lambda x.fx)(\lambda y.y) \rightarrow_{\beta} \lambda x.(\lambda y.y) \rightarrow_{\beta} \lambda x.x$

$\textcolor{#00ffff}{\text{One step } \beta \text{-reduction}}$ is the relation $\rightarrow_{\beta}$ axiomatised by the rules:

$\textcolor{#00ffff}{\beta \text{-conversion}}$ - $(\lambda x.M) N \rightarrow_{\beta} M[x \backslash N]$

$\textcolor{#00ffff}{\text{Left-apply}}$ - if $M \rightarrow_{\beta} N$ then $\text{M P} \rightarrow_{\beta} \text{N P}$
$\textcolor{#00ffff}{\text{Right-apply}}$ - if $M \rightarrow_{\beta} N$ then $\text{P M} \rightarrow_{\beta} \text{P N}$
$\textcolor{#00ffff}{\text{Lambda}}$ - if $M =_{\beta} N$ then $(\lambda x.M) \rightarrow_{\beta} (\lambda x.N)$

### Normal forms

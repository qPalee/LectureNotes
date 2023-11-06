Matching and finding problems are common types of problems, and because of this there are lots of tools to solve them.

To use such a tool, you have to specify what makes up a valid format. 
One of these format is the regular expression

Let $\Sigma$ be the alphabet, any set of characters
E.g $\Sigma$ = {a, b, c} OR it could be the ASCII/Unicode alphabet

$\Sigma$* is the set of all words

A **language** is a set of words
Examples:
- Set of all passwords
- Set of all emails
- Set of all poems

A regular expression (regexp) is a way of describing a language

The regexp a only matches on word, the word "a"
The regexp $\epsilon$ matches the empty word

Suppose we have regexp's E and F:
- EF matches any word thats a concatenation of words that *both* E and F match
- E|F matches an word that *either* E of F matches
- E* matches any word thats a concatenation of several words that E matches
- $E^+$ is ddefined as $EE^+$
- $E^?$ is either nothing or E
- 0 doesn't represent any word

Knowing the precedence rules of arithmetic allows you to parse 
$3+4*2$ as $3+(4*2)$

Likewise, we need to know the precedence rules of regular expressions 

Precedence order = $^*, Juxtaposition, |$

A language thats represented by a regex is a regular language

Q. is there and language that isnt regular? Yes
Q. Is the complement of a regular language regular? Yes
Q. Is the intersection of 2 regular languages regular? Yes

A decision problem is a problem that (for any instance) has a Yes/No answer
Such a problem is decidable when theres a program that can solve it. 



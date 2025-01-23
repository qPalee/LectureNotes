# Advanced Cryptography

Bring your ipad to this!

They are actually doing consolidation week properly
Mock exam week 10

### Coursework
2 lab sheets will be released
2 sections each
- formative exercises
- summative coursework
	- number of different tasks 
	- programming/paper and pen/theory
	- each question has a select number of points
	- need 25 points per submission
	- Latex lab report
	- Multiple files with programs
	- All programming will be in python
	- Some tasks will specify a library to use

slow to respond to emails
office hour directly after the lab on tuesdays

### Content

Secret sharing allows multi-party computation

splits up the key to avoid leakage during computation
- important for embedded systems

##### Homomorphic encryption
$Enc(x_1, x_2, ..., x_n) = Enc(x_1) + Enc(x_2) + ... + Enc(x_n)$

Parties can compute encrypted values without revealing their $x_n$ keys

##### Secret Sharing
Secret value $x$ is represented as a tuple so that each party gets at least one share

##### Garbled curcuits
Special technique for 2 party computation
Represents functions as boolean circuits

Will be spoke about more in week 9

#### Note thingys
the things in boxes are very important
the text mirrors the pictures

### Secure MPC
Capital inputs could mean that there is more than one input

#### Input privacy
when joint computing output, function output is learned but nothing else is learned about the input data

##### Robustness
Suppose some parties have been corrupted

If the non-corrupted parties are still guaranteed to produce the correct result this is **robust MPC**
If the non-corrupted parties abort then this is **MPC with abort**

If a wrong result is output, parties need to know that it is wrong. big problem if they don't
Protocols will often try to do 'verifiable secret sharing' to resolve this

#### What is an adversary
Its some entity who wishes to 'break' whatever security properties we are trying to achieve
- 'bad guy'

To characterise adversaries, we need to define their 'security goal', what help they may find and tactics they use in practice

##### Semi-honest adversary
Doesn't change the protocol flow, just reads shit

##### Malicious adversary
Changes part of the protocol in order to get data from it

security notion
it is secure

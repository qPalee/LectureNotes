### Hashes
Hash of a message is a short string generated from that message
Hash of message is always the same
Very hard to reverse
#### Uses
Verification of download of message
Tying parts of a message together
Hash message, then sign hash
Protect passwords
#### Attacks
Preimage: Find message for given hash
Collision: Find 2 messages with same hash
Prefix collision: Collision attack where attacker can add a prefix

### MAC
Message Authentication Codes
Sometimes used for authentication
Possible attack: Add data to MAC without knowing key

If we have a hash we could try to make a MAC by $MAC_{Key}(M) = H(Key, M)$

#### Cipher texts
Cipher texts can be altered
AES Encryption can map any 128-bit block to another 128-bit block

##### Block Modes
CBC mode: any change affects all of the rest of the message
ECB mode: any change affects only the block
CTR mode: any change affects only the bits altered

If the plaintext is known, you can change CTR encrypted messages

### Access Control
ACM is a matrix of all pricipals and objects
MAtrix entities describe permissions
Maintaining can be hard

#### Access Conrol Lists
Instead of using a massive matrix, we can store each column of the matrix with the object it refers to

#### Security Issues
Users can run process with more privileges
If theres a mistake in the passwd program we could use it to do root actions
<span style="color:#00bfff">Make sure proccess have a low level as possible</span>

#### Storing Passwords
Passwords not stored in clear text
Only hashes are stored
Store (salt, hash) where salt is random bitstring and hash is the hash of the salt + passwd
Makes cracking passwords much harder

### Symmetric Encryption
Historically caeser cipher used
Can be broken with cryptanalysis with sufficiently long ciphertext

#### Encypting with snaller keys
Block Cipher: Encrypt n-bit block via randomly chosen permutation
Stream Cipher: Generate random looking bit-stream from a smaller key and xor the message with the stream


Block Ciphers encrypt fixed length strings
##### CBC Mode
![[Pasted image 20240512140225.png]]
IV needs to be random!!

##### CTR Mode
![[Pasted image 20240512140250.png]]
Ciphertexts are malleable

### Public Key Cryptography
Each person has 2 keys: One public and one private
Keys are asymmetric: related but not identical
Public key is known to everyone but private key is kept secret

Encryption done with public key
Decryption done with private key

#### Diffie Hellman Key Exchange (DH)
G and P are public keys
![[Pasted image 20240512140609.png]]
A and B generate private keys (must be primes <= p)
Public keys are $g^a \text{ mod p}$ and $g^b \text{ mod p}$ 

#### RSA
##### Generating RSA
Generate 2 distinct primes $p$, $q$
Compute $N=pq$ and $\phi (N) = (p-1)(q-1)$
Choose e such that $1 \lt e \lt \phi$ and e and $\phi$ are coprime
Compute d such that $ed \equiv \text{1 mod }\phi$
Public Key = (e, N)
Private Key = (d, N)

Encyption: $c=m^e \text{ mod N}$
Decryption: $m = c^d \text{ mod N}$

### TCP/IP
IP is like well old
Has a header and shit
Bare packets were getting lost so TCP was made so packets get resent

#### DNS
Remembering IP addresses is hard for some ppl
Hierarchy of servers list handles requests
The route for most of Europe is RIPE in Amsterdam


#### IP Stack
Internet Communication uses a stack of protocols
Each protocol uses the protocol below it to send data

##### Applicaion
This layer just has the apps (like jhipster apps)

##### Transport
This is where TCP is and allat

##### Network
This is where the IP address gets added and shit

##### Link/Hardware
This is where the MAC address is known bruv

#### MAC and IP Addresses
Every machine has a unique MAC address
Every computer on the internet has an IP address

### Protocols
Written as $A \rightarrow B : \text{"I'm Alice"}$

This can be intercepted by an attacker
Attackers can pretend to be anyone

$E(A) \rightarrow B : \text{"I'm Alice"}$

If Alice and Bob share a key, then Alice can encrypt her message

$A \rightarrow B : \text{\{"I'm Alice"\}}_{K_{ab}}$

An attacker can intercept and replay messages

$E(A) \rightarrow B : \text{\{"I'm Alice"\}}_{K_{ab}}$

#### Nonces
A nonce is a number that is only used once, often in a challenge/response setting
- $A \rightarrow B : A$
- $B \rightarrow A : \{N_a\}_{K_{ab}}$
- $A \rightarrow B : \{N_a+1\}_{K_{ab}}, \text{\{Pay Elvis £5\}}_{K_{ab}}$

This is vulnerable to replay attacks, however this can be stopped by changing the protocol slightly

$A \rightarrow B : \{N_a, \text{Pay Elvis £5\}}_{K_{ab}}$

This protocol was possible because A and B shared a key
Often the principals need to set up a session key using a Key Establishment Protocol
They must know each others public keys or use a TTP

#### Needhan-Schroeder Public Key Protocol
Assume A and B know each others public keys

- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b)$
- $A \rightarrow B : E_B(N_b)$

$N_a$ and $N_b$ can then be used to generate a key

This is vulnerable to a mitm attack
![[Pasted image 20240512143239.png]]

This can be resolved with a very simple fix:
- $A \rightarrow B : E_B(N_a, A)$
- $B \rightarrow A : E_A(N_a, N_b$, <span style="color:#00fc00">B</span>$)$
- $A \rightarrow B : E_B(N_b)$

#### Forward Secrecy
After the protocol runs, govt can legally force people to hand over their private keys

A protocol has forward secrecy if it keeps the message secret from an attacker who has:
- A recording of the protocol run
- The long term keys of the principals

#### Station-to-Station Protocol
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : \{S_A(g^y, g^x)\}_{g^{xy}}$
- $B \rightarrow A : \{M\}_{g^{xy}}$

$x$, $y$, and $g^{xy}$ are not stored after the protocol run

A and B's keys dont let the attacker read M

STS has <span style="color:#00bfff">forward secrecy</span>

#### Certificates
What if Alice and Bob don't know each others public keys

Get a TTP to dign their identity and public key: <span style="color:#00bfff">a certificate</span>

#### Full STS
- $A \rightarrow B : g^x$
- $B \rightarrow A : g^y, Cert_B, \{S_B(g^y, g^x)\}_{g^{xy}}$
- $A \rightarrow B : Cert_A, \{S_A(g^y, g^x)\}_{g^{xy}}$

The full STS protocol adds certificates for A and B

These contain their public key signed by a TTP, so Alice and Bob don't need to know each others public keys

#### Key Establishment Goals
##### Key Freshness
The key established is new (either form a TTP or because it uses a new nonce)

##### Key Exclusivity
The Key si only known to the pricipals in the protocol

##### Good Key
The key is both Fresh and Exculsive

#### Authentication Goals
##### Far-end Operative
A knows that B is currently active
- B might have signed a nonce that A generated
- $A \rightarrow B : N_a$
- $B \rightarrow A : S_B(N_a)$

##### Once Authentication
A knows that B wishes to communicate with A

For instance, B might have the name A in the message
- $B \rightarrow A : S_B(A)$

##### Entity authentication
A knows that B is currently active AND wants to communicate with A
- $A \rightarrow B : N_a$
- $B \rightarrow A : S_B(A, N_a)$

#### Highest Goal
A protocol provides Mutual belief in a key for Alice with respect to Bob if Bob can be sure that:
- K is a good key with A
- Alice can be sure that Bob wishes to communicate with Alice using K
- Alice knows that Bob believes that K is a good key for B

### TLS
The Transport Layer Security Protocol provides encrypted socket communication and authentication based on public keys

it may use a range of ciphers which are negotiated at the start of the run

The TLS Layer runs between the Application anf Transport layer
Normal TCP and IP layers can be used at the low levels

#### Weaknesses in TLS
Config weaknesses
- Cipher downgrading
- Self-signed certificates

Direct attack against implementations
- goto fail bug
- LogJam
- HeartBleed

##### Cipher downgrading
An attacker that owns the network can remove strong ciphers
If both client and server support a weak cipher, then an attack can force its use

##### Self-signed certificates
Maintaining a set of certificates is hard
Its much easier to just accept any certificate
If the client accepts self-signed certificates, then its easy to man-in-the-middle
This has been shown to happen a lot 

##### LogJam
A weak DH key is compatible with a string DH key

##### HeartBleed
Programming error in openSSL

TLS client can request a 'heart beat' from the server to make sure the connection is still open

This memory could contain the servers key

### Virtual Private Networks
VPNs securely connect you to another network
- You can connect to the schools printers via the schools vpn
- Secured with certificates and encryption

To get some anonymity, you can route all traffic via the VPN
- Server thinks you are the VPN provider
- ISP only sees the connection to the VPN
- A global observer can probably link your connections
- There is <span style="color:#00bfff">no anonymity</span> to the vpn provider

#### Onion Routing
You get the best anonymity by routing your traffic via a number of proxies
Ensures that your message really is routed via the proxies that you want
Tor uses this protocol

Each Proxy only learns the IP of the proxy before it and the proxy after it
The public key of each proxy is known
Source IP is visible to the first node, dest IP is visible to the last node
User picks 3 proxies and is anonymous as long as they aren't all corrupt

### Attacks against websites
#### Cookies
Cookies let the server store a string on the client

This can be used to:
- Identify the user
- Store user name, preferences etc
- Track the user

##### Stealing cookies
Cookies can be stolen to allow attackers to log into your account

If the website uses HTTPS then it is secure
Many sites used to drop back to HTTP after a secure login

###### Countermeasures
- Use HTTPS all the time
- Set secure flag on cookie

#### SQL Injection
Assume there is an SQL statement `SELECT * FROM items where(item=$item)`

We can use malicious input to get the database to send back unintended items
let $item = `' OR '1' = '1' ) --`

This will return all values in the items table, including hidden items since 1=1

##### Preventing SQL Attacks
You can use prepared statements to stop SQL attacks

Not just websites are vulnerable to SQL injections
![[Pasted image 20240512151650.png]]

### Cross Site Scripting (XSS)
XSS is an input validation vulnerability

Allows an attacker to inject client-side code into web pages

#### Reflected XSS
The injected code is reflected off the web server
Only the user requesting the malicious request is affected

#### Stored XSS
The injected code is stored on the web site and is served to all its visitors on all page views

XSS can be used to steal users' cookies then log in as the victim

#### Phishing
An attacker can inject a script that looks and feels like the login page
This fake page can ask for user's credentials or other sensitive info

An attacker could also redirect users to the attackers site
```html
<script>
	document.location = "http://evil.com"
</script>
```
#### Solution for injection
Injections can be stopped by sanitising user inputs

### Path Traversal
The user can type anything they want to into the URL bar
`http://nameOfHost/../../../etc/shadow`

If the server is running with root permissions this will return the password file for the server

#### Fix for Path Traversal
Use access control settings
Make a specific user account for the webserver
Only give that account access to public files

### Stack
![[Pasted image 20240512152625.png]]

##### Push to the stack
When we want to push something to the stack we must <span style="color:#00bfff">push eax</span>
We must also increment the stack pointer, <span style="color:#00bfff">esp</span> (which goes down for x86)

##### Pop from the stack
When we pop from the stack, the top item is removed, and the value is added to <span style="color:#00bfff">eax</span>
After popping a value, <span style="color:#00bfff">esp</span> is decremented (which goes up for x86)

When values are popped from the stack, the data isn't actually removed from memory, it is just removed from the stack

##### Functions in the stack
When a function is initialised, it creates an <span style="color:#00bfff">ebp</span>, which is the base pointer of the function

The base pointer always points to the first item on the stack that belongs to the current function, which often stores the old <span style="color:#00bfff">ebp</span>, so that it can return to it after the function is finished running


### Buffer Overflows
Inputs can be generated which manipulate how the stack works to do things it isnt meant to do

![[Pasted image 20240512153032.png]]

If we input a string longer than 16 bytes, it will overflow the variable and start writing into the old ebp and the return address

If we use the input `Hello World XXXX XXXX97F9`, then this happens
![[Pasted image 20240512153154.png]]

If we write the return address as the address of the start of the input variable, we can then do ACE ![[Pasted image 20240512153255.png]]

Very cool things

It can also write over other variables such as authentication variables

#### Defenses against buffer overflows

##### NX-Bit
The NX-Bit works by provding a distinction between the text and stack, and will crash the program if the EIP ever points to the stack

To get around this, you need to reuse code from the executable part of memory such as:
- Jump to another function in the program
- Jump to a function from the standard C lib
- String together little pieces of existing code

##### ASLR
This adds a random offset to the stack and code base each time the program runs.

The idea is that its now hard for an attacker to guess the address of where they innject code or the address of particular functions

###### NOP
In x86, the instruction 0x90 does nothing

If the stack if 2MB, i could inkect 999000 bytes of 0x90 followed by my shell code
If i then guess a return address and hope it lands somewhere in the sea of NOPs
If it is, then the program will slide through then until it reaches my shell code
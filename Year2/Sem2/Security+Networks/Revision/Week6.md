# Week 6

### Transport Layer Security (TLS)
TLS provides encrypted socket communication and authentication, based on public keys

It may use a range of ciphers (PSA, DES, DH)
- These are negotiated at the start of communication

TLS runs between the Application and Transport Layer of the IP stack
The encryption is transparent to the application layer
Normal TCP/IP layers can be used for the lower layers of the stack

#### Weaknesses with TLS
Configuration weaknesses
- Ciphers can be downgraded
- Self-signed certs

Direct attack against implementations:
- Apple's goto fail bug
- LogJam attack
- HeartBleed

##### Cipher Downgrading
An attacker that owns the network can remove strong ciphers, so if both the client and server support a weak cipher then an attack can force its use
![[Pasted image 20240506143940.png]]

##### Self-Signed Certificates
Maintaining a set of certificates is hard
Its much easier to just accept any certificate, which can lead to a Man in the Middle attack

### Onion Routing
You get the best anonymity by routing your traffic via a number of proxies

Onion Routing ensures that your message is routed via the proxies you want

#### Tor
Tor uses onion routing

Each proxy only learns the IP of the proxy before it and the proxy after it
The public key of each proxy is known
Source IP is visible to the first node, destination IP is visible to the last node

##### Anonymity does not mean security
The web servers can still be attacked
- The FBI attacked criminal websites running Tor and implanted malware


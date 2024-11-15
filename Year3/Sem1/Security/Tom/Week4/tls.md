# TLS

If a program is using TLS its often not even worth trying to break it
### Internet Protocol Stack with TLS
![[Pasted image 20241024141734.png]]

The TLS layer runs between the Application Layer and Transport layer

The encryption is transparent to the Application layer

#### TLS 1.2
1. $C \rightarrow S : N_C$
2. $S \rightarrow C : N_S, Cert_S$
3. later
4. later

At its heart it is a very simple protocol

You can MitM and pretend to be C but can't pretend to be S

Certificates are based on knowing peoples certificates already
Certificates are downloaded when you install the browser
You just have to trust the certificates
- "Trust me bro"

TLS 1.2 can also have a client certificate which is very strong
##### Choosing an encryption method
1. $C \rightarrow S : N_C, \text{Possible CipherSuites}$
2. $S \rightarrow C : N_S, Cert_S, \text{CipherSuite}$

Its possible to do TLS with no encryption whatsoever
- This would be used when the network organiser wants to see all traffic on the network
- It is possible to disable weak ciphersuites
- If you set up a TLS server with Java it will have weak ciphers available out of the box

In reality, the messages look more like this
![[Pasted image 20241024143606.png]]

#### TLS_DHE
TLS doesn't originally have forward secrecy
Adding DH fixes this
![[Pasted image 20241024144131.png]]

#### Issues with TLS 1.2
- There are too many cipher suites
- Due to this there have been lots of attacks against particular cipher suites
- You need 2 round trips before you can start sending data
- Many attacks based on mistakes in implementations
- TLS 1.3 fixes many of these problems

### TLS 1.3
It only has forward secrecy
It only has about 4-5 cipher suites and they are all very secure

Key is based on DH handshake and all previous messages hashed together to make a key
- This makes the certificate name unreadable
- This means the network owner cant see where you are visiting anymore

![[Pasted image 20241024145513.png]]

TLS 1.3 also has a version with a client certificate

#### Improvements over 1.2
- Only 5 very secure cipher suites
	- TLS_AES_256_GCM_SHA384
	- TLS_CHACHA20_POLY1305_SHA256
	- TLS_AES_128_GCM_SHA256
	- TLS_AES_128_CCM_8_SHA256
	- TLS_AES_128_CCM_SHA256
- All Elliptic Curve DH, for forward secure
- Few modes of operation (RSA, no static DH)
- Hides the server name from passive eavesdroppers
- Starts sending data after 1 round trip of messages


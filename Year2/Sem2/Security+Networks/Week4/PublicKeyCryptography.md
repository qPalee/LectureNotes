# Public Key Cryptography

### Secure Key Exchange
![[Pasted image 20240205152948.png]]

Given $g^a \space mod \space p$ it takes $p$ operations to find a

All the parties have 2 keys, one public key and one private key
Alice: $g^a \space mod \space p$ as the public key, $a$ is the secret key
Bob: $g^b \space mod \space p$ as the public key, $b$ is the secret key

Encryption is done using the other persons public key
Encryption(receivers public key, message) = (senders public key, one-time-pad(message, agreed secret))

Decryption is done using the persons secret key
Decryption(receivers secret key, ciphertext) = message

Alice wants to send a message to Bob 
$m \in N \space \forall \space \{1...p-1\}$ 
Encryption($g^b \space mod \space p$, m) = ($g^b \space mod \space p$, $m \times g^{ab} \space mod \space p$)
Decryption($b$, ciphertext)=m



# Week 2

### Hashes
A hash of a message is a short string generated from that message
The hash of a message is always the same
A small change to the message changes the hash in a big way
Its nearly impossible to reverse a hash
Its very unlikely that 2 messages share the same hash

#### Uses of hashing
- Storing Passwords
- Tying parts of a message together
- Hash a message then sign the hash
- Protect Passwords
	- Storing the hash instead of the password

#### Attacks on hashes
- <span style="color:#00bfff">Preimage attack</span>: Find a message for a given hash
- <span style="color:#00bfff">Collision attack</span>: Find 2 messages with the same hash
- <span style="color:#00bfff">Prefix collision attack</span>: A collision attack where the attacker picks a prefix for the message

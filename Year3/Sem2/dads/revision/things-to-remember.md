# Things to remember

### M-of-N systems formula
$$P(S_t) = \sum^{N}_{i=M} {}^nC_i \cdot R(t)^i \cdot Q(t)^{N-i}$$

### Cut Sets and Tie Sets
Minimal Cut Set is the smallest combination of elements in which failures would lead to a system failure
- Subsets of this will not lead to system failure

Minimal Tie Set is the smallest combination of elements in which operations would lead to a correctly working system
- Subsets of this will not lead to a working system

### Leader Election

#### LCR Algorithm

```
current_value = u
send = null
match incoming_message:
	case incoming_message < current_value:
		send = incoming_message
	case incoming_message == current_value:
		stasus = leader
	case incoming_message > current_value:
		return
```

#### HS Algorithm

```
if message recieved has direction out then 
	if v == u:
		status = leader
	else:
		send v to next process

if message received (v) had direvtion in then
	if message from both directions are the same:
		goto next phase
	else:
		send message to next process
```

### Reliable Links

```
delivered = []
if event()
```
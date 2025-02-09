# Detectors
A detector is a class of program components that asserts the validity of a predicate in a running program

In its simplest form, this can be represented as
```
if(not predicate)
	exit;
```

### Example - Run-time Checks
Used for detecting errors, hence used in fail-safe tolerance design

There are many different types:
- <span style="color:#00bfff">Replication checks</span> - compare outputs of matching modules
- <span style="color:#00bfff">Validity checks</span> - divide by 0, check array bounds
- <span style="color:#00bfff">Reversal checks</span> - reverse output and check against inputs
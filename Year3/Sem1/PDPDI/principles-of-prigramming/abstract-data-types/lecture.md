# Abstraction
- The developer of a module should not have to fully understand another module to use it
- A module should be allowed to change without affecting the other modules
	- You can change a function and no-one will notice its different
- Hiding the complexity of a program
- Provide an abstract view of a program
	- Only need to understand the abstract view to use the program

There are several forms of abstraction
### Function Abstraction
- Separates the purpose of a function from its implementation
- To use a function we need to know
	- Its inputs
	- Its outputs
	- Its pre-conditions
	- Its post-conditions
		- The line between inputs and preconditions can be blurry
- We dont need to know how it works internally
- The implementation can change but not the interface

#### Example
$$sort :: Ord \ a \Rightarrow [a] \rightarrow [a]$$
- This is the type signature of Haskells sorting function
- It specifies inputs/outputs
- Its name indicates what it does
- It requires the type a to be totally ordered

The type signature is provided separately from the implementation

### Data Abstraction
Data Abstraction abstracts over data
- It doesn't specify how the data is implemented
- It also doesn't specify how the functions manipulating the data are implemented

An ADT (ABstract data type) can be seen as:
- an ...

#### Example 1
Say we want to define an ADT for counters
- Abstract name A: Counter
- Concrete representation Type T: Integer
- Abstract Interface:
	- $new :: Counter$
	- $get :: Counter \rightarrow Integer$
	- $inc :: Counter \rightarrow Counter$
- Concrete Implementation
	- $new = 0$
	- $get \ c = c$
	- $inc \ c = c+1$

A counter cannot be used as an Integer outside of the definition of this ADT

#### Example 2
We want to define an ADT for collections of Integers
- Abstract name A: Collection
- Concrete Representation Type T: $[Integer]$
- Abstract Interface:
	- $add :: Integer \rightarrow Collection \rightarrow Collection$
	- $remove :: Integer \rightarrow Collection \rightarrow Collection$
	- ...
- Concrete implantation
	- $add \ i \ list$
	- $remove \ i \ list$

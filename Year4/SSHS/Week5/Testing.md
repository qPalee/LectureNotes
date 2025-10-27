# Software Testing

Testing is the <span style="color:#00bfff">process of analysing a software item to detect</span> the differences between existing and required conditions and to evaluate the features of the software item

### Four levels of Testing
- Unit Testing
	- Individual components
- Integration Testing
	- Modules in combination
- System Testing
	- Fully integrated system
- Acceptance Testing
	- Users of the system

### Test Types
A test type is a group of test activities based on <span style="color:#00bfff">specific test objectives</span> aimed at <span style="color:#00bfff">specific characteristics</span> of a component/system

Examples of test types:
- Regression tests
	- Ensures new changes do not cause new defects
- Smoke tests
	- Tests to assess main/critical functionality of the software
- Conformance tests
	- Ensures that software behaves according to their specification
- Security tests
	- Tests to find security critical defects in the target software

### Test Automation
Automating test execution and result analysis is highly beneficial

Many languages have built in automation frameworks

#### CI/CD
Often used in modern software engineering
- Merge changes frequently into a single mainline
- Before merging, ensure functionality via testing

## Testing from a security perspective

### Box Model
Testing can be classified based on the information provided to the tester
- <span style="color:#00bfff">Black Box</span> - No information about the internals of the system
	- Can only observe input/output
- <span style="color:#00bfff">Grey Box</span> - Partial information about the system
	- Can create informed tests
- <span style="color:#00bfff">White Box</span> - Full information about the system
	- Can leverage source code

### Static and Dynamic Testing

#### Static Testing
- Testing the code without execution
- Reasons about the code
- Can create false positives

#### Dynamic Testing
- Testing by executing the program
- Observes the code's behaviour
- May not cover the full program

### Test Coverage
Metrics to understand how complete given tests are

#### Code Coverage Types
- <span style="color:#00bfff">Function Coverage</span>
	- What parts of the software are executed
- <span style="color:#00bfff">Line Coverage</span>
	- What parts of the source code is executed
- <span style="color:#00bfff">Block Coverage</span>
	- What parts of the machine code is executed
- <span style="color:#00bfff">Edge Coverage</span>
	- What parts of the control flow graph are executed


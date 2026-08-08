
### Dependency is a good candidate to be dependency injected if:
1. The dependency introduces a requirement to set up and configure a runtime environment. for the application.
	1. Examples: Database libraries, configuration files
2. The dependency doesn't exist yet, or still in development
3. The dependency isn't installed on all machines in the development organization.
4. The dependency contains nondeterministic behavior.
	1. Examples: random numbers, algorithms that depend on the current date/time
5. The dependency is not expected to be stable (likely to change in the future)

### What is DI?
Dependency injection is a set of software design principles and patterns that enables you to develop loosely coupled code.

### DI Patterns
- How do we guarantee that a necessary [[#Volatile Dependency = Dependency that changes or is not finished. | Volatile Dependency]] is always available to the class we’re currently developing?
	- Require all callers to supply the [[#Volatile Dependency = Dependency that changes or is not finished. | Volatile Dependency]] as a parameter to the class’s constructor.
	- Constructor Injection
	- Chapter 4.2
-  How can we inject a Dependency into a class when it’s different for each operation?
	- Supply it as a method parameter.
	- Use Method Injection 
	- Chapter 4.3
- How do we enable DI as an option in a class when we have a good [[#Local Default = A Local Default is a default implementation of a Dependency that originates in the same module or layer.|Local Default]]?
	- Expose a writable property that lets callers supply a Dependency if they want to override the default behavior.

### Questions
1. how do I implement x with dependency injection
	1. caching
	2. logging
	3. error handling
	4. configuration
	5. testing
		1. fake data
	6. authentication
	7. authorization

### Vocab
#### Volatile Dependency = Dependency that changes or is not finished.

#### Local Default = A Local Default is a default implementation of a Dependency that originates in the same module or layer.
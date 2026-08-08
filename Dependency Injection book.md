### Dependency is a good candidate to be dependency injected if:
1. The dependency introduces a requirement to set up and configure a runtime environment. for the application.
	1. Examples: Database libraries, configuration files
2. The dependency doesn't exist yet, or still in development
3. The dependency isn't installed on all machines in the development organization.
4. The dependency contains nondeterministic behavior.
	1. Examples: random numbers, algorithms that depend on the current date/time
5. The dependency is not expected to be stable (likely to change in the future)
### What is DI?
-  Dependency injection is a set of software design principles and patterns that enables you to develop loosely coupled code.
### Separation of concerns
The idea is that you do not have 


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
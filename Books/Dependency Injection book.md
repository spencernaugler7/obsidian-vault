---
tags:
  - books
  - tech
---
### What is DI?
Dependency injection is a set of software design principles and patterns that enables you to develop loosely coupled code.

### Good DI containers for Dotnet Core
- [SimpleInjector](https://www.nuget.org/packages/SimpleInjector)
	- [docs](https://docs.simpleinjector.org/en/latest/index.html)
	- [use with built in IServicesCollection](https://docs.simpleinjector.org/en/latest/servicecollectionintegration.html)
- [Decoratr](https://www.nuget.org/packages/DecoratR)
### How do I decide if a dependency should be Injected?
Dependency is a good candidate to be dependency injected if:
1. The dependency introduces a requirement to set up and configure a runtime environment. for the application.
	1. Examples: Database libraries, configuration files
2. The dependency doesn't exist yet, or still in development
3. The dependency isn't installed on all machines in the development organization.
4. The dependency contains nondeterministic behavior.
	1. Examples: random numbers, algorithms that depend on the current date/time
5. The dependency is not expected to be stable (likely to change in the future)

### DI Patterns
- Constructor Injection
	- How do we guarantee that a necessary [[#Volatile Dependency]] is always available to the class we’re currently developing? Require all callers to supply the [[#Volatile Dependency]] as a parameter to the class’s constructor.
	- Use if a dependency should be required. Ensures the class cannot be created without supplying the dependency.
	- Chapter 4.2
- Method Injection 
	- How can we inject a Dependency into a class when it’s different for each operation?Supply it as a method parameter.
	- Usual method definition looks like this `Method(DataClass data, IOptions options){...}` where `data` is the data to be operated followed by several injected args that provide functionality/context.
	- Chapter 4.3
- Property Injection
	- How do we enable DI as an option in a class when we have a good [[#Local Default]]? Expose a writable property that lets callers supply a Dependency if they want to override the default behavior.
	- Best used when the Dependency is optional. If the dependency is required use [[#Constructor Injection]] 
	- Chapter 4.4

### DI Anti-Patterns
- Control Freak
	- initializing concrete dependencies that are Volatile (changes frequently) instead of providing them via the di patterns.
		- new keyword, no interfaces
	- These dependencies should be handled via the composition root instead.
	- can be done through overloaded constructors. 
- Temporal Coupling
	- Implicit relationship between two or more members of a class, requiring clients to invoke one member after the other.
- Abstract factory that also uses Control Freak
	- just moves the coupling from the calling code to the new abstract factory.
- Service Locator
	- 

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
###### Constructor Injection
Supply a dependency through a classes constructor. Throw exceptions/errors if this dependency is not provided or null.
###### Volatile Dependency
Dependency that changes or is not finished.
###### Local Default
A Local Default is a default implementation of a Dependency that originates in the same module or layer.

**Foreign Default**
single default Implementation of an interface that is defined in a different assembly. Can lead to issues with typing assemblies together.
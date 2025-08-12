# Spring
## Dependency Injection Framework
## Index by Date:
```dataview
CALENDAR file.mtime
```
### Terminology:
##### [[Beans]]
	Different Objects managed by spring
##### [[Autowiring]]
- Process Spring goes through to identify [[Dependency]] and its matches and populates them
##### [[Dependency Injection]]
	prog technique
	class independent of its dependencies
##### [[Inversion of control]]
	taking control from class that needs dependency and giving it to the framework
##### [[IOC Container]]
	general term- anything implementing inversion of control
	usually in spring this = Application container
##### [[Application Context]]
	All beans are created and managed
	all core logic of Spring Framework happens
	

## What is Spring?
1. The Spring #Framework is an application framework and [[Inversion of control]] container for the #Java platform. 
2. The framework's core features can be used by any Java application, but there are extensions for building web applications on top of the Java EE platform.
3. Built modularly
	 - one can use the Core container, the Data Access and Integration modules, Web modules, etc
4. Great support for Transaction management
5. Great support for Websockets

## What does Spring do?
1. Spring instantiates objects, and populates dependencies
2. fines out what are the beans
3. what are the dependencies for the beans
4. and where to search for the #beans

## Why is Spring so popular?
1. Enables Testable code
2. No Plumbing code
	1. no need to add try- catch and exception handling code manually. 
3. Flexible Architecture
	1. Spring is very modular
	2. many modules for specific purposes
4. Able to stay with current trends in cloud and microservices

## Remember: 
---
### [[Tight Coupling]]
	Not good code
	Software Components are highly dependent on eachother
	any changes in component deeply affect the others


### Removing tight coupling:
	Remove instanciation of dependencies in the class
	create and instanciate Algo, create complex services
	pass algo through


## As a developer.. 
- tell Spring what objects need to be managed
- what are the dependencies of each class/object



## @Component & @Autowired

[[@Component]]
- Annotation that allows Spring to auto detect the custom beans at the class level
- Spring Scans app for classes annotated with @Component
- instantiates them and injects and specific dependencies
- injects the dependencies whenever needed

[[@Autowired]]
	- tells spring what are the dependencies
	- Spring will start looking at this dependency among @Component to find match for
	- Can autowire by type using the given constructor. This is referred to as [[Constructor Injection]]



### What's happening in the Background?

### Component Scan
- Using component scan is **one method of asking Spring to detect Spring-managed components**
- once component is found
- When we see @SpringBootApplication, automatically defines componentScan on the current package and its child packages
- look at it as a search
- 


## [[Spring Projects]]


#Spring
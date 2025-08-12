 # Beans

## Date: Aug 4, 2022

---

## What is a *'Bean'*?
- A Bean is an object Spring Instantiates, assembles, and manages

### Example Java Class that would be used as a Spring Bean:
```Java

public class AccountService {
		@Autowired 
		private AccountRepository accountRepository; 
		// getters and setters
	}

```

## Bean Scope
```java
@Scope("prorotype")
```
- Default - singleton
- ==[[singleton]] - One instance per Spring Context==
- ==prototype - New bean whenever requested==
	- the hashcodes will be different
- request - One bean per HTTP request
- session - One bean per HTTP session
    
- DAO - Data Access Object
- Whenever you have a request for a DAO, there needs to be a [[proxy]] configured
	- instead of giving direct access to jdbc connection, and proxy makes sure access is granted to an instance of jdbc connection each time


## Lifecycle of a Bean
- entire lifecycle managed by spring IoC container([[Inversion of control]] Container

### SubSubject

- four-color theorem
- GPS/maps

### SubSubject 2

- Social networks, such as facebook, twitter, and instagram
- gene/protein expression networks

## Equation Example:

$$
G = (V,E)
$$

- n vertices V ((nodes))
- m edges E (links)
- all elements are unique, aka **no repeated values**
- each edge is defined by its starting and ending edges.
    - ex: (a,b)

--- 

# REVIEW :

# Vocab:

- **undirected** graph
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    in other words, its possible to go from u to v, and vice versa
    
- **directed** graph
    
    it is not possible to go from u to v and vice versa
    
    so the 
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    equation does not hold..
    
- self loop
    
    the starting and ending vertices are the same 
    
    i.e. e=(v,v))
    
- path
    
    A path is a sequence of vertices (v1,v2,...,vk), such that vi+1 is a neighbor of vi .
    


## The notes review:

- question 1
- question 2
- question 3
- question 4

## Questions for next time

- [ ]  question 1
- [ ]  2
- [ ]  3
- [ ]  4
- [ ]  5
- [ ]  6
- [ ]  7
- [ ]  8
- [ ]  9
- [ ]  10




#Spring
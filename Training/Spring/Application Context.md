 # The Spring Application Context
 ## Primary job: Bean Manager
## Date: Aug 4, 2022

---

## Definition:

- The Spring Application Context is where Spring holds instances of objects that it has recognized to be managed and distributed automatically. 
	- These instances of objects are known as [[Beans]].
- Bean Management and opportunity for [[Dependency Injection]] all happen in this environment.
- Spring collects bean instances using [[Inversion of control]] and uses them at the appropriate time. 
- Spring can be shown the bean dependencies without needing to handle setup and instantiation of the objects (beans).


## Terms:
- BeanFactory:
	- The root interface for accessing the Spring bean container
	- basic client view of bean container
	- provides basic functionalities for managing beans. 
- ==Application Context==
	- sub-interface of the BeanFactory
		- provides all functionalities of BeanFactory as a result.

## Important Features

- Resolving messages
- supporting internationalization
- publishing events
- publishing application-layer specific contexts


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